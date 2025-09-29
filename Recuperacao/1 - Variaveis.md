## 📌 O que é uma variável?

Imagine que a **variável** é como uma **caixinha com um nome**, onde você guarda alguma **informação** (como um número, uma palavra, etc.) para usar depois no seu código.

---

## 🟦 Como criar uma variável em TypeScript?

Em TypeScript, usamos as **palavras-chave** `let` e `const` para criar variáveis:

### 🔹 `let` – variável que PODE mudar

```ts
let idade:number = 20;
```

Isso quer dizer: “Estou criando uma variável chamada `idade` e colocando o valor `20` nela”.

Depois, você pode **mudar** o valor dela:

```ts
idade = 25;
```

---

### 🔹 `const` – variável que NÃO pode mudar

```ts
const nome:string = "João";
```

Isso quer dizer: “Estou criando uma variável chamada `nome` e ela vai sempre ser `João`”.

Se você tentar mudar:

```ts
nome = "Maria"; // ❌ Vai dar erro!
```

---

## ✍️ Sintaxe geral

```ts
let nomeDaVariavel: tipo = valor;
```

Exemplo:

```ts
let numero: number = 10;
let texto: string = "Olá";
```

Mas TypeScript é **inteligente**! Ele pode **adivinhar o tipo**, então isso também funciona:

```ts
let numero = 10;         // number
let texto = "Olá";       // string
```

---

## 🧠 Tipos mais usados

| Tipo      | Exemplo              |
| --------- | -------------------- |
| `number`  | `let idade = 30;`    |
| `string`  | `let nome = "Ana";`  |
| `boolean` | `let ligado = true;` |

---

## ✅ Exercício

Vamos fazer um exercício passo a passo.

### ✏️ Enunciado:

1. Crie uma variável com seu nome (use `const`)
2. Crie uma variável com sua idade (use `let`)
3. Mostre os dois no console
4. Mude a idade e mostre de novo

---

## 👀 O que você aprendeu?

* `let` = variável que pode mudar
* `const` = variável que não pode mudar
* Tipos: `string`, `number`, `boolean`
* Como mostrar coisas no console com `console.log()`
