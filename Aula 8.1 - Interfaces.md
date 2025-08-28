# O que é uma Interface em TypeScript?

## Introdução

Em TypeScript, **interface** é uma das ferramentas mais importantes para garantir que seu código seja mais organizado, legível e seguro. Ela serve para **definir a forma de um objeto**, 
descrevendo quais propriedades e tipos ele deve ter.

---


### 🧩 Para que serve uma Interface?

1. **Definir contratos**: Especificar como objetos devem ser estruturados.
   É o conjunto de regras que os objetos devem seguir.

   ✅ **Exemplo:**

   ```ts
   interface Usuario {
     nome: string;
     idade: number;
   }

   const usuario: Usuario = {
     nome: "Maria",
     idade: 28
   };
   ```

   🛑 Se tentar criar um objeto sem seguir esse formato, dará erro:

   ```ts
   const usuarioInvalido: Usuario = {
     nome: "Carlos"
     // Erro: está faltando a propriedade 'idade'
   };
   ```

---

2. **Ajudar no autocomplete e validação de tipos** em editores como o VS Code.

   ✅ **Exemplo:**

   Quando você digita `usuario.` no VS Code, o editor sugere automaticamente `nome` e `idade`, pois ele **reconhece o formato da interface**.

   ```ts
   console.log(usuario.nome); // autocomplete ajuda aqui!
   ```

---

3. **Facilitar a manutenção e o entendimento do código**.

   ✅ **Exemplo:**

   Ao trabalhar em equipe, todos saberão exatamente como um `Produto` deve ser:

   ```ts
   interface Produto {
     nome: string;
     preco: number;
   }

   function mostrarPreco(produto: Produto) {
     console.log(`${produto.nome} custa R$${produto.preco}`);
   }
   ```

   Mesmo sem saber o que está dentro do objeto `Produto`, a interface deixa claro o que esperar — isso **ajuda muito na leitura e manutenção** do código.

---

4. **Evitar erros** ao garantir que objetos sigam um formato esperado.

   ✅ **Exemplo:**

   ```ts
   interface Config {
     modoEscuro: boolean;
   }

   const config: Config = {
     modoEscuro: "sim" // ❌ Erro: deveria ser boolean (true ou false)
   };
   ```

   O TypeScript impede esse erro antes mesmo de rodar o código, garantindo **mais segurança** no desenvolvimento.


---

## Exemplo Básico

```ts
interface Usuario {
  nome: string;
  idade: number;
  email: string;
}

const usuario1: Usuario = {
  nome: "Ana",
  idade: 25,
  email: "ana@email.com"
};
````

Se faltar alguma propriedade, o TypeScript mostrará um erro:

```ts
const usuario2: Usuario = {
  nome: "João",
  idade: 30
  // Erro! Está faltando a propriedade 'email'
};
```

---

## Interfaces em Funções

```ts
interface Produto {
  nome: string;
  preco: number;
}

function mostrarProduto(produto: Produto) {
  console.log(`${produto.nome} custa R$ ${produto.preco}`);
}

mostrarProduto({ nome: "Teclado", preco: 199.90 });
```

---

## Interface com Propriedades Opcionais

```ts
interface Configuracao {
  tema: string;
  modoEscuro?: boolean;
}

const config1: Configuracao = { tema: "claro" };
const config2: Configuracao = { tema: "escuro", modoEscuro: true };
```

---

## Usando Interface com Classes

Interfaces também são usadas para garantir que uma **classe siga um formato específico**.

```ts
interface Animal {
  nome: string;
  emitirSom(): void;
}

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

---

## Interface vs Tipo (type)

| Aspecto        | interface          | type                             |
| -------------- | ------------------ | -------------------------------- |
| Foco principal | Objetos e classes  | Tipos em geral                   |
| Herança        | Sim (extends)      | Limitada (intersecção)           |
| Preferência    | Melhor com classes | Mais flexível com união de tipos |

---

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

## Conclusão

Interfaces são essenciais para manter seu código limpo, seguro e bem organizado. Elas funcionam como **contratos** que garantem que objetos e classes tenham a estrutura esperada.

Dominar interfaces vai te ajudar a:

* Trabalhar com mais segurança
* Evitar bugs
* Escrever código escalável e de fácil manutenção

---

## Dica Final

> Use interfaces sempre que quiser definir a **estrutura de dados** ou garantir que **classes** sigam comportamentos esperados. Isso torna seu código mais confiável e mais fácil de entender por outras pessoas (ou por você no futuro 😄).
