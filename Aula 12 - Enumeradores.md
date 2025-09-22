# 📝 Enumeradores (Enums) em TypeScript

Em **TypeScript**, um **enumerador (enum)** é uma forma de **dar nomes mais legíveis para conjuntos de valores numéricos ou strings**, 
tornando o código mais fácil de entender e menos propenso a erros. Uma das principais razões para usar enums é garantir que uma variável só possa ter um dos valores definidos no enum, evitando valores inválidos ou erros de digitação.

---

## 🔹 Por que usar enums?

Imagine que você precise representar os dias da semana:

```ts
const domingo = 0;
const segunda = 1;
const terca = 2;
const quarta = 3;
const quinta = 4;
const sexta = 5;
const sabado = 6;
```

Problemas com essa abordagem:

* Difícil de ler e lembrar o que cada número representa.
* Fácil cometer erros ao usar os números diretamente.

Com **enums**, isso fica muito mais organizado:

```ts
enum DiaDaSemana {
  Domingo,
  Segunda,
  Terca,
  Quarta,
  Quinta,
  Sexta,
  Sabado,
}

let hoje: DiaDaSemana = DiaDaSemana.Segunda;
console.log(hoje); // 1
```

Agora é **claro** que `hoje` representa `Segunda`, e o TypeScript ainda associa automaticamente a posição numérica.

---

## 🔹 Tipos de enums

### 1. Enum numérico (default)

Valores automáticos atribuídos a partir do zero:

```ts
enum Status {
  Ativo,    // 0
  Inativo,  // 1
  Pendente, // 2
}

console.log(Status.Ativo); // 0
console.log(Status[1]);    // "Inativo"
```

Também é possível **atribuir valores específicos**:

```ts
enum Status {
  Ativo = 1,
  Inativo = 5,
  Pendente = 10,
}

console.log(Status.Pendente); // 10
```

---

### 2. Enum de string

Permite definir valores literais de string para melhor legibilidade:

```ts
enum Cor {
  Vermelho = "VERMELHO",
  Verde = "VERDE",
  Azul = "AZUL",
}

let minhaCor: Cor = Cor.Verde;
console.log(minhaCor); // "VERDE"
```

---

## 🔹 Quando usar enums?

* Representar **conjuntos fixos de valores**, como status, categorias ou tipos.
* Evitar **"magic numbers"** (números misteriosos) ou strings repetidas no código.
* Melhorar **legibilidade** e **manutenção** do código.

---

## 🔹 Exemplo prático

```ts
enum NivelUsuario {
  Administrador = "ADMIN",
  Moderador = "MOD",
  Comum = "USER",
}

function acessarPainel(nivel: NivelUsuario) {
  if (nivel === NivelUsuario.Administrador) {
    console.log("Acesso total liberado!");
  } else if (nivel === NivelUsuario.Moderador) {
    console.log("Acesso parcial liberado!");
  } else {
    console.log("Acesso restrito.");
  }
}

acessarPainel(NivelUsuario.Moderador); // "Acesso parcial liberado!"
```

---

## 🔹 Conclusão

Os **enums em TypeScript** são uma ferramenta poderosa para:

* Melhorar a **clareza do código**.
* Reduzir **erros de digitação** e inconsistências.
* Tornar a **manutenção mais simples**, principalmente em grandes projetos.

Sempre que você tiver **valores fixos e conhecidos**, considere usar enums!

## Exercício
Desenvolva um sistema para uma pizzaria em TypeScript.
Você deve definir um enum chamado SaborPizza que representará
os sabores disponíveis de pizzas.
Crie uma classe chamada Pizza que vai ter os parâmetros sabor, tamanho e preço. 
Crie nesta classe um método chamado descrição que retorna uma string contendo a descrição da pizza no formato "Pizza [sabor], Tamanho: [tamanho], Preço: R$ [preco]".
Crie três instâncias de pizzas com diferentes sabores, tamanhos e preços e exiba no console.

