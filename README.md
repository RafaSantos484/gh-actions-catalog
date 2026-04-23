# GitHub Actions Catalog

Catálogo público de **workflows reutilizáveis do GitHub Actions**, com foco em **padronização**, **reuso** e **manutenção centralizada** de pipelines de CI/CD.

Este repositório não executa pipelines próprios — ele fornece **reusable workflows** para serem consumidos por outros repositórios.

---

## 🎯 Objetivos

- Evitar duplicação de pipelines entre projetos
- Padronizar CI entre múltiplos repositórios
- Centralizar manutenção e evolução dos workflows
- Garantir previsibilidade por meio de versionamento explícito

---

## 🧩 O que há neste catálogo

✅ **Reusable workflows**, definidos com `workflow_call`  
✅ Documentação **espelhada** para cada workflow  
✅ Política clara de versionamento  
✅ Estrutura escalável para novos tipos de workflow

---

## 📁 Estrutura do repositório

```text
.
├── .github/
│   └── workflows/
│       └── ci-nodejs.yml
├── docs/
│   ├── README.md
│   ├── usage.md
│   ├── versioning.md
│   └── ci-nodejs.md
└── README.md
```

### Princípio de espelhamento

Para cada workflow em:

  .github/workflows/arquivo.yml

existe uma documentação correspondente em:

  docs/arquivo.md

Observacao: o GitHub Actions exige que reusable workflows estejam no nivel raiz de `.github/workflows/`.

---

## 🚀 Workflows disponíveis

### CI

- **Node.js**
  - Workflow: `.github/workflows/ci-nodejs.yml`
  - Documentação: `docs/ci-nodejs.md`

---

## 🧪 Como usar

Os workflows deste catálogo devem ser consumidos a partir de outros repositórios usando a diretiva `uses`.

Exemplo:

```yaml
jobs:
  ci:
    uses: ORG/REPO/.github/workflows/ci-nodejs.yml@v1.0.0
    with:
      node-version: 18
```

📘 Consulte sempre:

- `docs/usage.md` — uso geral
- `docs/versioning.md` — versionamento
- O `.md` espelhado do workflow desejado

---

## 🔖 Versionamento

- O catálogo segue **versionamento semântico**
- Consumidores **devem usar tags versionadas**
- Referências a `main` **não são suportadas**

Detalhes em: `docs/versioning.md`

---

## ✅ Princípios adotados

- Cada workflow é **autocontido**
- Documentação é **local e específica**
- Regras globais vivem em `docs/`
- Mudanças seguem versionamento explícito
- Clareza acima de conveniência

---

## 📚 Documentação

- Índice completo: `docs/README.md`
- Uso geral: `docs/usage.md`
- CI Node.js: `docs/ci-nodejs.md`

---

## 📌 Status

Este catálogo está em evolução e preparado para receber novos workflows, como:

- CI para frontend (Next.js)
- CI para backend
- CI para libraries
- Monorepos
- CD / Release

Contribuições devem respeitar o padrão de espelhamento e documentação.
