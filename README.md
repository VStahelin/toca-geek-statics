# Toca Geek Statics

Repositório de conteúdo estático para o site da **Toca Geek**. Este projeto usa **GitHub Pages** para hospedar imagens, dados JSON e outros recursos estáticos, com um sistema automatizado para gerar um mapa de arquivos (`site_map.json`).

## 📋 Sobre

Este repositório serve como fonte de dados estáticos para o site [toca-geek-launchpad](https://github.com/VStahelin/toca-geek-launchpad). Ele contém:

- **Galeria de projetos**: Estrutura JSON com projetos e fotos da Toca Geek
- **Imagens**: Assets visuais dos projetos e logos
- **Mapa de arquivos**: Gerado automaticamente pelo GitHub Actions

## 🗂️ Estrutura do Projeto

```
toca-geek-statics/
├── data/
│   ├── galeria.json      # Estrutura de projetos e fotos
│   └── site_map.json     # Mapa automático de todos os arquivos
├── images/
│   ├── logos/            # Logos da Toca Geek
│   └── [imagens dos projetos]
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

### Galeria de Projetos

O arquivo `data/galeria.json` contém a estrutura de projetos e fotos. Para adicionar novos projetos:

1. Adicione as imagens na pasta `images/`
2. Atualize o arquivo `data/galeria.json` com as informações do novo projeto
3. Faça commit e push - o GitHub Actions cuidará do resto!

**Estrutura do galeria.json:**
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
    "is_highlighted": true
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

3. **Adicione novos projetos:**
    - Adicione imagens em `images/`
    - Atualize `data/galeria.json`
    - Commit e push

## 🔗 URLs

- **Repositório**: https://github.com/VStahelin/toca-geek-statics
- **GitHub Pages**: https://vstahelin.github.io/toca-geek-statics/
- **Galeria JSON**: https://vstahelin.github.io/toca-geek-statics/data/galeria.json
- **Site Map**: https://vstahelin.github.io/toca-geek-statics/data/site_map.json

## 📝 Notas

- O arquivo `site_map.json` é gerado automaticamente - não edite manualmente
- As imagens devem ser otimizadas antes de adicionar ao repositório
- O formato de data no `galeria.json` é `YYYY-MM-DD`