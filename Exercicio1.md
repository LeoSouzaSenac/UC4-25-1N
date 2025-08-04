### 📝 **Exercício 1: Variáveis com Tipos**

Crie uma função que aceite como parâmetros o seguinte:

* Uma `string` chamada `nomeAluno` com o valor do nome de um aluno.
* Um `number` chamado `idadeAluno` com a idade do aluno.
* Um `boolean` chamado `estaMatriculado` que indica se o aluno está matriculado.

Esta função não deve ter retorno. Dentro dela, use `console.log()` para exibir uma frase com esses dados, como:

```ts
"Aluno João, 16 anos, está matriculado: true"
```

Execute a função ao final.

---

### 📝 **Exercício 2: Lista de Alunos**

Crie um array chamado `alunos` contendo o nome de 5 alunos (como strings). 
Depois, crie uma função que receberá este array como parâmetro. Esta função deve retornar apenas uma string (uma única string) que contém o nome de todos os alunos. Execute a função.
Exemplo de saída:

Alunos: 
Ana 
Bruno
Carlos
Diana
Eduardo
```

---

### 📝 **Exercício 3: Função de Saudação**

Crie uma função chamada `saudacao` que receba o nome de um aluno (parâmetro tipo `string`) e mostre no console:

```ts
"Olá, [nome]! Bem-vindo(a) à turma."
```

**Exemplo de chamada:**

```ts
saudacao("Larissa"); // Olá, Larissa! Bem-vindo(a) à turma.
```

---

### 📝 **Exercício 4: Função de Média**

Crie uma função chamada `calcularMedia` que receba **3 notas** (tipo `number`) e retorne a **média aritmética** dessas notas.

**Exemplo:**

```ts
let media = calcularMedia(8, 7.5, 9);
console.log("Média final:", media); // Média final: 8.17
```

---

### 📝 **Exercício 5: Contar Alunos**

Crie uma função chamada `contarAlunos` que receba um array de nomes de alunos (`string[]`) e exiba a quantidade de alunos.

**Exemplo:**

```ts
let turma = ["João", "Maria", "Pedro"];
contarAlunos(turma); // Deve mostrar: "Total de alunos: 3"
```
