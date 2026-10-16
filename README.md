# Guia Bash

Curso de Bash em português, do zero ao avançado, organizado em **3 níveis + projetos + referência** (88 páginas). Não é de nenhuma distro: vale para qualquer Linux, macOS (com Bash atualizado) e Windows (WSL/Git Bash).

Cada aula explica o comando ou o trecho de script parte por parte (anatomia), mostra a saída real, o código de saída, várias formas de fazer e os erros mais comuns com a mensagem verdadeira. Toda saída foi conferida no **GNU Bash 5.3.9** com as ferramentas GNU, em pt_BR.

Para praticar, as páginas trazem dois tipos de caixa que rodam no navegador:

- **Terminal simulado** (`.try`): a máquina fictícia `ana@notebook`, com missões que conferem se você chegou ao resultado.
- **Editor de script** (`.tryscript`): edite, clique em **Rodar** e veja a saída e o código de saída. O `read` pede a resposta ali mesmo.

Os dois usam `assets/bashsim.js`, um interpretador de Bash em JavaScript comparado automaticamente com o Bash real (587 casos idênticos).

Site 100% estático (HTML + CSS + JS, sem build e sem dependências externas): abre direto no navegador e funciona no GitHub Pages.

## Estrutura

```
index.html                 página inicial
<tema>.html                uma aula por tema
assets/style.css           visual (tema claro/escuro automático)
assets/site.js             níveis/menu (lista NIVEIS), Anterior/Próximo, terminais, anatomia, exercícios
assets/bashsim.js          o interpretador de Bash + interface do terminal e do editor
assets/bashsim-ajuda.js    textos do `help` (carregados sob demanda)
tools/sim.js               mostra uma sessão do simulador no formato das aulas
tools/testar-missoes.js    testa todas as missões (e compara com o Bash real do laboratório)
tools/testes/              bateria diferencial simulador × Bash real
CONTRIBUINDO.md            como escrever uma aula
```

## Testes

```bash
node tools/testar-missoes.js --sem-lab   # todas as missões, só no simulador
node tools/testar-missoes.js             # idem, comparando os scripts com o Bash real (precisa do laboratório)
node tools/testes/rodar.js               # bateria diferencial (precisa do laboratório)
```

## Publicar no GitHub Pages

Envie a pasta para um repositório e ative **Settings → Pages → Deploy from a branch → main / (root)**.
