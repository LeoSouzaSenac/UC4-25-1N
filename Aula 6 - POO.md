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
export class Pessoa {
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
* a palavra `export` serve para exportar a classe, para que possamos usá-la em outras partes do nosso projeto.
* `constructor` é um método especial que é chamado quando criamos um novo objeto, para inicializar seus atributos.
* `this` refere-se ao próprio objeto que está sendo criado.

---

## Propriedades e Métodos

* **Propriedades** são variáveis dentro da classe que guardam dados.
* **Métodos** são funções que definem comportamentos que os objetos da classe podem executar.

---

## Encapsulamento: controlando o acesso aos dados

Na Programação Orientada a Objetos, **encapsulamento** significa proteger o acesso direto aos atributos de um objeto, controlando como eles são lidos ou alterados. No caso, normalmente, encapsulamos os atributos (não os deixamos public) 

Em TypeScript, usamos **modificadores de acesso** para definir a visibilidade:

* `public` (padrão) → acessível de qualquer lugar.
* `private` → acessível **somente dentro da própria classe**.
* `protected` → acessível dentro da própria classe e em classes que herdam dela.

Quando usamos `private`, **não podemos acessar o atributo diretamente de fora da classe**.
Isso é intencional: serve para proteger os dados contra alterações inesperadas e manter a integridade do objeto. 
Por exemplo, se antes podíamos acessar/trocar o valor de um atributo assim:
´´´ts
objeto.nome = "Leonardo" // trocando
console.log(objeto.nome) // acessando
´´´

Agora, com o encapsulamento, só podemos acessá-lo/trocá-lo usando os métodos getters/setters:
´´´ts
objeto.setNome("Leonardo") // trocando
console.log(objeto.getNome) // acessando
´´´
 
Se o setter não tiver regras, realmente não adianta muito. A vantagem é justamente poder colocar lógica para impedir valores errados, avisar sobre alterações ou até calcular algo antes de retornar/alterar o valor.

---

### Por que precisamos de *getters* e *setters*?

Se um atributo é `private`, mas ainda precisamos **ler** ou **alterar** seu valor de forma controlada, usamos:

* **Getter** → um método que retorna o valor do atributo privado.
* **Setter** → um método que altera o valor do atributo privado, possivelmente com validações.

Usamos getters e setters para:

1. **Proteger dados sensíveis** (por exemplo, impedir que o saldo de uma conta seja alterado sem validação).
2. **Executar validações** antes de mudar um valor (por exemplo, não permitir idade negativa).
3. **Manter a flexibilidade do código** (podemos mudar a lógica interna sem alterar o resto do programa).

---

### Exemplo com Getter e Setter

```typescript
class ContaBancaria {
  private saldo: number;

  constructor(saldoInicial: number) {
    this.saldo = saldoInicial;
  }

  // Getter - permite ler o saldo
  getSaldo(): number {
    return this.saldo;
  }

  // Setter - permite modificar o saldo com validação
  setSaldo(valor: number): void {
    if (valor >= 0) {
      this.saldo = valor;
    } else {
      console.log("Erro: saldo não pode ser negativo.");
    }
  }
}

const conta = new ContaBancaria(1000);

// Ler usando getter
console.log(conta.getSaldo()); // 1000

// Alterar usando setter
conta.setSaldo(1500);
console.log(conta.getSaldo()); // 1500

// Tentativa inválida
conta.setSaldo(-200); // Erro: saldo não pode ser negativo
```

> 💡 **Resumo**: `private` evita acesso direto, mas getters e setters nos permitem acessar/modificar o dado de forma **segura e controlada**.

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
