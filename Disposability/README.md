# Disposability (Descartabilidade)

No contexto dos [12 Fatores](https://12factor.net/pt_br/), **Disposability** refere-se à capacidade de um aplicativo ser iniciado e finalizado rapidamente, de forma limpa e previsível. Isso significa que os processos do aplicativo devem ser efêmeros, ou seja, podem ser descartados a qualquer momento sem causar inconsistências ou perda de dados.

## Princípios

- **Inicialização rápida:** O aplicativo deve iniciar rapidamente, permitindo escalabilidade e deploys ágeis.
- **Encerramento gracioso:** O processo deve responder corretamente a sinais de término, liberando recursos e finalizando tarefas pendentes.
- **Tolerância a falhas:** O aplicativo deve lidar bem com encerramentos inesperados, garantindo que operações críticas sejam concluídas ou revertidas.

## Benefícios

- **Escalabilidade:** Facilita o aumento ou diminuição de instâncias conforme a demanda.
- **Resiliência:** Reduz o risco de corrupção de dados e facilita a recuperação de falhas.
- **Deploy contínuo:** Permite atualizações frequentes e seguras.

## Recomendações

- Use filas para tarefas demoradas.
- Garanta que o estado do aplicativo seja armazenado fora do processo (por exemplo, bancos de dados ou sistemas de cache).
- Implemente tratamento adequado para sinais de término (SIGTERM, SIGINT).

> Disposability é essencial para aplicações modernas, promovendo robustez, flexibilidade e facilidade de manutenção.
