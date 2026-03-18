# 📋 Documento de Requisitos - Vôlei Manager

Este documento lista todas as funcionalidades, regras de negócio e restrições técnicas do sistema, servindo como base para a modelagem orientada a objetos e o desenvolvimento do jogo.

---

## 1. Requisitos Funcionais (RF)
*Ações e interações que o sistema DEVE executar. Agrupados por domínio.*

### 💾 Criação de Perfil e Gestão de Campanhas
* **RF001:** O sistema deve permitir que o jogador crie e gerencie até 3 campanhas (saves) simultâneas e independentes.
* **RF002:** O sistema deve permitir a customização do avatar do treinador no início da jornada (escolha de gênero, estilo visual, nome e nacionalidade).
* **RF003:** O sistema deve iniciar todas as campanhas em um cenário "limpo", onde nenhum clube ou treinador possui títulos ou medalhas prévias no histórico.

### 👔 Gestão e Energia do Treinador (O Jogador)
* **RF004:** O sistema deve permitir que o jogador assine contratos com um clube no início de uma temporada dadas as opções disponíveis.
* **RF005:** O sistema deve enviar propostas esporádicas de outros clubes, baseando-se na Reputação do treinador.
* **RF006:** O jogador deve poder pagar a própria multa rescisória usando seu "Caixa Pessoal" para mudar de clube antecipadamente.
* **RF007:** O sistema deve permitir a conversão de "Moedas do Treinador" (Caixa Pessoal) para "Moedas do Clube" (Orçamento) a qualquer momento.
* **RF008:** O sistema deve permitir a compra de "Moedas do Treinador" utilizando dinheiro real (In-App Purchases / IAP).
* **RF009:** O sistema deve gerenciar a "Energia do Treinador" (0 a 100%), descontando pontos (ex: 20%) por ações como aplicar treinos na equipe ou dar entrevistas.
* **RF010:** O sistema deve enviar convites esporádicos para entrevistas, oferecendo moedas pessoais em troca do consumo de Energia.
* **RF011:** O sistema deve recarregar a Energia do treinador automaticamente após cada partida/rodada, ou ao longo do tempo (offline).
* **RF012:** O jogador pode iniciar uma partida com 0% de Energia, sendo bloqueado apenas de ações pré-jogo que exijam esforço.
* **RF013:** O sistema deve registrar as conquistas do treinador em seu histórico.

### 🏢 Gestão do Clube e Infraestrutura
* **RF014:** O sistema deve permitir a melhoria de 6 áreas da infraestrutura (Arquibancadas, Staff, Equipamentos, Médicos, Quadra, Marketing), descontando do orçamento do clube.
* **RF015:** O sistema deve calcular o nível geral do clube (0 a 100%) baseado na média dessas 6 áreas.
* **RF016:** O sistema deve decretar a falência do clube caso o orçamento fique negativo e não seja coberto, demitindo o treinador.

### 🛒 Mercado de Transferências e Elenco
* **RF017:** O sistema deve exibir uma aba de "Mercado" onde clubes definem um "Valor Pedido" por suas jogadoras disponíveis.
* **RF018:** O sistema deve permitir que o jogador faça contrapropostas (oferte um valor). Se a oferta for menor que o pedido, a chance de aceite diminui; se for maior, a chance aumenta.
* **RF019:** O sistema deve calcular o salário de uma jogadora de forma fixa, atrelado ao seu nível de desempenho (evoluindo gradativamente conforme ela melhora via treinos).
* **RF020:** O sistema deve permitir a venda ou dispensa de jogadoras do próprio elenco, exigindo o pagamento de uma multa rescisória (parcela do valor) à atleta em caso de dispensa.
* **RF021:** O sistema deve gerar eventos onde clubes rivais pagam a multa rescisória de uma jogadora do seu time, injetando o valor no orçamento do seu clube sem penalizar sua Reputação.
* **RF022:** O sistema deve permitir a aplicação de treinamentos, consumindo recursos e Energia do treinador para aumentar os atributos das jogadoras.
* **RF023:** O sistema deve diminuir a *Stamina* das jogadoras em quadra (baseado no tempo e na *Resistência*) e recuperá-la entre partidas (baseado na Equipe Médica).
* **RF024:** O sistema deve alterar o status físico de uma jogadora para "Lesionada" caso jogue com *Stamina* crítica ou sofra evento de lesão.

### 🏐 Escalação e Estatísticas
* **RF025:** O sistema deve permitir a formação de um elenco de no mínimo 10 e no máximo 14 jogadoras por temporada.
* **RF026:** O sistema deve exibir painéis de estatísticas individuais (ataque, bloqueio, saque, defesa/passe) adaptados por posição.
* **RF027:** O sistema deve calcular a média de desempenho coletivo e individual por partida e campeonato.

### 🎮 Motor de Partida e Intervenções Táticas
* **RF028:** O sistema deve simular a partida em "blocos de pontos", distribuindo a autoria obrigatoriamente para as jogadoras em quadra (ou erro adversário), batendo exatamente com o placar.
* **RF029:** O sistema deve interromper a simulação aleatoriamente para "Eventos de Texto" (lesões, desafios, inversão) com tempo limite de resposta.
* **RF030:** O sistema deve exibir um "Minigame de Cartas" durante a partida, oferecendo 3 opções ocultas (2 com buffs temporários positivos e 1 com debuff negativo) para o treinador escolher, adicionando risco/recompensa à tática.
* **RF031:** O sistema deve exibir uma interface de "Tempo Técnico", permitindo escolher 2 de 4 instruções táticas processuais.

### 🌎 Temporadas e Simulação Global
* **RF032:** O sistema deve inicializar o banco de dados com ligas de países tradicionais (Brasil, Itália, Turquia, Polônia, EUA, Japão, China e Rússia).
* **RF033:** O sistema deve avançar o calendário, intercalando partidas da Liga Nacional e competições mata-mata.
* **RF034:** Ao final de cada temporada, o sistema deve envelhecer jogadoras, distribuir prêmios e aplicar as classificações para torneios internacionais.
* **RF035:** O sistema deve utilizar um algoritmo de simulação para processar os resultados e atribuir títulos aos clubes controlados pelo computador nas outras ligas mundiais, mantendo o histórico consistente.

---

## 2. Regras de Negócio (RN)
*As leis do jogo que os Requisitos Funcionais devem obedecer rigorosamente.*

* **RN001 (Exclusividade de Títulos):** Um título de competição só pode ser atribuído a um único clube por temporada (não existem empates em campeonatos).
* **RN002 (Vitória de Partida):** Partidas são disputadas em formato "Melhor de 3". Vence quem ganhar 2 sets.
* **RN003 (Pontuação do Set):** Sets normais vão até 25 pontos. O *Tie-break* (3º set) vai até 15 pontos. É obrigatória a vantagem de 2 pontos.
* **RN004 (Limites de Interrupção):** Cada equipe tem direito a exatamente 2 Tempos Técnicos por set.
* **RN005 (Desafios de Arbitragem):** Cada equipe pode errar até 2 Desafios por set.
* **RN006 (Restrição de Posição):** Jogadoras não podem ser escaladas em posições divergentes de sua natureza.
* **RN007 (Formação Obrigatória):** A equipe titular (7 em quadra) DEVE conter: 2 Ponteiras, 2 Centrais, 1 Levantadora, 1 Oposta e 1 Líbero.
* **RN008 (Improvisação de Emergência):** Caso não haja reposição, outra posição pode ser improvisada no lugar de uma lesão, sofrendo severo "nerf" de atributos.
* **RN009 (Classificação em Cascata):** O acesso ao torneio Intercontinental exige chegada à final da Liga A no ano anterior. O Mundial exige chegada à final do Intercontinental no ano anterior.

---

## 3. Requisitos Não Funcionais (RNF)
*Restrições de arquitetura, performance, plataforma e experiência do usuário.*

* **RNF001 (Plataforma):** Desenvolvido para dispositivos móveis (Smartphones), focado em orientação retrato (Vertical).
* **RNF002 (Offline First e Armazenamento):** O progresso e todo o estado global simulado devem ser salvos em banco de dados local (ex: SQLite).
* **RNF003 (Desempenho da Simulação):** O cálculo dos blocos de pontos não deve causar engasgos na interface visual.
* **RNF004 (Desempenho da Atribuição):** O cálculo de distribuição de estatísticas deve ter complexidade leve ($O(1)$ ou $O(N)$) para tempo real.
* **RNF005 (Tamanho):** A build final do aplicativo não deve exceder 150 MB.
