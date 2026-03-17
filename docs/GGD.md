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
       
