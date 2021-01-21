# Tópico 103 - Trabalhando na linha de comando

## 103.1 shell, bash, echo, type, PATH

Existem 3 tipos de comandos: comandos internos, comandos instalados remotamente e scripts, o comando type serve para identificar isso

Comandos internos e comandos externos não precisa ser executados utilizando o caminho absoluto, scripts por usa vez se não estiverem em algum diretório do $PATH precisam ser executados com o caminho absoluto ou  

```bash
type cd
```

o $PATH identifica

```bash
echo $PATH
```

## 103.1 variaveis de ambiente

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
li
  - 
- ~ = home do usuário atual

## 103.1 Comandos sequenciais

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

Alias

Exemplo:
```bash
alias ll='ls -l'
```

witch - localiza qualquer comando (arquivos que estejam no $PATH)


Quoting

- Aspas Duplas - impede a interpretação de todos os caracteres especiais exceto $ ` \
- Aspas Simples - impede a interpretação de todos os caracteres especiais
- Barra invertida - impede a interpretação caracter especial seguinte (apenas o primeiro)
- 

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

### sed

Ferramenta de manipulação de caracteres.

- Substituir primeira ocorrencia de uma linha: sed 's/origem/destino/' arquivo.txt
- Substituir todas as correncias: sed 's/origem/destino/g' arquivo.txt 
  - G de global
- Apagar da linha 3 a 5: sed '3,5 d' arquivo.txt
- apagar sempre que aparecer a palavra X: sed '/texto/d'