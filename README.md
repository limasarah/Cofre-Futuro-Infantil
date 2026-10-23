# 👶 Cofre Futuro Infantil | Simulador de Patrimônio e Dividendos para os Filhos

[![Microsoft Excel](https://img.shields.io/badge/Microsoft_Excel-217346?style=for-the-badge&logo=microsoft-excel&logoColor=white)](https://www.microsoft.com/microsoft-365/excel)
[![GitHub](https://img.shields.io/badge/GitHub-181717?style=for-the-badge&logo=github&logoColor=white)](https://github.com/)

> **Desafio de Projeto — DIO (Digital Innovation One)**  
> **Tema:** Ferramenta de Simulação Financeira para Criação de Patrimônio Infantil por meio de Fundos de Investimento Imobiliário (FIIs).

---

## 🎯 Sobre o Projeto

O **Cofre Futuro Infantil** é uma ferramenta desenvolvida em Microsoft Excel, com interface interativa inspirada em uma aplicação, para auxiliar pais e responsáveis no planejamento financeiro do futuro dos seus filhos.

O simulador permite projetar a acumulação de patrimônio por meio de aportes mensais e estimar a renda passiva mensal proveniente de dividendos de Fundos de Investimento Imobiliário (FIIs), considerando o prazo definido pela família.

O projeto combina fórmulas financeiras, automação de cálculos, validação de dados e visualização dinâmica para tornar o planejamento financeiro mais acessível e intuitivo.

## 💡 As 5 Perguntas de Negócio

A ferramenta responde a cinco perguntas fundamentais na aba principal `APP`:

| # | Pergunta de Negócio | Localização na Planilha | Função / Lógica Utilizada |
|---|---|---|---|
| 1 | **Quanto investir por mês?** | Célula `D11` (`aporte`) | Entrada direta do valor mensal a investir. |
| 2 | **Por quantos anos investir?** | Célula `D12` (`anos`) | Definição do horizonte de investimento. |
| 3 | **Qual a taxa de rendimento mensal?** | Célula `D13` (`taxa_mensal`) | Percentual de rentabilidade mensal utilizado na simulação. |
| 4 | **Quanto patrimônio será acumulado?** | Célula `D14` (`patrimonio_acumulado`) | Cálculo do valor futuro por meio da função `VF`. |
| 5 | **Quanto poderá receber de dividendos por mês?** | Célula `D15` (`dividendos_mensais`) | Estimativa de renda mensal com base no patrimônio projetado e no rendimento da carteira. |

---

## 🛠️ Engenharia da Planilha e Fórmulas

### 1. Função `VF` — Valor Futuro

A função `VF` calcula o valor futuro de uma série de aportes periódicos, considerando uma taxa de rendimento e um prazo determinado.

**Fórmula utilizada:**

```excel
=VF(taxa_mensal; anos*12; -aporte)
```

**Parâmetros:**

- `taxa_mensal`: taxa de rendimento mensal utilizada na projeção.
- `anos*12`: converte o prazo em anos para o número total de meses.
- `-aporte`: valor do aporte mensal com sinal negativo, representando uma saída de caixa no cálculo financeiro.

O resultado representa uma projeção do patrimônio acumulado ao final do período, considerando as premissas informadas.

### 2. Chave Composta e Função `PROCV`

Para permitir a alteração dinâmica da distribuição da carteira conforme o perfil de investidor selecionado — **Conservador, Moderado ou Agressivo** —, foi utilizada a técnica de chave composta.

**Etapa 1 — Criação da chave na aba `APOIO`**

A coluna A concatena o perfil de investidor com o tipo de FII:

```excel
=B2&"-"&C2
```

Exemplo de chave gerada:

```text
Moderado-PAPEL
```

**Etapa 2 — Busca da distribuição na aba `APP`**

A função `PROCV` localiza a combinação entre o perfil selecionado e o tipo de fundo para retornar o percentual correspondente:

```excel
=PROCV(perfil&"-"&B30;APOIO!$A$2:$D$19;4;FALSO)
```

Essa estrutura permite consultar a distribuição configurada na aba de apoio e atualizar os percentuais apresentados conforme o perfil selecionado.

### 3. Intervalos Nomeados

Para facilitar a leitura e a manutenção das fórmulas, foram utilizados intervalos nomeados que representam os principais parâmetros e resultados da simulação.

| Intervalo Nomeado | Descrição |
|---|---|
| `salario` | Rendimento familiar utilizado como referência no planejamento. |
| `rendimento_carteira` | Taxa média de dividend yield estimada para a carteira. |
| `sugestao_investimento` | Valor sugerido para o aporte, calculado com base em 30% do salário. |
| `aporte` | Valor mensal efetivamente investido na simulação. |
| `anos` | Prazo do projeto em anos. |
| `taxa_mensal` | Taxa mensal utilizada no cálculo do valor futuro. |
| `patrimonio_acumulado` | Resultado projetado do patrimônio acumulado. |
| `dividendos_mensais` | Estimativa de renda passiva mensal. |
| `perfil` | Célula vinculada ao menu suspenso de seleção do perfil de investidor. |

---

## 📊 Matriz de Distribuição por Perfil de Investidor

Os percentuais foram estruturados na aba `APOIO`, totalizando **100% para cada perfil**.

| Tipo de FII | Conservador | Moderado | Agressivo |
|---|---:|---:|---:|
| **PAPEL** | 30% | 32% | 50% |
| **TIJOLO** | 50% | 35% | 10% |
| **HÍBRIDOS** | 10% | 8% | 10% |
| **FOFs** | 10% | 5% | 10% |
| **DESENVOLVIMENTO** | 0% | 10% | 10% |
| **HOTELARIAS** | 0% | 10% | 10% |
| **TOTAL** | **100%** | **100%** | **100%** |

A matriz permite visualizar diferentes estratégias de alocação, de acordo com o perfil selecionado. Os percentuais representam parâmetros definidos para a simulação, e não recomendações personalizadas de investimento.

---

## ✨ Destaques e Evoluções em Relação ao Modelo Base

1. **Contextualização infantil:** adaptação do objetivo e da apresentação visual para o planejamento financeiro de longo prazo voltado aos filhos.
2. **Gráfico dinâmico de distribuição:** inclusão de um gráfico circular ou de rosca vinculado à tabela de alocação dos FIIs, com atualização conforme o perfil selecionado.
3. **Validação de dados:** implementação de um menu suspenso com as opções `Conservador`, `Moderado` e `Agressivo`.
4. **Automação de cálculos:** utilização de fórmulas financeiras e intervalos nomeados para simplificar a simulação.
5. **Acabamento visual profissional:** ocultação das linhas de grade, aplicação de uma paleta de cores *Dark Blue & Gray* e destaque visual para as células calculadas.
6. **Experiência interativa:** organização da planilha para facilitar a entrada de dados e a interpretação dos resultados.

---

## 🚀 Como Executar o Projeto

1. Faça o clone ou o download deste repositório.
2. Abra o arquivo `Cofre_Futuro_Infantil_Simulador.xlsx` no Microsoft Excel ou em uma ferramenta compatível.
3. Acesse a aba `APP`.
4. Preencha os campos das seções **CONFIGURAÇÕES** e **INVESTIMENTO MENSAL & SIMULAÇÃO**.
5. Informe o aporte mensal, o prazo de investimento e a taxa de rendimento utilizada na projeção.
6. Selecione o perfil de investidor desejado: `Conservador`, `Moderado` ou `Agressivo`.
7. Observe a atualização dos percentuais de distribuição da carteira, do gráfico e dos resultados calculados.

---

## ⚠️ Aviso Importante

Este projeto tem finalidade educacional e demonstrativa. Os resultados apresentados são estimativas matemáticas baseadas nos parâmetros informados e não representam garantia de rentabilidade ou de recebimento de dividendos.

Fundos de Investimento Imobiliário estão sujeitos a riscos de mercado, oscilações de preços, variações nos rendimentos e possíveis perdas de capital. As premissas utilizadas devem ser avaliadas antes de qualquer decisão financeira.

---

## 👩‍💻 Autoria

Projeto desenvolvido como parte de um desafio prático da **DIO — Digital Innovation One**, com foco na aplicação do Microsoft Excel para simulação financeira, organização de dados e construção de uma ferramenta interativa de apoio ao planejamento patrimonial.

