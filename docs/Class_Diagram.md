# Diagrama de Classes - Vôlei Manager

Abaixo está o diagrama de classes do sistema, modelado com base na arquitetura definida no TDD. O GitHub renderiza este diagrama automaticamente usando Mermaid.js.

```mermaid
classDiagram
    %% Relacionamentos
    Campanha "1" *-- "1" Treinador : possui
    Treinador "0..1" -- "1" Clube : gerencia
    Clube "1" *-- "1" Infraestrutura : contem
    Clube "1" o-- "10..14" Jogadora : elenco
    GerenciadorDeTemporada "1" --> "*" Torneio : organiza
    Torneio "*" o-- "*" Clube : inscritos
    MotorDePartida --> "2" Clube : casa / visitante
    MercadoDeTransferencias "1" o-- "*" Jogadora : lista_disponiveis

    %% Classes de Domínio
    class Campanha {
        +UUID id_campanha
        +Int slot
        +DateTime data_criacao
        +salvar_progresso()
        +carregar_progresso()
    }

    class Treinador {
        +UUID id_treinador
        +String nome
        +Float energia_atual
        +Float caixa_pessoal
        +Int reputacao
        +gastar_energia(valor)
        +recarregar_energia()
        +pagar_multa_rescisoria()
    }

    class Clube {
        +UUID id_clube
        +String nome
        +Float orcamento
        +Int divisao_nacional
        +processar_falencia()
        +vender_jogadora(jogadora)
    }

    class Infraestrutura {
        +Int arquibancadas
        +Int equipe_medica
        +Int quadra_instalacoes
        +Int marketing
        +calcular_nivel_geral() Float
        +melhorar_area(tipo)
    }

    class Jogadora {
        +UUID id_jogadora
        +String nome
        +String posicao
        +Float stamina_atual
        +String status_fisico
        +Float valor_passe
        +desgastar_stamina()
        +recuperar_stamina(nivel_medico)
    }

    %% Classes de Controle
    class GerenciadorDeTemporada {
        +Int ano_atual
        +avancar_calendario()
        +simular_ligas_ia()
        +aplicar_envelhecimento()
    }

    class MotorDePartida {
        +Dict placar_sets
        +validar_formacao_obrigatoria()
        +simular_bloco_pontos()
        +invocar_minigame_cartas()
        +disparar_evento_texto()
    }

    class MercadoDeTransferencias {
        +calcular_probabilidade_aceite()
        +gerar_evento_multa_paga()
    }

    class MercadoDeTransferencias {
        +calcular_probabilidade_aceite()
        +gerar_evento_multa_paga()
    }
