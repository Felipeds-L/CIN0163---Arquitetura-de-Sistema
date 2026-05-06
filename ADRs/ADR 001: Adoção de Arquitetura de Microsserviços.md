# ADR 001: Adoção de Arquitetura de Microsserviços

*   Status: Aceita
*   Data: 06-05-2026
*   Decisores: Nathan Barbosa, Breno Augusto Ferreira, Hugo Coelho, Felipe Leite, Carlos Eduardo Teixeira, Vinicius Lidington, Guilherme Campelo

## Contexto e Problema

* Um sistema bancário moderno exige alta disponibilidade (24x7x365) e precisa gerenciar múltiplas funções (contas, transferências, antifraude) simultaneamente. O sistema não pode depender de um único servidor ou base de dados, pois a falha de um módulo não deve derrubar todo o ecossistema.


## Alternativas Consideradas
*   Monólito Tradicional (Layered): Descartado por apresentar acoplamento alto e escalabilidade limitada por módulo.
*   SOA Tradicional: Descartado devido ao overhead de um ESB centralizado, que cria pontos únicos de falha.

## Decisão
* A escolha foi pela Arquitetura de Microsserviços. O sistema é dividido em serviços independentes (Conta, Transferência, Autenticação, etc.), cada um com seu próprio deploy, banco de dados e escalabilidade.

## Consequências
*   **Positivas:** Positivas: Escala independente por módulo, isolamento de falhas e suporte a deploy contínuo.
*   **Negativas/Riscos:** Negativas/Riscos: Alta complexidade operacional, necessidade obrigatória de cultura DevOps e maior esforço em observabilidade.
