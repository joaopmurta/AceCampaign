# 📋 Documento de Requisitos - Vôlei Manager

Este documento lista todas as funcionalidades, regras e restrições técnicas do sistema, servindo como base para a modelagem orientada a objetos e o desenvolvimento do jogo.

---

## 1. Requisitos Funcionais (RF)
*Descrevem o que o sistema DEVE FAZER (ações, métodos e interações do usuário). Estão agrupados por domínio para facilitar a futura criação do Diagrama de Classes.*

### 👔 Gestão do Treinador (O Jogador)
* **RF001:** O sistema deve permitir que o jogador assine contratos com clubes no início de uma temporada ou recuse propostas.
* **RF002:** O jogador deve poder pagar a própria multa rescisória usando seu "Caixa Pessoal" para mudar de clube quando quiser.
* **RF003:** O jogador deve poder injetar dinheiro do seu Caixa Pessoal no Orçamento do Clube para evitar falência.
* **RF004:** O sistema deve registrar as conquistas (troféus e medalhas) do treinador em seu histórico.

### 🏢 Gestão do Clube e Infraestrutura
* **RF005:** O sistema deve permitir a melhoria de 6 áreas da infraestrutura (Arquibancadas, Staff, Equipamentos, Médicos, Quadra, Marketing), descontando do orçamento do clube.
* **RF006:** O sistema deve calcular o nível geral do clube (0 a 100%) baseado na média das suas 6 áreas de infraestrutura.
* **RF007:** O sistema deve permitir a contratação de novas jogadoras, deduzindo o valor do passe do orçamento e adicionando o salário à folha de pagamento.
* **RF008:** O sistema deve decretar a falência do clube caso o orçamento fique negativo e não seja coberto, demitindo o treinador (jogador).

### 🏐 Gestão do Elenco (Jogadoras)
* **RF009:** O sistema deve permitir a aplicação de treinamentos (Técnico, Físico, Tático), consumindo recursos e aumentando os atributos base das jogadoras.
* **RF010:** O sistema deve diminuir a *Stamina* das jogadoras que entrarem em quadra (proporcionalmente ao tempo jogado e à sua *Resistência*).
* **RF011:** O sistema deve recuperar a *Stamina* das jogadoras poupadas entre as partidas (a taxa de recuperação é influenciada pelo nível da Equipe Médica do clube).
* **RF012:** O sistema deve alterar o status físico de uma jogadora para "Lesionada" caso ela jogue com *Stamina* crítica ou sofra um evento de lesão.

### 🎮 Motor de Partida e Eventos
* **RF013:** O sistema deve simular o avanço da partida em "blocos de pontos" em vez de ponto a ponto, utilizando a média de atributos das equipes.
* **RF014:** O sistema deve interromper a simulação em momentos aleatórios para exibir "Eventos de Texto" (ex: lesões, desafios de arbitragem, inversão tática).
* **RF015:** O sistema deve processar a decisão do jogador nos Eventos de Texto, calculando o sucesso com base nos atributos do Treinador (Perspicácia) e das Jogadoras (Técnica/Visão).

### 🏆 Temporadas e Competições
* **RF016:** O sistema deve avançar o calendário do jogo, intercalando partidas da Liga Nacional e competições mata-mata.
* **RF017:** O sistema deve processar viradas de ano, envelhecendo jogadoras, distribuindo premiações e aplicando a lógica de classificação em cascata para a próxima temporada.

---

## 2. Regras de Negócio (RN)
*As leis do jogo que os Requisitos Funcionais devem obedecer rigorosamente.*

* **RN001 (Limite de Infraestrutura):** Nenhuma área da infraestrutura pode ultrapassar o nível máximo de 100%.
* **RN002 (Classificação em Cascata):** Um time só pode disputar o torneio Intercontinental se tiver chegado à final da Liga A (Nacional) na temporada *anterior*.
* **RN003 (Acesso ao Mundial):** Um time só pode disputar o Mundial se tiver chegado à final do Intercontinental na temporada *anterior*.
* **RN004 (Formatos de Torneio):** A Superliga possui fase de pontos corridos seguida de mata-mata. A Copa Nacional, Intercontinental e Mundial são exclusivamente no formato mata-mata (eliminação direta).
* **RN005 (Fadiga):** A probabilidade de erro (pontos para o adversário) e lesão de uma jogadora aumenta exponencialmente quando sua *Stamina* desce abaixo de um limite crítico (ex: 30%).

---

## 3. Requisitos Não Funcionais (RNF)
*Restrições de arquitetura, performance, plataforma e experiência do usuário.*

* **RNF001 (Plataforma):** O jogo deve ser desenvolvido e otimizado para dispositivos móveis (Smartphones), focado na orientação retrato (Vertical).
* **RNF002 (Armazenamento):** O progresso do jogador deve ser salvo localmente no dispositivo (ex: usando banco de dados SQLite ou JSON local), não exigindo conexão constante com a internet para jogar (Offline First).
* **RNF003 (Desempenho da Simulação):** O processamento dos blocos de pontos e os cálculos de probabilidade na partida não devem causar travamentos perceptíveis na interface do usuário.
* **RNF004 (Tamanho do Aplicativo):** Por ser um jogo mobile focado em UI e simulação (sem gráficos 3D pesados), o tamanho final da build não deve exceder 150 MB.
