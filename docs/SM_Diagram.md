# Diagrama de Máquina de Estados - Motor de Partida

Este diagrama mapeia o fluxo de execução e as transições de estado do Motor de Partida (Match Engine) durante um jogo. O uso de blocos de pontos e interrupções exige um controle rigoroso de estado para evitar conflitos na interface.

```mermaid
stateDiagram-v2
    %% Definição de Estados Iniciais e Finais
    [*] --> PreparacaoPreJogo

    %% Fluxo de Preparação
    state PreparacaoPreJogo {
        [*] --> ValidarEnergiaTreinador
        ValidarEnergiaTreinador --> ValidarFormacaoObrigatoria
        ValidarFormacaoObrigatoria --> [*] : 7 titulares (incluindo Líbero) definidos
    }

    PreparacaoPreJogo --> InicioSet : Iniciar Partida

    %% Loop Principal do Set
    InicioSet --> SimulacaoBlocoPontos : Reinicia placar do set e stamina local

    state SimulacaoBlocoPontos {
        [*] --> CalculoProbabilidade
        CalculoProbabilidade --> AtribuicaoEstatisticas
        AtribuicaoEstatisticas --> [*] : Placar atualizado (Ex: +3 pts Casa, +1 pt Visitante)
    }

    SimulacaoBlocoPontos --> AnalisePosBloco : Fim do cálculo do bloco

    %% Ponto de Decisão (Bifurcação / Fork)
    state AnalisePosBloco <<choice>>

    %% Condições de Interrupção da Simulação
    AnalisePosBloco --> EventoTexto : RNG ativou evento (Lesão, Desafio)
    AnalisePosBloco --> MinigameCartas : RNG ativou cartas (Buff/Debuff)
    AnalisePosBloco --> PausaTatica : Jogador interveio (Tempo/Substituição)
    AnalisePosBloco --> VerificacaoFimDeSet : Nenhuma interrupção, checar pontuação

    %% Retorno das Interrupções para o Loop
    EventoTexto --> VerificacaoFimDeSet : Decisão tomada ou Tempo Esgotado
    MinigameCartas --> VerificacaoFimDeSet : Carta selecionada
    PausaTatica --> VerificacaoFimDeSet : Alterações confirmadas

    %% Lógica de Fim de Set e Partida
    state VerificacaoFimDeSet <<choice>>
    VerificacaoFimDeSet --> FimDeSet : Condição de vitória do set atingida (25 ou 15 pts + 2 de vantagem)
    VerificacaoFimDeSet --> SimulacaoBlocoPontos : Set continua

    FimDeSet --> AnaliseFimPartida : Time venceu o set

    state AnaliseFimPartida <<choice>>
    AnaliseFimPartida --> FimDePartida : Algum time venceu 2 sets (Melhor de 3)
    AnaliseFimPartida --> InicioSet : Próximo set necessário (Troca de Lados)

    %% Encerramento e Pós-Jogo
    FimDePartida --> ProcessamentoPosJogo

    state ProcessamentoPosJogo {
        [*] --> DistribuirXP_Moedas
        DistribuirXP_Moedas --> AplicarFadigaGlobal
        AplicarFadigaGlobal --> AtualizarConquistas
        AtualizarConquistas --> [*]
    }

    ProcessamentoPosJogo --> [*] : Retornar ao Menu Principal
