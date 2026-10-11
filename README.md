#  Fluxo Multi Agentes | Legião Automática

<p align="center">
  <b>Sistema avançado de atendimento automatizado via WhatsApp utilizando n8n, OpenAI, Redis e Supabase.</b>
</p>

---

##  Visão Geral do Projeto

Este repositório contém a arquitetura de automação de atendimento inteligente desenvolvida para a **Legião Automática**. O projeto implementa um fluxo multi-agentes capaz de recepcionar leads, transcrever áudios, gerenciar buffers de mensagens em tempo real, consultar bases de conhecimento vetoriais (*RAG*) e disparar respostas humanizadas de forma fragmentada no WhatsApp através da Avisa API.

## 🛠️ Tecnologias Utilizadas

* **n8n** (Orquestração de fluxos e nós de LangChain)
* **OpenAI API** (GPT-4o-mini para geração de respostas e Whisper para transcrição de áudio)
* **Supabase** (Armazenamento relacional de usuários e Vector Store para bases de conhecimento)
* **Redis** (Gerenciamento de filas, controle de atendimento e buffer de mensagens)
* **PostgreSQL** (Armazenamento de histórico de chat para memória conversacional)

## 📐 Arquitetura e Funcionamento

1. **Recepção e Normalização:** Captura de webhooks do WhatsApp, filtragem de chats privados e conversão de mídias (áudio/texto/imagem).
2. **Buffer de Mensagens (Debounce):** Utilização do Redis para acumular mensagens enviadas em sequência pelo usuário dentro de uma janela de 15 segundos, evitando disparos picotados.
3. **Identificação e Contexto:** Validação e criação automática de perfis de usuários integrados ao Supabase.
4. **Camada Cognitiva (AI Agent):** Processamento inteligente com acesso dinâmico a ferramentas de consulta de perfil e base de conhecimento vetorial.
5. **Envio Fracionado:** Divisão de respostas longas em blocos naturais com intervalos cadenciados para simular uma digitação humana real.

## ⚙️ Como Importar e Configurar

1. Certifique-se de ter uma instância do **n8n** rodando (versão com suporte a LangChain recomendada).
2. Importe o arquivo JSON principal do fluxo (`08_ Vector Store.json`) no seu painel do n8n[cite: 1].
3. Configure as credenciais necessárias nas respectivas integrações:
   * Conta da OpenAI (API Key)
   * Supabase (API e Vector Store)
   * Redis
   * PostgreSQL (Memory)
   * Credenciais de API da Avisa API para o envio de mensagens.
4. Ative o fluxo e configure o webhook na sua plataforma de disparo de WhatsApp.

---
Desenvolvido com foco em alta performance e escalabilidade para automações de negócios.
