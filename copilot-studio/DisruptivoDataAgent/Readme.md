# Copilot Studio — Agente de Dados de Vendas Veicular

Solução Power Platform contendo o agente **"Agente de Dados de Vendas Veicular"**, criado no Microsoft Copilot Studio.

## Visão Geral

- **Nome:** Agente de Dados de Vendas Veicular
- **Idioma:** Português (pt-BR)
- **Canais:** Microsoft Teams, Microsoft 365 Copilot
- **IA:** Reconhecedor generativo com GPT e busca semântica
- **Integração:** Conectado ao **Fabric Data Agent** (`Disruptivo-Data-Agent`) via connection reference

## Estrutura da Solução

| Pasta | Conteúdo |
|---|---|
| `bots/` | Definição do bot (nome, canais, autenticação, ícone) |
| `botcomponents/` | 15 componentes: 1 ação customizada, 1 GPT, 13 tópicos (Saudação, Despedida, Fallback, etc.) |
| `botcomponent_connectionreferenceset/` | Vínculo entre a ação e a connection reference do Fabric Data Agent |
| `connectionreferences/` | Connection reference para o conector `shared_fabricdataagent` |
| `publishers/` | Publisher: Global Azure Angola (prefixo `dev`) |
| `solutions/` | Manifesto da solução v1.0.0.0 (unmanaged) |

## Como Importar

1. Instale o [PAC CLI](https://learn.microsoft.com/power-platform/developer/cli/introduction)
2. Autentique no ambiente: `pac auth create --environment <URL>`
3. Importe a solução:
   ```bash
   pac solution import --path copilot-studio/DisruptivoDataAgent/
   ```
4. No portal Power Apps, configure a **connection reference** do Fabric Data Agent
5. Abra o Copilot Studio e publique o agente