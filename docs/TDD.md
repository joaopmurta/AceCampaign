# 💻 Technical Design Document (TDD) - Vôlei Manager

## 1. Arquitetura do Sistema
Arquitetura orientada a objetos dividida em **Classes de Domínio** (dados e modelos persistentes) e **Classes de Controle** (sistemas de simulação e regras de negócio). O estado do jogo deve ser serializável (SQLite/JSON local) para suportar o design *Offline First*.

---

## 2. Classes de Domínio (Modelos de Dados)

### `Campanha` (Save Game)
* `id_campanha: String (UUID)`
* `slot: Integer` (1 a 3)
* `data_criacao: DateTime`
* `treinador_id: String`
* `banco_dados_mundo: Referencia` (Estado das outras ligas e histórico)

### `Treinador`
* `id_treinador: String (UUID)`
* `nome: String`, `genero: String`, `nacionalidade: String`
* `estilo_avatar: String`
* `experiencia_xp: Integer`
* `perspicacia: Integer`
* `reputacao: Integer`
* `energia_atual: Float` (0 a 100)
* `caixa_pessoal: Float`
* `clube_atual: Clube` (Pode ser nulo)
* `conquistas: Dicionario`
* **Métodos:** `gastar_energia(valor)`, `recarregar_energia()`, `converter_moedas_para_clube()`, `pagar_multa_rescisoria()`

### `Clube`
* `id_clube: String (UUID)`
* `nome: String`
* `is_controlado_por_jogador: Boolean`
* `orcamento: Float`
* `infraestrutura: Infraestrutura`
* `elenco: Lista<Jogadora>`
* `divisao_nacional_atual: Integer`
* `conquistas: Dicionario`
* **Métodos:** `processar_falencia()`, `vender_jogadora()`, `receber_injecao_capital()`

### `Infraestrutura`
* `arquibancadas: Integer`, `capacitacao_staff: Integer`
* `equipamentos_treino: Integer`, `equipe_medica: Integer`
* `quadra_instalacoes: Integer`, `marketing: Integer` (Todos de 0 a 100)
* **Métodos:** `calcular_nivel_geral(): Float`, `melhorar_area(tipo_area)`

### `Jogadora`
* `id_jogadora: String (UUID)`
* `nome: String`, `posicao: String` (LEV, OPO, PON, CEN, LIB)
* `atributos_base: Dicionario` (Tecnica, Forca, Agilidade, Visao, Resistencia)
* `stamina_atual: Float` (0 a 100)
* `status_fisico: String` (SAUDAVEL, FADIGADA, LESIONADA)
* `valor_passe: Float`
* `salario: Float`
* `conquistas: Dicionario`
* **Métodos:** `desgastar_stamina()`, `recuperar_stamina(nivel_medico)`, `calcular_desempenho_atual()`

---

## 3. Classes de Controle (Sistemas)

### `GerenciadorDeTemporada` (Season Manager & Simulação Global)
* `ano_atual: Integer`
* `torneios_ativos: Lista<Torneio>`
* **Métodos Principais:**
  * `avancar_calendario()`
  * `simular_ligas_ia()`: Processa os resultados e atribui títulos aos clubes não controlados pelo jogador.
  * `aplicar_envelhecimento_e_premiacoes()`

### `MercadoDeTransferencias`
* `lista_transferencias: Lista<Jogadora>`
* **Métodos Principais:**
  * `calcular_probabilidade_aceite(valor_ofertado, valor_pedido, nivel_clube, reputacao_treinador)`
  * `gerar_evento_multa_paga(clube_jogador)`: IA tenta comprar jogadora do jogador abruptamente.

### `Torneio`
* `id_torneio: String`
* `tipo: String` (SUPERLIGA, COPA, INTERCONTINENTAL, MUNDIAL)
* `formato: String` (PONTOS_CORRIDOS, MATA_MATA)
* `clubes_inscritos: Lista<Clube>`
* **Métodos:** `gerar_tabela()`, `processar_fase_mata_mata()`

### `MotorDePartida` (Match Engine)
* `time_casa: Clube`, `time_visitante: Clube`
* `placar_sets: Dicionario`
* `estatisticas_individuais: Dicionario` (Acompanha pontos de Atq/Blq/Saq por jogadora)
* **Métodos Principais:**
  * `validar_formacao_obrigatoria()`: Checa a regra dos 7 em quadra e posições.
  * `simular_bloco_pontos()`: Calcula probabilidade e atribui os pontos do bloco a jogadoras específicas em tempo real ($O(N)$ leve).
  * `verificar_limites_interrupcao()`: Controla os desafios e tempos técnicos (2 por set).
  * `invocar_minigame_cartas()`: Pausa o bloco de pontos e apresenta 3 cartas de buff/debuff temporário ao jogador.
  * `disparar_evento_texto()`: Chama avisos como lesão e inversões.
