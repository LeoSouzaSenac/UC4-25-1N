## 🧠 O que são operadores de comparação?

São símbolos usados para **comparar dois valores** e o resultado **sempre será um valor booleano**:
👉 `true` (verdadeiro) ou `false` (falso)

---

## 🔁 Lista dos principais operadores de comparação:

| Operador | Significado                       | Exemplo     | Resultado  |
| -------- | --------------------------------- | ----------- | ---------- |
| `==`     | Igual (valor)                     | `5 == "5"`  | `true` ⚠️  |
| `===`    | Estritamente igual (valor e tipo) | `5 === "5"` | `false` ✅  |
| `!=`     | Diferente (valor)                 | `5 != "5"`  | `false` ⚠️ |
| `!==`    | Estritamente diferente            | `5 !== "5"` | `true` ✅   |
| `>`      | Maior que                         | `10 > 5`    | `true`     |
| `<`      | Menor que                         | `3 < 8`     | `true`     |
| `>=`     | Maior ou igual                    | `7 >= 7`    | `true`     |
| `<=`     | Menor ou igual                    | `4 <= 3`    | `false`    |

> ⚠️ **Dica importante:** Use **`===`** e **`!==`** sempre que possível. Eles comparam **valor e tipo** (mais seguros).

---

## 💻 Exemplos com tipagem explícita

```ts
let numeroA: number = 10;
let numeroB: number = 5;
let numeroC: number = 10;

// Igual (===)
let ehIgual: boolean = numeroA === numeroC;
console.log("numeroA === numeroC:", ehIgual); // true

// Diferente (!==)
let ehDiferente: boolean = numeroA !== numeroB;
console.log("numeroA !== numeroB:", ehDiferente); // true

// Maior que (>)
let maior: boolean = numeroA > numeroB;
console.log("numeroA > numeroB:", maior); // true

// Menor que (<)
let menor: boolean = numeroB < numeroC;
console.log("numeroB < numeroC:", menor); // true

// Maior ou igual (>=)
let maiorOuIgual: boolean = numeroA >= numeroC;
console.log("numeroA >= numeroC:", maiorOuIgual); // true

// Menor ou igual (<=)
let menorOuIgual: boolean = numeroB <= numeroC;
console.log("numeroB <= numeroC:", menorOuIgual); // true
```

---

## 🧪 Exercício simples

### ✏️ Enunciado:

1. Crie duas variáveis `nota1` e `nota2` com valores numéricos.
2. Verifique se as notas são iguais.
3. Verifique se a primeira nota é maior que a segunda.
4. Verifique se a média das duas é maior ou igual a `6`.
5. Mostre os resultados no console.

---

## ✅ O que você aprendeu?

* Operadores de comparação **sempre retornam `true` ou `false`**
* Use `===` e `!==` para comparar **valor e tipo**
* Pode comparar números, strings, booleanos, etc.
