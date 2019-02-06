# Expressões Regulares - Javascript

## Índice

1. [Introdução](#introdução)
2. [String Literal](#string-literal)
3. [Flags](#flags)
   * [Case sensitive](#case-sensitive)
   * [Global](#global)

## Introdução

Depois de muito tempo quebrando a cabeça e copiando os Regex alheios :innocent:, decidi investir um tempo pra estudar, entender e aplicar os conhecimentos. Usei como fonte de estudo, o [FreecodeCamp](https://www.freecodecamp.org/). Pra quem não conhece é um site que oferece uma forma gratuita de aprender centenas de coisas relacionadas a desenvolvimento Web. Recomendo fortemente.

Mas afinal o que é expressão regular? Para que serve? O Wikipedia nos ajuda nessa missão :heart:, olha só:

>“ Em ciência da computação, uma expressão regular (ou os estrangeirismos regex ou regexp, abreviação do inglês regular expression) provê uma forma concisa e flexível de identificar cadeias de caracteres de interesse, como caracteres particulares, palavras ou padrões de caracteres. Expressões regulares são escritas numa linguagem formal que pode ser interpretada por um processador de expressão regular, um programa que serve um gerador de analisador sintático ou examina o texto e identifica as partes que casam com a especificação dada” 
-- [Wikipedia](https://pt.wikipedia.org/wiki/Express%C3%A3o_regular)


Acredite, manjar de REGEX (aka expressão regulares ou REGEXP) pode poupar um tempo precioso da sua vida de programador e fazer suas soluções ficarem mais finas e elegantes :sunglasses:. O uso do REGEX vai das buscas de texto simples até complexas validações de formulários. Vale muito a pena aprender.

Bem, neste tempo em que estou estudando decidi coletar tudo que vi de interessante e ir descrevendo aqui. A intenção é compartilhar o que estou aprendendo. Eu realmente espero que ajude!

Vamos começar, então? Hoje vou falar um pouco sobre o básico de REGEX e como implementar soluções utilizando o bom e não tão velho Vanilla Javascript.

Boa leitura & have fun! :books: :punch:

## String Literal

Se você precisa encontrar uma palavra ou um conjunto de caracteres na sua forma literal em um texto, o REGEX pode te ajudar! Vamos ao exemplo:

Digamos que Maria Florentina recebe uma tarefa de criar uma função que verifica se uma determinada frase contém a palavra “Josebaldo”.

O que Maria Florentina terá que fazer é criar uma função que receba uma frase como argumento, atribuir a uma constante a expressão regular e logo após executar o método do Javascript chamado test para verificar se a expressão existe na frase.

Para criar a expressão regular neste caso, é bem simples. Como é uma expressão literal, basta colocar a palavra ou conjunto de caracteres entre barras. Ex.: /**JoseBaldo**/

Simples não é?

```
function encontreJoseBaldo(frase){
  const testeRegex = /JoseBaldo/
  return testeRegex.test(frase)
}

encontreJoseBaldo(“JoseBaldo é um cara legal") 
// Irá retornar "true"
```

O método test realiza a busca de uma expressão regular em uma string (no nosso caso uma frase) e é um método nativo do Javascript. Caso encontre a expressão na string, o método retornará true. Caso contrário, retorna false.

Agora vamos adicionar um pouco de complexidade. Digamos que queremos que a funcão retorne verdadeiro também se houver o nome JecaBeludo.

Neste caso estaríamos dizendo para a função: “Olha função você deve localizar o JoseBaldo ou JecaBeludo, ok?”. Em REGEX usamos o caractere | para representar a palavra “ou”.

A função ficaria:

```
function encontreJoseEJeca(frase){
  const testeRegex = /JoseBaldo|JecaBeludo/
  return testeRegex.test(frase)
}

encontreJoseEJeca("JoseBaldo e Jeca são legais") 
// Irá retornar "true"
```

## Flags

As flags são indicativos para o programa que irá interpretar a expressão regular. Basta inserir a flag após a última barra e pronto.


### <a name="case-sensitive"></a> Case sensitive - Flag i

Utilizamos o REGEX para verificar se uma frase contém uma determinada palavra ou conjunto de caracteres, porém podemos ter um problema se considerarmos que o REGEX é case sensitive, ou seja, ele não encontraria o nome “JoseBaldo” se na frase estivesse tudo minúsculo.

Mas para isso existe uma solução. Se você quer que sua expressão não seja case sensitive, ou seja, não diferenciar para maiúscula e minúsculo, utilize a flag “i” para resolver isto.

Veja o exemplo abaixo:

```
function encontreJoseEJeca(frase){
  const testeRegex = /JoseBaldo|JecaBeludo/i
  return testeRegex.test(frase)
}

encontreJoseEJeca("Oi jecabeludo") // retorna true
encontreJoseEJeca("Oi joseBaldo") // retorna true
```

### <a name="global"></a> Global - Flag g

Até agora, você deve ter percebido que utilizamos o REGEX apenas para dizer se existe ou não uma expressão em determinada string. Mas podemos ir além. É possível criar uma função onde toda vez que a expressão for encontrada na string é retornado um array com essa expressão.

Digamos que temos a frase “*Tudo o que temos de decidir é o que fazer com o tempo que nos é dado.*” e queremos buscar a palavra “que” e o array abaixo seja retornado: 

```
[“que”, “que”, “que”]
```

Para que isso aconteça, precisamos utilizar a flag G. Essa flag é utilizada quando você precisa que o programa não pare na primeira combinação, mas que leia a string/frase até o final procurando outras combinações. Com isto sabemos que se não utilizarmos esta flag o resultado será apenas [“que”].

A função ficaria desta forma:

```
const frase = "Tudo o que temos de decidir é o que fazer com o tempo que nos é dado."

function encontreTodos(frase){
  const testeRegex = /que/g
  return frase.match(testeRegex)
}

encontreTodos(frase) // retornará ["que", "que", "que"]
```

Note que estamos usandoo método “match” do javascript, ele retorna exatamente o que precisamos, um array com todos os matches (combinações). Bacana não é?

