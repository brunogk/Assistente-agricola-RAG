# 🌱 Assistente Agrícola com RAG + Text-to-SQL

Sistema de perguntas e respostas em linguagem natural sobre dados de análise de solo, combinando **RAG (Retrieval-Augmented Generation)** para perguntas interpretativas e **Text-to-SQL** para perguntas quantitativas — unindo conhecimento agronômico de domínio com IA generativa aplicada.

> Projeto de portfólio desenvolvido por **Bruno** — Biólogo e Agrônomo, Doutorando em Ciências do Solo (UFPR), em transição para Ciência de Dados.

---

## 💡 Por que esse projeto existe

A maioria dos projetos de portfólio em IA generativa usa datasets genéricos do Kaggle. Este projeto nasce de um problema real: **agricultores e consultores recebem laudos de análise de solo cheios de números técnicos (pH, CTC, V%, micronutrientes) e precisam de respostas práticas, rápidas, em linguagem natural.**

Combinando 10+ anos de formação em ciências do solo com técnicas modernas de IA generativa, este projeto demonstra como o conhecimento de domínio pode tornar um sistema de IA genuinamente útil — não apenas tecnicamente correto.

---

## 🧠 Arquitetura

O sistema usa **duas estratégias complementares**, escolhidas dinamicamente conforme o tipo de pergunta:

```
┌─────────────────────┐
│   Pergunta do        │
│   produtor (PT-BR)   │
└──────────┬───────────┘
           │
           ▼
   ┌───────────────┐
   │  Pergunta é    │
   │ interpretativa │──── Sim ───┐
   │  ou numérica?  │            │
   └───────┬────────┘            ▼
           │              ┌─────────────┐
        Numérica          │     RAG     │
           │              │  Embeddings  │
           ▼              │  + FAISS    │
   ┌─────────────┐        │  + GPT-4o   │
   │ Text-to-SQL │        └─────────────┘
   │  GPT-4o-mini│
   │  + SQLite   │
   └─────────────┘
```

| Pipeline | Quando usar | Exemplo de pergunta |
|---|---|---|
| **RAG** | Perguntas interpretativas e contextuais | *"O talhão T03 está adequado para soja?"* |
| **Text-to-SQL** | Perguntas quantitativas e agregadas | *"Qual a média de pH dos talhões de soja?"* |

---

## ⚙️ Stack técnica

- **OpenAI `text-embedding-3-small`** — geração de embeddings semânticos
- **FAISS** — índice vetorial para busca por similaridade de cosseno
- **OpenAI `gpt-4o-mini`** — geração de respostas e tradução Text-to-SQL
- **SQLite** — execução segura de queries geradas dinamicamente
- **Pandas / Matplotlib** — manipulação e visualização de dados
- **ipywidgets** — interface interativa dentro do Google Colab

---

## 🔍 Funcionalidades

✅ Busca semântica sobre laudos de solo via embeddings + FAISS
✅ Respostas agronômicas contextualizadas com faixas de referência para Latossolo Vermelho (PR)
✅ Tradução de linguagem natural para SQL, com camada de validação de segurança (somente `SELECT`)
✅ Interface interativa com seletor de modo (RAG vs SQL)
✅ Visualizações de diagnóstico de fertilidade (pH, saturação por bases, relação P×K)

---

## 🚀 Como executar

1. Abra o notebook `assistente_agricola_rag.ipynb` no [Google Colab](https://colab.research.google.com)
2. Configure sua chave da OpenAI no painel de **Secrets** (🔑) do Colab, com o nome `OPENAI_API_KEY`
3. Execute as células em ordem, de cima para baixo
4. Use a interface na Etapa 10 para fazer perguntas em linguagem natural

> **Custo estimado:** menos de US$ 0,01 por execução completa do notebook (8 talhões, modelos `gpt-4o-mini` e `text-embedding-3-small`).

---

## 📊 Exemplos de uso

**RAG (interpretativo):**
> *"Quais talhões precisam de calagem urgente?"*
> → O sistema busca os talhões com pH baixo e alumínio elevado, e recomenda ação corretiva com base nas faixas técnicas de referência.

**Text-to-SQL (quantitativo):**
> *"Qual a média de pH dos talhões de soja?"*
> → O sistema gera `SELECT AVG(pH_CaCl2) FROM analise_solo WHERE cultura = 'Soja'`, executa, e interpreta o resultado numérico.

---

## 🗺️ Roadmap

- [ ] Substituir dataset sintético por laudos reais de laboratório
- [ ] Roteador automático entre RAG e SQL via function calling
- [ ] Deploy com interface Gradio
- [ ] Integração com dados climáticos (NASA POWER API)
- [ ] Upload de CSV próprio pelo usuário

---

## 👤 Sobre o autor

Bruno é biólogo e agrônomo, atualmente doutorando em Ciências do Solo pela UFPR, em transição para Ciência de Dados.

📫 [LinkedIn](#) · [GitHub](#)
