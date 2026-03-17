# 💻 Technical Design Document (TDD) - Vôlei Manager

## 1. Arquitetura do Sistema
O jogo utilizará uma arquitetura orientada a objetos com separação clara entre **Classes de Domínio** (dados físicos como Jogadoras, Clubes e Infraestrutura) e **Classes de Controle** (sistemas que gerenciam regras, como Temporadas, Torneios e o Motor da Partida).

---

## 2. Classes de Domínio (Modelos de Dados)

### `Treinador`
* `id_treinador: String (UUID)`
* `nome: String`
* `nacionalidade: String`
* `experiencia_xp: Integer`
* `perspicacia: Integer`
* `gerenciamento: Integer`
* `clube_atual: Clube` (Pode ser nulo)
* `caixa_pessoal: Float`
* `conquistas: Dicionario` (Ex: {"trofeus": 2, "ouro": 2, "prata": 0, "bronze": 1})

### `Clube`
* `id_clube: String (UUID)`
* `nome: String`
* `orcamento: Float`
* `infraestrutura: Infraestrutura` (Objeto aninhado detalhado abaixo)
* `elenco: Lista<Jogadora>`
* `divisao_nacional_atual: Integer` (1 para Liga A, 2 para Liga B)
* `conquistas: Dicionario`

### `Infraestrutura`
Controla o nível das instalações do clube. Cada atributo vai de 0 a 100. O nível geral do clube é a média desses 5 pilares, começando por volta de 10% em clubes menores.
* `arquibancadas: Integer` (Aumenta receita de bilheteria)
* `capacitacao_staff: Integer` (Aumenta a eficiência geral do clube)
* `equipamentos_treino: Integer` (Aumenta a eficácia dos treinos das jogadoras)
* `equipe_medica: Integer` (Reduz chance de lesão e acelera recuperação)
* `quadra_instalacoes: Integer` (Piso, iluminação, vestiários; atrai mais público e moral)
* **Método:** `calcular_nivel_geral(): Float` (Retorna a média máxima de 100%)

### `Jogadora`
* `id_jogadora: String (UUID)`
* `nome: String`
* `posicao: String` (Enum: LEV, OPO, PON, CEN, LIB)
* `atributos_base: Dicionario` (Tecnica, Forca, Agilidade, Visao, **Resistencia**)
* `stamina_atual: Float` (0 a 100%)
* `status_fisico: String` (Enum: SAUDAVEL, FADIGADA, LESIONADA)
* `salario: Float`
* `conquistas: Dicionario`
* **Métodos Principais:**
  * `desgastar(minutos_jogados: Integer)`: Reduz a `stamina_atual`. A taxa de perda é inversamente proporcional ao atributo `Resistencia`.
  * `recuperar_stamina(foi_poupada: Boolean)`: Roda após cada partida. Se `foi_poupada` for True, recupera muito. Se jogou, recupera pouco, dependendo do nível da `equipe_medica` do clube.

---

## 3. Classes de Controle (Sistemas)

### `GerenciadorDeTemporada` (Season Manager)
Controla o calendário e o pipeline de torneios.
* `ano_atual: Integer`
* `torneios_ativos: Lista<Torneio>`
* **Métodos:**
  * `avancar_temporada()`
  * `gerar_vagas_internacionais()`

### `Torneio`
Gerencia a estrutura e as fases das competições.
* `id_torneio: String`
* `tipo: String` (Enum: SUPERLIGA, COPA_NACIONAL, INTERCONTINENTAL, MUNDIAL)
* `formato: String` (Enum: PONTOS_CORRIDOS_COM_PLAYOFF, MATA_MATA_PURO)
* `fase_atual: String` (Ex: "Classificatória", "Quartas de Final", "Final")
* `clubes_inscritos: Lista<Clube>`
* **Mecânicas de Formato:**
  * **Superliga:** Todos contra todos na primeira fase. Os melhores avançam para um mata-mata final.
  * **Copas, Intercontinental e Mundial:** Formato de chaveamento direto (mata-mata). Se perder, está eliminado daquela edição.

### `MotorDePartida` (Match Engine)
Simula os jogos de forma dinâmica, em blocos, para não entediar o jogador.
* `time_casa: Clube`
* `time_visitante: Clube`
* `placar_sets: Dicionario`
* `pontos_set_atual: Dicionario`
* **Métodos Principais:**
  * `simular_trecho()`: Em vez de processar ponto a ponto, a engine calcula um "salto" no placar (ex: de 0x0 para 5x3). A probabilidade de quem marcou os pontos nesse trecho depende da média dos atributos em quadra (ex: ataque x bloqueio).
  * `verificar_gatilho_evento()`: Após cada `simular_trecho()`, a engine checa se um evento aleatório deve acontecer (baseado em RNG e atributos). Se sim, pausa o jogo e chama o evento.
  * `disparar_evento()`: Mostra o aviso na tela (ex: Inversão de 5x1, Lesão, Desafio) aguardando a decisão do treinador.

### `EventoPartida` (Avisos e Decisões)
* `id_evento: String`
* `texto_mensagem: String` 
* `opcoes_resposta: Dicionario`
* `consequencia(opcao_escolhida)`
