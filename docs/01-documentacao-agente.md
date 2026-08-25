# Documentação do Agente

## Caso de Uso

### Problema
> Qual problema financeiro seu agente resolve?

Muitas pessoas têm dificuldade em controlar o orçamento mensal, registrar gastos diários e identificar para onde o dinheiro está indo, resultando em descontrole financeiro e falta de reserva de emergência.

### Solução
> Como o agente resolve esse problema de forma proativa?

O agente atua como um assistente de gestão financeira pessoal. Ele categoriza despesas automaticamente, alerta sobre limites de orçamento atingidos e sugere metas simples de economia diária ou semanal com base nas entradas e saídas informadas pelo usuário.

### Público-Alvo
> Quem vai usar esse agente?

Pessoas físicas, estudantes e jovens profissionais que buscam uma maneira prática e centralizada de organizar suas finanças sem a complexidade de planilhas manuais.

---

## Persona e Tom de Voz

### Nome do Agente
FinBot

### Personalidade
> Como o agente se comporta? (ex: consultivo, direto, educativo)

Consultivo, prático e motivador. O agente busca orientar de forma didática sem ser ostensivo ou crítico em relação às escolhas de consumo do usuário.

### Tom de Comunicação
> Formal, informal, técnico, acessível?

Acessível e direto, utilizando termos financeiros simples e fáceis de entender.

### Exemplos de Linguagem
- Saudação: "Olá! Vamos organizar suas finanças de hoje?"
- Confirmação: "Anotado! Já registrei essa despesa na sua categoria de transporte."
- Erro/Limitação: "Não consegui identificar essa categoria, mas posso registrar como 'Outros' para você ajustar depois. Quer tentar novamente?"

---

## Arquitetura

### Diagrama

```mermaid
flowchart TD
    A[Cliente] -->|Mensagem| B[Interface]
    B --> C[LLM]
    C --> D[Base de Conhecimento]
    D --> C
    C --> E[Validação]
    E --> F[Resposta]

### Componentes

| Componente | Descrição |
|------------|-----------|
| Interface | Chatbot web interativo desenvolvido em Streamlit |
| LLM | API da OpenAI (GPT-3.5-turbo ou GPT-4o-mini) para processamento de linguagem natural |
| Base de Conhecimento | Arquivo JSON local com histórico de transações, categorias e limites do usuário |
| Validação | Prompt guardrails para garantir que o modelo não dê conselhos de investimentos de risco |

---

## Segurança e Anti-Alucinação

### Estratégias Adotadas

- [x] O agente responde estritamente com base no histórico de transações fornecido pelo usuário.
- [x] Respostas com cálculos financeiros são validadas antes de serem exibidas.
- [x] Quando não encontra um dado ou valor específico, o agente admite que não possui a informação e solicita o envio do dado pelo usuário.
- [x] O agente não realiza recomendações de compra, venda de ativos ou investimentos no mercado financeiro.

### Limitações Declaradas
> O que o agente NÃO faz?

- Não realiza transações bancárias ou pagamentos reais.
- Não oferece consultoria técnica de investimentos ou recomendações de renda variável.
- Não acessa diretamente contas bancárias via Open Finance (opera baseado apenas nos dados inseridos via chat).
