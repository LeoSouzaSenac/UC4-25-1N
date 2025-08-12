# Introdução à Programação Orientada a Objetos (POO) em TypeScript

## O que é Programação Orientada a Objetos?

Programação Orientada a Objetos (POO) é um paradigma de programação que organiza o código em **objetos** que representam entidades do mundo real ou conceitos abstratos. Cada objeto é uma instância de uma **classe** e combina dados (atributos) e comportamentos (métodos).

Em vez de pensar em dados e funções separadamente, na POO você modela coisas do mundo real em código, agrupando suas características e ações.

---

## Conceitos Fundamentais

### Classe

* Uma **classe** é como uma "planta" ou "molde" que define a estrutura e o comportamento de objetos.
* Ela descreve **quais dados** o objeto terá (atributos) e **o que ele poderá fazer** (métodos).
* Uma classe é um conceito abstrato, ou seja, você não pode usá-la diretamente — precisa criar objetos (instâncias) dela.

### Objeto

* Um **objeto** é uma instância concreta de uma classe.
* É o “item” criado a partir do molde, com seus próprios valores nos atributos.
* Objetos interagem entre si através de seus métodos.

---

## Como criar classes e objetos em TypeScript

```typescript
// Definição da classe
class Pessoa {
  nome: string;
  idade: number;

  constructor(nome: string, idade: number) {
    this.nome = nome;
    this.idade = idade;
  }

  apresentar(): string {
    return `Olá, meu nome é ${this.nome} e tenho ${this.idade} anos.`;
  }
}

// Criando um objeto a partir da classe
const pessoa1 = new Pessoa("Ana", 25);

console.log(pessoa1.apresentar()); // Olá, meu nome é Ana e tenho 25 anos.
```

* `constructor` é um método especial que é chamado quando criamos um novo objeto, para inicializar seus atributos.
* `this` refere-se ao próprio objeto que está sendo criado.

---

## Propriedades e Métodos

* **Propriedades** são variáveis dentro da classe que guardam dados.
* **Métodos** são funções que definem comportamentos que os objetos da classe podem executar.

---

## Encapsulamento: controlar o acesso a dados

Em TypeScript, você pode usar **modificadores de acesso** para controlar quem pode acessar propriedades e métodos:

* `public` (padrão): acessível de qualquer lugar.
* `private`: acessível somente dentro da própria classe.
* `protected`: acessível na própria classe e em classes que herdam dela.

Exemplo:

```typescript
class ContaBancaria {
  private saldo: number;

  constructor(saldoInicial: number) {
    this.saldo = saldoInicial;
  }

  depositar(valor: number): void {
    if (valor > 0) {
      this.saldo += valor;
    }
  }

  obterSaldo(): number {
    return this.saldo;
  }
}

const conta = new ContaBancaria(1000);
conta.depositar(500);
console.log(conta.obterSaldo()); // 1500
// conta.saldo = 0; // Erro: saldo é privado e não pode ser acessado aqui
```

---

## Exercícios Criativos de Programação Orientada a Objetos em TypeScript

### 1. Sistema de Personagens de RPG

Crie uma classe `Personagem` que tenha atributos como `nome`, `classe` (guerreiro, mago, arqueiro, etc), `vida` e `força`.
Implemente métodos para:

* `atacar(outroPersonagem: Personagem)`: diminui a vida do personagem atacado de acordo com a força do atacante.
* `curar(valor: number)`: aumenta a vida do personagem, mas nunca ultrapassa um máximo (defina um limite).

Depois, crie pelo menos 3 personagens diferentes e simule uma pequena batalha entre eles, exibindo o status dos personagens após cada ataque.

---

### 2. Biblioteca de Livros

Crie uma classe `Livro` com propriedades `titulo`, `autor`, `anoPublicacao` e `emprestado` (booleano).
Implemente métodos para:

* `emprestar()`: marca o livro como emprestado, mas só se ele não estiver emprestado.
* `devolver()`: marca o livro como disponível.
* `mostrarInfo()`: exibe todas as informações do livro e se está disponível.

Depois, crie uma classe `Biblioteca` que gerencia uma coleção de livros, com métodos para:

* `adicionarLivro(livro: Livro)`
* `emprestarLivro(titulo: string)`
* `devolverLivro(titulo: string)`
* `listarLivrosDisponiveis()`

Teste criando uma biblioteca, adicionando livros e realizando operações de empréstimo e devolução.

---

### 3. Controle de Tráfego de Veículos

Crie uma classe abstrata `Veiculo` com propriedades comuns como `marca`, `modelo`, `ano`, e método abstrato `mover()`.

Crie classes que estendem `Veiculo`:

* `Carro`: implementa o método `mover()` mostrando uma mensagem que o carro está dirigindo.
* `Bicicleta`: implementa o método `mover()` mostrando uma mensagem que a bicicleta está pedalando.

Depois, crie um array que armazena veículos diferentes e chame o método `mover()` para cada um, demonstrando polimorfismo.

---

### 4. Cadastro de Usuários com Regras de Validação

Crie uma classe `Usuario` com atributos `nome`, `email`, `senha`.
Implemente:

* Validação no construtor para garantir que o email tenha um formato válido (exemplo simples: contém `@`).
* Um método `alterarSenha(senhaAntiga: string, novaSenha: string)` que só altera a senha se a senha antiga for correta.
* Um método `exibirPerfil()` que retorna uma string com nome e email (não deve mostrar a senha).

Teste criando usuários e validando as regras.
