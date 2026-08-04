# MediAgent-RL - Tratamento de Paciente Virtual com Aprendizado por Reforço Profundo

Projeto desenvolvido para simular o tratamento de um paciente virtual utilizando **Aprendizado por Reforço Profundo (Deep Reinforcement Learning - DRL)**.

Foi criado um ambiente personalizado utilizando **Gymnasium**, no qual diferentes algoritmos de aprendizado por reforço aprendem automaticamente a escolher o melhor tratamento para maximizar as chances de cura do paciente.

## Objetivo

O objetivo do projeto é comparar o desempenho de diferentes algoritmos de **Deep Reinforcement Learning** em um ambiente médico simplificado.

O agente deve aprender a tratar um paciente administrando medicamentos corretos para reduzir:

- Infecção
- Febre
- Dor

Ao mesmo tempo, deve minimizar os custos do tratamento e evitar que o paciente evolua para óbito.

---

## Representação do Ambiente

O estado do paciente é composto por três variáveis:

```
[Infecção, Febre, Dor]
```

Cada variável pode assumir três níveis:

| Valor | Estado |
|------:|--------|
| 0 | Controlado / Normal |
| 1 | Moderado |
| 2 | Grave |

O ambiente é estocástico, ou seja, um medicamento nem sempre produz o resultado esperado.

---

## Espaço de Observação

Tipo:

```
Box(0.0, 2.0, (3,))
```

Representando:

```
[Infecção, Febre, Dor]
```

---

## Espaço de Ações

O agente possui quatro ações possíveis:

| Ação | Descrição |
|------:|-----------|
| 0 | Administrar antibiótico |
| 1 | Administrar antitérmico |
| 2 | Administrar analgésico |
| 3 | Aguardar |

Cada ação possui probabilidades diferentes de sucesso e pode gerar efeitos adversos.

---

## Sistema de Recompensas

A função de recompensa foi projetada para incentivar tratamentos eficientes.

| Situação | Recompensa |
|----------|-----------:|
| Cura | +100 |
| Óbito | -100 |
| Administração de medicamento | -1 |
| Aguardar | -2 |
| Sintomas graves | -5 |

O objetivo do agente é maximizar a recompensa acumulada ao longo do episódio.

---

## Algoritmos Utilizados

Foram implementados e comparados três algoritmos da biblioteca **Stable-Baselines3**:

- **DQN (Deep Q-Network)**
- **A2C (Advantage Actor-Critic)**
- **PPO (Proximal Policy Optimization)**

Todos os modelos utilizam uma rede neural do tipo **MLP (Multi-Layer Perceptron)** para aproximação da função de valor ou política.

---

## Tecnologias Utilizadas

- Python
- Gymnasium
- Stable-Baselines3
- PyTorch
- NumPy
- Matplotlib
- tqdm

---

## Instalação

Clone o repositório:

```bash
git clone https://github.com/seu-usuario/MedRL.git
cd MedRL
```

Instale as dependências:

```bash
pip install gymnasium stable-baselines3 torch matplotlib tqdm numpy
```

---

## Execução

Execute o notebook (`.ipynb`) ou o script Python.

Durante a execução serão realizados automaticamente:

- Criação do ambiente personalizado;
- Treinamento do DQN;
- Treinamento do A2C;
- Treinamento do PPO;
- Avaliação do melhor modelo encontrado;
- Comparação dos resultados obtidos.

Ao final será exibida uma tabela semelhante à seguinte:

```
======================================================================
Resultados Finais
======================================================================

Algoritmo      | Recompensa Média | Taxa de Cura
-------------------------------------------------------------
DQN            | 95.30            | 99.70%
A2C            | 92.10            | 98.50%
PPO            | 96.40            | 100.00%
-------------------------------------------------------------
```

*(Os valores acima são apenas ilustrativos.)*

---

## Estrutura do Projeto

```
.
├── MedRL.ipynb
├── README.md
├── best_model_DQN/
├── best_model_A2C/
├── best_model_PPO/
└── temp_logs/
```

---

## Funcionamento do Ambiente

O ambiente representa um paciente cuja evolução depende tanto das ações escolhidas quanto da probabilidade de sucesso de cada tratamento.

Exemplos:

- O antibiótico reduz a infecção na maioria das vezes.
- O antitérmico reduz a febre.
- O analgésico reduz a dor.
- Aguardar pode agravar a infecção.

Como as transições são probabilísticas, o agente precisa aprender uma estratégia robusta para maximizar as chances de cura.

---

## Avaliação

Após o treinamento, cada algoritmo é avaliado em diversos episódios.

As métricas consideradas são:

- Recompensa média acumulada;
- Taxa de cura (%).

O melhor modelo encontrado durante o treinamento é salvo automaticamente utilizando o `EvalCallback` da Stable-Baselines3.

---

## Possíveis Melhorias

Algumas extensões que podem ser implementadas futuramente:

- Inclusão de novas doenças;
- Maior variedade de medicamentos;
- Efeitos colaterais;
- Histórico clínico e idade do paciente;
- Observações contínuas;
- Ambiente mais próximo de um cenário hospitalar real;
- Ajuste automático de hiperparâmetros.

---

## Licença

Este projeto foi desenvolvido para fins acadêmicos e de estudo sobre Aprendizado por Reforço Profundo.
