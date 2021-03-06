# Tópico 103 - Trabalhando na linha de comando

## 103.1

Existem 3 tipos de comandos: comandos internos, comandos instalados remotamente e scripts, o comando type serve para identificar isso

Comandos internos e comandos externos não precisa ser executados utilizando o caminho absoluto, scripts por usa vez se não estiverem em algum diretório do $PATH precisam ser executados com o caminho absoluto ou  

```bash
type cd
```

o $PATH identifica

```bash
echo $PATH
```

Para uma variavel ser global é necessário exportar a váriavel

```bash
NOME_VARIAVEL=teste
export NOME_VARIAVEL
```

ou

```bash
export NOME_VARIAVEL=teste
```

o export só funciona para processor originados de um bash, caso abra um novo processo do bash o export não funcionará

comando set mostra todas as variaveis do bash atual
comando env mostra as variaveis globais

Alterar variavel na execução:

```bash
env TESTE=aaaa /home/script/script_teste.sh
```

Remover definição de variavel

```bash
unset TESTE
```

Variaveis de ambientes importantes

- HISTFILE = caminho do arquivos de histórico
- HISTFILESIZE = tamanho do arquivo
- HISTFILES = numero de linhas
- HOME = home do usuário logado
- LOGNAME = usuário que fez o login
- PWD = mostra diretorio atual
- TERM =

Variaveis de ambiente dinamicas, são identificadas por $ no começo

- $$ = PID do processo atual
- $! = PID ultimo processo em background
- $? = Mostra o codigo de retorno do ultimo comando
  - 0 = sucesso
- ~ = home do usuário atual
- ;   = Executa os comandos em sequencia idenpendente do retorno do comando
- &&  = Só executa o proximo comandos se o anterior teve sucesso (codigo de retorno 0)
- ||  = Só execura se o comando anterior não teve sucesso (codigo de retorno diferente de 0)
- !!  = executa o ultimo comando que foi digitado
- !90 = executa o comando número 90 no history
- !cd = Executa o ultimo comando com aquele nome

Histórico:

- history -c = Limpa o histórico

Manual:

- man = consulta o manual do comando, para comandos interno consultar man bash
- info = descrição menos detalhada
- whatis
- apropos

### Alias

Exemplo:

```bash
alias ll='ls -l'
```

witch - localiza qualquer comando (arquivos que estejam no $PATH)

Quoting

- Aspas Duplas - impede a interpretação de todos os caracteres especiais exceto $ ` \
- Aspas Simples - impede a interpretação de todos os caracteres especiais
- Barra invertida - impede a interpretação caracter especial seguinte (apenas o primeiro)

## 103.2

### cat

- -n numera as linhas
- -b numera linhas não brancas
- -s no maximo uma linha em branco
- -a Caracteres especiais

### tac

- inverso do cat

### head

mostra as primeiras linhas de um arquivo

- -n numero de linhas para saida do comando
- -b mostra em bites

### tail

Motras as ultimas linhas de um arquivo

- -f para ver logs

### less

Pagina os a saida de um comando

- / procura palavras
- n proxima palavra
- Ctrl + G mostra informações do arquivo
- Q sair

### wc

- mostra o numero de linhas, palavras e bytes de um arquivo

### nl (number lines)

numera linhas

### sort

Odena arquivos

- -r ordena ao contrario
- -k ordena pela coluna escolhida

### uniq

apenas identifica as linhas duplicadas se a saida estiver ordenada.

- -c mostra quntas vezes a palavra aparece na saida
- -d mostra apenas os duplicados

### od (octal dump)

mostra arquivos em octal por padrão

### join

combina dois arquivos atraves de um indice

### paste

combina dois arquivos sem precisar de indice

### split

separa um arquivo em varios

- -l separa em x linhas
- -b separa por bytes

### tr

manipula arquivos
Utilizar em conjunto com cat

modo de utilizar:

```bash
tr A-Z a-z
```

transforma letras maiusculas em minusculas

- -d deleta

### cut

manipula saidas de arquivos

- -c corta as linhas passando o numero de linhas ou um range
- -d delimita um campo
- -f coluna do delimitador

```bash
cut -d ";" -f1,2,3 .\arquivo.txt
```

### sed

Ferramenta de manipulação de caracteres.

- Substituir primeira ocorrencia de uma linha: sed 's/origem/destino/' arquivo.txt
- Substituir todas as correncias: sed 's/origem/destino/g' arquivo.txt
  - G de global
- Apagar da linha 3 a 5: sed '3,5 d' arquivo.txt
- apagar sempre que aparecer a palavra X: sed '/texto/d'

### checksums

md5sum
sha1sum
sha256sum
sha512sum

-c arquivosum valida o hash

### bonus

Quebras de linha

Line Feed = Nova Linha
\n

CR = Carriage Return
\r

Windows     = CR-LF   \r\n      ^M
Unix\Linux  = LF      \n         $

### Linux Directory Structure

Caminho absoluto = /var/log/
Caminho Relativo ./log

## 103.3

### cd

Volta para o diretorio anterior:

```bash
cd -
```

Ir para home do usuário:

```bash
cd ~
```

### ls

Arquivos ocultos:

```bash
ls -a
```

Lista detalhada, mostra a hora da ultima alteração:

```bash
ls -l
```

Lista Recursivamente

```bash
ls -R /directorio
```

### cp

pergunta se um arquivo vai ser sobrescrit

```bash
cp -i
```

preservar as caracteristicas do arquivo

```bash
cp -p
```

### touch

Cria um arquivo ou altera a data de modificação do arquivo

Modifica a data do ultiM
Data e hora da ultima modificação

```bash
touch -m arquivo.txt
```

Data customizada (31/12/2021):

```bash
touch -t 202131122359 arquivo.txt
```

### rm

Remove arquivos e diretorios

só remove diretorios vazios

```bash
rmdir /diretorio/
```

Remover a arvore de diretorios

```bash
rmdir -p /diretorio1/diretorio2/diretorio3/
```

### mkdir

Cria diretorios

Cria diretorios recursivo

```bash
mkdir -p /diretorio1/diretorio2/diretorio3
```

### find

Procura diretorios e arquivos

```bash
find / -name algumacoisa.txt
```

Procura arquivos e diretorios que pertencem ao usuario root

```bash
find / -user root
```

Arquivos que foram executados um dia antes:

```bash
find / -ctime -1
```

### tar

gerenciador de compactação e descompactação de arquivos.

Principais parametros

- -c criar um arquivo
- -x extrair um arquivo
- -t listar um arquivo
- -f nome do arquivo
- -p preservar as permissoes

```bash
tar -cpvf backup.tar arquivo.log
```

Visualiza arquivos compactados

```bash
tar -tlf backup.tar
```

Os pricipais compactadores

- gzip
- bzip
- xz

Para compactar:

Mantem o arquivo original

```bash
gzip backup.tar
```

```bash
bzip2 -k backup.tar
```

```bash
xz -k backup.tar
```

Para descompactar:

-d descompress

```bash
gzip -d backup.tar.gz
gunzip backup.tar.gz
```

```bash
bzip2 -d backup.tar.bz
bunzip2 backup.tar.bz
```

```bash
xz -d backup.tar.xz
unxz backup.tar.xz
```

## 103.4

Entrada padrão STDIN (0)

Saída Padrão STDOUT (1)

Erro Padrão STDERR (2)

### > >> 2> 2>>

Redirecionamento da saida padrão (sobrescreve o arquivo)

```bash
echo linux > arquivo.txt
```

Redirecionamento da saida padrão (Escreve na ultima linha)

```bash
echo linux >> arquivo.txt
```

Redirecionamento de erro padrão (sobrescreve o arquivo)

```bash
ls -l  arquivo.log 2> arquivo.txt
```

Redirecionamento de erro padrão (Escreve na ultima linha)

```bash
ls -l  arquivo.log 2>> arquivo.txt
```

Redirecionar a saida padrão e a saída de erro pro mesmo arquivo

```bash
ls -l {arquivo,ARQUIVO}3 > saida_padrao.txt 2>$1
```

OBS: não redirecionar um arquivo para o mesmo arquivo

### cpio

similar ao tar

cria uma lista de arquivo, agrupa com o cpio, compacta com gzip

```bash
find ./ -name "*.conf" | cpio -o | gzip > backup.cpio.gz
```

desagrupar arquivos

```bash
cpio -i < backup.cpio.gz
```

desagrupar arquivos e criar os subdiretorios

```bash
cpio -d -i < backup.cpio
```

### dd

### tee

le de uma entrada padrão e escreve uma saida padrão num arquivo

```bash
ls -l \ | tee barra.txt
```

### xargs

exemplo:

```bash
find / -name "*conf" | xargs ls -l
```

### executar comandos dentro de outros comandos

exemplo

```bash
echo "versão do kernel:" `uname -r`
```

```bash
echo "versão do kernel:" $(uname -r)
```

## 103.5

PID = Process ID

PPID = Parent Process ID

Primeiro processo do linux é o init que tem o ID 1

### ps

Visualiza os prcessos em execução

- -u usuario
- -x processos ão ligados ou pts
- -f mostra os parentescos dos processos
- -a
- -C {nome do processo}
- -l mostra a prioridade do processo

exemplo:

```bash
ps -uxf
```

### pstree

-p mostra os id dos processos

### pgrep

mostra o numero do processo

```bash
pgrep firefox
```

```bash
pgrep bash -u root
```

### top

- Shift + M = ordena por Memória
- Shift + P = ordena por Processador
- U = Filtra por usuario
- R =
- N = Numero de processos pra visualizar
- K = mata um processo (kill)

Parecido com um tail -f

```bash
top -b
```

-d = Fica com um delay de 3 segundos
-n = mostra 3 vezes

```bash
top -b -d3 -n3 > log-process.log
```

### kill

- SIGHUP terminar ou reiniair um processo ou reler as configurações
- SIGINT interrompe um processo (Ctrl + C)
- SIGQUIT fecha o processo
- SIGKILL Matar abroptamente, nenhum processo consegue ignorar esse sinal
- SIGTERM encerra o processo de forma não abrupta

### killall

mata o processo baseado no nome

```bash
killall firefox
```

### pkill

faz filtro similar ao pgrep

```bash
pkill -9 nginx -u nginx
```

### free

visualização de memória

### screen

varias telas no mesmo ssh

- ctrl a + n = proxima pagina (next)
- ctrl a + c = Cria uma nova aba
- exit encerra o screen

### bg

processos em backgroud

```bash
firefox &
```

- ctrl Z = pausa o processo

### jobs

mostra os processos em backgroud

### nohup

roda um comando imune a desligamentos e joga a saida do comando para um arquivo

```bash
nohup fireofox &
```

### watch

persiste a saida de um comando na tela

### tmux

similar ao screen só que melhor

ctrl + b c - Criar uma nova janela
ctrl + b w - Escolhe uma janela de uma lista
ctrl + b 0 - Troca pra janela 0
ctrl + b , - Renomear a janela atual
ctrl + b % - Divide horizontalmente em 2 telas
ctrl + b " - Divide verticalmente em 2 telas
ctrl + b o - Ir para próxima página
ctrl + b ; - Alterar entre o painel atual e o anterior
ctrl + b x - Fechar o painel atual

## 103.6

### Priorização de processos

Dentro do comando top

PR - Diz a prioridade naquele momento
NI - Admin influenciar a prioridade

### nice renice

Definir o nice de um processo

```bash
nice
```

Alterar o nice de um processo que já está em execução

```bash
renice
```

A escala vai de -20 até +19. Valor negativo mais prioridade, valor positivo menos prioridade.

Apenas o root pode aumentar a prioridade dos processos.

O padrão do nice é 10

```bash
nice firefox
```

## 103.7

### grep

Numero de ocorrências:

```bash
grep -c linux texto.txt
```

Ignorar case sensetive

```bash
grep -i linux texto.txt
```

Recursivo

```bash
grep -r linux /etc
```

Todas as linhas que não contem a palavra especificada

```bash
grep -v linux texto.txt
```

Expande as expressoes regulares

```bash
grep -E 
egrep
```

Não considera expressões regulares

```bash
fgrep
```

### Expressões Regulares

help: man 7 regex

- [] lista
- ^ começo da linha
- $ final da linha
- ^$ linha em branco
- "*" todas as ocorrências ou nenhuma
- "+" pelo menos uma vez
- ? Nenhuma ou apenas uma vez
- . qualquer caracter, apenas um
- {} numero de ocorrencias
- () agrupar
- | ou

Exemplos com Egrep:

Mostrar apenas as linhas não comentadas e sem linhas em branco

```bash
egrep -v "#|^$" nginx.conf
```

Mostrar as ocorrencias com bag, beg, big:

```bash
egrep "b[aei]g" arquivo.txt
```

Mostrar apenas endereços ipv4:

```bash
ip -br a | egrep -o "([0-9]{1,3}[\.]){3}([0-9]{1,3})"
```

## 103.8

### vim

/ - para pesquisar de baixo pra baixo
? - para pesquisar de cima pra baixo
n - Proximo pra baixo
N - Próximo pra cima
h - um caracter pra trás
j - desce uma linha
k - sobe uma linha
l - um caracter pra frente

Recortar com edição - cc
Recortar sem edição - dd
Recortar 10 linhas - c10c ou d10d
Copiar - yy (yanked)
Copiar 10 - y10y
Colar - p

Salvar        - :w
Sair          - :q
Salvar e Sair - :x
Salvar e Sair - ZZ
Novo Arquivo - :w nome_do arquivo
Carregar a ultima alteração - :e

### emacs e nano
