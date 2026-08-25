# Base de Conhecimento

## Dados Utilizados

| Arquivo | Formato | Utilização no Agente |
|---------|---------|---------------------|
| `historico_atendimento.csv` | CSV | Consultar interações anteriores (dúvidas sobre CDB, Tesouro e suporte) para dar continuidade aos atendimentos. |
| `perfil_investidor.json` | JSON | Acessar dados do cliente (João Silva, perfil moderado, renda R$ 5.000,00 e metas como reserva de emergência). |
| `produtos_financeiros.json` | JSON | Consultar catálogo de produtos (Tesouro Selic, CDB, LCI/LCA, Fundo Multimercado) para sugerir opções adequadas. |
| `transacoes.csv` | CSV | Mapear receitas (Salário) e despesas (Aluguel, Mercado, Netflix, etc.) para análise de padrão de gastos. |

---

## Adaptações nos Dados

Utilizamos os arquivos mockados da pasta `data` em sua estrutura original, realizando apenas o parsing automático de datas e tipos numéricos no código para garantir que os cálculos de orçamento e recomendações sejam feitos sem erros.

---

## Estratégia de Integração

### Como os dados são carregados?
Os arquivos em formato JSON e CSV são lidos localmente via código Python durante a inicialização da aplicação e mantidos no estado da sessão do usuário.

### Como os dados são usados no prompt?
Os dados estruturados do cliente e o histórico recente de transações são injetados diretamente no **system prompt** como contexto inicial. As informações sobre produtos e histórico prévio são consultadas de forma dinâmica para complementar as respostas do agente.

---

## Exemplo de Contexto Montado

[DADOS DO CLIENTE]
- Nome: João Silva (32 anos)
- Profissão: Analista de Sistemas
- Renda Mensal: R$ 5.000,00 | Perfil: Moderado
- Reserva Atual: R$ 10.000,00 (Meta: R$ 15.000,00 até 06/2026)

[ÚLTIMAS TRANSAÇÕES REGISTRADAS]
- 01/10/2025: Salário | Receita | +R$ 5.000,00
- 02/10/2025: Aluguel | Moradia | -R$ 1.200,00
- 03/10/2025: Supermercado | Alimentação | -R$ 450,00
- 05/10/2025: Netflix | Lazer | -R$ 55,90
- 07/10/2025: Farmácia | Saúde | -R$ 89,00
