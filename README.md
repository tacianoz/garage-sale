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

## O anúncio do carro

O MG Hector Plus tem uma seção própria em destaque, logo abaixo do menu de
categorias — fundo escuro, galeria de 12 fotos e tabela de especificações.
O conteúdo fica no objeto `CAR` dentro do bloco `<script>` (preço, fotos,
descrição, specs e equipamentos). Para definir o preço, troque
`price: null` pelo valor em rupias (ex.: `price: 1250000`); enquanto for
`null`, a página mostra "Price on request".

## Modo admin (marcar itens como vendidos pelo site)

O site tem um modo admin protegido por senha para marcar itens como
**Sold / Reserved / Available** sem mexer em código:

1. Abra o site e clique no link discreto **· admin ·** no rodapé
   (ou acesse o site com `#admin` no final da URL)
2. Digite a senha do admin
3. Aparecem três botões em cada card — clique para mudar o status.
   A mudança é gravada no `status.json` deste repositório e vale para
   todos os visitantes (novos carregamentos da página leem esse arquivo).

### Configuração única (dono do repositório)

O modo admin grava no repositório via API do GitHub usando um token que
fica salvo **criptografado com a senha** em `token.enc.json`:

1. Crie um token em GitHub → Settings → Developer settings →
   **Fine-grained personal access tokens**:
   - Repository access: **somente este repositório**
   - Permissions → Repository permissions → **Contents: Read and write**
   - Defina uma expiração (ao expirar, repita este processo)
2. No site, entre no modo admin com a senha; no primeiro acesso ele pede
   o token e o salva criptografado no repositório
3. A partir daí, qualquer pessoa com a senha consegue usar o admin em
   qualquer aparelho — só a senha é necessária

Nota de segurança: o `token.enc.json` é público (repositório público),
protegido por criptografia AES-GCM com chave derivada da senha (PBKDF2).
Use um token restrito a este repositório e com expiração.

## Desenvolvimento local

```sh
python3 -m http.server 8000
# abra http://localhost:8000
```
