# 📘 O que é uma Classe Abstrata em TypeScript?

## 🧭 Introdução

Em TypeScript (e em POO), uma **classe abstrata** é uma **classe que não pode ser instanciada diretamente**.

Ela serve como **modelo base** para outras classes, **forçando-as a implementar certos métodos ou propriedades**.

> 💡 **Pense em uma classe abstrata como um esqueleto**: ela define a estrutura principal, mas deixa detalhes para as subclasses preencherem.

Classes abstratas em programação são como **modelos** que definem um conjunto de características e comportamentos, mas não podem ser instanciadas diretamente. Elas servem como uma base para outras classes que precisam herdar suas propriedades e métodos.

Pense em uma **fábrica de móveis**. A fábrica pode ter uma classe abstrata chamada `Mobília`, que define características comuns a todos os móveis, como cor, material e métodos como `montar()` e `desmontar()`. No entanto, você não pode criar um objeto da classe `Mobília` diretamente, pois ela não é um móvel específico. Em vez disso, você cria classes concretas, como `Sofa` e `Mesa`, que herdam de `Mobília` e implementam suas particularidades.

### Exemplo:
```ts
// Classe abstrata
abstract class Mobilia {
  protected cor: string;
  protected material: string;

  // Construtor
  constructor(cor: string, material: string) {
    this.cor = cor;
    this.material = material;
  }

  // Método abstrato (sem implementação)
  abstract montar(): void;

  // Método concreto (com implementação)
  desmontar(): void {
    console.log("Desmontando a mobília.");
  }
}

// Classe concreta que herda de Mobilia
class Sofa extends Mobilia {
  constructor(cor: string, material: string) {
    super(cor, material);
  }

  montar(): void {
    console.log(`Montando o sofá de cor ${this.cor} feito de ${this.material}.`);
  }
}

// Classe concreta que herda de Mobilia
class Mesa extends Mobilia {
  constructor(cor: string, material: string) {
    super(cor, material);
  }

  montar(): void {
    console.log(`Montando a mesa de cor ${this.cor} feita de ${this.material}.`);
  }
}

// Código principal (main)
const sofa: Mobilia = new Sofa("azul", "madeira");
const mesa: Mobilia = new Mesa("preta", "metal");

sofa.montar();      // Saída: Montando o sofá de cor azul feito de madeira.
mesa.montar();      // Saída: Montando a mesa de cor preta feita de metal.
sofa.desmontar();   // Saída: Desmontando a mobília.

```

---

## 🧩 Para que serve uma Classe Abstrata?

### 1. **Fornecer uma base comum para outras classes**

Ela define **métodos genéricos** que todas as subclasses devem ter, mas sem precisar implementar tudo nela mesma.

```ts
abstract class Animal {
  nome: string;

  constructor(nome: string) {
    this.nome = nome;
  }

  abstract emitirSom(): void; // método obrigatório, sem implementação
}
```

---

### 2. **Evitar instanciar classes genéricas**

Não faz sentido criar um `Animal` genérico — o certo é criar um `Cachorro`, `Gato`, etc. A classe abstrata **impede instanciar diretamente**:

```ts
const animal = new Animal("Bicho"); 
// ❌ Erro: classes abstratas não podem ser instanciadas
```

---

### 3. **Forçar subclasses a implementar certos comportamentos**

Uma classe abstrata pode definir **métodos abstratos**, que **devem ser implementados** pelas classes filhas.

```ts
class Gato extends Animal {
  emitirSom(): void {
    console.log("Miau");
  }
}
```

Se a classe `Gato` não implementar `emitirSom()`, TypeScript irá apontar erro.

---

## ✅ O que PODE ir em uma classe abstrata?

* Propriedades (com ou sem valor)
* Construtores
* Métodos com implementação
* Métodos abstratos (sem implementação)

```ts
abstract class Veiculo {
  marca: string;

  constructor(marca: string) {
    this.marca = marca;
  }

  buzinar() {
    console.log("Biiiip!");
  }

  abstract acelerar(): void; // cada veículo acelera de forma diferente
}
```

---

## ❌ O que NÃO pode em uma classe abstrata?

* Não pode ser instanciada diretamente (`new ClasseAbstrata()`)
* Não pode **deixar de implementar** métodos abstratos nas subclasses

```ts
const v = new Veiculo("Toyota"); 
// ❌ Erro: não pode instanciar classe abstrata

class Carro extends Veiculo {
  // ❌ Erro: método 'acelerar' não foi implementado
}
```

---

## 🆚 Interface vs Classe Abstrata

### Quando usar Interface e quando usar Classe Abstrata?

| Característica                   | Interface          | Classe Abstrata        |
| -------------------------------- | ------------------ | ---------------------- |
| Pode ter implementação?          | ❌ Não              | ✅ Sim                  |
| Pode ter construtor?             | ❌ Não              | ✅ Sim                  |
| Pode ter propriedades com valor? | ❌ Não              | ✅ Sim                  |
| Pode herdar de múltiplas?        | ✅ Sim (implementa) | ❌ Não (apenas 1)       |
| Pode ser instanciada?            | ❌ Não              | ❌ Não                  |
| Mais adequada para...            | Estrutura/tipos    | Herança + lógica comum |

---

### 📊 Exemplo comparando os dois

#### 📌 Interface:

```ts
interface Animal {
  nome: string;
  emitirSom(): void;
}

class Gato implements Animal {
  nome: string;
  constructor(nome: string) {
    this.nome = nome;
  }

  emitirSom(): void {
    console.log("Miau");
  }
}
```

✅ Boa para contratos
❌ Sem reutilização de código

---

#### 📌 Classe Abstrata:

```ts
abstract class Animal {
  constructor(public nome: string) {}

  mover(): void {
    console.log(`${this.nome} está se movendo`);
  }

  abstract emitirSom(): void;
}

class Cachorro extends Animal {
  emitirSom(): void {
    console.log("Au au!");
  }
}
```

✅ Reutiliza `mover()`
✅ Força `emitirSom()`
❌ Só pode estender uma classe abstrata

---

## ❓ Quando escolher cada um?

### 🟢 Use **interface** quando:

* Você quer **apenas descrever a estrutura** de um objeto ou classe
* Você precisa de **múltiplos contratos** (múltiplas interfaces)
* Você está tipando objetos, funções, APIs, etc.
* Precisa de algo **leve e simples**

### 🔵 Use **classe abstrata** quando:

* Você quer **compartilhar lógica comum** entre classes (métodos com implementação)
* Deseja **forçar implementação** de métodos em subclasses
* Precisa de um **construtor padrão** ou propriedades com lógica inicial
* Quer trabalhar com **herança real e polimorfismo**

---

## Exemplo Prático

```ts
abstract class ContaBancaria {
  titular: string;
  saldo: number;

  constructor(titular: string, saldoInicial: number) {
    this.titular = titular;
    this.saldo = saldoInicial;
  }

  depositar(valor: number): void {
    this.saldo += valor;
  }

  abstract sacar(valor: number): void; // método obrigatório nas subclasses
}
```

```ts
class ContaCorrente extends ContaBancaria {
  sacar(valor: number): void {
    if (valor <= this.saldo) {
      this.saldo -= valor;
    } else {
      console.log("Saldo insuficiente.");
    }
  }
}
```

---

## 🧠 Classes Abstratas e Polimorfismo

Você pode usar o **tipo abstrato como referência**, e criar diferentes tipos de objetos a partir dele:

```ts
let conta: ContaBancaria;

conta = new ContaCorrente("João", 1000);
conta.sacar(200); // funciona como ContaBancaria, mas executa comportamento de ContaCorrente
```

---

## 💡 Dica Final

> Use `interface` quando quiser **descrever a estrutura** de objetos ou classes.
>
> Use `abstract class` quando quiser **compartilhar implementação comum** e **forçar comportamento específico** nas subclasses.

---

## 📝 Exercícios

### 🟢 Exercícios Básicos

1. Crie uma **classe abstrata** `Funcionario` com:

   * Propriedade `nome: string`
   * Método abstrato `calcularSalario(): number`

2. Crie duas subclasses:

   * `FuncionarioCLT` com salário fixo
   * `FuncionarioPJ` com pagamento por hora

3. Instancie objetos de ambas e calcule seus salários.

---

### 🟡 Exercícios Intermediários

4. Crie uma **classe abstrata** `Forma` com:

   * Método abstrato `calcularArea(): number`

5. Crie as classes `Retangulo` e `Triangulo` que estendem `Forma`.

6. Crie um array de `Forma[]` com instâncias de `Retangulo` e `Triangulo`, e use polimorfismo para imprimir as áreas.

---

### 🔴 Desafio

7. Crie uma interface `Autenticavel` com método `autenticar(usuario: string, senha: string): boolean`

8. Crie uma **classe abstrata** `UsuarioSistema` com:

   * Propriedade `nome`
   * Método abstrato `acessarPainel(): void`

9. Crie duas classes:

   * `Administrador` → implementa `UsuarioSistema` e `Autenticavel`
   * `Cliente` → implementa `UsuarioSistema` e `Autenticavel`

10. Faça com que o sistema valide o login e mostre o painel correto.


**Exercício: Clãs de Konoha (Naruto)**

Neste exercício, você vai criar um sistema que representa os clãs de Konoha usando classes abstratas em Java. Cada clã terá suas características e especialidades, mas todos herdarão de uma classe abstrata base chamada `Cla`.

### Requisitos:

1. Crie uma **classe abstrata** chamada `Cla` com os seguintes atributos e métodos:
   - Atributos:
     - `String nomeDoCla`: nome do clã.
     - `String lider`: nome do líder atual do clã.
   - Métodos:
     - `public abstract void habilidadeEspecial()`: método abstrato que descreve a habilidade especial de cada clã.
     - `public void exibirDetalhes()`: método concreto que exibe o nome do clã e o nome do líder.

2. Crie as subclasses que herdam de `Cla`, representando diferentes clãs de Konoha:
   - `ClaUchiha`: Implementa o método `habilidadeEspecial()`, que descreve o *Sharingan* como sua habilidade especial. Seu líder atual é Sasuke.
   - `ClaHyuuga`: Implementa o método `habilidadeEspecial()`, que descreve o *Byakugan* como sua habilidade especial. Seu líder atual é Hiashi.
   - `ClaNara`: Implementa o método `habilidadeEspecial()`, que descreve a manipulação de sombras como sua habilidade especial. Seu líder atual é Shikamaru.
   - `ClaAkimichi`: Implementa o método `habilidadeEspecial()`, que descreve a ampliação corporal como sua habilidade especial. Seu líder atual é Chouza.

3. Crie uma classe principal chamada `Konoha` que contenha o método `main`, onde você:
   - Crie instâncias de cada clã (`ClaUchiha`, `ClaHyuga`, `ClaNara`, `ClaAkimichi`).
   - Chame os métodos `habilidadeEspecial()` e `exibirDetalhes()` para cada clã.

### Tarefas Adicionais:
- Adicione mais clãs com suas habilidades especiais.
- Crie um método adicional em `Cla` chamado `ataqueEspecial()` que cada clã pode personalizar para descrever um ataque exclusivo.
