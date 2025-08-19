# Modificador `protected` em TypeScript

## O que é `protected`?

Em **TypeScript**, o modificador `protected` é usado em **Propriedades** e **Métodos** de uma classe. Ele funciona de forma intermediária entre `private` e `public`:

- **public** → acessível de qualquer lugar.
- **private** → acessível **somente dentro da própria classe**.
- **protected** → acessível **dentro da própria classe e em classes que herdam dela**.

Ou seja, `protected` permite **herança segura**, permitindo que subclasses utilizem os membros da classe pai sem expô-los publicamente.

---

## Sintaxe

```typescript
class Animal {
    protected nome: string;

    constructor(nome: string) {
        this.nome = nome;
    }

    protected fazerSom(): void {
        console.log(`${this.nome} está fazendo um som.`);
    }
}

class Cachorro extends Animal {
    latir() {
        console.log(`${this.nome} está latindo.`); // Acesso permitido porque é protected
        this.fazerSom(); // Também permitido
    }
}

const dog = new Cachorro("Rex");
dog.latir();          // Funciona
// dog.nome;          // ERRO! Não é permitido acessar fora da classe ou herança
// dog.fazerSom();    // ERRO! Não é permitido acessar fora da classe ou herança
````

---

## Diferença entre `protected` e `private`

| Modificador | Acesso dentro da classe | Acesso fora da classe | Acesso em subclasses |
| ----------- | ----------------------- | --------------------- | -------------------- |
| public      | ✅                       | ✅                     | ✅                    |
| private     | ✅                       | ❌                     | ❌                    |
| protected   | ✅                       | ❌                     | ✅                    |

**Resumo:**
`protected` é útil quando você quer **proteger informações** da classe para que **só subclasses possam acessar**, sem permitir que qualquer código externo interfira diretamente.

---

## Exemplo prático

Imagine que estamos criando um jogo com personagens:

```typescript
export class Personagem {
    protected vida: number;

    constructor(vida: number) {
        this.vida = vida;
    }

    protected sofrerDano(valor: number) {
        this.vida -= valor;
        console.log(`Vida atual: ${this.vida}`);
    }
}

export class Guerreiro extends Personagem {
    constructor(vida: number){
      supor(vida)
    }
    atacar(inimigo: Personagem) {
        console.log("Atacando inimigo...");
        
        inimigo.sofrerDano(10); // Permite chamar método protected
    }
}

const heroi = new Guerreiro(100);
const vilao = new Guerreiro(80);

heroi.atacar(vilao);
// vilao.sofrerDano(5); // ❌ ERRO: método protected não acessível fora da classe ou subclasses
```

---

## Exercícios para praticar

1. Crie uma classe `Veiculo` com uma propriedade `protected velocidade`.
   Crie uma subclasse `Carro` que possa acessar e modificar `velocidade` através de um método chamado `acelerar`.
   Instancie o objeto Carro e chame o método `acelerar`.

2. Crie uma classe `ContaBancaria` com um saldo `protected`. Dentro desta classe, crie também um método `atualizarSaldo` que deve ser protected (sim, podemos encapsular métodos também).
   Este método deve receber um valor como parâmetro e acrescenta este valor ao atributo `saldo`.
   Crie depois uma subclasse `ContaPoupanca` e, nela, crie um método público chamado `aplicarJuros`.
   Em index, instancie ContaPoupanca e tente acessar os dois métodos para ver o que acontece.
   Tente acessar o saldo diretamente fora das classes e veja o que acontece.

---

> **Dica:**
> Use `protected` sempre que você quer **esconder informações do mundo externo**, mas ainda permitir que **classes derivadas manipulem esses dados**. Isso ajuda a manter o **encapsulamento**, que é um dos pilares da POO.
