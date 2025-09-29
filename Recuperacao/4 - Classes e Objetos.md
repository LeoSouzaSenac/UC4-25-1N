## 🧱 O que é uma **classe**?

Uma **classe** é como um **molde** (modelo) para criar objetos.

> Exemplo: imagine uma **classe Carro**. Ela define como um carro deve ser — com cor, modelo, velocidade, etc.
> Depois, podemos **criar vários carros diferentes** a partir desse molde.

---

## 📦 O que são **atributos**?

Os **atributos** são as **características** do objeto.
No caso do carro: `cor`, `modelo`, `velocidade`...

São como **variáveis dentro da classe**.

---

## 🧱 O que é o **construtor**?

O **construtor** é uma função especial que **roda automaticamente** quando a gente **cria (instancia) um objeto**.

Serve para **inicializar os atributos**.

---

## ⚙️ O que são **métodos**?

São as **ações** que o objeto pode fazer.
São como **funções dentro da classe**.

Exemplo: `acelerar()`, `frear()`, `mostrarInfo()`...

---

## ✅ Exemplo completo com `export`

### 📁 Arquivo: `Carro.ts`

```ts
// Exportando a classe para poder usar em outro lugar
export class Carro {
  // Atributos
  cor: string;
  modelo: string;
  velocidade: number;

  // Construtor: inicializa os atributos
  constructor(cor: string, modelo: string) {
    this.cor = cor;
    this.modelo = modelo;
    this.velocidade = 0; // começa parado
  }

  // Método: mostra as informações do carro
  mostrarInfo(): void {
    console.log(`Modelo: ${this.modelo}, Cor: ${this.cor}, Velocidade: ${this.velocidade}km/h`);
  }

  // Método: acelera o carro
  acelerar(): void {
    this.velocidade += 10;
    console.log(`${this.modelo} acelerou para ${this.velocidade}km/h`);
  }

  // Método: freia o carro
  frear(): void {
    this.velocidade -= 5;
    if (this.velocidade < 0) {
      this.velocidade = 0;
    }
    console.log(`${this.modelo} freou para ${this.velocidade}km/h`);
  }
}
```

---

## 🧪 Como instanciar (criar) um objeto?

### 📁 Arquivo: `index.ts`

```ts
import { Carro } from "./Carro";

// Criando (instanciando) um objeto da classe Carro
let meuCarro: Carro = new Carro("vermelho", "Fusca");

// Chamando métodos
meuCarro.mostrarInfo();    // Mostra info do carro
meuCarro.acelerar();       // Acelera
meuCarro.acelerar();       // Acelera mais
meuCarro.frear();          // Freia
meuCarro.mostrarInfo();    // Mostra info atualizada
```
---

## 📝 **Exercício: Criando uma classe Aluno**

### 🎯 Objetivo:

Criar uma classe chamada `Aluno` que representa um estudante, com seus dados e comportamentos.

---

### 📋 Enunciado:

1. Crie uma **classe** chamada `Aluno` (com `export`) que tenha os seguintes **atributos**:

   * `nome` (string)
   * `idade` (number)
   * `nota1` (number)
   * `nota2` (number)

2. Crie um **construtor** que receba `nome`, `idade`, `nota1` e `nota2` como parâmetros e inicialize os atributos.

3. Crie os seguintes **métodos**:

   * `calcularMedia()`: deve retornar a **média** entre `nota1` e `nota2`.
   * `verificarAprovacao()`: deve retornar uma **mensagem** indicando se o aluno foi aprovado ou reprovado (média maior ou igual a 6). Use if/else para verificar se o valuno está aprovado ou reprovado.

4. No arquivo `main.ts`, instancie 2 objetos da classe `Aluno` com dados diferentes, ou seja, crie dois alunos, e chame os métodos `calcularMedia()` e `verificarAprovacao()` para cada um.

---

### ✅ Exemplo de saída esperada no console:

```
Aluno: Ana
Média: 7.5
Situação: Aprovado

Aluno: João
Média: 5
Situação: Reprovado
```

---

## ✅ O que você aprendeu?

* **Classe** = modelo para criar objetos
* **Atributos** = características do objeto
* **Construtor** = função que roda ao criar o objeto
* **Métodos** = ações que o objeto pode fazer
* Como **instanciar** (criar) objetos com `new`
* Como **usar `export`** para reutilizar a classe em outros arquivos
