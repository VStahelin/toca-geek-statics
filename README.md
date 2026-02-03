# Toca Geek Statics

Repositório de conteúdo estático para o site da **Toca Geek**. Este projeto usa **GitHub Pages** para hospedar imagens, dados JSON e outros recursos estáticos, com um sistema automatizado para gerar um mapa de arquivos (`site_map.json`).

## 📋 Sobre

Este repositório serve como fonte de dados estáticos para o site [toca-geek-launchpad](https://github.com/VStahelin/toca-geek-launchpad). Ele contém:

- **Projetos**: Estrutura JSON com projetos e fotos da Toca Geek (portfólio)
- **Produtos**: Estrutura JSON com produtos à venda e links para Shoppe e Mercado Livre
- **Imagens**: Assets visuais dos projetos, produtos e logos
- **Mapa de arquivos**: Gerado automaticamente pelo GitHub Actions

## 🗂️ Estrutura do Projeto

```
toca-geek-statics/
├── data/
│   ├── projetos.json     # Estrutura de projetos e fotos (portfólio)
│   ├── produtos.json      # Produtos à venda (links Shoppe / Mercado Livre)
│   └── site_map.json     # Mapa automático de todos os arquivos
├── images/
│   ├── logos/            # Logos da Toca Geek
│   ├── projetos/        # Imagens dos projetos
│   ├── produtos/        # Imagens dos produtos
│   └── [outras imagens]
├── scripts/
│   └── map_generator.py  # Script para gerar site_map.json
└── .github/workflows/    # GitHub Actions para automação
```

## 🚀 Como Funciona

### Automação

- **GitHub Actions**: Sempre que um push é feito para a branch `main`, uma workflow é executada que:
  1. Gera/atualiza o arquivo `site_map.json` automaticamente
  2. Faz commit e push das mudanças
  3. Faz deploy no GitHub Pages

### Projetos (portfólio)

O arquivo `data/projetos.json` contém a estrutura de projetos e fotos. Para adicionar novos projetos:

1. Adicione as imagens na pasta `images/projetos/` (ou `images/`)
2. Atualize o arquivo `data/projetos.json` com as informações do novo projeto
3. Faça commit e push - o GitHub Actions cuidará do resto!

**Estrutura do projetos.json:**
```json
[
  {
    "id": 1,
    "title": "Nome do Projeto",
    "category": "Categoria",
    "description": "Descrição do projeto",
    "images": [
      {
        "url": "https://vstahelin.github.io/toca-geek-statics/images/imagem.png",
        "alt": "Texto alternativo",
        "is_primary": true
      }
    ],
    "tags": ["tag1", "tag2"],
    "date": "2024-01-15",
    "is_highlighted": true,
    "instagram_url": "https://www.instagram.com/p/..."
  }
]
```

### Produtos (loja)

O arquivo `data/produtos.json` contém os produtos à venda, com links para Shoppe e/ou Mercado Livre. Para adicionar novos produtos:

1. Adicione a imagem na pasta `images/produtos/`
2. Atualize o arquivo `data/produtos.json` com título, descrição, preço e URLs das lojas
3. Use `shoppe_url` e/ou `mercado_livre_url`; deixe vazio (`""`) o link que não existir

**Estrutura do produtos.json:**
```json
[
  {
    "id": 1,
    "title": "Nome do produto",
    "description": "Descrição curta do anúncio.",
    "image_url": "https://.../imagem-produto.png",
    "image_alt": "Texto alternativo da imagem",
    "price": "R$ 99,90",
    "category": "Colecionável",
    "tags": ["tag1", "tag2"],
    "shoppe_url": "https://shoppe.com.br/...",
    "mercado_livre_url": "https://produto.mercadolivre.com.br/..."
  }
]
```

## 📦 Uso Local

1. **Clone o repositório:**
    ```bash
    git clone git@github.com:VStahelin/toca-geek-statics.git
    cd toca-geek-statics
    ```
   
2. **Execute o script manualmente (opcional):**
    ```bash
    python scripts/map_generator.py
    ```

3. **Adicione novos projetos ou produtos:**
    - Projetos: imagens em `images/projetos/` ou `images/`, edite `data/projetos.json`
    - Produtos: imagens em `images/produtos/`, edite `data/produtos.json`
    - Commit e push

## 🔗 URLs

- **Repositório**: https://github.com/VStahelin/toca-geek-statics
- **GitHub Pages**: https://vstahelin.github.io/toca-geek-statics/
- **Projetos JSON**: https://vstahelin.github.io/toca-geek-statics/data/projetos.json
- **Produtos JSON**: https://vstahelin.github.io/toca-geek-statics/data/produtos.json
- **Site Map**: https://vstahelin.github.io/toca-geek-statics/data/site_map.json

## 📝 Notas

- O arquivo `site_map.json` é gerado automaticamente - não edite manualmente
- As imagens devem ser otimizadas antes de adicionar ao repositório
- O formato de data no `projetos.json` é `YYYY-MM-DD`
- Para mais detalhes da alteração Galeria → Projetos e criação da aba Produtos, veja [ALTERACAO-GALERIA-PROJETOS-PRODUTOS.md](ALTERACAO-GALERIA-PROJETOS-PRODUTOS.md)
