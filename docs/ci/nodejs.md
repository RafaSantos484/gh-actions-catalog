# CI Node.js

Workflow reutilizável de CI para projetos **Node.js**.

Este documento descreve **exclusivamente** o workflow localizado em:

```

.github/workflows/ci/nodejs.yml

```

---

## ✅ O que este workflow faz

Este CI executa, **em paralelo**, as principais etapas de validação e build de um projeto Node.js.

Jobs executados:

| Job       | Script executado       |
| --------- | ---------------------- |
| Typecheck | `npm run typecheck`    |
| Format    | `npm run format:check` |
| Lint      | `npm run lint`         |
| Test      | `npm run test:run`     |
| Build     | `npm run build`        |

➡️ Se **qualquer job falhar**, o workflow falha.

---

## ▶️ Como o workflow é acionado

Este é um **reusable workflow**, definido com:

```

on:
workflow\_call

```

Ele **não executa sozinho**.  
Deve ser chamado a partir de outro repositório usando `uses`.

---

## 📥 Inputs esperados

| Nome         | Tipo   | Obrigatório | Descrição         |
| ------------ | ------ | ----------- | ----------------- |
| node-version | string | ✅ Sim      | Versão do Node.js |

Exemplo:

```yaml
with:
  node-version: 18
```

---

## 📦 Scripts exigidos no projeto consumidor

O projeto que consome este workflow **DEVE** definir no `package.json` os seguintes scripts:

```json
{
  "scripts": {
    "typecheck": "...",
    "format:check": "...",
    "lint": "...",
    "test:run": "...",
    "build": "..."
  }
}
```

Os nomes devem coincidir **exatamente**.

---

## 🧱 Características técnicas

- Cada job:
  - Executa em máquina isolada
  - Faz `npm ci`
  - Usa cache baseado em `package-lock.json`
- Jobs não dependem uns dos outros
- Execução paralela maximiza feedback rápido

---

## 🧪 Exemplo de uso

```yaml
jobs:
  ci-nodejs:
    uses: ORG/gh-actions-catalog/.github/workflows/ci/nodejs.yml@v1.0.0
    with:
      node-version: 18
```

---

## ⚠️ Observações importantes

- O workflow assume uso de **npm**
- Não há fallback para `yarn` ou `pnpm`
- Scripts ausentes causam falha imediata
- Versionamento deve seguir o definido em `docs/versioning.md`

---

## 📎 Documentação relacionada

- Regras gerais de uso: `docs/usage.md`
- Convenções de CI: `docs/ci/README.md`
- Versionamento do catálogo: `docs/versioning.md`
