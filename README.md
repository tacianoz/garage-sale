# The Zimmermanns' Garage Sale

Site estático da garage sale, hospedado no GitHub Pages.

## Estrutura

- `index.html` — o site completo (versão empacotada, pronta para publicar)
- `photos/` — fotos dos itens usadas pelo site
- `Garage Sale.dc.html` + `support.js` — arquivos-fonte editáveis do design
- `.github/workflows/deploy-pages.yml` — deploy automático para o GitHub Pages

## Publicação

O deploy é feito automaticamente pelo GitHub Actions a cada push. Se o site
ainda não estiver ativo, vá em **Settings → Pages** do repositório e defina
**Source: GitHub Actions** (o workflow também tenta habilitar isso sozinho na
primeira execução).

Depois do primeiro deploy, o site fica disponível em:

`https://tacianoz.github.io/garage-sale/`

## Desenvolvimento local

```sh
python3 -m http.server 8000
# abra http://localhost:8000
```
