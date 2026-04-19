# Workspace Fabric

Artefatos do Microsoft Fabric exportados via **Git Integration** (schema v2.0).

## Itens do Workspace

| Pasta | Tipo | Descrição |
|---|---|---|
| `Disruptivo-Data-Agent.DataAgent/` | Data Agent | Agente de dados de vendas veiculares — v1.0 publicada, instruções em pt-BR |
| `Vendas-Veiculares.SemanticModel/` | Semantic Model | Modelo tabular com a tabela `TabVendas` (vendas veiculares) |
| `Vendas-RLS.SemanticModel/` | Semantic Model | Modelo com RLS dinâmico (`USERNAME()`) e estático (Região Norte) |

## Como Restaurar no Fabric

1. Acesse o [Microsoft Fabric](https://app.fabric.microsoft.com) e crie um workspace com capacidade ativa
2. Vá em **Configurações do Workspace → Git Integration**
3. Conecte ao repositório e selecione a pasta `workspace-fabric/` como raiz
4. Faça o **Sync** para importar todos os artefatos
5. Abra cada Semantic Model e configure as **credenciais da fonte de dados**
6. Faça o refresh dos dados

## Observações

- Os Semantic Models usam formato **TMDL** (Tabular Model Definition Language)
- O Data Agent referencia o modelo `Vendas-Veiculares` via `artifactId` (logicalId)
- A cultura dos modelos é `pt-BR`