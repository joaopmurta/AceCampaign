# 📋 Documento de Requisitos - Vôlei Manager

Este documento lista todas as funcionalidades, regras de negócio e restrições técnicas do sistema, servindo como base para a modelagem orientada a objetos e o desenvolvimento do jogo.

---

## 1. Requisitos Funcionais (RF)
*Ações e interações que o sistema DEVE executar. Agrupados por domínio.*

### 👔 Gestão e Energia do Treinador (O Jogador)
* **RF001:** O sistema deve permitir que o jogador assine contratos com clubes no início de uma temporada ou recuse propostas.
* **RF002:** O sistema deve enviar propostas esporádicas de outros clubes, que podem ou não cobrir a taxa de rescisão atual, baseando-se na Reputação do treinador.
* **RF003:** O jogador deve poder pagar a própria multa rescisória usando seu "Caixa Pessoal" para mudar de clube antecipadamente.
* **RF004:** O jogador deve poder injetar dinheiro do seu Caixa Pessoal no Orçamento do Clube para evitar falência.
* **RF005:** O sistema deve gerenciar a "Energia do Treinador" (0 a 100%), descontando pontos por ações como aplicar treinos específicos na equipe ou dar entrevistas.
* **RF006:** O sistema deve enviar convites esporádicos para entrevistas (TV/Rádio/Podcast), oferecendo moedas pessoais ao jogador em troca do consumo de 100% da sua Energia.
* **RF007:** O sistema deve recarregar parcialmente a Energia do treinador automaticamente após cada partida/rodada, ou ao longo do tempo (offline).
* **RF008:** O sistema deve permitir que o jogador inicie uma partida mesmo com 0% de Energia, bloqueando apenas ações pré-jogo que exijam esforço.
* **RF009:** O sistema deve registrar as conquistas (troféus e medalhas) do treinador em seu histórico.

### 🏢 Gestão do Clube e Infraestrutura
* **RF010:** O sistema deve permitir a melhoria de 6 áreas da infraestrutura (Arquibancadas, Staff, Equipamentos, Médicos, Quadra, Marketing), descontando do orçamento do clube.
* **RF011:** O sistema deve calcular o nível geral do clube (0 a 100%) baseado na média das suas 6 áreas de infraestrutura.
* **RF012:** O sistema deve decretar a falência do clube caso o orçamento fique negativo e não seja coberto, demitindo o treinador.

### 🛒 Mercado de Transferências e Elenco
* **RF013:** O sistema deve exibir uma aba de "Mercado" com jogadoras disponíveis para contratação.
* **RF014:** O sistema deve permitir que o jogador faça ofertas, deduzindo o "Valor de Contratação" (passe) do orçamento do clube e adicionando o "Salário" à folha de pagamento.
* **RF015:** O sistema deve processar o aceite ou recusa de uma jogadora à proposta com base no nível do clube interessado e na Reputação do treinador.
* **RF016:** O sistema deve gerar eventos onde clubes rivais pagam a multa rescisória de uma jogadora do seu time de forma abrupta, injetando o valor no orçamento do seu clube sem penalizar a Reputação do treinador.
* **RF017:** O sistema deve permitir a aplicação de treinamentos (Técnico, Físico, Tático), consumindo recursos do clube e energia do treinador para aumentar os atributos base das jogadoras.
* **RF018:** O sistema deve diminuir a *Stamina* das jogadoras em quadra (proporcional ao tempo jogado e à sua *Resistência*) e recuperá-la entre partidas (influenciado pelo nível da Equipe Médica).
* **RF019:** O sistema deve alterar o status físico de uma jogadora para "Lesionada" caso ela jogue com *Stamina* crítica ou sofra um evento de lesão.

### 🏐 Escalação e Estatísticas
* **RF020:** O sistema deve permitir a escalação de um elenco de até 14 jogadoras por partida.
* **RF021:** O sistema deve exibir painéis de estatísticas individuais (ataque, bloqueio, saque, defesa/passe) adaptados por posição.
* **RF022:** O sistema deve calcular e exibir a média de desempenho do time e das jogadoras em cada fundamento, tanto por partida quanto por campeonato.

### 🎮 Motor de Partida e Intervenções Táticas
* **RF023:** O sistema deve simular o avanço da partida em "blocos de pontos", distribuindo a autoria dos pontos obrigatoriamente para as jogadoras em quadra (em Saque, Ataque, Bloqueio ou Erro Adversário). A soma dos pontos individuais deve bater exatamente com o placar do set.
* **RF024:** O sistema deve interromper a simulação em momentos aleatórios para exibir "Eventos de Texto" (ex: lesões, desafios de arbitragem, inversão tática).
* **RF025:** O sistema deve impor um tempo limite em tela para o jogador tomar decisões durante os Eventos de Texto.
* **RF026:** O sistema deve processar a decisão do jogador nos Eventos, calculando o sucesso com base nos atributos do Treinador (Perspicácia) e das Jogadoras (Técnica/Visão).
* **RF027:** O sistema deve exibir uma interface de "Tempo Técnico", permitindo ao treinador escolher 2 de 4 opções de instruções táticas geradas proceduralmente (ex: "Focar ataque na Oposta").

### 🌎 Temporadas e Simulação Global
* **RF028:** O sistema deve inicializar o banco de dados com ligas de países tradicionais: Brasil, Itália, Turquia, Polônia, EUA, Japão, China e Rússia.
* **RF029:** O sistema deve avançar o calendário, intercalando partidas da Liga Nacional e competições mata-mata.
* **RF030:** Ao final de cada temporada, o sistema deve processar viradas de ano, envelhecendo jogadoras, distribuindo premiações e aplicando a lógica de classificação em cascata para torneios internacionais.
* **RF031:** O sistema deve simular e atribuir títulos a clubes gerenciados pela IA em todas as ligas mundiais não jogadas pelo usuário, mantendo o histórico global vivo.

---

## 2. Regras de Negócio (RN)
*As leis do jogo que os Requisitos Funcionais devem obedecer rigorosamente.*

* **RN001 (Vitória de Partida):** Partidas são disputadas em formato "Melhor de 5". Vence quem ganhar 3 sets.
* **RN002 (Pontuação do Set):** Sets normais vão até 25 pontos. O *Tie-break* (5º set) vai até 15 pontos. É obrigatória a vantagem de 2 pontos para fechar qualquer set.
* **RN003 (Matemática de Placar):** A pontuação gerada pelo motor da partida não pode exceder limites lógicos de um jogo de vôlei.
* **RN004 (Limites de Interrupção):** Cada equipe tem direito a exatamente 2 Tempos Técnicos por set.
* **RN005 (Desafios de Arbitragem):** Cada equipe pode errar até 2 Desafios (Video Challenge) por set. Desafios bem-sucedidos não são descontados do limite.
* **RN006 (Restrição de Posição):** Jogadoras não podem ser escaladas em posições divergentes de sua natureza (ex: Levantadora não pode jogar de Líbero).
* **RN007 (Formação Obrigatória):** A equipe titular (7 em quadra) DEVE conter: 2 Ponteiras, 2 Centrais, 1 Levantadora, 1 Oposta e 1 Líbero.
* **RN008 (Improvisação de Emergência):** Caso o clube não tenha reposição exata para uma lesão, outra posição pode ser improvisada no lugar, sofrendo uma severa redução (nerf) em seus atributos durante a partida.
* **RN009 (Limite de Infraestrutura):** Nenhuma área da infraestrutura pode ultrapassar o nível máximo de 100%.
* **RN010 (Fadiga Exponencial):** A probabilidade de erro (pontos para o adversário) e lesão de uma jogadora aumenta exponencialmente quando sua *Stamina* desce abaixo de um limite crítico (ex: 30%).
* **RN011 (Classificação em Cascata):** O acesso ao torneio Intercontinental exige chegada à final da Liga A na temporada *anterior*. O acesso ao Mundial exige chegada à final do Intercontinental na temporada *anterior*.
* **RN012 (Formatos de Torneio):** A Superliga possui fase de pontos corridos seguida de mata-mata. A Copa Nacional, Intercontinental e Mundial são exclusivamente no formato mata-mata (eliminação direta).

---

## 3. Requisitos Não Funcionais (RNF)
*Restrições de arquitetura, performance, plataforma e experiência do usuário.*

* **RNF001 (Plataforma):** O jogo deve ser desenvolvido e otimizado para dispositivos móveis (Smartphones), focado na orientação retrato (Vertical).
* **RNF002 (Armazenamento e Offline First):** O jogo deve funcionar prioritariamente offline. O progresso do jogador e todo o estado global (campeonatos de outros países simulados pela IA) devem ser salvos em banco de dados local no dispositivo (ex: SQLite).
* **RNF003 (Desempenho da Simulação):** O processamento dos blocos de pontos e os cálculos de probabilidade na partida não devem causar travamentos perceptíveis na interface do usuário.
* **RNF004 (Desempenho da Atribuição):** O cálculo de distribuição de pontos para estatísticas individuais deve ocorrer em tempo real (complexidade $O(1)$ ou $O(N)$ leve) para não travar a UI durante a simulação.
* **RNF005 (Tamanho do Aplicativo):** O tamanho final da build não deve exceder 150 MB.
