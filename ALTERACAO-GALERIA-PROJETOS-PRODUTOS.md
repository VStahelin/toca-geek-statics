# Documento de alteração: Galeria → Projetos + nova aba Produtos

Este documento descreve a alteração na navegação e no conteúdo do site Toca Geek: renomear a aba **Galeria** para **Projetos** e criar uma nova aba **Produtos** com listagem de produtos (anúncios) e redirecionamento para Shoppe e Mercado Livre.

---

## 1. Resumo da alteração

| Item | Antes | Depois |
|------|--------|--------|
| Aba 1 | **Galeria** (lista de projetos/portfólio) | **Projetos** (mesmo conteúdo, novo rótulo) |
| Aba 2 | — | **Produtos** (lista de produtos à venda, com links para lojas) |
| Fonte de dados – projetos | `data/galeria.json` | `data/projetos.json` (ou manter `galeria.json` e só trocar o label na UI) |
| Fonte de dados – produtos | — | `data/produtos.json` (novo) |

---

## 2. Escopo por repositório

### 2.1 toca-geek-statics (este repositório)

- **Projetos**
  - Opção A: Renomear `data/galeria.json` → `data/projetos.json` e atualizar `site_map.json` / README / qualquer referência a `galeria.json`.
  - Opção B: Manter `galeria.json` e apenas documentar que na UI do site o rótulo da aba deve ser "Projetos".
- **Produtos**
  - Criar `data/produtos.json` com a estrutura definida abaixo.
  - Incluir `produtos.json` no `site_map.json` (se o mapa for gerado por script, atualizar o script para incluir o novo arquivo).
- **Documentação**
  - Atualizar README: trocar "Galeria" por "Projetos" onde fizer sentido e descrever a nova seção "Produtos" e o arquivo `produtos.json`.

### 2.2 toca-geek-launchpad (consumidor do estático)

- **Navegação**
  - Trocar o label da aba de "Galeria" para "Projetos".
  - Adicionar nova aba "Produtos".
  - Se a fonte de projetos mudar para `projetos.json`, apontar a requisição para a nova URL.
- **Página Projetos**
  - Manter o mesmo layout/conteúdo que hoje existe para a galeria; apenas o nome da aba e, se aplicável, a URL do JSON mudam.
- **Página Produtos**
  - Nova página que consome `data/produtos.json`.
  - Listar produtos em formato de anúncios (cards).
  - Em cada card: imagem, título, descrição/resumo, preço (opcional), e botões de ação:
    - "Ver na Shoppe" → abre link do produto na Shoppe.
    - "Ver no Mercado Livre" → abre link do produto no Mercado Livre.
  - Cada produto pode ter um ou ambos os links; mostrar apenas os botões cujos links existirem.

---

## 3. Estrutura de dados

### 3.1 Projetos (atual galeria.json)

A estrutura atual de `galeria.json` permanece válida para **Projetos**. Não é obrigatório mudar o nome do arquivo; o importante é que na UI a aba se chame "Projetos".

Campos existentes (resumo): `id`, `title`, `category`, `description`, `images[]`, `tags`, `date`, `is_highlighted`, `instagram_url`.

### 3.2 Produtos (novo produtos.json)

Estrutura sugerida para cada item em `data/produtos.json`:

```json
{
  "id": 1,
  "title": "Nome do produto",
  "description": "Descrição curta ou resumo do anúncio.",
  "image_url": "https://.../imagem-produto.png",
  "image_alt": "Texto alternativo da imagem",
  "price": "R$ 99,90",
  "category": "Colecionável",
  "tags": ["tag1", "tag2"],
  "shoppe_url": "https://shoppe.com.br/...",
  "mercado_livre_url": "https://produto.mercadolivre.com.br/..."
}
```

Regras:

- `shoppe_url` e `mercado_livre_url` são opcionais. Na UI, exibir apenas "Ver na Shoppe" ou "Ver no Mercado Livre" quando o respectivo link estiver presente.
- `price` é opcional (pode ser exibido como "Sob consulta" ou omitido se não houver).
- `image_url` pode ser absoluta (ex.: GitHub Pages) ou caminho relativo, conforme padrão do projeto.

Exemplo de array em `produtos.json`:

```json
[
  {
    "id": 1,
    "title": "Figura Anime - Personagem X",
    "description": "Figura personalizada impressa em alta qualidade.",
    "image_url": "https://vstahelin.github.io/toca-geek-statics/images/produtos/figura-exemplo.png",
    "image_alt": "Figura anime",
    "price": "R$ 89,90",
    "category": "Colecionável",
    "tags": ["anime", "figura", "PLA"],
    "shoppe_url": "https://shoppe.com.br/...",
    "mercado_livre_url": ""
  }
]
```

---

## 4. Linha de design e referências do projeto

### 4.1 Onde o design está definido

- **Print Vault (web-manager)**  
  - Tema: `web-manager/src/shared/styles/theme.ts`  
  - Paleta: `docs/08-guidelines/color-palette.md`  
  - Uso: tema escuro (dark), primary/secondary em roxo/magenta, bordas e superfícies consistentes.

- **Toca Geek / Wiki**  
  - Diretrizes gerais: `docs/08-guidelines/ui-ux-guidelines.md` (GitHub Primer, tema escuro, componentes, espaçamento, acessibilidade).

- **Estáticos (toca-geek-statics)**  
  - Apenas dados (JSON + imagens). O visual é definido no **toca-geek-launchpad** ao consumir esses dados.

Recomendação: a página de **Produtos** no launchpad deve seguir a mesma linha visual do restante do site (dark, mesma paleta e componentes), para manter consistência.

### 4.2 Componentes Magic UI (referência para o launchpad)

O projeto já usa Magic UI em partes do **web-manager** (ex.: `MagicCard`, `ShimmerButton`). Para a nova aba **Produtos** no **toca-geek-launchpad**, estes componentes podem ser úteis:

- **Cards de produto**
  - **Magic Card**: borda com efeito de spotlight no hover; combina com o tema escuro e gradiente primary.
  - **Neon Gradient Card**: destaque visual para itens em evidência.
  - **Bento Grid**: se quiser layout em grid assimétrico para destacar alguns produtos.

- **Botões de redirecionamento (Shoppe / Mercado Livre)**
  - **Shimmer Button**: já usado no projeto para ações principais; ideal para "Ver na Shoppe" / "Ver no Mercado Livre".
  - **Interactive Hover Button**: alternativa para CTA com seta/feedback visual.
  - **Ripple Button**: opção para feedback de clique.

- **Lista e animação**
  - **Animated List**: entrada em sequência dos cards de produtos.
  - **Blur Fade**: transição suave ao carregar a seção de produtos.

- **Layout e fundo**
  - **Grid Pattern** / **Dot Pattern**: fundo sutil na seção de produtos, alinhado ao restante do site.

Sugestão prática: cada produto em um **MagicCard** (ou Neon Gradient Card para destaques), com imagem, título, descrição curta, preço (se houver) e dois **ShimmerButton** (ou links estilizados como botão) para Shoppe e Mercado Livre, exibidos conforme a presença das URLs em `produtos.json`.

---

## 5. Exemplos de referência (lojas e página de produto)

- **Lojas**: usar como referência páginas de listagem e de produto da Shoppe e do Mercado Livre para:
  - Organização da informação (título, imagem, preço, botão de ação).
  - Hierarquia: imagem em destaque, título, depois descrição/resumo, depois CTAs.
- **Página de produto**: um card por produto com link externo é suficiente; não é obrigatório ter página interna de detalhe do produto. O botão já leva direto para o anúncio na loja.

---

## 6. Checklist de implementação

### toca-geek-statics

- [ ] Decidir: renomear `galeria.json` → `projetos.json` ou manter nome do arquivo e só trocar label na UI.
- [ ] Se renomear: atualizar `site_map.json`, README e scripts que referenciam `galeria.json`.
- [ ] Criar `data/produtos.json` com a estrutura definida na seção 3.2.
- [ ] Adicionar imagens dos produtos em `images/produtos/` (ou caminho definido no projeto).
- [ ] Incluir `produtos.json` no mapa de arquivos / script de geração do `site_map.json`.
- [ ] Atualizar README (Projetos + Produtos, URLs, estrutura de `produtos.json`).

### toca-geek-launchpad

- [ ] Alterar label da aba "Galeria" para "Projetos".
- [ ] Se a fonte mudar para `projetos.json`: atualizar URL da API/fetch para o novo JSON.
- [ ] Adicionar aba "Produtos" na navegação.
- [ ] Criar página/rota que carrega `data/produtos.json`.
- [ ] Implementar listagem em cards (um card por produto).
- [ ] Por card: imagem, título, descrição, preço (opcional), botão "Ver na Shoppe" (se `shoppe_url`), botão "Ver no Mercado Livre" (se `mercado_livre_url`).
- [ ] Aplicar componentes e estilo alinhados à linha de design (Magic Card, Shimmer Button, paleta dark).
- [ ] Testar com um produto que tenha só Shoppe, outro só Mercado Livre e outro com os dois links.

---

## 7. Observações

- **Compatibilidade**: Se o launchpad ainda não estiver preparado para `projetos.json`, manter temporariamente suporte a `galeria.json` e trocar apenas o label "Galeria" → "Projetos" evita quebra.
- **SEO e links externos**: Links para Shoppe e Mercado Livre devem abrir em nova aba (`target="_blank"`) e usar `rel="noopener noreferrer"` por segurança.
- **Acessibilidade**: Botões/links devem ter texto claro ("Ver na Shoppe", "Ver no Mercado Livre") e, se usar ícones, manter `aria-label` ou texto alternativo.

---

*Documento criado para gerenciar a alteração da aba Galeria para Projetos e a criação da aba Produtos. Atualize este arquivo conforme decisões (ex.: nome do arquivo de projetos) forem fechadas.*
