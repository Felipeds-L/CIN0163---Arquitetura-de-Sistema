# ADR 003: Gestão de Transações Distribuídas via Saga Pattern

*   **Status:** Aceita
*   **Data:** 29-04-2026
*   **Decisores:** Nathan Barbosa, Breno Augusto Ferreira, Hugo Coelho, Felipe Leite, Carlos Eduardo Teixeira, Vinicius Lidington, Guilherme Campelo

## Contexto e Problema
* Em um ambiente de microsserviços com bancos de dados independentes, não é possível utilizar transações ACID globais para garantir que um saldo jamais fique inconsistente durante uma transferência entre contas.

## Alternativas Consideradas
* Transação ACID Global (2PC): Descartada pois locks distribuídos causam contenção severa sob alta concorrência.

## Decisão
* Adoção do Saga Pattern para gerenciar transações distribuídas. O processo é tratado como uma sequência de transações locais (ex: 1. Debita A -> 2. Credita B) com compensação automática (estorno) em caso de falha em qualquer etapa.

## Consequências
*   **Positivas:** Permite transações sem lock global, garantindo escala sem contenção e recuperação de erros através de compensações.
*   **Negativas/Riscos:** Implementação complexa; as funções de compensação devem estar perfeitamente corretas e é difícil testar casos de borda (edge cases).
