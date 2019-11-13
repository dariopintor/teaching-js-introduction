# Estrutura `while`

Usamos esse tipo de laço quando não sabemos quantas vezes queremos executar uma determinado bloco de instruções, mas sabemos que temos que repetí-lo algumas vezes enquanto alguma condição for satisfeita.
O `for` tem a seguinte estrutura:

```js
while ([condicao]){
  instruções
}
```

Quando executamos esse for ocorre o seguinte:
- `condicao` é avaliada. Se o valor de condição é falso, então o laço terminará. Se a expressão condição é verdadeira o laço continua.

Veja o seguinte exemplo, vamos fazer um programa em que teu objetivo é acertar um objetivo, o número 7. Você vai sortear um número de 1 até 10. Se esse número for o número 7 então o laço para, senão ele deverá continuar a sortear números até que o número sorteado sejá o número 7.

```javascript
// sorteio/sorteio.js
function sortear(max) {
    return 1 + Math.floor(Math.random() * max);
}

var objetivo = 7;
var numero = sortear(10);
while (numero != objetivo) {
    console.log('O número sorteado foi ' + numero + '.Vamos sortear outro número.')
    numero = sortear(10);
}
console.log('Você atingiu seu objetivo, o número sorteado foi o ' + numero)
```

*Para praticar:* implemente um programa que faça o sorteio de números de 1 a 100 e sorteie o valor do `objetivo`.

**Problema 1**

O professor gostaria de calcular a média das notas de uma turma, mas comumente nos dias de prova alguns alunos faltam. Calcular a média das notas consiste em somar as notas e dividir pelo total de notas. Mas o professor não sabe exatamente quantas notas ele deve somar para posteriormente calcular a média. Você vai receber um arquivo de entrada contendo notas de 1 a 10 com uma casa decimal, uma nota por linha. Na última linha você vai encontrar o valor -1, o que indica que não há mais notas a serem somadas.

Arquivo de entrdada:
```js
// media_notas_while/input.txt
9.0
8.8
8.3
9.1
9.2
-1
```

Solução:

```javascript
var input = require('fs').readFileSync('input.txt', 'utf8');
var lines = input.split('\n');

var n = 0;
var soma = 0;

var valor = Number(lines.shift());

while (valor != -1){        
    soma += valor;
    n += 1;
    valor = Number(lines.shift());
}

var media = soma / n;
console.log('Média: ', media.toFixed(1));
```

Passo a passo o que está acontecendo no programa:

1. Lemos o conteúdo do arquivo `input.txt` com as notas e armazenamos isso na variável `lines`.
2. Inicializa uma variável contadora `n` que vai armazenar o número de notas presentes no arquivo.
3. Inicializa uma variável acumuladora `soma` que vai armazenar a soma das notas, o que é útil para calcular a média ao final do programa.
4. Lê o primeiro valor do arquivo de entrada e armazena na variável `valor`. O valor armazenado será `9.0`.
5. Verifica se `valor != -1`. Como é verdadeiro executa o bloco de instruções. Acumula o valor da nota à variável `soma` e aumenta em uma unidade o contador de notas `n`.
6. Lê o próximo valor do arquivo de entrada e armazena na variável `valor`. O valor armzazenado será `8.8`.
7. Verifica se `valor != -1`. Como é verdadeiro executa o bloco de instruções. Acumula o valor da nota à variável `soma` e aumenta em uma unidade o contador de notas `n`.
8. Lê o próximo valor do arquivo de entrada e armazena na variável `valor`. O valor armzazenado será `8.3`.
9. Verifica se `valor != -1`. Como é verdadeiro executa o bloco de instruções. Acumula o valor da nota à variável `soma` e aumenta em uma unidade o contador de notas `n`.
10. Lê o próximo valor do arquivo de entrada e armazena na variável `valor`. O valor armzazenado será `9.1`.
11. Verifica se `valor != -1`. Como é verdadeiro executa o bloco de instruções. Acumula o valor da nota à variável `soma` e aumenta em uma unidade o contador de notas `n`.
12. Lê o próximo valor do arquivo de entrada e armazena na variável `valor`. O valor armzazenado será `9.2`.
13. Verifica se `valor != -1`. Como é verdadeiro executa o bloco de instruções. Acumula o valor da nota à variável `soma` e aumenta em uma unidade o contador de notas `n`.
14. Lê o próximo valor do arquivo de entrada e armazena na variável `valor`. O valor armzazenado será `-1`.
15. Verifica se `valor != -1`. Como é **falso** não executa o bloco de comandos e sai do laço while.
16. Realiza o cálculo da média usando as variáveis `soma` e `n`.
17. Mostra a média com uma casa decimal.
18. Termina o programa.

**Problema 2**

Você está construíndo uma página Web e quer obrigar o cliente a comprar o teu produto. Assim, ao abrir a página você vai mostrar uma mensagem para o usuário perguntando se ele quer comprar o produto. Se ele não quiser comprar, clicando em cancelar, você vai mostrar a mensagem novamente, até que ele cliquei em Ok e finalmente compre o teu produto.

```javascript
<html>
    <head>
        <title>Comprar Produto</title>
    </head>

    <body>
        <h1>Comprando um produto</h1>
        <p id='mensagem'></p>
    </body>

    <script>
    var resposta = confirm('Você gostaria de comprar o produto?');
    while (resposta != true){
        resposta = confirm('Você gostaria de comprar o produto?');
    }
    var mensagem = document.getElementById('mensagem');
    mensagem.innerHTML = "Parabéns, você acabou de comprar o produto!";
    </script>
</html>
```

**Problema 3**

Você está recebendo dados provenientes de uma fila de entrada ao cinema. Para um determinado filme a idade mínima é de 16 anos. Por isso, o teu programa deve deixar passar as pessoas com idade maior ou igual que 16 anos. Em caso de haver alguém com menos que 16 anos deverá chamar o segurança para retirar essa pessoa da fila e parar o programa.

No arquivo de entrada você receberá valores identificadores dos clientes e a sua idade, como segue:

```
12113, 17
10221, 20
99454, 32
56445, 17
34585, 16
88332, 80
34573, 14
12947, 23
88349, 12
11100, 60
```


Solução:

```javascript
var input = require('fs').readFileSync('input.txt', 'utf8');
var lines = input.split('\n');

var cliente_dados = lines.shift().split(", ");
var cliente_id = cliente_dados[0];
var cliente_idade = Number(cliente_dados[1]);

var idade_minima = 16;

while (cliente_idade >= idade_minima){
    console.log('Cliente ' + cliente_id + " pode passar.");
    
    cliente_dados = lines.shift().split(", ");
    cliente_id = cliente_dados[0];
    cliente_idade = Number(cliente_dados[1]);    
}

console.log('Cliente ' + cliente_id + " não pode passar. Chamar o segurança.");
```

## Exercícios

**Exercício 1**

Você foi contratado para melhorar o programa de fila de cinema implementado anteriormente. Como existem filmes que tem diferentes valores de idade mínima o teu programa tem que se adaptar para diferentes valores de idade mínima. Assim, a única alteração em relação ao exercício anterior é que a idade mínima será apresentada na primeira linha do arquivo, da seguinte forma:

```
14
12113, 17
10221, 20
99454, 32
56445, 17
34585, 16
88332, 80
34573, 14
12947, 23
88349, 12
11100, 60
```

**Exercício 2**

Desenvolva um programa que faça o sorteio de dois dados, com valores de 1 a 6. Repita o processo até que os dois dados sorteados possuam o mesmo valor.

**Exercício 3**

Crie uma nova versão do exercício anterior com 3 dados.