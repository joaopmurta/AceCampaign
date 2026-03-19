---

### 2. Diagrama de Banco de Dados / DER Atualizado (`DER.md`)

Como o jogo usará SQLite (relacional), transformar aquele "Dicionário" em colunas reais na tabela `JOGADORA` é a melhor prática. Isso permite que você faça buscas rápidas no código, como: *"Me traga todas as jogadoras disponíveis no mercado que tenham Força maior que 80"*.

Substitua seu arquivo do DER por este:

```markdown
# Diagrama Entidade-Relacionamento (DER) - Base de Dados

Este diagrama ilustra a estrutura das tabelas na base de dados relacional (SQLite) para guardar o estado do jogo localmente no dispositivo (*Offline First*).

```mermaid
erDiagram
    %% Relacionamentos do Mundo do Jogo (Isolamento por Campanha)
    CAMPANHA ||--|| TREINADOR : "possui (1:1)"
    CAMPANHA ||--|{ CLUBE : "contém estado de (1:N)"
    CAMPANHA ||--|{ JOGADORA : "contém estado de (1:N)"
    CAMPANHA ||--|{ TORNEIO : "contém (1:N)"

    %% Relacionamentos de Negócio
    CLUBE ||--o| TREINADOR : "emprega (1:0..1)"
    CLUBE ||--|| INFRAESTRUTURA : "possui (1:1)"
    CLUBE ||--|{ JOGADORA : "contrata (1:N)"

    %% Relacionamento Muitos-para-Muitos resolvido com Tabela de Junção
    CLUBE }|--|{ CLUBE_TORNEIO : "disputa"
    TORNEIO ||--|{ CLUBE_TORNEIO : "agrega"

    %% Tabelas e Atributos
    CAMPANHA {
        string id PK
        int slot "1 a 3"
        datetime data_criacao
    }

    TREINADOR {
        string id PK
        string campanha_id FK
        string clube_id FK "Pode ser nulo"
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
        string clube_id FK "Nulo se agente livre"
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

    %% Tabela de Junção (Registo de histórico e participação)
    CLUBE_TORNEIO {
        string clube_id FK
        string torneio_id FK
        string fase_alcancada "Ex: Final, Quartos, Campeão"
    }
