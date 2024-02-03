# Script - Introdução ao Shell Script

## Variáveis

```bash
nome="Lucas"
idade=11
```

```bash
echo $nome
echo $idade
echo "$nome; $idade anos"
```

## Tipos de Váriaveis

**Variáveis de ambiente**: Variáveis do sistema operacional

- listar variáveis de ambiente no Linux: `printenv`
- criar uma Nova Variável de Ambiente Linux: `export MY_VAR="value"`
- desativar uma Variável de Ambiente Linux: `unset MY_VAR`
- para manter a variável salva após reiniciar o terminal, salvar o comando ao final do arquivo `~/.bashrc`; para aplicar as mudanças digite o comando `source ~/.bashrc`

**Variáveis do Shell**: Definidas pelo usuário.

**Variáveis de Script**: Recebem valores para executar o script - `$1, $2, $3`

## Functions

```bash
# Definição
nome_da_funcao() {
  # codigo da funcao;
  # ...;
}
```

```bash
# Exemplo
function saudacao() {
  echo "Ola $1, voce tem $2 anos de idade.";
  echo "Seja bem vindo aos estudos de script!";
}
saudacao Lucas
```

## Argumentos

**$0**: Contém o nome do próprio script

**$1, $2, $3**: Contêm os valores dos argumentos passados na ordem em que foram fornecidos

**$@**: Contém todos os argumentos passados, separados por espaço

**$***: Contém todos os argumentos passados como uma única string separados por espaço

**$#**: Contém o número total de argumentos passados

```bash
function testar_param() {
  echo $0;
  echo $1, $2;
  echo $@;
  echo $*;
  echo $#;
}

testar_param Lucas Andre
```

## Condicionais IF

- Operadores relacionais

## Loops

- for
- while
- until

## Arquivo de Script

- criar um arquivo contendo o script: `meu_script.sh`; iniciado com a linha `#!/bin/bash`
- rodar o comando: `chmod +x meu_script.sh`
- chamar o script: `./script.sh`

```bash
vi saudacao.sh
```

```bash
#!/bin/bash

echo "Ola $1, você tem $2 anos de idade."
echo "Seja bem vindo aos estudos de script."
```

```bash
chmod +x saudacao.sh
./saudacao.sh Lucas 11
```

## Arquivo de Funções

- criar um arquivo com a definição das funções
- usar comando `source` no arquivo criado
- chamar as funções no bash para executar

```bash
vi funcoes_math
```

```bash
function somar() {
  echo "A soma de $1 + $2 é:" $(($1+$2));
}

function subtrair() {
  echo "A subtração de $1 - $2 é:" $(($1-$2));
}

function multiplicar() {
  echo "A multiplicação de $1 x $2 é:" $(($1*$2));
}

function dividir() {
  echo "A divisão de $1 / $2 é:" $(($1/$2));
}
```

```bash
source funcoes_math
```

```bash
somar 1 2
subtrair 2 1
multiplicar 2 4
dividir 4 2
```
