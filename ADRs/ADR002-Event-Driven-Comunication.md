# ADR 002: Comunicação Assíncrona Baseada em Eventos (Event-Driven)

*   **Status:** Aceita
*   **Data:** 29-04-2026
*   **Decisores:** Nathan Barbosa, Breno Augusto Ferreira, Hugo Coelho, Felipe Leite, Carlos Eduardo Teixeira, Vinicius Lidington, Guilherme Campelo

## Contexto e Problema
* Para garantir a resiliência e o alto throughput necessários para milhares de transações simultâneas, os serviços precisam interagir sem criar dependências de tempo real que possam gerar gargalos.

## Alternativas Consideradas
* Chamadas REST Síncronas: Evitadas para a comunicação core entre serviços para prevenir o acoplamento temporal e falhas em cascata.

## Decisão
* Implementação de uma Arquitetura Orientada a Eventos (Event-Driven) utilizando um Event Bus (Kafka ou RabbitMQ). Os serviços se comunicam via eventos como TransferCreated e BalanceUpdated.

## Consequências
*   **Positivas:** Desacoplamento total entre produtor e consumidor, alta resiliência a picos de carga e alto throughput.
*   **Negativas/Riscos:** Consistência eventual dos dados, depuração (debug) mais complexa e a necessidade crítica de garantir a ordenação dos eventos.