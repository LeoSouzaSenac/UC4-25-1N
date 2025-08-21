# **Trabalho: Sistema de Abrigos Temporários**

O objetivo deste trabalho é desenvolver um programa em **TypeScript** que ajude a população em situação de rua a encontrar abrigos temporários em dias frios. O programa deve utilizar a biblioteca **`readline-sync`** para receber entradas dos usuários e aplicar conceitos de **Programação Orientada a Objetos (POO)**: **herança, encapsulamento e polimorfismo**.

---

## **Funcionalidades do Sistema**

O programa deve apresentar um menu com as seguintes opções:

1. Cadastrar abrigo
2. Listar abrigos
3. Procurar abrigo por cidade
4. Sair

* A opção **Cadastrar abrigo** permite ao usuário adicionar um novo abrigo, fornecendo nome, endereço, cidade, telefone e capacidade de lotação.
* A opção **Listar abrigos** exibe todos os abrigos cadastrados, mostrando código, nome, endereço, telefone, capacidade, vagas disponíveis e cidade.
* A opção **Procurar abrigo** permite que o usuário informe a cidade onde se encontra e receba a lista de abrigos disponíveis nessa cidade, mostrando todas as informações e vagas disponíveis.
* A opção **Sair** encerra o programa.

---

# Exemplo

## **Menu Principal**

```text
===== ABRIGOS TEMPORÁRIOS =====
1. Cadastrar abrigo
2. Listar abrigos
3. Procurar abrigo
4. Sair
Escolha uma opção:
```

---

## **Listar abrigos**

```text
--------------------
LISTAGEM DE ABRIGOS:
--------------------
CÓDIGO |         NOME         |              ENDEREÇO              |   TELEFONE   |  CAPACIDADE | CIDADE
---------------------------------------------------------------------------------------------------------
  001  | Casa do Caminho      | Rua do Amanhecer, 123, Centro      |  (11) 1234-5678  |     20  | Canoas
  002  | Abrigo Esperança     | Rua da Solidariedade, 321, Bairro  |  (11) 9876-5432  |     30  | São Leopoldo
  003  | Casa dos Amigos      | Av. da Fraternidade, 456, Centro   |  (11) 5555-4444  |     25  | Novo Hamburgo
  004  | Abrigo do Bem        | Rua da Esperança, 789, Bairro      |  (11) 7777-8888  |     35  | Canoas
  005  | Casa dos Anjos       | Av. da Paz, 159, Centro            |  (11) 3333-2222  |     15  | Porto Alegre
---------------------------------------------------------------------------------------------------------
```

---

## **Procurar abrigo**

```text
Qual cidade você está?
Canoas

--------------------
LISTAGEM DE ABRIGOS:
--------------------
CÓDIGO |         NOME         |              ENDEREÇO              |   TELEFONE   |  CAPACIDADE | CIDADE
---------------------------------------------------------------------------------------------------------
  001  | Casa do Caminho      | Rua do Amanhecer, 123, Centro      |  (11) 1234-5678  |     20  | Canoas
  004  | Abrigo do Bem        | Rua da Esperança, 789, Bairro      |  (11) 7777-8888  |     35  | Canoas
---------------------------------------------------------------------------------------------------------
```

---



## **Classes e Estrutura**

### **1. Classe `Local` (classe base)**

* **Atributos (protected):**

  * `nome: string` – nome do local.
  * `endereco: string` – endereço do local.
  * `cidade: string` – cidade do local.
  * `telefone: string` – telefone de contato.

* **Métodos públicos:**

  * `mostrarInfo(): string` – retorna uma string com as informações do local (deve ser polimórfico e poder ser sobrescrito por classes filhas).
  * `getters e setters

---

### **2. Classe `Abrigo` (classe filha de `Local`)**

* **Atributos (protected):**

  * `capacidade: number` – capacidade máxima do abrigo.
  * `vagasOcupadas: number` – número de vagas já ocupadas.

* **Métodos públicos:**

  * `mostrarInfo(): string` – sobrescreve o método da classe base, retornando informações completas do abrigo, incluindo capacidade e vagas disponíveis.
  * `ocuparVaga(qtd: number): void` – registra a ocupação de vagas no abrigo.
  * `getVagasDisponiveis(): number` – retorna o número de vagas livres.

---

### **3. Classe `SistemaAbrigos`**

* **Atributos (privado):**

  * `abrigos: Abrigo[]` – lista de abrigos cadastrados.

* **Métodos públicos:**

  * `cadastrarAbrigo(): void` – solicita dados do usuário e adiciona um novo abrigo na lista.
  * `listarAbrigos(): void` – exibe todos os abrigos cadastrados em formato de tabela.
  * `procurarAbrigos(): void` – solicita a cidade do usuário e exibe os abrigos disponíveis nessa cidade.

---

## **Regras e Recomendações**

1. **Encapsulamento:**

   * Use `protected` para atributos que devem ser acessíveis apenas pelas classes filhas (`Local` → `Abrigo`).
   * Use `private` para atributos que devem ser acessíveis apenas dentro da própria classe (`SistemaAbrigos.abrigos`).
   * Sempre que precisar acessar atributos fora da classe, forneça **getters públicos**.

2. **Herança:**

   * `Abrigo` deve herdar de `Local`.

3. **Polimorfismo:**

   * O método `mostrarInfo()` deve ser sobrescrito em `Abrigo` para exibir informações adicionais (capacidade e vagas disponíveis).

4. **Entrada de dados:**

   * Utilize `readline-sync` para receber dados do usuário.

5. **Saída:**

   * Ao listar ou procurar abrigos, exiba as informações de forma organizada, com código, nome, endereço, telefone, capacidade, vagas disponíveis e cidade.
