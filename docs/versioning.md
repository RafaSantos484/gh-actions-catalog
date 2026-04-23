# Versionamento do catálogo

Este repositório de catálogo de GitHub Actions segue **versionamento semântico** para todos os workflows reutilizáveis disponibilizados.

O versionamento se aplica ao **conjunto de workflows**, e não a arquivos individuais.

---

## 📌 Convenção adotada

Formato:

```

vMAJOR.MINOR.PATCH

```

### Significado

- **MAJOR**  
  Mudanças incompatíveis que podem quebrar workflows consumidores.

- **MINOR**  
  Novas funcionalidades ou melhorias **compatíveis** com versões anteriores.

- **PATCH**  
  Correções internas ou ajustes que não alteram comportamento esperado.

---

## ✅ Exemplos

- `v1.0.0` — versão inicial estável do catálogo
- `v1.1.0` — melhorias compatíveis (ex.: novos inputs opcionais)
- `v2.0.0` — mudança incompatível (ex.: remoção ou renomeação de inputs)

---

## 🔒 Regra obrigatória para consumidores

Workflows consumidores **devem sempre** referenciar:

✅ Uma **tag versionada**:

```yaml
@v1.0.0
```

✅ Ou um **SHA específico**:

```yaml
@3f2c1a9e4b...
```

❌ Não utilize referências flutuantes:

```yaml
@main
```

---

## 🧠 Racional

Essa política garante:

- Previsibilidade para pipelines consumidores
- Reprodutibilidade de builds
- Segurança contra quebras inesperadas
- Evolução controlada do catálogo

---

## 🔄 Atualização de versão

Toda alteração que afete comportamento deve ser acompanhada de:

1.  Incremento correto da versão
2.  Nova tag Git
3.  Documentação atualizada nos arquivos `docs/**` relevantes

O uso consistente desse modelo é obrigatório para manter a confiabilidade do catálogo.
