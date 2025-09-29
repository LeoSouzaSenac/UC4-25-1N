## 🧮 O que são operadores aritméticos?

São símbolos usados para **fazer contas** (operações matemáticas) com números.

---

## ✍️ Tipos aritméticos em TypeScript

Aqui estão os **principais operadores** e o que eles fazem:

| Símbolo | Nome           | O que faz                     | Exemplo (com resultado) |
| ------- | -------------- | ----------------------------- | ----------------------- |
| `+`     | Soma           | Adiciona dois valores         | `5 + 3 = 8`             |
| `-`     | Subtração      | Subtrai um valor do outro     | `10 - 4 = 6`            |
| `*`     | Multiplicação  | Multiplica dois valores       | `6 * 2 = 12`            |
| `/`     | Divisão        | Divide um valor pelo outro    | `8 / 2 = 4`             |
| `%`     | Módulo (resto) | Mostra o **resto** da divisão | `7 % 3 = 1`             |


OBS: o **resto** é quanto que sobra de uma divisão igualitária.
Por exemplo, se eu tenho 10 laranjas em uma cesta para dividir entre duas pessoas, consigo dividir igualmente 5 para cada uma, e sobram 0 laranjas na cesta. Ou seja, o **resto** é zero.
Agora, se tenho 20 maçãs em uma cesta para dividir entre três pessoas, consigo dividir igualmente 6 para cada uma, mas sobram 2 maçãs na cesta, pois não consigo dividir essas duas que restaram entre as 3 pessoas. Ou seja, nesse caso, o **resto** é 2.

---

## 💻 Exemplos com tipagem explícita:

```ts
// Soma
let soma: number = 10 + 5;
console.log("Soma:", soma); // 15

// Subtração
let subtracao: number = 20 - 7;
console.log("Subtração:", subtracao); // 13

// Multiplicação
let multiplicacao: number = 4 * 3;
console.log("Multiplicação:", multiplicacao); // 12

// Divisão
let divisao: number = 16 / 4;
console.log("Divisão:", divisao); // 4

// Módulo (resto da divisão)
let resto: number = 10 % 3;
console.log("Resto da divisão (10 % 3):", resto); // 1
```

---

## 🧠 Dica importante:

* Sempre que você usar operadores aritméticos, os valores devem ser do tipo `number`.
* O resultado também será sempre do tipo `number`.

---

## 🧪 Exercício simples

### ✏️ Enunciado:

1. Crie duas variáveis chamadas `a` e `b`, com valores numéricos.
2. Faça e mostre no console: soma, subtração, multiplicação, divisão e o módulo.

---



