# 📘 O que é uma Interface em TypeScript?

## 🧭 Introdução

Em TypeScript, uma **interface** é uma ferramenta usada para **descrever a forma que um objeto deve ter**.

Ela define:

* **Quais propriedades** o objeto deve conter
* **Quais tipos** essas propriedades devem ter
* **Quais métodos** devem existir (se necessário)

⚠️ **Interfaces não contêm lógica ou implementação**, apenas a **descrição do que deve existir**.

---

## 🧩 Para que serve uma Interface?

### 1. **Definir contratos de estrutura**

Você pode pensar em uma interface como um **contrato**: qualquer objeto que "assine esse contrato" deve obedecer a ele **exatamente**.

✅ **Exemplo:**

```ts
// Interface definindo a estrutura de um objeto do tipo Usuario
interface Usuario {
  nome: string;   // deve ter uma propriedade 'nome' do tipo string
  idade: number;  // deve ter uma propriedade 'idade' do tipo number
}

// Criando um objeto que segue exatamente o formato da interface
const usuario: Usuario = {
  nome: "Maria",
  idade: 28
};
```

🛑 Se faltar alguma propriedade, ou se o tipo estiver errado, TypeScript irá reclamar:

```ts
const usuarioInvalido: Usuario = {
  nome: "Carlos"
  // Erro: Está faltando a propriedade 'idade'
};
```

---

### 2. **Autocomplete e validação de tipos nos editores**

Interfaces ajudam o editor (como VS Code) a sugerir os campos certos e evitar erros:

```ts
console.log(usuario.nome); 
// Ao digitar "usuario.", o VS Code sugere "nome" e "idade"
// Isso acontece porque o TS sabe o formato esperado
```

---

### 3. **Facilitam a manutenção e compreensão do código**

Ao definir a interface de um objeto, todo o time sabe o que aquele objeto deve conter.

```ts
interface Produto {
  nome: string;
  preco: number;
}

function mostrarPreco(produto: Produto) {
  console.log(`${produto.nome} custa R$${produto.preco}`);
}
```

➡️ Mesmo sem ver a implementação da função, a interface `Produto` deixa claro o que ela espera.

---

### 4. **Ajudam a evitar erros comuns**

Se você tentar atribuir um tipo errado, o TypeScript alerta antes mesmo do código rodar.

```ts
interface Config {
  modoEscuro: boolean;
}

const config: Config = {
  modoEscuro: "sim" // ❌ Erro: o valor deve ser um boolean (true ou false)
};
```

---

## ✅ O que PODE ir em uma interface?

* Propriedades (obrigatórias ou opcionais)
* Métodos (apenas a **assinatura**, sem implementação)

```ts
interface Pessoa {
  nome: string;
  idade: number;

  falar(): void; // método que deve existir, sem lógica
}
```

---

## ❌ O que NÃO vai em uma interface?

* Implementação de métodos (nada de lógica)
* Modificadores como `private` ou `protected`
* Instâncias ou construtores

```ts
interface Animal {
  emitirSom(): void; // OK: assinatura
  // emitirSom() { console.log("som"); } ❌ ERRADO: não pode ter lógica
}
```

---

## Exemplo Básico

```ts
interface Usuario {
  nome: string;
  idade: number;
  email: string;
}

// Objeto seguindo exatamente o contrato da interface
const usuario1: Usuario = {
  nome: "Ana",
  idade: 25,
  email: "ana@email.com"
};
```

Erro se faltar algo:

```ts
const usuario2: Usuario = {
  nome: "João",
  idade: 30
  // ❌ Erro: propriedade 'email' está faltando
};
```

---

## Interfaces em Funções

Interfaces também podem ser usadas para tipar os parâmetros de funções:

```ts
interface Produto {
  nome: string;
  preco: number;
}

// A função exige um objeto que siga o formato da interface Produto
function mostrarProduto(produto: Produto) {
  console.log(`${produto.nome} custa R$ ${produto.preco}`);
}

mostrarProduto({ nome: "Teclado", preco: 199.90 });
```

---

## Interface com Propriedades Opcionais

Propriedades podem ser marcadas como **opcionais** com `?`

```ts
interface Configuracao {
  tema: string;
  modoEscuro?: boolean; // propriedade opcional
}

const config1: Configuracao = { tema: "claro" };
const config2: Configuracao = { tema: "escuro", modoEscuro: true };
```

---

## Usando Interface com Classes

Interfaces também funcionam como **contrato para classes**. Isso garante que a classe **implemente os métodos e propriedades declaradas** na interface.

```ts
// Interface declarando um método que deve existir
interface Animal {
  nome: string;
  emitirSom(): void; // método sem implementação
}

// Classe que IMPLEMENTA a interface (segue o contrato)
class Cachorro implements Animal {
  nome: string;

  constructor(nome: string) {
    this.nome = nome;
  }

  emitirSom(): void {
    console.log("Au au!");
  }
}
```

⚠️ Se a classe não implementar **exatamente** os itens exigidos pela interface, TypeScript mostra erro.

---

## Conclusão

Interfaces são essenciais para manter seu código limpo, seguro e bem organizado. Elas funcionam como **contratos** que garantem que objetos e classes tenham a estrutura esperada.

Dominar interfaces vai te ajudar a:

* Trabalhar com mais segurança
* Evitar bugs
* Escrever código escalável e de fácil manutenção

---

## 💡 Dica Final

> Sempre que quiser **definir a estrutura de objetos ou classes**, use `interface`. Isso torna seu código mais confiável e mais fácil de entender por outras pessoas (ou por você no futuro).
> Se o seu objetivo é apenas garantir que um objeto tenha um determinado formato, você deve usar uma interface, e não uma class. Classes são mais pesadas, e usadas quando você quer criar objetos com comportamento (métodos, construtores, herança). 

## Exercícios

### 🟢 Exercícios Básicos

1. **Crie uma interface chamada `Livro`** com as seguintes propriedades:

   * `titulo` (string)
   * `autor` (string)
   * `anoPublicacao` (number)
   * `disponivel` (boolean, opcional)

2. **Crie um objeto** chamado `livro1` que siga a interface `Livro`.

3. **Crie uma função chamada `mostrarLivro`** que receba um objeto `Livro` e imprima suas informações no console.

---

### 🟡 Exercícios Intermediários

4. **Crie uma interface `Funcionario`** com:

   * `nome` (string)
   * `cargo` (string)
   * `salario` (number)

5. **Crie uma função `calcularBonus`** que receba um `Funcionario` e retorne 10% do salário.

6. **Crie uma interface chamada `FormaGeometrica`**, que tenha um método `calcularArea(): number`.

7. **Crie duas classes**, `Quadrado` e `Circulo`, que implementem `FormaGeometrica`:

   * `Quadrado` com lado (number)
   * `Circulo` com raio (number)

8. Crie objetos dessas classes e chame o método `calcularArea()` para verificar os resultados.

---

### 🔴 Desafio

9. Crie uma interface `Autenticavel` com um método `autenticar(usuario: string, senha: string): boolean`.

10. Crie uma classe `SistemaLogin` que implementa `Autenticavel`. Faça com que ela valide se o usuário é `"admin"` e a senha é `"1234"`.

---
