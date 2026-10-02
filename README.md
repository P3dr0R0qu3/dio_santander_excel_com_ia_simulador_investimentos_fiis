# Simulador de Investimentos em Fundos Imobiliários (FIIs)

Projeto desenvolvido como parte do desafio prático de Excel da DIO. Esta ferramenta simula a projeção de patrimônio e o recebimento de dividendos através de aportes mensais em Fundos Imobiliários, ajustando a alocação da carteira com base no perfil do investidor.

## O que a ferramenta responde?
A planilha foi construída para responder a 5 perguntas centrais de negócio em sua interface principal (Dashboard):
1. **Quanto investir por mês?** (Definido pelo usuário, com sugestão automática de 30% da renda).
2. **Por quantos anos?** (Definido pelo usuário).
3. **Qual a taxa de rendimento mensal?** (Definido pelo usuário).
4. **Quanto de patrimônio vai acumular?** (Calculado automaticamente via função `VF`).
5. **Quanto vai receber de dividendos por mês?** (Calculado sobre o patrimônio acumulado).

## Lógica por trás das Fórmulas

### A Função `VF` (Valor Futuro)
Utilizada para projetar o efeito dos juros compostos ao longo do tempo. 
`=VF(Taxa_Mensal; Prazo_Anos * 12; -Aporte_Mensal; 0; 0)`
- **Taxa:** Rendimento mensal.
- **NPER:** Prazo convertido para meses (`Anos * 12`).
- **PGTO:** O aporte mensal inserido de forma negativa, representando a saída de caixa do investidor para a corretora.

### A Chave Composta e o `PROCV`
Para a divisão da carteira, foi utilizada uma aba de apoio com as diretrizes de cada perfil (Conservador, Moderado, Arrojado). 
Como o `PROCV` precisa de um valor único de busca, criei uma **Chave Composta** concatenando o Perfil escolhido e o Tipo de Fundo (ex: `ConservadorTijolo`). A fórmula junta o perfil selecionado na validação de dados com o nome do fundo na linha, localizando o percentual exato na matriz de apoio.

## Configurações Técnicas Aplicadas
- **Intervalos Nomeados:** Para manter as fórmulas legíveis e à prova de erros de arrasto, as variáveis principais foram nomeadas (ex: `Salario`, `Aporte_Mensal`, `Taxa_Mensal`, `Prazo_Anos`, `Perfil_Escolhido`).
- **Validação de Dados:** Lista suspensa para seleção do perfil do investidor.
- **Formatação Condicional / UI:** Ocultação de linhas de grade, bloqueio visual de células de cálculo (fundo cinza) e foco na experiência do usuário (UX).

## Perfis de Investimento e Alocação
Os percentuais foram definidos para fins de simulação e aprendizado (não configuram recomendação de investimento):

| Tipo de Fundo | Conservador | Moderado | Arrojado |
| :--- | :--- | :--- | :--- |
| **Tijolo** | 60% | 40% | 20% |
| **Papel** | 30% | 40% | 20% |
| **Fiagro** | 10% | 10% | 20% |
| **FoF** | 0% | 10% | 20% |
| **Infra / Misto** | 0% | 0% | 20% |

## Evoluções do Projeto (Extras implementados)
- [x] Sugestão automática de investimento focada em 30% do salário informado.
- [x] Gráfico de rosca dinâmico para visualização da carteira.
- [x] Projeção de cenários de longo prazo (2, 5, 10, 20 e 30 anos) em tabela paralela.

## Demonstração
<img width="816" height="577" alt="Tela2" src="https://github.com/user-attachments/assets/7e35a79d-77c8-42eb-af5a-46f2e7228d9b" />
<img width="805" height="578" alt="Tela1" src="https://github.com/user-attachments/assets/9969b580-cb4f-4f36-b1be-7d0a4eed5671" />
