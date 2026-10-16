# Como escrever uma página do Guia Bash

O guia é uma **escola**, estilo W3Schools, não uma lista de comandos. O leitor é iniciante: nunca mostre um comando ou um trecho de script "seco", sem antes explicar cada parte, o que ele devolve e o que fazer quando não funciona. As aulas dos outros guias servem de modelo de profundidade (`../guia-ubuntu/criar.html`, `../guia-debian/script-lacos.html`). Aqui, porém, o assunto é **o Bash em si**, e ele não é exclusivo de nenhuma distro: toda saída é conferida no **GNU Bash 5.3** com ferramentas GNU, usando o laboratório da seção 5.

## 1. Esqueleto do arquivo

```html
<!doctype html>
<html lang="pt-BR">
<head>
<meta charset="utf-8">
<meta name="viewport" content="width=device-width, initial-scale=1">
<title>Bash TEMA — descrição curta | Guia Bash</title>
<meta name="description" content="Uma frase sobre a página.">
<link rel="stylesheet" href="assets/style.css">
<script>try{var t=localStorage.getItem("tema");if(t)document.documentElement.setAttribute("data-theme",t)}catch(e){}</script>
</head>
<body>
<div class="layout">
<nav class="sidebar" id="sidebar" aria-label="Tópicos"></nav>
<main class="main">
<div class="content">
<div class="pager"></div>
<h1>Bash <span class="hl">TEMA</span></h1>
… conteúdo …
<div class="pager"></div>
</div>
</main>
</div>
<script src="assets/site.js"></script>
</body>
</html>
```

O menu, o selo de nível e os botões Anterior/Próximo vêm de `assets/site.js` (lista `NIVEIS`). **Não mude a `NIVEIS`** sem combinar; links internos só para páginas que estão nela.

## 2. Ordem de uma aula

1. **Intro** (`p.intro`): o que é e para que serve, em 2–3 frases.
2. **"Você vai aprender"** (`div.note` com lista de 3–5 itens).
3. **Conceito antes da sintaxe**: o problema que o recurso resolve, com um exemplo do dia a dia.
4. **Do simples ao completo**: primeiro a forma mais simples; depois **uma novidade por vez**. Cada forma nova ganha uma `dl.anatomy`.
5. **Toda saída explicada**: depois de cada sessão, diga o que o leitor está vendo. Use anotações `«` nas linhas importantes.
6. **O que devolve**: saída + código de saída (`echo $?`), principalmente quando nada aparece na tela.
7. **Formas diferentes de fazer** a mesma tarefa, com tabela "Qual usar?" (ex.: `[ ]` × `[[ ]]` × `test`; `$( )` × crases).
8. **Experimente**: missão no terminal (`.try`) ou no editor de script (`.tryscript`) — o Guia Bash deve ter **pelo menos uma por aula** (exceto páginas de referência e as puramente conceituais).
9. **Quando não funciona** (`div.cenario`): mensagem real → o que aconteceu → como confirmar → como resolver. Inclua o caso "não apareceu nada" e os erros clássicos do tema (espaço no `[`, `=` com espaço, aspas faltando…).
10. **Referência** (`table.ref`) das opções/formas vistas.
11. **Exercícios** (3 ou mais: `.exercise` e `.mc`).
12. **Resumo** (lista curta).

## 3. Componentes

### Sessão de terminal
```html
<pre class="term">$ nome=Ana
$ echo "Olá, $nome"
Olá, Ana                   « as aspas duplas deixam a variável ser trocada pelo valor
$ for i in 1 2 3; do
>   echo "volta $i"
> done
volta 1
volta 2
volta 3
</pre>
```
- `$ ` = comando digitado (vira `ana@notebook:~$`). `#> ` = como root.
- `> ` **logo depois de um comando** = linha de continuação (o prompt secundário `PS2` do Bash). Use para comandos de várias linhas, exatamente como o Bash mostra.
- O prompt acompanha os `cd`. Pasta inicial: `data-cwd="~/scripts"`. `data-user`, `data-host`, `data-title` mudam a janela.
- `«` inicia uma anotação (etiqueta laranja, não é copiada).
- Dentro de qualquer `<pre>` escreva `&lt;` `&gt;` `&amp;`.

### Arquivo / script
```html
<pre class="file" data-file="ola.sh">#!/usr/bin/env bash
echo "Olá, $USER!"
</pre>
```
Depois de mostrar um script, mostre a sessão que o executa (`$ bash ola.sh` ou `$ ./ola.sh`) e explique a saída **linha por linha** do script quando for novidade (uma `dl.anatomy` ou uma tabela "linha → o que faz").

### Anatomia
```html
<dl class="anatomy">
  <dt>${arquivo%.txt}</dt><dd>Remove ".txt" do final do valor.</dd>
  <dt>.bak</dt><dd>Texto colado logo depois.</dd>
</dl>
```

### Experimente no terminal (`.try`)
```html
<div class="try" data-setup="mkdir projeto;;cd projeto" data-goal="dir:~/projeto/src,var:nome=Ana" data-solucao="mkdir src;;nome=Ana">
<p class="try-task"><strong>Missão:</strong> crie a pasta src e uma variável nome com o valor Ana.</p>
</div>
```
- `data-setup`: comandos rodados antes (separados por `;;`), invisíveis para o leitor.
- `data-goal`: metas separadas por vírgula, **todas** precisam ser verdade (lista na seção 4).
- `data-solucao` (**obrigatório**): os comandos que cumprem a missão, separados por `;;`. Vira o botão "Ver solução" e é usado pelo teste automático.
- A missão **não** pode estar cumprida já pelo setup.

### Experimente no editor de script (`.tryscript`) — o "Try it Yourself" do guia
```html
<div class="tryscript" data-file="saudacao.sh" data-args="Ana" data-goal="out:Bom dia, Ana!">
<p class="try-task"><strong>Missão:</strong> mude o script para dizer "Bom dia" em vez de "Olá" e clique em Rodar.</p>
<pre class="script">#!/usr/bin/env bash
nome=$1
echo "Olá, $nome!"
</pre>
<pre class="solucao">#!/usr/bin/env bash
nome=$1
echo "Bom dia, $nome!"
</pre>
</div>
```
- O leitor edita o script num editor de verdade e clica em **Rodar**; o simulador grava o arquivo em `~/data-file`, roda `bash data-file ARGS` e mostra a saída e o código de saída.
- `data-args`: argumentos iniciais (o leitor pode mudar num campo). `data-stdin`: texto que vai para a entrada padrão (use `\n` para quebra de linha); sem ele, cada `read` abre um campo para o leitor digitar.
- `data-setup` e `data-goal` funcionam como no `.try`. `pre.solucao` é **obrigatório** quando há `data-goal` (vira "Ver solução" e alimenta o teste).
- Sem `data-goal`, a caixa é só um "rode e brinque" (sem missão) — use para exemplos que o leitor deve modificar livremente.

## 4. O simulador (`assets/bashsim.js`)

É um interpretador de Bash escrito em JavaScript, com um sistema de arquivos fictício. Ele é comparado automaticamente com o Bash 5.3 real (`tools/`), então **o que ele mostra deve ser igual ao Bash**.

**Linguagem:** listas `; & && ||`, pipelines (com `!`), `if/elif/else`, `while`, `until`, `for x in`, `for ((;;))`, `case` (com `;;` `;&` `;;&`), `select`, `{ ...; }`, `( ... )` subshell, `(( ))`, `[[ ]]` (com `=~` e `BASH_REMATCH`, `==` com padrão, `-v`), `[`/`test`, funções (`f() {…}` e `function f {…}`, várias linhas, `local`, `return`, recursão), `break/continue N`, aliases, comentários, continuação com `\`.
**Expansões, na ordem do Bash:** chaves, til, parâmetros (todas as formas `${…}`: `:-  :=  :+  :?  #  ##  %  %%  /  //  /#  /%  ^  ^^  ,  ,,  :n:m  !prefixo*  !nome  @Q @U @L @u @E @A`), aritmética `$(( ))`, substituição de comando `$( )` e crases, separação de palavras por `IFS`, curingas (incl. `shopt -s nullglob dotglob globstar extglob nocaseglob`), remoção de aspas. Aspas simples, duplas, `$'…'`, escapes.
**Variáveis:** escopo, `export`, `declare` (`-i -a -A -r -x -l -u -n -p`), `readonly`, `unset`, `local`, arrays indexados e associativos (`${a[@]}`, `${!a[@]}`, `${#a[@]}`, `+=`, fatias), `$?  $#  $@  $*  $0  $1…  ${10}  $$  $!  $-  $_  RANDOM  SRANDOM  LINENO  SECONDS  EPOCHSECONDS  BASH_VERSION  BASH_VERSINFO  FUNCNAME  PIPESTATUS  IFS  PS1  PS2  PS4`.
**Redirecionamentos:** `> >> < 2> 2>> &> &>> 2>&1 >&2 <&- n> n< n<> >|`, here-docs (`<<`, `<<-`, `<<'FIM'`), here-strings (`<<<`), `exec` com descritores, `/dev/null`, `/dev/stdin`, `/dev/stdout`, `/dev/stderr`, substituição de processo `<( )` e `>( )`.
**Comandos internos:** `echo printf read (com -r -p -s -n -t -a -d) mapfile/readarray cd pwd pushd popd dirs export unset set shopt declare typeset local readonly let shift getopts source . eval exec exit return true false : test [ type command builtin hash help alias unalias history jobs fg bg wait kill trap (EXIT ERR DEBUG RETURN INT TERM) times umask printf -v caller compgen complete`.
**Opções:** `set -e -u -x -o pipefail -o noclobber -o noglob -n -v`, `PS4`, `shopt` (lista acima + `lastpipe`, `nocasematch`, `expand_aliases`).
**Programas externos simulados (GNU):** `ls cat head tail wc sort uniq cut tr tee grep (-E -i -v -c -n -o -w -r -l -q) sed (s, d, p, -n, -i, -E, endereços) awk (o básico: campos, -F, padrões, BEGIN/END, printf, variáveis, arrays) find xargs mkdir rmdir touch rm cp mv ln chmod basename dirname realpath date seq sleep (instantâneo) env printenv expr bc (o básico) rev nl paste column diff stat du df file which whoami id hostname uname ps pgrep kill bash sh (`bash script.sh`, `bash -c`, `bash -n`, `bash -x`) e a execução de scripts com `./script.sh` (shebang + permissão de execução).**
**Não sabe:** rede (curl, ssh…), pacotes, editores (nano/vim), `cron`/`systemctl` de verdade, `tput` real (só `tput setaf/sgr0/bold/cols/lines` com valores fixos), `less`/`more` interativos (mostram tudo de uma vez). Para esses, use só `pre.term`, nunca finja um `.try`.

**Metas (`data-goal`):**

| Meta | Verdade quando… |
| --- | --- |
| `dir:CAMINHO` / `file:CAMINHO` / `absent:CAMINHO` | existe pasta / existe arquivo / não existe |
| `exec:CAMINHO` | o arquivo existe e tem permissão de execução para a ana |
| `contains:CAMINHO=texto` | o arquivo contém o texto |
| `cwd:CAMINHO` | a pasta atual é essa |
| `var:NOME=valor` / `var:NOME` | a variável tem esse valor / existe (no shell do `.try`) |
| `func:NOME` / `alias:NOME` | a função / o alias existe |
| `ran:REGEX` | algum comando digitado casa com a regex |
| `out:TEXTO` | a saída (stdout) do último comando/rodada contém o texto |
| `outre:REGEX` | a saída casa com a regex (multilinha) |
| `err:TEXTO` | a saída de erro contém o texto |
| `exit:N` | o último código de saída foi N |
| `src:REGEX` | (`.tryscript`) o código do script casa com a regex — use para exigir que o leitor use certo recurso (`src:\bwhile\b`) |

Use `\,` para uma vírgula dentro de uma meta.

**Máquina fictícia (estado inicial — igual à pasta do laboratório):** usuária `ana` (uid 1000; grupos `ana adm cdrom sudo dip plugdev users`), máquina `notebook`, Bash 5.3.9, `LANG=pt_BR.UTF-8`, `HOME=/home/ana` (modo 750) com `Área de trabalho/ Documentos/ Downloads/ Imagens/ Modelos/ Música/ Público/ Vídeos/ frutas.txt .bashrc .profile .bash_history`; `Documentos/` tem `notas.txt acesso.log alunos.csv relatorio.odt projetos/{backup.sh, site/{index.html, style.css}}`; `Downloads/` tem `ubuntu-26.04-desktop-amd64.iso manual.pdf foto.jpg musica.mp3 fotos-viagem.zip`; `Imagens/` tem `ferias.jpg perfil.png`. Conteúdos: `frutas.txt` = banana maçã laranja banana uva maçã banana (uma por linha); `notas.txt` = Comprar café / Ligar para o João / Estudar Bash / Fazer backup das fotos; `alunos.csv` = `nome,idade,cidade,nota` + Ana,29,Recife,9.5 / Bruno,34,Curitiba,7.0 / Carla,22,Salvador,8.5 / Diego,41,Manaus,6.0 / Elisa,27,Porto Alegre,10.0; `acesso.log` = 6 linhas de log de servidor web (IPs 192.168.0.10/23/57, códigos 200/403/404). O `.bashrc` define `HISTCONTROL=ignoreboth`, `PS1='\u@\h:\w\$ '` e os aliases `ls grep ll la l`. Data e hora do simulador: 15/10/2026 10:30. Processos: systemd(1), gnome-shell(1534), firefox(2210), gnome-terminal-(2950), bash(3001).

Se precisar de um arquivo que não existe na máquina, crie-o no `data-setup` (ex.: `printf 'a\nb\n' > lista.txt`).

**Testar suas missões:** `node tools/testar-missoes.js pagina.html` (roda setup → confere que a meta ainda não foi cumprida → roda a solução → confere que foi; e compara a saída da solução com o Bash real do laboratório). `node tools/sim.js 'comandos'` mostra uma sessão do simulador no formato do `pre.term`.

## 5. Fidelidade: o laboratório (`~/guia-bash-lab/lab`)

O computador onde o guia é feito usa versões não-GNU de alguns comandos (`ls` em Rust, `ugrep`). Por isso **nunca confira saídas direto no seu shell**: use o laboratório, uma caixa isolada (bubblewrap) que imita a máquina da Ana com Bash 5.3.9, GNU coreutils 9.7, GNU grep 3.12, GNU sed 4.9, findutils 4.10, mawk 1.3.4 (`awk`), `dash` (para `sh`) e ShellCheck 0.11. Nada dentro dela mexe nos arquivos de verdade.

```bash
L=~/guia-bash-lab/lab
# como se a Ana digitasse no terminal: a saída já sai no formato do pre.term ($ / >)
printf '%s\n' 'nome=Ana' 'echo "Olá, $nome"' 'for i in 1 2; do' '  echo $i' 'done' | $L -n SEUNOME -i
# rodar um script que está na pasta da Ana
$L -n SEUNOME -- bash -c 'cat > teste.sh <<"EOF"
echo "$# argumentos"
EOF
bash teste.sh a b'
$L -n SEUNOME -r -i < sessao.txt   # -r recomeça a pasta da Ana do zero (estado inicial do simulador)
$L -n SEUNOME -t < sessao.txt      # terminal de verdade (cores, ls em colunas, [[ -t 1 ]])
```
- `-n SEUNOME`: cada autor usa **a própria** pasta pessoal (`homes/SEUNOME`), para não atrapalhar os outros. Use `-r` quando quiser o estado inicial.
- No modo `-i`, o shell é interativo: as mensagens de erro saem como no terminal (`bash: xyz: comando não encontrado`). Em script, o Bash acrescenta o nome e a linha (`teste.sh: linha 3: xyz: comando não encontrado`) — mostre a forma certa para cada caso.
- `id`/`groups` no laboratório não mostram os grupos extras da Ana; use os do estado inicial acima.
- Datas e horas: o laboratório usa o relógio real. Nas aulas, prefira datas coerentes com 15/10/2026.
- **Proibido:** `sudo`, instalar pacotes, rodar comandos fora do laboratório que alterem `~` real, usar a internet a partir do laboratório, mexer em `~/guia-bash-lab/template`, `bin` ou `etc`.
- O que não dá para rodar no laboratório (cron real, systemd, rede, ssh) é mostrado como **saída ilustrativa**, e o texto avisa.

### Versões do Bash
O guia ensina o Bash 5.3 (Ubuntu 26.04, Fedora, Arch…). Quando um recurso não existe em versões que o leitor pode ter, marque com `<span class="versao">bash 5.3+</span>` (ou `4.0+`, `5.1+`…) ao lado do título/texto e diga a alternativa. Referências: Debian 13 e Ubuntu 24.04 têm 5.2; o `/bin/bash` do macOS é **3.2** (sem arrays associativos, `mapfile`, `${x,,}`, `|&`, `;&`, `**` …); o padrão do macOS é o zsh.

## 6. Escrita

- Português do Brasil, frases curtas, um assunto por parágrafo. Fale com o leitor ("você").
- Explique a origem em inglês de cada nome (`fi` = `if` ao contrário; `elif` = *else if*; `$#` = "quantos").
- Termo técnico novo → explique na hora ou link para `glossario.html`.
- Use a máquina fictícia: os exemplos acontecem na pasta da Ana, com os arquivos dela (`frutas.txt`, `alunos.csv`, `acesso.log`…), para o leitor poder repetir no simulador.
- Sempre que algo "não faz nada", mostre o código de saída e explique.
- Nada específico de distro, exceto quando inevitável — aí mostre uma tabela "no Debian/Ubuntu × Fedora × Arch × macOS".
