# ADR 003: Gestão de Transações Distribuídas via Saga Pattern

*   **Status:** Aceita
*   **Data:** 29-04-2026
*   **Decisores:** Nathan Barbosa, Breno Augusto Ferreira, Hugo Coelho, Felipe Leite, Carlos Eduardo Teixeira, Vinicius Lidington, Guilherme Campelo

## Contexto e Problema
* O sistema precisa de alta performance tanto em operações de escrita (transferir, depositar) quanto de leitura (consultar saldo, extratos). Além disso, o núcleo do negócio (regras de débito/crédito) deve ser protegido de mudanças tecnológicas em bancos de dados ou protocolos de comunicação.

## Alternativas Consideradas
* Modelo de Dados Único: Descartado por não permitir otimização específica para leitura e escrita simultaneamente.
* Arquitetura em Camadas (Layered): Descartada para evitar que a lógica de negócio dependesse diretamente de frameworks ou drivers de DB.

## Decisão
* Adotou-se CQRS para separar modelos de escrita (Commands) e leitura (Queries). Complementarmente, usa-se Arquitetura Hexagonal internamente em cada serviço, isolando a Regra de Negócio através de Adapters (REST, Kafka, DB).

## Consequências
*   **Positivas:** Leitura extremamente performática, regra de negócio isolada da tecnologia e modelos otimizados por caso de uso.
*   **Negativas/Riscos:** Duplicação de modelos de dados, necessidade de sincronização entre escrita e leitura e maior volume de código (surface) para manter.