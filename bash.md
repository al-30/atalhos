# Atalhos

## Bash

## Comandos

1. [Cat](#cat)

### Cat

O comando cat (concatenate) é usado para ler, exibir, concatenar e criar
arquivos de texto.

Sintaxe basica

```bash
cat [opções] [arquivo(s)]
```

Algumas opcoes que podem ser passadas sao:

| Opção                       | Descrição                                                                      |
| --------------------------- | ------------------------------------------------------------------------------ |
| `-A` ou `--show-all`        | Mostra todos os caracteres invisíveis (`^I` para tabs, `$` no final de linhas) |
| `-b` ou `--number-nonblank` | Numera apenas linhas não vazias                                                |
| `-e`                        | Mostra `$` no final de cada linha + ativa `-v` (caracteres não imprimíveis)    |
| `-E`                        | Mostra `$` no final de cada linha                                              |
| `-n`                        | Numera todas as linhas                                                         |
| `-s` ou `--squeeze-blank`   | Remove linhas em branco repetidas consecutivas                                 |
| `-T`                        | Mostra tabs como `^I`                                                          |
| `-v`                        | Mostra caracteres não imprimíveis (exceto tabs e newline)                      |

Ler arquivos com cat:

```bash
# Imprimir conteudo de arquivo no terminal
cat nome-do-arquivo
```

Criar aquivos com o cat:

```bash

# Criar arquivo novo e digitar conteúdo
cat > novo-arquivo.txt
# Digite texto e pressione Ctrl+D para finalizar

# Criar arquivo com múltiplas linhas
cat > arquivo-final.txt <<EOF
Linha 1
Linha 2
Linha 3
EOF

```

### Estruturas de Controle

### if / else

```bash

if [[ condição ]]; then
    echo "Condição verdadeira"
elif [[ outra_condição ]]; then
    echo "Outra condição verdadeira"
else
    echo "Condição falsa"
fi
```

Testa se variável não está vazia

```bash

if [[ -n "$var" ]]; then
  echo "Não está vazia"
fi
```

Testa se variável está vazia

```bash

if [[ -z "$var" ]]; then
  echo "Está vazia"
fi
```

Comparação de strings

```bash

if [[ "$var" == "texto" ]]; then
  echo "É igual a 'texto'"
fi
```

Comparação numérica

```bash

if [["$num" -eq 10]]; then
  echo "Número é 10"
fi
```

while / until

```bash

while [[ condição ]]; do
    echo "Loop while"
done
```

```bash

until [[condição]]; do echo "Loop until" done
```

Tipos de for

Loop com incremento personalizado .Conta de 2 em 2 (0, 2, 4, 6, 8, 10).

```bash

for i in {1..5}; do
    echo "Número: $i"
done
```

Loop com seq, Conta de 1 até 15 de 3 em 3 (1, 4, 7, 10, 13).

```bash

for i in $(seq 1 3 15); do
    echo "Valor: $i"
done
```

Iterando sobre arquivos

```bash

for file in *.txt; do
    echo "Arquivo encontrado: $file"
done
```

Iterando sobre palavras

```bash
for palavra in eu gosto de bash; do
    echo "Palavra: $palavra"
done
```

Tradicional

```bash

for (( i=0; i<5; i++ )); do
   echo "i = $i"
done
```

Loop em diretórios, Lista apenas pastas do diretório atual

```bash

for dir in */; do
    echo "Diretório: $dir"
done

```

Loop com resultado de comando, Lista todos os IDs de processos.

```bash

for pid in $(ps -e -o pid=); do
    echo "Processo rodando: $pid"
done
```

## Obter entrada iterativa no teclado.

Para obter uma leitura dinamica de dados via terminal é necessario utilizar o
comando read, com ele é possivel que o usuario insira dados de acordo com a
execucao do script. A flag -p permite que imprimir uma mensagem para o usario na
mesma linha onde ele digita a entrada.

O exemplo a seguir simula o cadastro de um cliente.

```bash

cadastro_cliente() {
    # Solicita o nome
    read -p "Digite um nome: " nome

    if [[ -z "$nome" ]]; then
        echo "❌ Nome inválido!"
        return 1
    fi

    # Solicita a data de nascimento
    read -p "Digite a data de aniversário (dd/mm/aaaa): " aniversario

    if [[ -z "$aniversario" ]]; then
        echo "❌ Data de aniversário inválida!"
        return 1
    fi

    # Exibe os dados coletados
    echo ""
    echo "✅ Cadastro realizado com sucesso!"
    echo "Nome: $nome"
    echo "Aniversário: $aniversario"
}

```

### Outras flags

- -s → Silent mode (não mostra o que o usuário digita, útil para senhas).

- -n <num> → lê apenas n caracteres sem precisar de Enter.

- -t <segundos> → define um timeout para a entrada.

- -a array → lê valores separados por espaço e guarda em um array.

- -r → impede que caracteres de escape (\) sejam interpretados.

Exemplos de uso

### -p → Usando para mostrar um prompt

```bash

read -p "Digite seu nome: " nome
echo "Bem-vindo, $nome!"
```

Usando valor padrão se vazio

```bash

read -p "Digite sua cidade: " cidade
cidade=${cidade:-"Não informada"}
echo "Cidade: $cidade"

```

-s → entrada silenciosa (oculta, útil para senha)

```bash

read -s -p "Digite sua senha: " senha
echo -e "\nSenha recebida!"
```

### -n → Número de caracteres

```bash

read -n 1 -p "Pressione uma tecla para continuar..." tecla
echo -e "\nVocê digitou: $tecla"
```

### -t → Tempo limite (timeout), Se o usuário não digitar nada em 5s, a variável

fica vazia.

```bash

read -t 5 -p "Digite algo em até 5 segundos: " resposta
echo "Você digitou: $resposta"

```

### -a → Salvar em array

```bash

read -a frutas
echo "Você digitou: ${frutas[0]}, ${frutas[1]}, ${frutas[2]}"

```

### -r → Evitar interpretação de \. Sem -r, algo como \n poderia ser interpretado

como quebra de linha.

```bash

read -r caminho
echo "Caminho: $caminho"

```
