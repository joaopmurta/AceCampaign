# Diagrama Entidade-Relacionamento (DER) - Base de Dados

Este diagrama ilustra a estrutura das tabelas na base de dados relacional (SQLite) para guardar o estado do jogo localmente no dispositivo (Offline First).

```mermaid
erDiagram
    %% Relacionamentos do Mundo do Jogo (Isolamento por Campanha)
    CAMPANHA ||--|| TREINADOR : "possui"
    CAMPANHA ||--|{ CLUBE : "contem estado de"
    CAMPANHA ||--|{ JOGADORA : "contem estado de"
    CAMPANHA ||--|{ TORNEIO : "contem"

    %% Relacionamentos de Negócio
    CLUBE ||--o| TREINADOR : "emprega"
    CLUBE ||--|| INFRAESTRUTURA : "possui"
    CLUBE ||--|{ JOGADORA : "contrata"

    %% Relacionamento Muitos-para-Muitos resolvido com Tabela de Juncao
    CLUBE }|--|{ CLUBE_TORNEIO : "disputa"
    TORNEIO ||--|{ CLUBE_TORNEIO : "agrega"

    %% Tabelas e Atributos
    CAMPANHA {
        string id PK
        int slot
        datetime data_criacao
    }

    TREINADOR {
        string id PK
        string campanha_id FK
        string clube_id FK
        string nome
        float energia_atual
        float caixa_pessoal
        int reputacao
    }

    CLUBE {
        string id PK
        string campanha_id FK
        string nome
        float orcamento
        int divisao_nacional
        boolean is_controlado_por_jogador
    }

    INFRAESTRUTURA {
        string id PK
        string clube_id FK
        int ct
        int marketing
        int staff
        int equipamentos
    }

    JOGADORA {
        string id PK
        string campanha_id FK
        string clube_id FK
        string nome
        string posicao
        int tecnica
        int forca
        int agilidade
        int visao
        int resistencia
        float stamina_atual
        string status_fisico
        float salario
        float valor_passe
    }

    TORNEIO {
        string id PK
        string campanha_id FK
        string tipo
        int ano_edicao
    }

    CLUBE_TORNEIO {
        string clube_id FK
        string torneio_id FK
        string fase_alcancada
    }
