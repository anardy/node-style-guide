# Guia de Estilo Node.js

Este guia foi escrito para escrever códigos consistentes e esteticamente agradável em node.js.
É inspirado nas práticas dentro da comunidade e com algumas percepções pessoais.

O guia foi criado por [Felix Geisendärfer](http://felixge.de/) e está sob a licença
[CC BY-SA 3.0](http://creativecommons.org/licenses/by-sa/3.0/).
Você pode fazer o fork deste repositório e fazer ajuste conforme a sua preferência.

A tradução para o português foi realizada por [André Nardy](https://github.com/anardy)

![Creative Commons License](http://i.creativecommons.org/l/by-sa/3.0/88x31.png)

## 2 Spaces for indention

Use 2 spaces for indenting your code and swear an oath to never mix tabs and
spaces - a special kind of hell is awaiting you otherwise.

## 2 Espaços para identação

Use 2 espaços para identar seu código spaces for indenting your code and swear an oath to never mix tabs and
spaces - a special kind of hell is awaiting you otherwise.

## Novas Linhas

O UNIX utiliza (`\n`) para identificar uma nova linha e é colocado como último caracter do arquivo.
Já o Windows a nova linha é indicada com (`\r\n`) e é proibido dentro de qualquer repositório.

## Sem espaço em branco

Assim como você escova os dentes após cada refeição, você deve limpar qualquer espaço em branco em seu arquivo JS antes de realizar o commit.

## Use Semicolons

According to [scientific research][hnsemicolons], the usage of semicolons is
a core value of our community. Consider the points of [the opposition][], but
be a traditionalist when it comes to abusing error correction mechanisms for
cheap syntactic pleasures.

[the opposition]: http://blog.izs.me/post/2353458699/an-open-letter-to-javascript-leaders-regarding
[hnsemicolons]: http://news.ycombinator.com/item?id=1547647

## Use Ponto e Vírgula

De acordo com a [scientific research][hnsemicolons], o uso de vírgula é fundamental dentro da nossa comunidade. Considere os pontos chaves do [the opposition][], mas seja um tradicionalista quando se refere aos mecanismos de correção de erros

[the opposition]: http://blog.izs.me/post/2353458699/an-open-letter-to-javascript-leaders-regarding
[hnsemicolons]: http://news.ycombinator.com/item?id=1547647

## 80 caracteres por linha

Faça com que suas linhas tenham 80 caracteres.

## Use aspas simples

Use aspas simpes, ao menos que esteja escrevendo JSON.

*Correto:*

```js
var foo = 'bar';
```

*Errado:*

```js
var foo = "bar";
```

## Chaves de abertura na mesma linha

As chaves de abertura vão na mesma linha da instrução de condição

*Correto:*

```js
if (true) {
  console.log('winning');
}
```

*Errado:*

```js
if (true)
{
  console.log('losing');
}
```

Além disso, observe o uso de espaços antes e depois da instrução de condição.

## Declare uma variável por instrução var

Declare uma variável para cada instrução var, isto torna mais fácil a reordenação das linhas. Porém, ignore [Crockford][crockfordconvention] when it comes to
declaring variables deeper inside a function, just the declarations wherever
they make sense.

*Certo:*

```js
var keys   = ['foo', 'bar'];
var values = [23, 42];

var object = {};
while (keys.length) {
  var key = keys.pop();
  object[key] = values.pop();
}
```

*Errado:*

```js
var keys = ['foo', 'bar'],
    values = [23, 42],
    object = {},
    key;

while (keys.length) {
  key = keys.pop();
  object[key] = values.pop();
}
```

[crockfordconvention]: http://javascript.crockford.com/code.html

## Use lowerCamelCase para variáveis, propriedades e nome de funções

Variáveis, propriedades e nome de funções devem user `lowerCamelCase`. Também devem ser descritivos. Variáveis com apenas um caracter e abreviaturas incomuns também devem ser evitadas.

*Certo:*

```js
var adminUser = db.query('SELECT * FROM users ...');
```

*Errado:*

```js
var admin_user = db.query('SELECT * FROM users ...');
```

## Use UpperCamelCase para nome de classes

Os nomes das Classes devem usar `UpperCamelCase`.

*Certo:*

```js
function BankAccount() {
}
```

*Errado:*

```js
function bank_Account() {
}
```

## Use UPPERCASE para Constantes

As constantes devem ser declaradas as regular variables or static class properties,
using all uppercase letters.

Atualmente Node.js / V8 suporta a extensão [const][const], mas infelizmente isso não pode ser aplicado aos membros da classe e nem faz parte de qualquer parte do padrão ECMA.

*Correto:*

```js
var SECOND = 1 * 1000;

function File() {
}
File.FULL_PERMISSIONS = 0777;
```

*Errado:*

```js
const SECOND = 1 * 1000;

function File() {
}
File.fullPermissions = 0777;
```

[const]: https://developer.mozilla.org/en/JavaScript/Reference/Statements/const

## Criação de Objetos / Array

Use uma única linhas para declarações curtas e use espaçõ depois da vírgula. Only quote
keys when your interpreter complains:

*Correto:*

```js
var a = ['hello', 'world'];
var b = {
  good: 'code',
  'is generally': 'pretty',
};
```

*Errado:*

```js
var a = [
  'hello', 'world'
];
var b = {"good": 'code'
        , is generally: 'pretty'
        };
```

## Use o operador ===

Programação não é só lembrar das [stupid rules][comparisonoperators]. Use
o operador triplo de igualdade, já que irá funcionar como o esperado.

*Correto:*

```js
var a = 0;
if (a !== '') {
  console.log('winning');
}

```

*Errado:*

```js
var a = 0;
if (a == '') {
  console.log('losing');
}
```

[comparisonoperators]: https://developer.mozilla.org/en/JavaScript/Reference/Operators/Comparison_Operators

## Use várias linhas para operador ternário

O operador ternário não deve ser usado em uma única linha. Quebre em várias linhas.

*Correto:*

```js
var foo = (a === b)
  ? 1
  : 2;
```

*Errado:*

```js
var foo = (a === b) ? 1 : 2;
```

## Do not extend built-in prototypes

Do not extend the prototype of native JavaScript objects. Your future self will
be forever grateful.

*Correto:*

```js
var a = [];
if (!a.length) {
  console.log('winning');
}
```

*Errado:*

```js
Array.prototype.empty = function() {
  return !this.length;
}

var a = [];
if (a.empty()) {
  console.log('losing');
}
```

## Use descriptive conditions

Any non-trivial conditions should be assigned to a descriptively named variable or function:

*Correto:*

```js
var isValidPassword = password.length >= 4 && /^(?=.*\d).{4,}$/.test(password);

if (isValidPassword) {
  console.log('winning');
}
```

*Errado:*

```js
if (password.length >= 4 && /^(?=.*\d).{4,}$/.test(password)) {
  console.log('losing');
}
```

## Escreva funções curtas

Mantenha suas funções curtas. Uma função boa é aquele que as pessas que estão na última fileira de um grande sala conseguem ler confortavelmente. Portanto, não conte que eles tenham uma visão perfeita e limite-se a ~ 15 linhas de código por função.

## Return early from functions

To avoid deep nesting of if-statements, always return a function's value as early
as possible.

*Correto:*

```js
function isPercentage(val) {
  if (val < 0) {
    return false;
  }

  if (val > 100) {
    return false;
  }

  return true;
}
```

*Errado:*

```js
function isPercentage(val) {
  if (val >= 0) {
    if (val < 100) {
      return true;
    } else {
      return false;
    }
  } else {
    return false;
  }
}
```

Com esse exemplo é possível reduzir ainda mais a função:

```js
function isPercentage(val) {
  var isInRange = (val >= 0 && val <= 100);
  return isInRange;
}
```

## Nomei seus closures

Feel free to give your closures a name. It shows that you care about them, and
will produce better stack traces, heap and cpu profiles.

*Correto:*

```js
req.on('end', function onEnd() {
  console.log('winning');
});
```

*Errado:*

```js
req.on('end', function() {
  console.log('losing');
});
```

## Não alinhe (nest) closures

Use closures, mas não os alinhe (nest). Caso contrário, seu código ficará uma bagunça.

*Correto:*

```js
setTimeout(function() {
  client.connect(afterConnect);
}, 1000);

function afterConnect() {
  console.log('winning');
}
```

*Errado:*

```js
setTimeout(function() {
  client.connect(function() {
    console.log('losing');
  });
}, 1000);
```

## Use barras para comentar

Use as barra tanto para comentários em uma única linha como para múltiplas linhas. Tente sempre escrever comentários que explicam o mecanismo do código ou esclarecer uma parte complexa do mesmo. Não use comentário para descrever coisas triviais.

*Correto:*

```js
// 'ID_SOMETHING=VALUE' -> ['ID_SOMETHING=VALUE'', 'SOMETHING', 'VALUE']
var matches = item.match(/ID_([^\n]+)=([^\n]+)/));

// This function has a nasty side effect where a failure to increment a
// redis counter used for statistics will cause an exception. This needs
// to be fixed in a later iteration.
function loadUser(id, cb) {
  // ...
}

var isSessionValid = (session.expires < Date.now());
if (isSessionValid) {
  // ...
}
```

*Errado:*

```js
// Execute a regex
var matches = item.match(/ID_([^\n]+)=([^\n]+)/));

// Usage: loadUser(5, function() { ... })
function loadUser(id, cb) {
  // ...
}

// Check if the session is valid
var isSessionValid = (session.expires < Date.now());
// If the session is valid
if (isSessionValid) {
  // ...
}
```

## Object.freeze, Object.preventExtensions, Object.seal, with, eval

Instruções que provavelmente você nunca vai usar. Fique longe delas.

## Getters e setters

Do not use setters, they cause more problems for people who try to use your
software than they can solve.

Feel free to use getters that are free from [side effects][sideeffect], like
providing a length property for a collection class.

[sideeffect]: http://en.wikipedia.org/wiki/Side_effect_(computer_science)