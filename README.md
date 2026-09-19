

[README.md](https://github.com/user-attachments/files/32407852/README.md)
# Assistente Tigo (treinamento T.I.G.O.N)

Chatbot em Google Colab que responde até 3 perguntas sobre o curso fictício **T.I.G.O.N** (Treinamento Introdutório de Git, Orientação e Noções de programação), um programa de 5 semanas que introduz versionamento de código (Git), lógica de programação e mentoria. Depois da terceira resposta, o bot gera automaticamente um **resumo do atendimento** e encerra a conversa.

## Comportamento

- A saudação aparece apenas na interface e não conta como pergunta.
- Cada mensagem enviada vale 1 de 3 perguntas.
- Falha de API (ex.: 503 de alta demanda) não consome a pergunta: basta enviar de novo.
- Ao fim da terceira resposta, uma chamada separada gera o resumo e a entrada é bloqueada.

## LLM

- Google Gemini (modelo `gemini-3.6-flash`) via SDK `google-genai`.
- Retry automático em chamadas instáveis.

## Como executar

1. Abra o notebook no Google Colab.
2. Configure a chave da API (seção abaixo).
3. Execute **Runtime**, depois **Run all**.
4. Converse com o Tigo. Para reiniciar, execute novamente a última célula (a da interface).

## Configuração da chave

A chave é lida de um arquivo `.env` e, se ele não existir, usa o segredo `KEY_FATEC` do Colab.

### Via arquivo .env

Crie um arquivo `.env` na pasta `/content` do Colab:

```
GEMINI_API_KEY=sua_chave_aqui
```

### Via segredo do Colab

Adicione um segredo chamado `KEY_FATEC` na barra lateral (ícone de chave, New secret) com a chave da API e autorize o notebook a usar esse segredo.

## Estrutura do notebook

1. **Instalação** – instala `google-genai`, `python-dotenv` e `panel`.
2. **Configuração** – lê a chave e define a chamada ao modelo com retry.
3. **Contexto** – persona, regras e base de conhecimento do T.I.G.O.N.
4. **Lógica** – classe `Sessao`, contagem de perguntas e geração do resumo.
5. **Interface** – chat com Panel.

## Dependências

- Python 3
- `google-genai`, `python-dotenv`, `panel` (instalados na primeira célula)
