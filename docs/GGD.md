# 🏐 Game Design Document (GDD) - Vôlei Manager

## 1. Core Loop
> **Escala o time** ➔ **Duela via eventos de texto** ➔ **Recebe pontos e recursos** ➔ **Treina time / Aprimora sede** ➔ **Repete**

---

## 2. Regras de Negócio (Economia)

A economia do jogo é dividida em dois pilares: o caixa da instituição e o patrimônio pessoal do treinador.

### 🏢 A) Moedas do Clube
Representa o orçamento oficial e os recursos da equipe.

**Entradas (Como o clube recebe):**
* Orçamento liberado pela diretoria
* Patrocínios
* Recompensas por vitórias em partidas
* Recompensa dourada por títulos (Premiações)

**Saídas (Como o clube gasta):**
* Contratação de reforços
* Aprimoramento da sede e infraestrutura
* Treinamento do time
* Tratamento médico de lesões
* Taxas de inscrição em torneios
* Custos de viagem e logística para amistosos fora de casa

**Perdas (Riscos financeiros):**
* Queda de arrecadação por derrotas em partidas
* Cortes de orçamento impostos pela diretoria
* Falência do clube (Zerar o caixa)

### 👔 B) Moedas do Treinador
Representa o dinheiro pessoal do jogador.

**Entradas (Como o treinador recebe):**
* Salário pago pelo clube
* Cachês de entrevistas e marketing pessoal

**Saídas (Como o treinador gasta):**
* Pagamento de multa rescisória (para sair do clube atual)
* Investimento no clube do próprio bolso (injeção de capital de emergência)

**Perdas (Riscos pessoais):**
* Cortes no salário por mau desempenho
* Calote devido à falência do clube

---

## 3. Game Over e Progressão
O jogo **não** possui um "Game Over" tradicional onde o jogador perde o perfil e precisa recriar o personagem. A progressão é contínua e punitiva caso haja má gestão:

* **Demissão e Falência:** Caso o treinador seja demitido por má performance ou o clube vá à falência, a **reputação** do jogador sofre uma queda drástica.
* **Consequência:** Com a reputação manchada, portas se fecham. Será muito difícil conseguir propostas de clubes de nível médio ou alto. O jogador é obrigado a recomeçar com recursos escassos, assumindo um clube da **Superliga B**, precisando provar seu valor novamente para reerguer sua carreira.

## 4. Entidades e Atributos (Mecânicas de Jogo)

Esta seção define as características de cada elemento do jogo e como elas impactam a jogabilidade, a simulação das partidas e a gestão do time.

### 👔 4.1. O Treinador (Personagem do Jogador)
Os atributos do treinador definem a sua capacidade de liderança e abrem portas para clubes melhores.
* **Experiência (XP):** Aumenta ao jogar e vencer partidas (vitórias por 3x0 dão bônus). Define o nível geral do treinador.
* **Perspicácia:** Afeta o sucesso das decisões táticas tomadas em tempo real durante os eventos de texto das partidas (ex: pedir um desafio de arbitragem ou fazer uma inversão de 5x1).
* **Gerenciamento:** Determina a eficiência do uso de recursos do clube. Um nível alto aqui pode reduzir os custos de aprimoramento da arena ou baratear o salário pedido por uma nova jogadora.
* **Reputação:** O seu "currículo". Afetado por títulos ganhos, demissões ou falências de clubes. Define o nível dos clubes que farão propostas de emprego no final da temporada.

### 🏐 4.2. As Jogadoras (As Cartinhas)
Cada jogadora possui atributos que influenciam diretamente no desempenho do time nas simulações de partidas e eventos.

**Atributos Base (Fixos / Evolutivos via Treino):**
* **Posição:** Levantadora, Oposta, Ponteira, Central ou Líbero.
* **Técnica:** Define a precisão dos passes, saques e capacidade de furar bloqueios.
* **Força:** Potência do ataque e do saque.
* **Agilidade:** Tempo de reação para defesas e bloqueios.
* **Visão de Jogo:** Inteligência tática, reduzindo a chance de erros não forçados.
* **Resistência:** A capacidade máxima de esforço físico. Define quão rápido a jogadora perde *Stamina* e a sua imunidade a lesões.

**Atributos Dinâmicos (Variam ao longo da temporada e partidas):**
* **Stamina:** O principal recurso durante o jogo. Cai ao longo dos sets. Jogadoras sem stamina erram mais e têm alta chance de lesão se mantidas em quadra.
* **Condição Física (Lesão):** Pode ser Saudável, Fadigada ou Lesionada. Impacta se a jogadora pode ser escalada.
* **Moral:** Afetada por vitórias, derrotas e infraestrutura do clube. Jogadoras com moral baixa rendem abaixo dos seus atributos base.

**Atributos Contratuais:**
* **Nacionalidade e Salário:** Jogadoras de nível internacional (ex: Egonu) exigem salários altíssimos que podem quebrar clubes com baixa estrutura financeira.

### 🏢 4.3. O Clube
A estrutura que o jogador gerencia.
* **Nível da Sede / Arena:** Começa precário em clubes da Liga B. Melhorar a arena atrai mais público (mais moedas), patrocínios melhores e propostas de amistosos mais lucrativos.
* **Orçamento Disponível:** O dinheiro em caixa do clube no momento.
* **Divisão Atual:** Define em quais campeonatos nacionais o clube tem permissão para jogar.

### 🏆 4.4. Competições (Ligas, Copas e Internacionais)
Cada torneio tem características que definem o risco e a recompensa para o clube.
* **Nível de Prestígio:** Campeonatos maiores (como o Mundial e Continental) dão muito mais XP e Reputação ao treinador.
* **Premiação Base:** O valor financeiro que entra no caixa do clube ao final da competição, de acordo com a posição na tabela.
* **Custo de Participação:** Torneios menores ou amistosos longes podem ter custos logísticos altos em relação à premiação, exigindo planejamento financeiro.
* **Vagas de Acesso:** Vencer uma divisão garante vaga na divisão superior. Vencer o Continental dá acesso ao Mundial na temporada seguinte.
