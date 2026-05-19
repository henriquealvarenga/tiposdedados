# Tipos de Dados em Saúde

Material didático sobre variáveis e tipos de dados para pesquisa em saúde — da coleta à análise. Construído com [Quarto](https://quarto.org/), com exemplos em R e Python.

---

## ⚠️ Antes de fazer `git push`: rode `quarto render` localmente

Este projeto **executa código R e Python** (via `reticulate`) durante a renderização. Para manter o GitHub Actions rápido e estável, ele **não instala R nem Python** — apenas monta o HTML a partir dos resultados já congelados em `_freeze/`.

Isso significa que **você** precisa renderizar localmente antes de empurrar para o GitHub. Se esquecer e tiver mudado código R/Python, o build no GitHub vai falhar (visivelmente — você vê o X vermelho na aba Actions).

### Fluxo de publicação

```bash
quarto render                  # 1. renderiza localmente → atualiza _freeze/
git add -A
git commit -m "sua mensagem"
git push                       # 2. GitHub Actions monta o HTML e publica
```

---

## Estrutura do projeto

| Caminho | Função |
|---|---|
| `index.qmd`, `about.qmd`, `referencias.qmd` | Páginas principais |
| `cap01-…` a `cap10-…` `.qmd` | Capítulos do material |
| `data/` | Dados de exemplo usados pelos capítulos |
| `images/`, `assets/`, `styles/` | Imagens, logos e CSS |
| `references/` | Bibliografia (`.bib`) e estilos CSL |
| `_freeze/` | Resultados congelados das chunks R/Python — **versionado**, regenerado por `quarto render` |
| `.github/workflows/publish.yml` | Workflow que monta o HTML e publica no GitHub Pages |

`_quarto.yml` define `output-dir: docs`, mas `docs/` **não é versionado** — o workflow o gera a cada push.

---

## Pré-requisitos para renderizar localmente

- [Quarto](https://quarto.org/docs/get-started/)
- R com os pacotes: `dplyr`, `ggplot2`, `kableExtra`, `knitr`, `readr`, `reticulate`, `tidyr`
- Python com `numpy` e `pandas` (o `reticulate` encontra automaticamente)

---

## Por que essa estratégia (e não rodar R/Python no GitHub Actions)?

- **Mais rápido:** o GitHub Actions faz só `quarto render` (~30s) em vez de instalar R, Python e pacotes (~5-10min).
- **Mais estável:** sem risco de quebrar quando algum pacote do CRAN/PyPI é atualizado.
- **Sem `renv`/`requirements.txt` para manter:** simplifica o projeto.

O preço é o passo manual `quarto render` antes do push.
