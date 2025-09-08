# 📘 Generics em TypeScript

## ✅ O que são Generics?

* Imagine que você tem uma **função** ou uma **classe** que precisa funcionar com **diferentes tipos de dados**.
* Você poderia criar **uma versão para string**, outra para **number**, outra para **boolean**… mas isso dá muito trabalho e deixa o código repetitivo.
* É aí que entra o **Generics**:

👉 Generics são como **“caixas vazias”**.
Você não diz logo de cara se vai usar `string`, `number` ou outro tipo.
Você cria um **molde** que pode se adaptar ao tipo de dado que você passar depois.

💡 Resumindo: Generics servem para escrever **código reutilizável e flexível**.

---

## 1. Função sem Generics

```ts
function retornaNumero(item: number): number {
  return item;
}

retornaNumero(10);   // ✅ funciona
retornaNumero("oi"); // ❌ erro, só aceita número
```

🔎 Explicação:

* Aqui a função está **presa ao tipo number**.
* Se quisermos a mesma lógica para `string`, teríamos que duplicar a função:

  ```ts
  function retornaString(item: string): string {
    return item;
  }
  ```

➡️ Isso gera **código duplicado e difícil de manter**.

---

## 2. Função com Generics

```ts
function retornaItem<T>(item: T): T {
  return item;
}

retornaItem<number>(10);     // ✅ retorna um número
retornaItem<string>("oi");   // ✅ retorna uma string
retornaItem<boolean>(true);  // ✅ retorna um boolean
```

🔎 Explicação:

* O `<T>` é um **parâmetro de tipo**.
* Ele diz: *"essa função vai receber algum tipo `T`, e vai devolver o mesmo tipo `T`"*.
* Quando chamamos `retornaItem<number>(10)`, estamos dizendo que o `T` é `number`.
* Quando chamamos `retornaItem<string>("oi")`, o `T` vira `string`.

➡️ Agora temos **uma função só**, que serve para qualquer tipo.

---

## 3. Generics em Arrays

```ts
function pegaPrimeiro<T>(lista: T[]): T {
  return lista[0];
}

const numeros = [1, 2, 3];
const palavras = ["a", "b", "c"];

pegaPrimeiro(numeros);  // 1
pegaPrimeiro(palavras); // "a"
```

🔎 Explicação:

* `T[]` significa "um array de elementos do tipo `T`".
* Se passarmos `number[]`, o `T` será `number`.
* Se passarmos `string[]`, o `T` será `string`.
* A função devolve sempre o **mesmo tipo dos itens do array**.

➡️ Isso é muito útil para **listas**, porque o TypeScript mantém o tipo certo automaticamente.

---

## 4. Restringindo Generics (extends)

Às vezes não queremos aceitar qualquer tipo. No exemplo abaixo, a função só aceita algo que contenha a propriedade length.

```ts
function mostraTamanho<T extends { length: number }>(item: T): number {
  return item.length;
}

mostraTamanho("Oi");        // ✅ funciona (string tem length)
mostraTamanho([1, 2, 3]);   // ✅ funciona (array tem length)
mostraTamanho(123);         // ❌ erro (number não tem length)
```

🔎 Explicação:

* O `extends` significa: *"o T precisa ser algo que tenha um `length`"*.
* Isso limita os tipos que podem ser usados.
* Por isso, `string` e `array` funcionam, mas `number` não.

➡️ Bom para criar funções que só fazem sentido em tipos específicos.


Podemos também restringir a tipos específicos. Você pode dizer, por exemplo, que o T só pode ser string ou number:
```ts
function mostraValor<T extends string | number>(valor: T): T {
  return valor;
}

mostraValor("Olá");  // ✅ string permitido
mostraValor(123);    // ✅ number permitido
mostraValor(true);   // ❌ boolean não é aceito

```

Também podemos aceitar apenas algo que implemente uma interface:

```ts
interface TemNome {
  nome: string;
}

function mostraNome<T extends TemNome>(obj: T): string {
  return obj.nome;
}

mostraNome({ nome: "Ana" });             // ✅ ok
mostraNome({ nome: "João", idade: 20 }); // ✅ ok
mostraNome({ idade: 20 });               // ❌ erro, não tem nome

```

Pode-se também aceitar apenas um objeto que extenda uma classe pai:

```ts
class Animal {
  mover() {
    console.log("Movendo...");
  }
}

class Cachorro extends Animal {
  latir() {
    console.log("Au au!");
  }
}

function fazMover<T extends Animal>(animal: T) {
  animal.mover(); // ✅ garantido que existe
}

fazMover(new Animal());   // ✅
fazMover(new Cachorro()); // ✅
fazMover({});             // ❌ erro

```

Dá ainda para limitar a valores específicos:

```ts
function corEscolhida<T extends "vermelho" | "azul" | "verde">(cor: T): T {
  return cor;
}

corEscolhida("vermelho"); // ✅
corEscolhida("azul");     // ✅
corEscolhida("preto");    // ❌ não permitido

```

E por último, pode-se ter mais de uma restrição:

````ts
interface Identificavel {
  id: number;
}

interface Nomeavel {
  nome: string;
}

function mostraInfo<T extends Identificavel & Nomeavel>(obj: T) {
  console.log(obj.id, obj.nome);
}

mostraInfo({ id: 1, nome: "Ana" }); // ✅ funciona
mostraInfo({ id: 1 });              // ❌ falta nome

```


---

## 5. Generics em Interfaces

```ts
interface RespostaAPI<T> {
  data: T;
  sucesso: boolean;
}

type Usuario = { id: number; nome: string };

const respostaUsuario: RespostaAPI<Usuario> = {
  data: { id: 1, nome: "Ana" },
  sucesso: true,
};

const respostaNumeros: RespostaAPI<number[]> = {
  data: [10, 20, 30],
  sucesso: true,
};
```

🔎 Explicação:

* A interface `RespostaAPI<T>` tem um `data` que pode ser de qualquer tipo `T`.
* Quando usamos `RespostaAPI<Usuario>`, o `T` vira `Usuario`.
* Quando usamos `RespostaAPI<number[]>`, o `T` vira `number[]`.

➡️ Isso é **muito usado em sistemas reais**, porque uma resposta de API pode trazer dados de vários tipos.

---

## 6. Generics em Classes

```ts
class Caixa<T> {
  conteudo: T;

  constructor(item: T) {
    this.conteudo = item;
  }

  pegar(): T {
    return this.conteudo;
  }
}

const caixaDeString = new Caixa<string>("Oi");
console.log(caixaDeString.pegar()); // "Oi"

const caixaDeNumero = new Caixa<number>(123);
console.log(caixaDeNumero.pegar()); // 123
```

🔎 Explicação:

* A classe `Caixa<T>` é uma **caixa que pode guardar qualquer tipo**.
* Quando criamos `Caixa<string>`, só podemos guardar `string`.
* Quando criamos `Caixa<number>`, só podemos guardar `number`.

➡️ Assim criamos **uma classe única** que serve para vários tipos diferentes.

---

# 🚀 Resumindo

* **Generics** = "caixa vazia" para tipos.
* Usamos quando queremos código **flexível e reaproveitável**.
* Principais usos:

  1. Funções genéricas (`retornaItem<T>`)
  2. Arrays genéricos (`T[]`)
  3. Restrições (`extends`)
  4. Interfaces genéricas (`RespostaAPI<T>`)
  5. Classes genéricas (`Caixa<T>`)

---

# 🎒 Estoque Genérico

## 1️⃣ Problema

Imagine que você precisa criar um **estoque** para armazenar produtos diferentes: livros, roupas, brinquedos…

Você poderia criar **uma classe para cada tipo de produto**, algo assim:

```ts
// EstoqueLivro.ts
class EstoqueLivro {
  private livros: Livro[] = [];

  adicionar(livro: Livro) { this.livros.push(livro); }
  listar() { return this.livros; }
}

// EstoqueRoupa.ts
class EstoqueRoupa {
  private roupas: Roupa[] = [];

  adicionar(roupa: Roupa) { this.roupas.push(roupa); }
  listar() { return this.roupas; }
}
```

❌ Problema: se tivermos 10 tipos de produtos, teremos 10 classes praticamente iguais!
Isso gera **muito código duplicado** e torna a manutenção difícil.

---

## 2️⃣ Pergunta

💡 Como podemos criar **uma única classe de estoque** que funcione para qualquer tipo de produto, sem repetir código e ainda garantindo **segurança de tipos**?

---

## 3️⃣ Solução com Generics

A resposta é: **usando Generics** em TypeScript.

Generics permitem criar **uma classe “genérica”**, que vai funcionar para qualquer tipo de dado, mas ainda assim mantendo **a tipagem correta**.

---

## 4️⃣ Classe Estoque Genérica

```ts
// Estoque.ts
class Estoque<T> {
  private itens: T[] = [];

  // Adiciona qualquer item do tipo T
  adicionar(item: T): void {
    this.itens.push(item);
  }

  // Retorna todos os itens
  listar(): T[] {
    return this.itens;
  }

  // Remove um item pelo índice
  remover(indice: number): void {
    this.itens.splice(indice, 1);
  }
}

export default Estoque;
```

> Aqui, o `<T>` é o **placeholder de tipo**. Quando usamos a classe, escolhemos o tipo real: `Livro`, `Roupa`, etc.

---

## 5️⃣ Tipos de Produtos

```ts
// Tipos.ts
export type Livro = {
  titulo: string;
  autor: string;
};

export type Roupa = {
  tipo: string;
  tamanho: string;
};
```

---

## 6️⃣ Usando o Estoque Genérico

```ts
// index.ts
import Estoque from "./Estoque";
import { Livro, Roupa } from "./Tipos";

// Estoque de livros
const estoqueLivros = new Estoque<Livro>();
estoqueLivros.adicionar({ titulo: "Harry Potter", autor: "J.K. Rowling" });
estoqueLivros.adicionar({ titulo: "O Hobbit", autor: "Tolkien" });

console.log("📚 Livros no estoque:", estoqueLivros.listar());

// Estoque de roupas
const estoqueRoupas = new Estoque<Roupa>();
estoqueRoupas.adicionar({ tipo: "Camiseta", tamanho: "M" });
estoqueRoupas.adicionar({ tipo: "Calça Jeans", tamanho: "42" });

console.log("👕 Roupas no estoque:", estoqueRoupas.listar());
```

✅ Resultado:

* Uma **única classe de estoque** para qualquer tipo.
* **Segurança de tipos**: não dá pra adicionar uma roupa no estoque de livros.
* Código **mais limpo e reaproveitável**.

---


