# 12 Fatores, uma codebase, muitos deploys

> A metodologia dos 12 fatores completa quinze anos. Kubernetes, containers e serverless mudaram o vocabulário. Os problemas que ela resolve continuam os mesmos.

---

Tem um tipo de bug que só aparece depois do deploy. Na máquina de quem desenvolveu, a aplicação sobe, autentica e grava no banco. Em homologação, a fila não conecta. Em produção, uma credencial ficou no código, o processo guarda sessão em memória e, na hora de escalar, o usuário perde o carrinho no meio do caminho.

Nenhuma dessas falhas é mistério de framework. São sintomas de uma aplicação que ainda trata ambiente, configuração e processo como detalhes de infraestrutura, e não como parte do desenho do software.

Em 2011, Adam Wiggins, cofundador da Heroku, formalizou uma resposta a esse tipo de problema. O nome ficou conhecido como _The Twelve-Factor App_: doze princípios para construir aplicações web — sobretudo SaaS — que sejam portáteis, fáceis de operar e capazes de crescer sem reescrever a arquitetura a cada novo ambiente. O texto original está em [12factor.net](https://12factor.net/pt_br/). O que segue é uma leitura prática desses princípios, pensada para quem entrega software hoje.

A metodologia nasceu de dores concretas: ambientes de desenvolvimento e produção que divergiam, configuração espalhada pelo repositório, e aplicações que só escalavam se alguém aumentasse a máquina. Quinze anos depois, o cenário mudou de Heroku para Kubernetes, de dyno para pod, de PaaS para nuvem pública. A lista continua útil porque descreve o contrato entre a aplicação e a plataforma, independentemente do fornecedor.

---

## 1. Base de código (Codebase)

Cada aplicação tem uma única base de código, versionada, e essa base gera muitos deploys.

Desenvolvimento, homologação e produção compartilham o mesmo repositório. O que muda entre eles é a configuração e os serviços aos quais a aplicação se conecta. Quando o time mantém “uma versão do código para cada ambiente”, a divergência vira bug: o que passou no notebook não é o que subiu.

Reuso entre sistemas acontece por biblioteca ou API. Copiar uma pasta de um repositório para outro cria duas aplicações que parecem a mesma até a primeira correção de segurança.

Na prática, cada aplicação vive no próprio repositório:

```text
repos/
├── auth-api/
├── products-api/
└── web-app/
```

Um histórico único facilita integração contínua, rollback e a entrada de alguém novo no time. Sem esse alicerce, os outros onze fatores ficam frágeis: não há o que promover de um ambiente para o outro.

## 2. Dependências (Dependencies)

Tudo o que a aplicação precisa para rodar está declarado e isolado.

O manifesto — `package.json`, `requirements.txt`, `pom.xml`, `csproj` — é o contrato. Quem clona o repositório instala exatamente o conjunto de bibliotecas esperado, com versões controladas. Pacote instalado “na mão” na máquina, ou dependência que só existe porque o servidor já tinha algo global, quebra esse contrato no primeiro ambiente limpo.

Isolar dependências também reduz conflito de versão entre projetos que dividem a mesma máquina e torna a atualização uma decisão explícita, revisável no controle de versão.

## 3. Configurações (Config)

Credenciais, URLs, chaves de API e qualquer valor que mude entre ambientes ficam fora do código.

A mesma compilação sobe em desenvolvimento e em produção. O que diferencia os dois é um conjunto de variáveis de ambiente, ou um mecanismo equivalente fornecido pela plataforma. Trocar de região, de banco ou de provedor de e-mail passa a ser uma mudança de configuração, sem recompilar e sem abrir um pull request só para apontar outro host.

Há um efeito direto de segurança: segredo não entra no histórico do Git. Quem já rotacionou uma chave que estava commitada sabe o tamanho desse retrabalho.

## 4. Serviços de apoio (Backing Services)

Banco, cache, fila, armazenamento de arquivos e serviço de e-mail são recursos anexados à aplicação, acessados por URL ou por configuração.

A aplicação fala com um Postgres. Ela não precisa saber se esse Postgres está num container local, num serviço gerenciado ou num cluster de outro provedor. Trocar o recurso é trocar o endpoint. O código de acesso permanece o mesmo.

Pois é esse desacoplamento que permite testar com um serviço descartável, promover o mesmo artefato para produção e migrar de fornecedor sem reescrever a regra de negócio. Resiliência e portabilidade começam aqui: a aplicação depende de um contrato, não de uma máquina específica.

## 5. Construa, lance, execute (Build, Release, Run)

O caminho até a produção tem três etapas separadas.

No **build**, o código vira um artefato e as dependências entram nesse pacote. Na etapa do **release**, o artefato se junta à configuração daquele ambiente e ganha um identificador de versão. Executando o **run**, essa versão sobe e atende tráfego.

Quando as três etapas se misturam — compilar no servidor, ler segredo durante o build, ajustar arquivo no ambiente já em execução — ninguém consegue responder com precisão o que está no ar. Separá-las devolve rastreabilidade: o mesmo build percorre os ambientes, e só a configuração muda. Automação de pipeline fica natural, porque cada estágio tem uma entrada e uma saída claras.

## 6. Processos (Processes)

A aplicação roda como um ou mais processos sem estado local durável.

Sessão de usuário, carrinho e qualquer dado que precise sobreviver à próxima requisição moram num serviço externo: banco ou cache compartilhado. Memória do processo e disco local são efêmeros. A instância pode cair, ser substituída ou multiplicada, e o usuário continua de onde estava.

Esse desenho é o que torna a escala horizontal viável. Duas instâncias atrás de um balanceador só funcionam de verdade quando qualquer uma delas pode atender qualquer requisição.

## 7. Vínculo de porta (Port Binding)

A aplicação sobe sozinha e escuta numa porta.

Ela não espera um servidor web externo injetar o runtime para começar a responder. O processo é o servidor. Isso simplifica container, orquestração e balanceamento: a plataforma só precisa saber em qual porta o processo aceita conexões.

Autossuficiência aqui é operacional. O mesmo binário ou a mesma imagem responde em um notebook, num pipeline e num cluster, porque o contrato de rede está na própria aplicação.

## 8. Concorrência (Concurrency)

Escala é aumentar o número de processos, cada um com um papel definido.

Um tipo de processo atende HTTP. Outro consome a fila. Outro executa trabalho agendado. Quando a demanda de API cresce, sobem mais processos web. Quando a fila acumula, sobem mais consumidores. O dimensionamento segue o gargalo real, em vez de inflar um processo único que faz tudo.

Aplicações desenhadas assim acompanham o tráfego sem um redesenho a cada pico. A unidade de escala é o processo, e a plataforma — Heroku ontem, um orquestrador hoje — só multiplica essa unidade.

## 9. Descartabilidade (Disposability)

Processos começam depressa e terminam com educação.

Subida rápida encurta deploy e reação a pico. Encerramento gracioso, ao receber o sinal de término, para de aceitar trabalho novo, conclui o que já estava em andamento e libera recursos. Tarefa longa demais para caber nesse intervalo vai para uma fila, com estado guardado fora do processo.

Essa combinação é o que torna um rollout contínuo algo rotineiro. A plataforma pode matar uma instância e subir outra no lugar porque a aplicação foi feita para ser substituída. Falha deixa de ser um evento excepcional e passa a ser um caminho previsto.

## 10. Dev/prod Semelhantes (Dev/Prod Parity)

O ambiente em que o time programa se parece com o ambiente que atende o usuário.

Quanto menor a distância de tempo, de pessoas e de ferramentas entre os dois, menor a classe de bugs que “só existem em produção”. Banco com a mesma engine, mesmas versões principais de runtime, mesmos tipos de serviço de apoio. Dados e escala diferem; a forma do sistema, não.

Paridade também muda o ritmo. Quem confia que o que quebrou localmente é o que quebraria lá na frente corrige antes do merge. Pipelines de teste e deploy deixam de compensar diferenças estruturais e passam a verificar o comportamento da aplicação.

## 11. Logs (Logs)

Decerto, log é um fluxo de eventos, escrito na saída padrão.

A aplicação não abre arquivo, não rotaciona disco e não decide onde o histórico vai morar. Ela emite eventos. Outro sistema — o da plataforma, um agregador, um pipeline — coleta, armazena, indexa e alerta.

Com várias instâncias, arquivo local é um beco sem saída: cada processo tem um pedaço da história, e esse pedaço some quando o processo é descartado. Fluxo contínuo mantém o processo leve e sem estado, e entrega à operação um lugar único para diagnosticar, auditar e montar painéis.

## 12. Processos de Admin (Admin Processes)

Migração de banco, backfill, correção de dado e rotina de manutenção rodam como processos avulsos, com o mesmo código e a mesma configuração da aplicação, fora do ciclo das requisições.

Esses comandos usam a base de código da aplicação, então falam com os mesmos modelos e as mesmas bibliotecas. Eles sobem, executam uma vez e terminam. O processo que atende HTTP continua disponível enquanto a tarefa administrativa faz o trabalho dela, com rastreio e permissão próprios.

Misturar os dois — uma rota interna que dispara migração, um script solto que ninguém versiona — cria operações que ninguém consegue repetir com segurança.

---

## Como os doze se encontram

Imagine uma alteração pequena: um endpoint novo.

Ela entra num único repositório. O pipeline resolve as dependências declaradas e produz um artefato. O release combina esse artefato com as variáveis do ambiente de homologação, onde o banco e a fila são serviços anexados por URL. O processo sobe, escuta uma porta, não guarda sessão em memória e escreve log na saída padrão. Um comando de migração roda à parte, uma vez, antes do tráfego. Quando o mesmo artefato segue para produção, muda a configuração, não o build. Se a demanda cresce, a plataforma multiplica os processos. Se um deles cai, outro assume, porque nenhum deles era insubstituível.

Esse encadeamento é o método. Isolado, cada fator parece uma boa prática de checklist. Juntos, eles descrevem uma aplicação que a plataforma consegue operar: promover, escalar, substituir e observar.

## Por onde começar

A ordem da lista já é um caminho.

1. Uma base de código por aplicação, com histórico de verdade.
2. Dependências explícitas, instaláveis num ambiente limpo.
3. Configuração fora do repositório, com segredo fora do Git.
4. Banco, fila e cache tratados como recursos trocáveis.
5. Um pipeline que separe build, release e execução.

Os fatores de processo, porta, concorrência, descarte, paridade, log e administração ficam mais simples depois que esses cinco estão no lugar. Escalar um processo que guarda estado, ou agregar log de uma aplicação que escreve em arquivo local, exige desfazer decisões anteriores.

A metodologia não escolhe linguagem nem nuvem. Ela pede que a aplicação seja um artefato previsível, configurável por fora e descartável por dentro. Quem entrega software em 2026 continua esbarrando nas mesmas três perguntas de 2011: o que está rodando, com qual configuração, e o que acontece quando esse processo deixa de existir. Os doze fatores são uma forma disciplinada de responder às três.

---

### Acompanhe o Projeto no GitHub

Todavia, estou construindo uma documentação detalhada para cada um desses 12 fatores, incluindo **exemplos práticos de código**, guias de implementação e análises aprofundadas de cada princípio.

**Acesse o repositório completo e contribua:** [github.com/samorysundjata/12fatores](https://github.com/samorysundjata/12fatores)

_Texto adaptado a partir do material deste repositório, inspirado em [The Twelve-Factor App](https://12factor.net/pt_br/), de Adam Wiggins. Código e texto sob [Creative Commons Attribution 4.0](https://creativecommons.org/licenses/by/4.0/)._

**Sugestão de tags no Medium:** Software Engineering, DevOps, Cloud Computing, Software Architecture, Twelve-Factor App
