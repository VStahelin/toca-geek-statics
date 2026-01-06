# Toca Geek Statics

Este projeto usa **GitHub Pages** para hospedar o conteúdo estático da Toca Geek, com um sistema automatizado para gerar um mapa de arquivos (`site_map.json`). A estrutura gerada inclui arquivos JSON, imagens e outros recursos estáticos do repositório.

## Estrutura do Projeto

O arquivo `site_map.json` mapeia os recursos do projeto da seguinte forma:

- **data**: Arquivos JSON que contêm dados estruturados, incluindo `site_map.json` e `galeria.json`.
- **images**: Recursos de imagem como `.png`, `.jpg`, `.jpeg`, e `.gif`.
- **scripts**: Contém o script Python usado para gerar o `site_map.json`.
- Outros arquivos são listados diretamente na raiz da estrutura.

Exemplo da estrutura gerada:

```json
{
    "README.md": "https://vstahelin.github.io/toca-geek-statics/README.md",
    "images": {
        "projeto_1.png": "https://vstahelin.github.io/toca-geek-statics/images/projeto_1.png",
        "projeto_2.jpg": "https://vstahelin.github.io/toca-geek-statics/images/projeto_2.jpg"
    },
    "scripts": {
        "map_generator.py": "https://vstahelin.github.io/toca-geek-statics/scripts/map_generator.py"
    },
    "data": {
        "galeria.json": "https://vstahelin.github.io/toca-geek-statics/data/galeria.json",
        "site_map.json": "https://vstahelin.github.io/toca-geek-statics/data/site_map.json"
    }
}
```

## Como Funciona

- Sempre que um push é feito para a branch main, uma **GitHub Action** é executada para atualizar o arquivo `site_map.json`. Este arquivo contém URLs apontando para os arquivos hospedados no GitHub Pages.
- O script responsável por gerar o mapa pode ser encontrado no repositório como `scripts/map_generator.py`.

## Galeria de Projetos

O arquivo `data/galeria.json` contém a estrutura de projetos e fotos da Toca Geek. Você pode adicionar novos projetos e fotos futuramente apenas atualizando este arquivo JSON.

## Uso

1. Clone o repositório:
    ```bash
    git clone https://github.com/vstahelin/toca-geek-statics.git
    ```
   
2. Execute o script manualmente (opcional):
    ```bash
    python scripts/map_generator.py
    ```

3. O arquivo `site_map.json` será atualizado automaticamente em novos pushes, mas você pode executar o script localmente para verificar a estrutura.