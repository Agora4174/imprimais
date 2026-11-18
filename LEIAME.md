# Loja em Angular 22 (Etapa 2: vitrine)

Código-fonte da vitrine (home, categorias, produto, carrinho e pedido de orçamento).
Os dados usados agora são **de exemplo** (`src/app/core/mock-data.ts`). Esta versão **não foi compilada nem testada**
no ambiente em que foi escrita; rode os passos abaixo e corrija qualquer ajuste de versão.

## Como usar

1. Requisitos: Node compatível com o Angular 22 (veja a documentação oficial do Angular) e o CLI na versão 22.
2. Crie o projeto (com SSR, para SEO):

   ```bash
   npm install -g @angular/cli@22
   ng new loja --ssr --style=css
   cd loja
   ```

3. Copie por cima do projeto criado, mantendo as pastas:
   - `src/app/**` (substitui `app.ts`, `app.html`, `app.config.ts`, `app.routes.ts`, `app.routes.server.ts`)
   - `src/styles.css`

   Apague o `src/app/app.spec.ts` gerado pelo CLI (testa o conteúdo antigo do `app.html`).
   Se o `app.config.ts` gerado tiver providers que o nosso não tem, mantenha os do CLI e acrescente
   `withComponentInputBinding()`, `provideHttpClient(withFetch())` e `withInMemoryScrolling(...)`.

4. Rode:

   ```bash
   ng serve        # desenvolvimento
   ng test         # testes do carrinho (cart.service.spec.ts)
   ng build        # build com SSR
   ```

## O que cada parte faz

- `core/config.ts`: nome da loja, URL da API, `useMock` e WhatsApp. Texto de consentimento LGPD (rascunho).
- `core/catalog.service.ts`, `quote.service.ts`: usam dados de exemplo enquanto `useMock` for `true`.
  Ao ligar a API (Etapa 1), troque para `false` e ajuste os formatos de resposta (`TODO(api)`).
- `core/cart.service.ts`: carrinho com signals e `localStorage` (só no navegador). Preços aqui são só de exibição;
  o servidor recalcula preço, estoque e frete no checkout.
- `core/seo.service.ts`: título, descrição e JSON-LD (`schema.org/Product`) por página.
- `app.routes.server.ts`: renderização no servidor (SSR) para as páginas dinâmicas.

## Pendências desta etapa

- Checkout, pagamento e frete (Etapa 3). O botão "Finalizar compra" está desativado.
- Upload da logomarca e widget Turnstile no orçamento (Etapa 5): há `TODO` marcados no código.
- Aviso de cookies e textos de privacidade e termos (Etapa 7): hoje são páginas provisórias.
- Fotos reais dos produtos (o campo `imageUrl` já é suportado).
- Redirecionamentos 301 das URLs antigas da Nuvemshop (Etapa 10).
