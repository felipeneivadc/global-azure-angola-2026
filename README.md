# Global Azure Angola 2026 — Demos & Recursos

Repositório de demonstrações apresentadas no **Global Azure Angola 2026**, cobrindo cenários de **Microsoft Fabric**, **Power BI Semantic Models** e **Microsoft Copilot Studio**.

## Conteúdo do Repositório

```
.
├── copilot-studio/                      # Solução Power Platform (Copilot Studio)
│   └── DisruptivoDataAgent/             # Agente "Vendas Veicular" → Teams / M365 Copilot
│
├── workspace-fabric/                    # Workspace Fabric (Git Integration)
│   ├── Disruptivo-Data-Agent.DataAgent/ # Fabric Data Agent conectado ao modelo de vendas
│   ├── Vendas-Veiculares.SemanticModel/ # Modelo semântico — tabela TabVendas
│   └── Vendas-RLS.SemanticModel/        # Modelo semântico — Row-Level Security
│
├── .gitignore
└── README.md
```

## Arquitetura

```
┌─────────────────────┐       ┌───────────────────────────────────┐
│  Microsoft Copilot  │       │        Microsoft Fabric           │
│       Studio        │       │                                   │
│                     │       │  ┌─────────────────────────────┐  │
│  Agente de Dados ───┼───────┼─▶│  Disruptivo Data Agent      │  │
│  de Vendas Veicular │       │  └──────────┬──────────────────┘  │
│                     │       │             │                      │
│  (Teams / M365      │       │  ┌──────────▼──────────────────┐  │
│   Copilot)          │       │  │  Vendas-Veiculares          │  │
└─────────────────────┘       │  │  (Semantic Model)           │  │
                              │  │  TabVendas: produto, UF,    │  │
                              │  │  cidade, total, comissão... │  │
                              │  └─────────────────────────────┘  │
                              │                                   │
                              │  ┌─────────────────────────────┐  │
                              │  │  Vendas-RLS                 │  │
                              │  │  (Semantic Model)           │  │
                              │  │  RLS Dinâmico + Reg Norte   │  │
                              │  └─────────────────────────────┘  │
                              └───────────────────────────────────┘
```

## Tecnologias Utilizadas

- **Microsoft Copilot Studio** — Agente conversacional com IA generativa
- **Microsoft Fabric** — Data Agent + Semantic Models via Git Integration
- **Power BI / TMDL** — Modelos semânticos com Row-Level Security
- **Power Platform / PAC CLI** — Exportação e importação de soluções

## Pré-requisitos

| Requisito | Detalhes |
|---|---|
| Microsoft Fabric | Licença trial ou capacidade ativa (F64+) |
| Copilot Studio | Licença Power Platform com Copilot Studio |
| PAC CLI | [Instalar](https://learn.microsoft.com/power-platform/developer/cli/introduction) |
| Git | Qualquer cliente Git com suporte a long paths |
| Acesso | Microsoft Teams ou Microsoft 365 Copilot |

## Como Replicar

### 1. Clonar o repositório

```bash
git clone <URL-do-repositorio>
cd global-azure-angola-2026
git config core.longpaths true
```

### 2. Importar o workspace no Microsoft Fabric

1. Acesse o [Microsoft Fabric](https://app.fabric.microsoft.com) e crie um workspace com capacidade ativa
2. Vá em **Configurações do Workspace → Git Integration**
3. Conecte ao repositório e selecione a branch `main`, pasta raiz: `workspace-fabric/`
4. Clique em **Sync** — os Semantic Models e o Data Agent serão criados automaticamente
5. Abra cada Semantic Model e configure as **credenciais da fonte de dados**
6. Faça o refresh dos dados

### 3. Importar o agente no Copilot Studio

1. Instale o [PAC CLI](https://learn.microsoft.com/power-platform/developer/cli/introduction)
2. Autentique no ambiente:
   ```bash
   pac auth create --environment <URL-do-ambiente>
   ```
3. Importe a solução:
   ```bash
   pac solution import --path copilot-studio/DisruptivoDataAgent/
   ```
4. No portal Power Apps → **Soluções**, abra `DisruptivoDataAgent`
5. Configure a **connection reference** do Fabric Data Agent (aponte para o Data Agent criado no passo 2)
6. Abra o **Copilot Studio** e publique o agente

### 4. Configurações obrigatórias após importação

| Item | O que configurar |
|---|---|
| `workspaceId` no Copilot Studio | No action `Disruptivo-Data-Agent`, substitua `00000000-0000-0000-0000-000000000000` pelo ID real do seu workspace Fabric |
| Fonte de dados `TabVendas` | O caminho `C:\Dados\Base primeiros passos.xlsx` é um placeholder — aponte para o local real do arquivo Excel |
| Connection reference | Configure a conexão do Fabric Data Agent no Power Apps |
| Credenciais dos Semantic Models | Configure as credenciais de acesso às fontes no Fabric |

### 5. Testar

- Abra o **Microsoft Teams** e converse com o agente
- Pergunte sobre vendas veiculares — ex: *"Qual o total de vendas em SP?"*

## Estrutura dos Dados

### Vendas-Veiculares (Semantic Model)

Tabela `TabVendas` com dados de vendas veiculares:

| Coluna | Tipo | Descrição |
|---|---|---|
| `DATAVENDA` | DateTime | Data da venda |
| `IDPRODUTO` | Int64 | ID do produto |
| `PRODUTO` | String | Nome do veículo |
| `UF` | String | Unidade federativa |
| `CIDADE` | String | Cidade da venda |
| `REGIÃO` | String | Região do Brasil |
| `TOTAL` | Int64 | Valor total da venda |
| `COMISSÃO` | Double | Comissão do vendedor |

### Vendas-RLS (Semantic Model)

Demonstra **Row-Level Security** com duas abordagens:

| Role | Tipo | Regra |
|---|---|---|
| `RLS_Dinâmico` | Dinâmico | Filtra pelo e-mail do usuário via `USERNAME()` |
| `Reg NORTE` | Estático | Filtra vendas da região Norte |

## Evento

**Global Azure Angola 2026**  
Palestrante: Felipe Neiva  
Idioma: Português (pt-BR)