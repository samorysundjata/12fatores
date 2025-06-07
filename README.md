# 12 Fatores: Desenvolvendo Apps Modernos e Escaláveis

Este repositório tem como objetivo apresentar, explicar e demonstrar os [12 Fatores](https://12factor.net/pt_br/), uma metodologia para construção de aplicações modernas, escaláveis e de fácil manutenção.

O The Twelve-Factor App ou 12 Fatores é uma metodologia criada para auxiliar no desenvolvimento de aplicações web modernas, especialmente aquelas voltadas para o modelo de Software como Serviço (SaaS). Ela oferece um conjunto de 12 princípios que visam otimizar o desenvolvimento, a implantação e a escalabilidade dessas aplicações, garantindo portabilidade entre diferentes ambientes de execução. Ao adotar essa metodologia, as equipes de desenvolvimento podem reduzir custos, simplificar a integração de novos membros e facilitar a implantação em plataformas de nuvem, como AWS, Google Cloud e Heroku, por exemplo.

## O que são os 12 Fatores?

O The Twelve-Factor App ou 12 Fatores é uma metodologia criada para auxiliar no desenvolvimento de aplicações web modernas, especialmente aquelas voltadas para o modelo de Software como Serviço (SaaS). Ela oferece um conjunto de 12 princípios que visam otimizar o desenvolvimento, a implantação e a escalabilidade dessas aplicações, garantindo portabilidade entre diferentes ambientes de execução. Ao adotar essa metodologia, as equipes de desenvolvimento podem reduzir custos, simplificar a integração de novos membros garantir portabilidade, resiliência e facilitar a implantação em ambientes na nuvem.

## Contexto e Criação

O The Twelve-Factor App surgiu em 2011, em um contexto de crescente popularização da computação em nuvem e da necessidade de aplicações web altamente escaláveis. A metodologia foi formalizada por Adam Wiggins, um dos fundadores da Heroku, uma plataforma de nuvem que permite a implantação e o gerenciamento de aplicações. A ideia era criar um padrão que garantisse que as aplicações fossem facilmente implantadas, escaladas e mantidas na infraestrutura da Heroku, mas que também fosse aplicável a outras plataformas de nuvem.

Por isso, a metodologia foi desenvolvida com base em desafios reais enfrentados por equipes de desenvolvimento, como a dificuldade de manter consistência entre ambientes de desenvolvimento e produção, a complexidade na gestão de configurações e a necessidade de escalabilidade em aplicações modernas. Os 12 fatores foram criados para resolver esses problemas, oferecendo diretrizes claras e práticas para a construção de aplicações que funcionam bem em ambientes de nuvem.

## Então quais são os 12 Fatores?

São diretrizes para a construção de aplicações web escaláveis, portáteis e fáceis de manter. Aqui estão:

1. **Base de código (Codebase)**

Descrição: Colocar todo o código em um sistema de controle de versão, como Git ou Mercurial.

Objetivo: Manter o código organizado e rastreável.

2. **Dependências (Dependencies)**

Descrição: Declarar explicitamente todas as dependências necessárias para a aplicação.

Objetivo: Evitar conflitos de versão e garantir que a aplicação funcione corretamente em diferentes ambientes.

3. **Configurações (Config)**

Descrição: Armazenar configurações em variáveis de ambiente, em vez de arquivos específicos do ambiente.

Objetivo: Facilitar a alteração de configurações sem modificar o código.

4. **Serviços de apoio (Backing Services)**

Descrição: Tratar serviços de apoio (como bancos de dados e filas de mensagens) como recursos anexados.

Objetivo: Permitir a troca fácil entre diferentes provedores de serviços.

5. **Gerar, subir, executar (Build, Release, Run)**

Descrição: Separar as fases de build, release e run para garantir que cada uma seja independente.

Objetivo: Automatizar o processo de implantação e garantir a consistência.

6. **Processos(Processes)**

Descrição: Executar a aplicação como processos stateless (sem estado) que não armazenam dados persistentes.

Objetivo: Garantir escalabilidade e flexibilidade.

7. **Vinculação de portas(Port Binding)**

Descrição: Fazer com que a aplicação seja um serviço independente, não dependendo de um servidor de aplicativos.

Objetivo: Facilitar a implantação em diferentes ambientes.

8. **Concorrência (Concurrency)**

Descrição: Utilizar múltiplos processos para alcançar concorrência e escalabilidade horizontal.

Objetivo: Maximizar a capacidade de processamento sem limitações de hardware.

9. **Descarte (Disposability)**

Descrição: Garantir que os processos sejam iniciados e parados rapidamente, minimizando o tempo de inatividade.

Objetivo: Reduzir erros e melhorar a disponibilidade. [link](Disposability.md)

10. **Paridade entre desenvolvimento e produção (Dev/Prod Parity)**

Descrição: Manter o ambiente de desenvolvimento e produção o mais semelhante possível.

Objetivo: Reduzir a divergência entre desenvolvimento e produção.

11. **Registros (Logs)**

Descrição: Tratar logs como fluxos de eventos que devem ser coletados e processados por serviços externos. A palavra “log” vem de uma abreviação de “logbook”, que em inglês naval era o diário de bordo.

Objetivo: Facilitar o monitoramento e a análise.

12. **Administração de processos (Admin Processes)**

Descrição: Executar tarefas administrativas como processos separados, sem afetar o funcionamento da aplicação.

Objetivo: Manter a estabilidade e a segurança da aplicação durante atualizações ou manutenção.

> Inspirado em [12factor.net](https://12factor.net/pt_br/)

## Licença

Este projeto está licenciado sob a [Licença MIT](./LICENSE).
