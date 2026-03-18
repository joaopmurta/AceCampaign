# 🏐 Game Design Document (GDD) - Vôlei Manager

## 1. Core Loop
> **Escala o time** ➔ **Duela via simulação/eventos/cartas** ➔ **Recebe pontos e recursos** ➔ **Treina time / Aprimora sede** ➔ **Repete**

---

## 2. Regras de Negócio (Economia e Energia)

A economia e a gestão de recursos são divididas em dois pilares principais: o clube e a pessoa física do treinador.

### 🏢 A) Recursos do Clube (Moedas e Orçamento)
Representa o orçamento oficial para operações da equipe.
* **Entradas:** Orçamento da diretoria, patrocínios, prêmios por vitórias/títulos, venda de jogadoras e conversões feitas pelo treinador (injeção de capital pessoal).
* **Saídas:** Contratação de reforços (passe e salário), aprimoramento das 6 áreas da infraestrutura, taxas de torneios, pagamento de multas rescisórias por dispensa de atletas e custos de treinos.
* **Riscos:** Queda de arrecadação por derrotas, cortes de diretoria ou falência (que resulta na demissão do treinador).

### 👔 B) Recursos do Treinador (Moedas Pessoais e Energia)
Representa a capacidade física e o patrimônio do jogador.
* **Moedas do Treinador (Entradas):** Salário do clube, cachês de entrevistas e compra via dinheiro real (IAP).
* **Moedas do Treinador (Saídas):** Pagamento da própria multa rescisória (para trocar de clube) e doações para salvar o clube da falência.
* **Energia (0 a 100%):** O recurso vital para ações de gestão. Aplicação de treinos táticos e dar entrevistas consomem Energia. Iniciar partidas não exige Energia, mas estar zerado bloqueia a preparação da equipe. A Energia recarrega passivamente após as rodadas ou ao longo do tempo (offline).

---

## 3. Game Over e Progressão de Campanhas
* **Saves:** O jogador pode gerenciar até 3 campanhas simultâneas, criando avatares customizados para cada uma.
* **Progresso Contínuo:** O jogo não possui "Game Over" de perda de perfil. Caso seja demitido ou o clube falia, a **Reputação** do treinador cai drasticamente, forçando-o a assumir clubes de divisões inferiores para reconstruir a carreira.
* **Simulação Global:** O mundo do jogo é vivo. Clubes controlados pelo computador (IA procedural) disputam títulos em outras ligas, mantendo um histórico global realista de vitórias e transferências.

---

## 4. Entidades e Atributos (Mecânicas de Jogo)

### 👔 4.1. O Treinador (Personagem do Jogador)
* **Atributos de Progressão:** Experiência (XP), Perspicácia (tática em partidas) e Reputação (currículo).
* **Atributos de Status:** Energia Atual (0-100%) e Caixa Pessoal.

### 🏐 4.2. As Jogadoras (As Cartinhas)
* **Atributos Base:** Posição, Técnica, Força, Agilidade, Visão de Jogo e Resistência.
* **Atributos Dinâmicos:** 
  * **Stamina:** Cai ao longo dos sets. Afeta o rendimento e aumenta chance de lesões (Status: Saudável, Fadigada, Lesionada).
  * **Moral:** Afetada pelo ambiente do clube e minutos jogados.
* **Mercado:** Jogadoras possuem Valor de Passe dinâmico. Propostas abaixo do valor exigido têm chance alta de recusa. Clubes rivais podem pagar a multa e levar a jogadora abruptamente.

### 🏢 4.3. O Clube e Infraestrutura
* **Nível Geral (0 a 100%):** Média das 6 áreas (Arquibancadas, Staff, Equipamentos, Médicos, Quadra e Marketing). Infraestruturas altas atraem patrocínios, reduzem lesões e facilitam contratações de estrelas.
* **Divisão Atual:** Define permissões de torneios e o orçamento base.

### 🏆 4.4. Competições
* **Formato de Acesso:** Vencer a divisão sobe de liga. Chegar à final da Liga A garante vaga no Intercontinental no ano seguinte. A final do Intercontinental garante vaga no Mundial.
* **Regras de Partida:** Jogos são "Melhor de 3" (sets até 25, tie-break até 15). É obrigatória a formação 7 em quadra correta, limites de desafios (2 erros) e tempos técnicos (2 por set).

### 🃏 4.5. Intervenções Táticas e Minigame
* **Blocos de Pontos:** A partida avança em blocos simulados.
* **Eventos de Texto:** Interrupções para decisões rápidas (lesões, inversões).
* **Minigame de Cartas:** Durante a partida, o treinador pode escolher entre 3 cartas ocultas (2 buffs positivos, 1 debuff negativo) para tentar alterar o ritmo do jogo, assumindo riscos.
