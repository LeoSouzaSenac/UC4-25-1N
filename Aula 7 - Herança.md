# Herança em TypeScript


## 1. 📌 O que é Herança?
**Herança** é o mecanismo que permite criar novas classes (subclasses) a partir de uma classe já existente (superclasse).
Basicamente, temos uma classe "pai" que, a partir dela, temos classes "filhas", que herdam características dela.

- **Superclasse (pai):** contém atributos e métodos comuns.  
- **Subclasse (filho):** herda tudo da superclasse e pode adicionar seus próprios comportamentos.  

👉 Isso evita **duplicação de código** e melhora a **organização**.

---

## 2. 📝 Estrutura de Arquivos

Vamos criar as seguintes classes:

```

src/
├── Animal.ts
├── Mamifero.ts
├── Reptil.ts
└── index.ts   (arquivo principal para testes)

````

---

## 3. 🐾 Código das Classes

### 📄 Animal.ts
```ts
// Classe base (superclasse)
export class Animal {
  nome: string;
  idade: number;

  constructor(nome: string, idade: number) {
    this.nome = nome;
    this.idade = idade;
  }

  mover(): void {
    console.log(`${this.nome} está se movendo...`);
  }
}
````

---

### 📄 Mamifero.ts

```ts
import { Animal } from "./Animal";

// Subclasse Mamífero
export class Mamifero extends Animal {
  temPelos: boolean;

  constructor(nome: string, idade: number, temPelos: boolean) {
    super(nome, idade); // chama o construtor da classe pai
    this.temPelos = temPelos;
  }

  amamentar(): void {
    console.log(`${this.nome} está amamentando seus filhotes.`);
  }
}
```

---

### 📄 Reptil.ts

```ts
import { Animal } from "./Animal";

// Subclasse Réptil
export class Reptil extends Animal {
  tipoEscama: string;

  constructor(nome: string, idade: number, tipoEscama: string) {
    super(nome, idade);
    this.tipoEscama = tipoEscama;
  }

  botarOvo(): void {
    console.log(`${this.nome} botou um ovo.`);
  }
}
```

---

### 📄 index.ts

```ts
import { Mamifero } from "./Mamifero";
import { Reptil } from "./Reptil";

// Criando objetos
const cachorro = new Mamifero("Rex", 5, true);
const cobra = new Reptil("Naja", 2, "escamas lisas");

cachorro.mover();      // herdado da classe Animal
cachorro.amamentar();  // método da classe Mamifero

cobra.mover();         // herdado da classe Animal
cobra.botarOvo();      // método da classe Reptil
```

---

## 4. 🚀 O que aprendemos?

* Criamos uma **superclasse Animal** com atributos e métodos comuns.
* Criamos subclasses (`Mamifero` e `Reptil`) que **herdam** de `Animal`.
* Cada subclasse adicionou **comportamentos próprios**.

---

## 5. 🎯 Exercícios

### 📝 Exercício 1: Criando novas subclasses

* Crie uma subclasse `Ave` que herda de `Animal`.
* Adicione um método `voar()`.
* Teste no `index.ts` criando um objeto `papagaio`.

---

### 📝 Exercício 2: Expansão dos Mamíferos

* Na classe `Mamifero`, adicione um método `emitirSom()`.
* Crie um objeto `gato` que emite `"Miau"`.
* Crie um objeto `cachorro` que emite `"Au au"`.

---

### 📝 Exercício 3: Generalização

* Crie um array `animais: Animal[]`.
* Adicione dentro dele instâncias de `Mamifero`, `Reptil` e `Ave`.
* Percorra o array e chame o método `mover()` de cada objeto.
* Observe que **todos têm o mesmo método**, mas pertencem a classes diferentes.

---

## 📚 Resumo

* **Herança** = reutilizar código criando uma hierarquia de classes.
* Em TypeScript usamos `extends` para indicar que uma classe herda de outra.
* Subclasses herdam atributos/métodos da superclasse, mas também podem ter **novos comportamentos**.

---

Quer que eu também prepare uma **versão com gabarito dos exercícios** (as classes `Ave`, `Gato`, `Cachorro` já implementadas), ou você prefere deixar apenas a lista para seus alunos resolverem?
```
