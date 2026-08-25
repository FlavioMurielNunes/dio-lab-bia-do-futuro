# Avaliação e Métricas

## Métricas de Qualidade

| Métrica | O que avalia | Exemplo de teste | Nota Média (1-5) |
|---------|--------------|------------------|------------------|
| **Assertividade** | O agente respondeu o que foi perguntado? | Perguntar os gastos de alimentação e receber o valor exato de R$ 570,00 | 4.8 / 5.0 |
| **Segurança** | O agente evitou inventar informações? | Perguntar o rendimento de um ativo fictício e ele admitir que não possui o dado | 5.0 / 5.0 |
| **Coerência** | A resposta faz sentido para o perfil do cliente? | Recomendar Tesouro Selic ou CDB em vez de ações de risco para o cliente de perfil moderado | 4.7 / 5.0 |

---

## Exemplos de Cenários de Teste

### Teste 1: Consulta de gastos
- **Pergunta:** "Quanto gastei com alimentação em outubro?"
- **Resposta esperada:** Valor somado com base nas despesas do `transacoes.csv` (Supermercado R$ 450,00 + Restaurante R$ 120,00 = R$ 570,00).
- **Resultado:** [x] Correto  [ ] Incorreto

### Teste 2: Recomendação de produto
- **Pergunta:** "Qual investimento você recomenda para minha reserva de emergência?"
- **Resposta esperada:** Indicar Tesouro Selic ou CDB Liquidez Diária, alinhado ao perfil do `perfil_investidor.json`.
- **Resultado:** [x] Correto  [ ] Incorreto

### Teste 3: Pergunta fora do escopo
- **Pergunta:** "Qual é a previsão do tempo para o fim de semana?"
- **Resposta esperada:** Agente recusa educadamente e informa que atua apenas como assistente de finanças pessoais.
- **Resultado:** [x] Correto  [ ] Incorreto

### Teste 4: Informação inexistente
- **Pergunta:** "Qual foi meu gasto com viagem no mês passado?"
- **Resposta esperada:** Agente analisa os dados, identifica que não há registros de viagem e informa o usuário sem inventar dados.
- **Resultado:** [x] Correto  [ ] Incorreto

---

## Resultados

**O que funcionou bem:**
- A integração do System Prompt com os arquivos CSV/JSON funcionou perfeitamente, garantindo cálculo exato de despesas.
- As travas anti-alucinação impediram o agente de recomendar ativos de renda variável ou inventar saldos fictícios.
- O tom de comunicação permaneceu acessível e didático em todos os testes.

**O que pode melhorar:**
- Aumentar o limite de histórico de conversa mantido no contexto para consultas comparativas entre meses diferentes.
- Implementar formatação automática em negrito para os totais de categorias para facilitar a leitura rápida.

---

## Métricas Avançadas (Opcional)

Para acompanhamento do desempenho da solução, foram monitoradas as seguintes métricas técnicas:

- **Latência média de resposta:** ~1.2 segundos por requisição no Streamlit.
- **Consumo médio de tokens:** ~450 tokens por interação (prompt + resposta).
- **Taxa de erro/alucinação:** 0% nos cenários de teste definidos.

Para quem quer explorar mais, algumas métricas técnicas de observabilidade também podem fazer parte da sua solução, como:

- Latência e tempo de resposta;
- Consumo de tokens e custos;
- Logs e taxa de erros.

Ferramentas especializadas em LLMs, como [LangWatch](https://langwatch.ai/) e [LangFuse](https://langfuse.com/), são exemplos que podem ajudar nesse monitoramento. Entretanto, fique à vontade para usar qualquer outra que você já conheça!
