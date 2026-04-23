# Uso dos workflows reutilizáveis

Este catálogo fornece **workflows reutilizáveis do GitHub Actions**, que devem ser consumidos por outros repositórios por meio da diretiva `uses`.

---

## Tipo de workflow

Todos os workflows deste catálogo são do tipo **reusable workflow**, definidos com:

```

on:
workflow\_call:

```

Eles **não são executados diretamente** neste repositório.

---

## Como usar em um repositório consumidor

No repositório que irá consumir o workflow, crie um arquivo em:

```

.github/workflows/ci.yml

```

Exemplo mínimo:

```yaml
name: CI

on:
  push:
    branches: [main]
  pull_request:
    branches: [main]

jobs:
  ci:
    uses: ORG/REPO/.github/workflows/caminho.yml@TAG
    with:
      input-exemplo: valor
```

---

## Referência do workflow

- O caminho do workflow deve ser **exato**
- O repositório pode ser público ou privado
- Sempre informe uma **tag versionada** ou SHA

✅ Correto:

    @v1.0.0

❌ Evite:

    @main

---

## Inputs

Cada workflow define seus próprios `inputs`.  
Consulte sempre o arquivo de documentação **espelhado** em `docs/**` antes de usar.

---

## Boas práticas

- Leia a documentação específica do workflow antes de integrá-lo
- Não assuma scripts ou comportamentos implícitos
- Atualize a versão de forma consciente
- Trate falhas como bloqueantes no CI

---

## Onde encontrar a documentação

- Regras gerais: arquivos na raiz de `docs/`
- Workflows de CI: `docs/ci/`
- Cada workflow possui um arquivo `.md` com o mesmo caminho relativo do `.yml`

Esse padrão garante uso consistente e previsível em múltiplos projetos.
