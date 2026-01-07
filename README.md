# 12 Fatores: Desenvolvendo Apps Modernos e Escaláveis

Este repositório tem como objetivo apresentar, explicar e demonstrar os [12 Fatores](https://12factor.net/pt_br/), uma metodologia para construção de aplicações modernas, escaláveis e de fácil manutenção.

O The Twelve-Factor App ou 12 Fatores é uma metodologia criada para auxiliar no desenvolvimento de aplicações web modernas, especialmente aquelas voltadas para o modelo de Software como Serviço (SaaS). Ela oferece um conjunto de 12 princípios que visam otimizar o desenvolvimento, a implantação e a escalabilidade dessas aplicações, garantindo portabilidade entre diferentes ambientes de execução. Ao adotar essa metodologia, as equipes de desenvolvimento podem reduzir custos, simplificar a integração de novos membros e facilitar a implantação em plataformas de nuvem, como AWS, Google Cloud e Heroku, por exemplo.

Sendo assim, a metodologia foi criada para atender às demandas das aplicações web contemporâneas, que exigem alta escalabilidade, agilidade no desenvolvimento e portabilidade entre ambientes. Os 12 fatores foram definidos com base em experiências práticas e nas melhores práticas da indústria, servindo como um guia para a construção de aplicações robustas, fáceis de manter e adequadas para a nuvem. Ao seguir esses princípios, as equipes podem garantir que suas aplicações sejam flexíveis, escaláveis e prontas para o mercado atual.

## Contexto e Criação

O The Twelve-Factor App surgiu em 2011, em um contexto de crescente popularização da computação em nuvem e da necessidade de aplicações web altamente escaláveis. A metodologia foi formalizada por Adam Wiggins, um dos fundadores da Heroku, uma plataforma de nuvem que permite a implantação e o gerenciamento de aplicações. A ideia era criar um padrão que garantisse que as aplicações fossem facilmente implantadas, escaladas e mantidas na infraestrutura da Heroku, mas que também fosse aplicável a outras plataformas de nuvem.

12 FatoresPor isso, a metodologia foi desenvolvida com base em desafios reais enfrentados por equipes de desenvolvimento, como a dificuldade de manter consistência entre ambientes de desenvolvimento e produção, a complexidade na gestão de configurações e a necessidade de escalabilidade em aplicações modernas. Os 12 fatores foram criados para resolver esses problemas, oferecendo diretrizes claras e práticas para a construção de aplicações que funcionam bem em ambientes de nuvem.

## Quais são os 12 Fatores então?

Os doze fatores do The Twelve-Factor App são diretrizes para a construção de aplicações web escaláveis, portáteis e fáceis de manter. Aqui estão os doze fatores:

1. [**Base de código (Codebase)**](Codebase/README.md)

Este é o alicerce fundamental de uma aplicação. Cada aplicação deve possuir uma única base de código versionada, normalmente armazenada em sistemas de controle de versão como o Git. Essa base é compartilhada entre todos os ambientes — desenvolvimento, homologação, staging e produção — o que garante consistência, rastreabilidade e controle das mudanças aplicadas em cada etapa. A separação entre ambientes não deve significar múltiplas bases de código, mas sim múltiplos deploys da mesma codebase.

Manter uma única base de código evita divergências e reduz o risco de bugs que surgem de inconsistências entre ambientes. Reutilização de funcionalidades deve ser feita através de bibliotecas ou APIs, não pela duplicação de código. Armazenar o repositório em plataformas como GitHub é uma prática comum e recomendada, pois centraliza a gestão do código, facilita a colaboração entre equipes e torna mais eficiente o controle de versões. Essa abordagem fortalece a disciplina de entrega contínua e alinhamento com boas práticas de engenharia de software.

2. **Dependências (Dependencies)**

Declare explicitamente todas as dependências do projeto, especificando as bibliotecas, pacotes e componentes externos que a aplicação necessita para funcionar corretamente. Essas dependências devem ser isoladas e gerenciadas de forma consistente, utilizando arquivos específicos de manifesto como package.json, requirements.txt, pom.xml ou csproj. Isso garante que o ambiente da aplicação seja previsível e replicável em qualquer máquina ou servidor, evitando surpresas por falta de pacotes ou incompatibilidades de versões.

Manter as dependências declaradas de forma explícita facilita a instalação, manutenção e atualização dos pacotes, contribuindo para a portabilidade e escalabilidade do sistema. Além disso, evita que bibliotecas sejam instaladas globalmente ou de maneira implícita, o que pode gerar conflitos e problemas de versionamento. Ferramentas de gerenciamento de dependências permitem controlar versões usadas entre desenvolvimento, testes e produção, realizar atualizações seguras e garantir maior segurança e estabilidade do software.

3. **Configurações (Config)**

As configurações da aplicação devem ser armazenadas separadamente do código-fonte, geralmente em variáveis de ambiente ou arquivos externos que não façam parte do repositório de código. Isso inclui informações específicas do ambiente, como credenciais, URLs de serviços, chaves de API e parâmetros que podem variar entre desenvolvimento, teste e produção. Manter essas configurações fora do código permite que a mesma base de código seja utilizada em múltiplos ambientes apenas alterando seus dados de configuração.

Essa separação aumenta a segurança, evitando que dados sensíveis sejam expostos no controle de versão, e facilita o gerenciamento e a automação dos ambientes, permitindo que as configurações sejam alteradas sem necessidade de recompilar ou modificar o código. Além disso, favorece a portabilidade da aplicação, pois configurações específicas ficam isoladas, tornando simples a migração entre servidores ou provedores de nuvem.

4. **Serviços de apoio (Backing Services)**

Os serviços de apoio, como bancos de dados, sistemas de cache, filas de mensagens e provedores de armazenamento, devem ser tratados como recursos anexáveis, acessados por meio de URLs ou endpoints configuráveis. Isso significa que esses serviços podem ser facilmente adicionados, substituídos ou removidos sem alterar o código da aplicação, permitindo maior flexibilidade e escalabilidade.

Tratar esses serviços como recursos externos desacopla a aplicação das infraestruturas específicas, facilitando migrações, testes e atualizações. Além disso, essa abordagem promove ambientes mais resilientes e portáveis, onde a conexão com serviços de apoio pode ser configurada dinamicamente conforme o ambiente, garantindo que a aplicação funcione de forma consistente independentemente do local onde está executando.

5. **Gerar, subir, executar (Build, Release, Run)**

O processo de gerar, subir e executar a aplicação deve ser rigorosamente separado em três etapas distintas: build, release e run. Na etapa de build, o código-fonte é transformado em um pacote executável e todas as dependências são resolvidas e incorporadas. Na fase de release, esse pacote é combinado com as configurações específicas do ambiente para formar uma versão pronta para ser executada. Por fim, na etapa de run, essa versão é executada em um ambiente de produção ou outro ambiente designado.

Essa separação garante controle e previsibilidade em cada fase do ciclo de vida da aplicação, facilitando a automação e a rastreabilidade das versões. Além disso, ao manter as configurações separadas do build, permite que a mesma compilação seja promovida entre diferentes ambientes apenas alterando os dados de configuração, aumentando a portabilidade e reduzindo riscos de inconsistências durante a implantação.

6. **Processos (Processes)**

A aplicação deve ser executada como um ou mais processos stateless (sem estado), o que significa que nenhuma informação do estado do usuário ou da aplicação deve ser armazenada localmente na memória ou no sistema de arquivos entre as requisições. Qualquer dado persistente precisa ser armazenado em serviços externos, como bancos de dados ou caches compartilhados.

Essa abordagem permite que múltiplas instâncias da aplicação sejam executadas em paralelo, facilitando a escalabilidade horizontal e a tolerância a falhas. Como os processos não mantêm estado, eles podem ser iniciados, interrompidos ou substituídos a qualquer momento sem afetar a continuidade do serviço, garantindo maior flexibilidade e resiliência.

7. **Vinculação de portas (Port Binding)**

A aplicação deve ser autossuficiente e expor seus serviços por meio da vinculação direta a uma porta TCP, tornando-se um servidor que escuta e responde a requisições HTTP, por exemplo. Dessa forma, ela não depende de servidores web externos para funcionar, facilitando o controle e a implantação do serviço.

Essa abordagem torna a aplicação portátil e independente do ambiente em que está executando, permitindo que seja facilmente containerizada, escalada e gerenciada. Além disso, ao expor sua interface por uma porta específica, ela se integra melhor com sistemas de orquestração, balanceamento de carga e infraestrutura em nuvem.

8. **Concorrência (Concurrency)**

A aplicação deve ser projetada para suportar múltiplos processos concorrentes que possam ser escalados horizontalmente, permitindo distribuir a carga de trabalho entre várias instâncias. Cada processo deve ser capaz de executar uma ou mais funções específicas (como lidar com requisições web, processar tarefas em background ou consumir filas), possibilitando a organização da aplicação em diferentes tipos de trabalhadores.

Essa abordagem facilita o dimensionamento dinâmico conforme a demanda, aumentando a capacidade de resposta e a resiliência do sistema. Ao dividir o trabalho em processos independentes e escaláveis, a aplicação pode se adaptar a diferentes volumes de tráfego e manter a estabilidade mesmo sob alta carga.

9. [**Descarte (Disposability)**](Disposability/README.md)

A aplicação deve ser construída para iniciar e parar rapidamente, garantindo agilidade tanto no escalonamento quanto na recuperação de falhas. Processos que desligam rapidamente minimizam o tempo de inatividade e facilitam a manutenção, como implantações contínuas e atualizações sem impacto perceptível para o usuário.

Essa capacidade de descarte rápido aumenta a resiliência do sistema, permitindo que instâncias sejam reiniciadas ou substituídas com facilidade em caso de erro, sem comprometer a estabilidade geral da aplicação. Além disso, processos descartáveis facilitam a automação e o gerenciamento eficiente dos recursos em ambientes escaláveis e dinâmicos.

10. **Paridade entre desenvolvimento e produção (Dev/Prod Parity)**

É fundamental manter a paridade entre os ambientes de desenvolvimento, teste e produção, reduzindo ao máximo as diferenças entre eles em termos de software, configuração, banco de dados e dependências. Quanto mais semelhantes forem esses ambientes, menores serão os riscos de bugs e falhas que só aparecem após a implantação.

Manter essa consistência acelera o ciclo de desenvolvimento e entrega, pois problemas detectados durante o desenvolvimento tendem a ser os mesmos que ocorreriam em produção, facilitando a correção antecipada. Além disso, ambientes alinhados promovem maior confiança na qualidade da aplicação e simplificam a automação dos processos de build, teste e deploy.

11. **Registros (Logs)**

A aplicação deve tratar os registros (logs) como fluxos de eventos que são enviados para um sistema de captura externo, em vez de gravá-los em arquivos locais ou armazenamento interno. Dessa forma, os logs podem ser agregados, monitorados e analisados de maneira centralizada, facilitando a detecção de problemas e o diagnóstico de falhas.

Ao enviar os logs para serviços externos ou pipelines de processamento, a aplicação permanece stateless e mais leve, além de possibilitar a criação de dashboards, alertas e auditorias em tempo real. Essa abordagem também melhora a escalabilidade e a manutenção, pois não depende de recursos locais que podem variar entre instâncias ou ambientes.

12. **Administração de processos (Admin Processes)**

Tarefas administrativas, como migrações de banco de dados, scripts de manutenção, backups e outros comandos de gerenciamento, devem ser executadas como processos únicos, isolados da execução principal da aplicação. Esses processos são invocados manualmente ou por meio de scripts automatizados, garantindo que suas operações não interfiram no funcionamento contínuo do sistema.

Manter esses processos separados facilita a manutenção e o controle, além de permitir maior segurança e previsibilidade nas operações administrativas. Dessa forma, as tarefas de gerenciamento podem ser executadas de forma controlada, sem impactar a disponibilidade ou a performance da aplicação em produção.

> Inspirado em [12factor.net](https://12factor.net/pt_br/)

## Licença

- Código-fonte: Creative Commons Attribution 4.0 International (CC BY 4.0). Veja o arquivo [LICENSE](./LICENSE) para detalhes.
<!-- - Documentação e textos explicativos: Creative Commons Attribution 4.0 International (CC BY 4.0). Veja [LICENSE_DOC](./LICENSE_DOC) para detalhes. -->
