# Prova UC4 T

## Questões Objetivas

<details>
<summary>1. O encapsulamento é alcançado usando:</summary>

- A) Modificadores de acesso como `private`, `public` e `protected`.  
- B) Métodos getters e setters.  
- C) Classes e objetos.  
- D) Todas as opções acima.  
</details>

<details>
<summary>2. Qual é a maneira correta de definir uma classe filha que herda propriedades e métodos de uma classe pai?</summary>

- A) Usando a palavra-chave `implements` na declaração da classe filha.  
- B) Usando a palavra-chave `inherits`.  
- C) Usando a palavra-chave `extends` na declaração da classe filha.  
- D) Usando a palavra-chave `interface`.  
</details>

<details>
<summary>3. As interfaces são usadas para:</summary>

- A) Executar código em tempo de execução.  
- B) Controlar o fluxo de um programa.  
- C) Definir estruturas de dados e contratos para objetos.  
- D) Armazenar dados em arrays.  
</details>

<details>
<summary>4. O polimorfismo refere-se a:</summary>

- A) Um tipo de encapsulamento.  
- B) A capacidade de uma classe ter múltiplos métodos com o mesmo nome, mas com diferentes implementações.  
- C) Uma técnica de depuração.  
- D) Um tipo de herança múltipla.  
</details>

<details>
<summary>5. Qual é a diferença fundamental entre herança de classes e implementação de interfaces?</summary>

- A) Herança de classes permite a reutilização de código, enquanto interfaces não.  
- B) Interfaces permitem a reutilização de código, enquanto herança não.  
- C) Ambas são iguais.  
- D) Interfaces podem conter lógica, herança não.  
</details>

<details>
<summary>6. A estrutura de dados mais adequada para implementar um sistema de gerenciamento de tarefas em um aplicativo de lista de afazeres, onde as tarefas são adicionadas no final, removidas do início e processadas na ordem em que foram adicionadas, é:</summary>

- A) Pilha.  
- B) Lista ligada.  
- C) Fila.  
- D) Conjunto.  
</details>

<details>
<summary>7. Qual é a vantagem de usar getters e setters em classes?</summary>

- A) Eles facilitam a manipulação de dados privados.  
- B) Eles evitam a criação de objetos.  
- C) Eles eliminam a necessidade de construtores.  
- D) Eles são mais rápidos que acessar propriedades diretamente.  
</details>

<details>
<summary>8. O que é um construtor em uma classe?</summary>

- A) Um método usado para criar instâncias da classe.  
- B) Um método que só pode ser usado internamente.  
- C) Um método especial que é automaticamente invocado quando uma instância da classe é criada.  
- D) A e C estão corretas.  
</details>

<details>
<summary>9. Como enumeradores são definidos e qual sua finalidade?</summary>

- A) Enumeradores são definidos usando a palavra-chave `enum` e são usados para representar um conjunto de valores nomeados.  
- B) Enumeradores são usados apenas para criar objetos.  
- C) Enumeradores são tipos especiais de funções.  
- D) Enumeradores não existem em TypeScript.  
</details>

<details>
<summary>10. Como TypeScript lida com a visibilidade de membros (public, private, protected) em classes?</summary>

- A) TypeScript ignora completamente as palavras-chave de visibilidade.  
- B) TypeScript respeita as palavras-chave de visibilidade e impõe restrições de acesso conforme especificado.  
- C) Todas as propriedades são públicas por padrão e não podem ser modificadas.  
- D) A visibilidade é controlada apenas no tempo de execução.  
</details>


## Questões de Interpretação de Código

<details>
<summary>1. Encapsulamento - Considere o seguinte código:</summary>

```typescript
class Person {
    private name: string;
    constructor(name: string) {
        this.name = name;
    }
    getName(): string {
        return this.name;
    }
}

const person = new Person("John");
console.log(person.name);
````

O que será impresso no console? Haverá algum erro? Se sim, como você poderia corrigi-lo?

</details>

<details>
<summary>2. Herança - Considere o seguinte código:</summary>

```typescript
class Animal {
    sound: string;

    constructor(sound: string) {
        this.sound = sound;
    }

    makeSound() {
        console.log(this.sound);
    }
}

class Dog extends Animal {
    breed: string;

    constructor(breed: string) {
        super("Woof!");
        this.breed = breed;
    }

    displayInfo() {
        console.log(`This dog is a ${this.breed} breed.`);
    }
}

class GoldenRetriever extends Dog {
    constructor() {
        super("Golden Retriever");
    }

    fetch() {
        console.log("Fetching...");
    }
}

const golden = new GoldenRetriever();
golden.makeSound();
golden.displayInfo();
golden.fetch();
```

O que será impresso no console?

</details>

<details>
<summary>3. Polimorfismo - Considere o seguinte código:</summary>

```typescript
class Shape {
    draw(): void {
        console.log("Desenhando forma...");
    }
}

class Circle extends Shape {
    draw(): void {
        console.log("Desenhando círculo...");
    }

    calculateArea(): void {
        console.log("Calculando área do círculo...");
    }
}

class Square {
    draw(): void {
        console.log("Desenhando quadrado...");
    }
}

function drawShapes(shapes: Shape[]): void {
    shapes.forEach(shape => {
        shape.draw();
    });
}

const circle = new Circle();
const square = new Square();

const shapes: Shape[] = [circle, square];

drawShapes(shapes);
```

O que acontecerá neste código? Ocorrerá algum erro? Se sim, qual?

</details>

<details>
<summary>4. Interfaces - Considere o seguinte código:</summary>

```typescript
interface Calculator {
    add(a: number): number {
        return a + 10;
    }
}

class BasicCalculator implements Calculator {
    add(a: number): number {
        return a + 10;
    }
}

const calculator: Calculator = new BasicCalculator();
const result = calculator.add(5, 7);
console.log(result);
```

O que acontecerá neste código? Ocorrerão erros? Se sim, quais?

</details>

<details>
<summary>5. Enumeradores - Considere o seguinte código:</summary>

```typescript
enum DayOfWeek {
    Monday = 1,
    Tuesday = 2,
    Wednesday = 3,
    Thursday = 4,
    Friday = 5,
    Saturday = 6,
    Sunday = 7
}

function getNextDay(day: DayOfWeek): DayOfWeek {
    if (day === DayOfWeek.Sunday) {
        return DayOfWeek.Monday;
    } else {
        return day + 1;
    }
}

const currentDay: DayOfWeek = DayOfWeek.Wednesday;
const nextDay: DayOfWeek = getNextDay(currentDay);
console.log("Next day:", nextDay);
```

O que será mostrado no console?

</details>
```

---


