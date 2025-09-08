# 📘 Generics em TypeScript

## ✅ O que são Generics?

* Imagine que você tem uma **função** ou uma **classe** que precisa funcionar com **diferentes tipos de dados**.
* Você poderia criar **uma versão para string**, outra para **number**, outra para **boolean**… mas isso gera **muito código repetitivo**.
* É aí que entram os **Generics**:

👉 Generics são como **“caixas vazias”**.
Você não diz logo de cara se vai usar `string`, `number` ou outro tipo.
Você cria um **molde** que pode se adaptar ao tipo de dado que você passar depois.

💡 Resumindo: Generics servem para escrever **código reutilizável e flexível**.

---

## 1️⃣ Função sem Generics

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

## 2️⃣ Função com Generics

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

## 3️⃣ Generics em Arrays

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

➡️ Muito útil para **listas**, porque o TypeScript mantém o tipo certo automaticamente.

---

## 4️⃣ Restringindo Generics (extends)

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

---

### Outras restrições possíveis

* Tipos específicos:

```ts
function mostraValor<T extends string | number>(valor: T): T {
  return valor;
}

mostraValor("Olá");  // ✅
mostraValor(123);    // ✅
mostraValor(true);   // ❌ não aceito
```

* Implementando interface:

```ts
interface TemNome { nome: string; }

function mostraNome<T extends TemNome>(obj: T): string {
  return obj.nome;
}

mostraNome({ nome: "Ana" });             // ✅ ok
mostraNome({ nome: "João", idade: 20 }); // ✅ ok
mostraNome({ idade: 20 });               // ❌ erro
```

* Extensão de classe:

```ts
class Animal { mover() { console.log("Movendo..."); } }
class Cachorro extends Animal { latir() { console.log("Au au!"); } }

function fazMover<T extends Animal>(animal: T) {
  animal.mover(); // ✅ garantido que existe
}

fazMover(new Animal());   // ✅
fazMover(new Cachorro()); // ✅
fazMover({});             // ❌ erro
```

---

## 5️⃣ Generics em Classes

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

➡️ Uma **classe única** serve para vários tipos diferentes.

---

# 🎒 Estoque Genérico

## 1️⃣ Problema

Imagine criar um **estoque** para produtos diferentes: livros, roupas, brinquedos…

```ts
class EstoqueLivro {
  private livros: Livro[] = [];

  adicionar(livro: Livro) { this.livros.push(livro); }
  listar() { return this.livros; }
}

class EstoqueRoupa {
  private roupas: Roupa[] = [];

  adicionar(roupa: Roupa) { this.roupas.push(roupa); }
  listar() { return this.roupas; }
}
```

❌ Problema: **código duplicado** se tivermos muitos tipos de produtos.

---

## 2️⃣ Solução com Generics

```ts
// Estoque.ts
class Estoque<T> {
  private itens: T[] = [];

  adicionar(item: T): void { this.itens.push(item); }

  listar(): T[] { return this.itens; }

  remover(indice: number): void { this.itens.splice(indice, 1); }
}

export default Estoque;
```

> `<T>` é o **placeholder de tipo** que definimos quando usamos a classe.

---

## 3️⃣ Produtos como classes

```ts
export class Livro {
  descricao: string;
  autor: string;

  constructor(descricao: string, autor: string) {
    this.descricao = descricao;
    this.autor = autor;
  }
}

export class Roupa {
  descricao: string;
  tamanho: string;

  constructor(descricao: string, tamanho: string) {
    this.descricao = descricao;
    this.tamanho = tamanho;
  }
}
```

---

## 4️⃣ Usando o Estoque Genérico

```ts
import Estoque from "./Estoque";
import { Livro, Roupa } from "./Produtos";

// Estoque de livros
const estoqueLivros = new Estoque<Livro>();
estoqueLivros.adicionar(new Livro("Harry Potter", "J.K. Rowling"));
estoqueLivros.adicionar(new Livro("O Hobbit", "Tolkien"));
console.log("📚 Livros no estoque:", estoqueLivros.listar());

// Estoque de roupas
const estoqueRoupas = new Estoque<Roupa>();
estoqueRoupas.adicionar(new Roupa("Camiseta", "M"));
estoqueRoupas.adicionar(new Roupa("Calça Jeans", "42"));
console.log("👕 Roupas no estoque:", estoqueRoupas.listar());
```

✅ Resultado:

* **Uma única classe** para qualquer tipo de produto.
* **Segurança de tipos**: não dá pra misturar livros com roupas.
* Código **mais limpo e reaproveitável**.
