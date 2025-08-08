# Loops em TypeScript

Em TypeScript, você pode usar diversos tipos de loops para iterar sobre arrays, objetos ou valores. Este guia mostra todos os principais loops com exemplos práticos.

---

## 1. `for` tradicional

O loop `for` clássico é útil quando você precisa de controle total sobre o índice.

```ts
const numeros: number[] = [10, 20, 30];

for (let i = 0; i < numeros.length; i++) {
  console.log(`Índice ${i}: ${numeros[i]}`);
}
````

✅ **Vantagens:**

* Controle completo do índice.
* Permite pular elementos ou parar o loop com `break`.

---

## 2. `for...of`

Itera sobre **valores** de arrays, strings, mapas, sets ou qualquer iterável.

```ts
const frutas = ['maçã', 'banana', 'laranja'];

for (const fruta of frutas) {
  console.log(fruta);
}
```

⚠️ **Não funciona diretamente em objetos comuns**.

---

## 3. `for...in`

Itera sobre **chaves ou índices** de objetos ou arrays.

```ts
const pessoa = { nome: 'Ana', idade: 25 };

for (const chave in pessoa) {
  console.log(`${chave}: ${pessoa[chave as keyof typeof pessoa]}`);
}
```

```ts
const numeros = [10, 20, 30];

for (const indice in numeros) {
  console.log(`Índice ${indice}: ${numeros[indice]}`);
}
```

⚠️ Para arrays, `for...in` retorna **índices como string**, então geralmente é melhor usar `for` ou `for...of`.

---

## 4. `forEach`

Método de array que executa uma função para cada elemento.

```ts
const numeros = [1, 2, 3];

numeros.forEach((num, i) => {
  console.log(`Elemento ${i}: ${num}`);
});
```

✅ **Vantagens:**

* Código mais limpo para percorrer arrays.
* Não precisa se preocupar com índices manualmente.

---

## 5. `while`

Executa um bloco de código enquanto a condição for verdadeira.

```ts
let contador = 0;

while (contador < 5) {
  console.log(`Contador: ${contador}`);
  contador++;
}
```

✅ **Vantagem:** Útil quando não se sabe exatamente quantas vezes o loop vai rodar.

---

## 6. `do...while`

Semelhante ao `while`, mas garante que o bloco execute **pelo menos uma vez**.

```ts
let contador = 0;

do {
  console.log(`Contador: ${contador}`);
  contador++;
} while (contador < 5);
```

---

## Resumo dos loops

| Loop         | Itera sobre    | Retorna | Observações                                            |
| ------------ | -------------- | ------- | ------------------------------------------------------ |
| `for`        | Índices        | nada    | Controle manual do índice                              |
| `for...of`   | Valores        | nada    | Iteráveis como arrays, strings, mapas                  |
| `for...in`   | Chaves/índices | nada    | Para objetos ou arrays (retorna índice como string)    |
| `forEach`    | Valores        | nada    | Método de array, não permite `break`                   |
| `while`      | Condição       | nada    | Executa enquanto a condição for verdadeira             |
| `do...while` | Condição       | nada    | Executa pelo menos uma vez, depois verifica a condição |

---

## Dicas finais

* Use `for` ou `for...of` quando precisar de controle completo ou parar o loop.
* Use `forEach` para código mais limpo em arrays.
* Use `while` quando a condição depende de algo que muda dentro do loop.
* Use `do...while` quando o bloco deve rodar pelo menos uma vez.
* Evite `for...in` em arrays, pois os índices retornados são strings.

---

# Exercícios

## 1. **`for` tradicional** – Tema: Senhor dos Anéis

**Exercício:**

Você tem uma lista dos membros da Sociedade do Anel. Use um `for` para imprimir **somente os hobbits**.

```ts
const sociedade = ['Frodo', 'Sam', 'Gandalf', 'Legolas', 'Gimli', 'Merry', 'Pippin', 'Aragorn', 'Boromir'];
```

**Como fazer:**

* Use o `for` tradicional com índice.
* Imprima: `"Hobbit encontrado: <nome>"`

---

## 2. **`for...of`** – Tema: Star Wars

**Exercício:**

Você tem uma lista de personagens de Star Wars. Use `for...of` para imprimir **todos os personagens que são jedis**.

```ts
const personagens = [
  { nome: 'Luke Skywalker', jedi: true },
  { nome: 'Leia Organa', jedi: false },
  { nome: 'Yoda', jedi: true },
  { nome: 'Darth Vader', jedi: false },
];
```

**Desafio:**

* Imprima: `"Jedi encontrado: <nome>"`

---

## 3. **`for...in`** – Tema: Naruto

**Exercício:**

Você tem um objeto com personagens de Naruto e seus clãs. Use `for...in` para imprimir todos os clãs e seus membros.

```ts
const personagens = {
  Naruto: 'Uzumaki',
  Sasuke: 'Uchiha',
  Sakura: 'Haruno',
  Kakashi: 'Hatake'
};
```

**Desafio:**

* Imprima: `"<Personagem> pertence ao clã <clã>"`

---

## 4. **`forEach`** – Tema: Dragon Ball

**Exercício:**

Você tem uma lista de personagens de Dragon Ball e seus níveis de poder. Use `forEach` para imprimir **somente aqueles com nível de poder maior que 8000**.

```ts
const personagens = [
  { nome: 'Goku', poder: 15000 },
  { nome: 'Vegeta', poder: 14999 },
  { nome: 'Krillin', poder: 7500 },
  { nome: 'Freeza', poder: 20000 },
];
```

**Desafio:**

* Imprima: `"O poder de <nome> é de mais de 8000!"`

---

## 5. **`while`** – Tema: Pokémon

**Exercício:**

Você tem uma lista de Pokémon. Use `while` para capturar Pokémon até encontrar um **Pokémon lendário**.

```ts
const pokemons = ['Pikachu', 'Charmander', 'Bulbasaur', 'Mewtwo', 'Squirtle'];
```

**Desafio:**

* Imprima: `"Capturando <nome>"`
* Quando encontrar `"Mewtwo"`, imprima `"Pokémon lendário encontrado: Mewtwo!"` e pare o loop.

---

## 6. **`do...while`** – Tema: Senhor dos Anéis

**Exercício:**

Você está jogando um jogo de aventura e precisa **andar pela Terra Média até chegar em Mordor**. Use `do...while` para simular os passos.

```ts
let passos = 0;
const passosParaMordor = 5;
```

**Desafio:**

* A cada passo, imprima: `"Dando passo <passos>"`
* Quando chegar em Mordor, imprima: `"Chegamos em Mordor!"`

---

# 📥 Respostas

<details>
<summary>Clique aqui para mostrar as respostas dos exercícios</summary>

```ts
// 1 - Sociedade do Anel - Hobbits
const sociedade = ['Frodo', 'Sam', 'Gandalf', 'Legolas', 'Gimli', 'Merry', 'Pippin', 'Aragorn', 'Boromir'];

for (let i = 0; i < sociedade.length; i++) {
    if (sociedade[i] === 'Frodo'
        || sociedade[i] === 'Sam'
        || sociedade[i] === 'Merry'
        || sociedade[i] === 'Pippin') {
        console.log(`Hobbit encontrado: ${sociedade[i]}`);
    }
}

// 2 - Star Wars - Jedis
const personagensSW = [
    { nome: 'Luke Skywalker', jedi: true },
    { nome: 'Leia Organa', jedi: false },
    { nome: 'Yoda', jedi: true },
    { nome: 'Darth Vader', jedi: false },
];

for (let personagem of personagensSW) {
    if (personagem.jedi) {
        console.log(`Jedi encontrado: ${personagem.nome}`);
    }
}

// 3 - Naruto - Clãs
const personagensNaruto = {
    Naruto: 'Uzumaki',
    Sasuke: 'Uchiha',
    Sakura: 'Haruno',
    Kakashi: 'Hatake'
};

for (let personagem in personagensNaruto) {
    console.log(`${personagem} pertence ao clã ${personagensNaruto[personagem as keyof
```


typeof personagensNaruto]}\`);
}

// 4 - Dragon Ball - Poder
const personagensDBZ = \[
{ nome: 'Goku', poder: 15000 },
{ nome: 'Vegeta', poder: 14999 },
{ nome: 'Krillin', poder: 7500 },
{ nome: 'Freeza', poder: 20000 },
];

personagensDBZ.forEach((personagem) => {
if (personagem.poder > 8000) {
console.log(`O poder de ${personagem.nome} é de mais de 8000!`);
}
});

// 5 - Pokémon - While
const pokemons = \['Pikachu', 'Charmander', 'Bulbasaur', 'Mewtwo', 'Squirtle'];
let contador = 0;

while (contador < pokemons.length) {
if (pokemons\[contador] === 'Mewtwo') {
console.log('Pokémon lendário encontrado: Mewtwo!');
break;
}
console.log(`Capturando ${pokemons[contador]}`);
contador++;
}

// 6 - Terra Média - do...while
let passos = 0;
const passosParaMordor = 5;

do {
console.log(`Dando passo ${passos}`);
passos++;
} while (passos < passosParaMordor);

console.log('Chegamos em Mordor!');

```

</details>
```

