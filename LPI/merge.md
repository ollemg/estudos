
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
- apagar sempre que aparecer a palavra X: sed '/texto/d' arquivo.txt