# **Trabalho: Sistema de Cadastro de Doadores de Sangue**

O objetivo deste trabalho é desenvolver um programa em **TypeScript** que permita o cadastro e consulta de doadores de sangue para o Hemocentro da sua cidade. O programa deve utilizar a biblioteca **`readline-sync`** para receber entradas dos usuários e aplicar conceitos de **Programação Orientada a Objetos (POO)**: **herança, encapsulamento e polimorfismo**.

---

## **Funcionalidades do Sistema**

O programa deve apresentar um menu com as seguintes opções:

1. Cadastrar doador
2. Listar doadores
3. Buscar doador por tipo sanguíneo
4. Buscar doador por data da última doação
5. Sair

* A opção **Cadastrar doador** permite ao usuário adicionar um novo doador, fornecendo nome, idade, peso, tipo sanguíneo e data da última doação.
* A opção **Listar doadores** exibe todos os doadores cadastrados, mostrando todas as informações.
* A opção **Buscar por tipo sanguíneo** permite que o usuário informe o tipo sanguíneo e receba a lista de doadores correspondentes.
* A opção **Buscar por data da última doação** permite que o usuário informe uma data e receba a lista de doadores que fizeram a última doação antes dessa data.
* A opção **Sair** encerra o programa.

---

# Exemplo

## **Menu Principal**

```text
===== SISTEMA DE CADASTRO DE DOADORES DE SANGUE =====
1. Cadastrar doador
2. Listar doadores
3. Buscar doador por tipo sanguíneo
4. Buscar doador por data da última doação
5. Sair
Escolha uma opção:
```

---

## **Listagem de Doadores**

```text
--------------------
LISTAGEM DE DOADORES:
--------------------
NOME             | IDADE | PESO | TIPO SANGUÍNEO | ÚLTIMA DOAÇÃO
-----------------------------------------------------------------
João da Silva    |  25   |  70  |      AB-       |   01/01/2022  
Maria Santos     |  35   |  65  |      A+        |   03/02/2022  
José Almeida     |  45   |  80  |      O+        |   10/01/2022  
Ana Oliveira     |  27   |  58  |      B-        |   22/04/2022  
Carlos Silva     |  30   |  75  |      A-        |   14/03/2022  
-----------------------------------------------------------------
```

---

## **Buscar por Tipo Sanguíneo**

```text
Digite o tipo sanguíneo desejado: A+

------------------------
RESULTADO DA BUSCA:
------------------------
NOME             | IDADE | PESO | TIPO SANGUÍNEO | ÚLTIMA DOAÇÃO
-----------------------------------------------------------------
Maria Santos     |  35   |  65  |      A+        |   03/02/2022  
Carlos Silva     |  30   |  75  |      A-        |   14/03/2022  
-----------------------------------------------------------------
```

---

## **Buscar por Data da Última Doação**

```text
Digite a data desejada (dd/mm/aaaa): 01/03/2024

------------------------
RESULTADO DA BUSCA:
------------------------
NOME             | IDADE | PESO | TIPO SANGUÍNEO | ÚLTIMA DOAÇÃO
-----------------------------------------------------------------
Calito Teves     |  35   |  65  |      A+        |   01/03/2022  
Carla Maria      |  30   |  75  |      A-        |   01/03/2022  
-----------------------------------------------------------------
```

---

## **Classes e Estrutura**

### **1. Classe `Pessoa` (classe base)**

* **Atributos (protected):**

  * `nome: string` – nome da pessoa
  * `idade: number` – idade da pessoa
  * `peso: number` – peso da pessoa

* **Métodos públicos:**

  * `mostrarInfo(): string` – retorna uma string com informações básicas da pessoa (polimórfico, pode ser sobrescrito).
  * `getters` – para acessar atributos protegidos quando necessário.

---

### **2. Classe `Doador` (classe filha de `Pessoa`)**

* **Atributos (protected):**

  * `tipoSanguineo: string` – tipo sanguíneo do doador
  * `dataUltimaDoacao: string` – data da última doação

* **Métodos públicos:**

  * `mostrarInfo(): string` – sobrescreve o método da classe base, retornando informações completas do doador.
  * `getTipoSanguineo(): string` – retorna o tipo sanguíneo do doador
  * `getDataUltimaDoacao(): string` – retorna a data da última doação

---

### **3. Classe `SistemaHemocentro`**

* **Atributos (private):**

  * `doadores: Doador[]` – lista de doadores cadastrados

* **Métodos públicos:**

  * `cadastrarDoador(): void` – solicita os dados do usuário e adiciona um novo doador na lista
  * `listarDoadores(): void` – exibe todos os doadores cadastrados em formato de tabela
  * `buscarPorTipoSanguineo(): void` – solicita tipo sanguíneo e exibe doadores correspondentes
  * `buscarPorDataUltimaDoacao(): void` – solicita data e exibe doadores cuja última doação foi antes da data informada

---

## **Regras e Recomendações**

1. **Encapsulamento:**

   * Use `protected` para atributos que devem ser acessíveis apenas pelas classes filhas (`Pessoa` → `Doador`).
   * Use `private` para atributos que devem ser acessíveis apenas dentro da própria classe (`SistemaHemocentro.doadores`).
   * Sempre que precisar acessar atributos fora da classe, forneça **getters públicos**.

2. **Herança:**

   * `Doador` deve herdar de `Pessoa`.

3. **Polimorfismo:**

   * O método `mostrarInfo()` deve ser sobrescrito em `Doador` para exibir informações adicionais.

4. **Entrada de dados:**

   * Utilize **`readline-sync`** para receber dados do usuário.

5. **Saída:**

   * Ao listar ou buscar doadores, exiba as informações em forma de tabela, com colunas:
     `NOME | IDADE | PESO | TIPO SANGUÍNEO | ÚLTIMA DOAÇÃO`.
