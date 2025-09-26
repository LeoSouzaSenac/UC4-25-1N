# 📘 Quiz de TypeScript

> Clique em cada pergunta para revelar a resposta.

---

## 🧠 1. TypeScript Básico

<details>
<summary>1. O que é TypeScript?</summary>
<p>É uma linguagem de programação que estende o JavaScript, adicionando tipagem estática opcional.</p>
</details>

<details>
<summary>2. Qual comando compila um arquivo TypeScript?</summary>
<p><code>tsc arquivo.ts</code></p>
</details>

<details>
<summary>3. TypeScript roda diretamente?</summary>
<p>Não. Ele precisa ser transpilado para JavaScript antes.</p>
</details>

<details>
<summary>4. Como se instala o TypeScript?</summary>
<p><code>npm install typescript</code></p>
</details>

<details>
<summary>5. Qual a extensão padrão dos arquivos TypeScript?</summary>
<p><code>.ts</code></p>
</details>

---

## 💻 2. Comandos de Terminal (TypeScript)

<details>
<summary>1. Qual o comando para criar o package.json?</summary>
<p><code>npm init -y</code></p>
</details>

<details>
<summary>2. Como compilar todos os arquivos TypeScript de um projeto?</summary>
<p><code>tsc</code></p>
</details>

<details>
<summary>3. O que é transpilar?</summary>
<p><code>É transformar os arquivos typescript em javascript.</code></p>
</details>

<details>
<summary>4. Como transpilar um arquivo específico?</summary>
<p><code>tsc nome-do-arquivo.ts</code></p>
</details>

<details>
<summary>5. Como criar o tsconfig.json?</summary>
<p><code>npx tsc --init</code></p>
</details>

---

## 🔡 3. Tipagem

<details>
<summary>1. Como declarar uma variável do tipo string?</summary>
<p><code>let nome: string = "João";</code></p>
</details>

<details>
<summary>2. Como declarar uma função com tipo de retorno number?</summary>
<p><code>function soma(a: number, b: number): number { return a + b; }</code></p>
</details>

<details>
<summary>3. Qual o tipo para um valor que pode ser string ou número?</summary>
<p><code>string | number</code></p>
</details>

<details>
<summary>4. O que significa o tipo <code>any</code>?</summary>
<p>Permite que qualquer tipo de valor seja atribuído.</p>
</details>

<details>
<summary>5. Como declarar um array?</summary>
<p><code>let pessoa: string[] = ["João"];</code></p>
</details>

---

## 🧱 4. Classes

<details>
<summary>1. Como se declara uma classe em TypeScript?</summary>
<p><code>class Pessoa { }</code></p>
</details>

<details>
<summary>2. Como se define um construtor?</summary>
<p><code>constructor(nome: string) { this.nome = nome; }</code></p>
</details>

<details>
<summary>3. Como criar uma instância de uma classe?</summary>
<p><code>let p = new Pessoa("Maria");</code></p>
</details>

<details>
<summary>4. Como declarar um método em uma classe?</summary>
<p><code>falar(): void { console.log("Olá"); }</code></p>
</details>

<details>
<summary>5. Como acessar uma propriedade da classe?</summary>
<p><code>this.nome</code></p>
</details>

---

## 👪 5. Herança

<details>
<summary>1. Como herdar de outra classe?</summary>
<p><code>class Aluno extends Pessoa { }</code></p>
</details>

<details>
<summary>2. Como chamar o construtor da superclasse?</summary>
<p><code>super(nome);</code></p>
</details>

<details>
<summary>3. É possível sobrescrever métodos?</summary>
<p>Sim, basta declarar novamente na subclasse com a mesma assinatura.</p>
</details>

<details>
<summary>4. Qual palavra-chave usamos para acessar a superclasse?</summary>
<p><code>super</code></p>
</details>

<details>
<summary>5. Herança múltipla é permitida em classes?</summary>
<p>Não. TypeScript (como JavaScript) não suporta herança múltipla com classes.</p>
</details>

---

## 🔁 6. Polimorfismo

<details>
<summary>1. O que é polimorfismo?</summary>
<p>Capacidade de um método se comportar de diferentes formas dependendo do contexto.</p>
</details>

<details>
<summary>2. Como o TypeScript suporta polimorfismo?</summary>
<p>Através de herança e interfaces.</p>
</details>

<details>
<summary>3. Pode-se sobrescrever métodos nas subclasses?</summary>
<p>Sim, isso é parte do polimorfismo.</p>
</details>

<details>
<summary>4. É possível ter métodos com mesmo nome mas comportamento diferente?</summary>
<p>Sim, usando sobrecarga.</p>
</details>

<details>
<summary>5. Qual benefício do polimorfismo?</summary>
<p>Permite escrever código mais flexível e reutilizável.</p>
</details>

---

## 🔐 7. Encapsulamento

<details>
<summary>1. Quais são os modificadores de acesso em TypeScript?</summary>
<p><code>public</code>, <code>private</code> e <code>protected</code></p>
</details>

<details>
<summary>2. Qual é o padrão de visibilidade?</summary>
<p><code>public</code></p>
</details>

<details>
<summary>3. O que significa <code>private</code>?</summary>
<p>Que só pode ser acessado dentro da própria classe.</p>
</details>

<details>
<summary>4. O que significa <code>protected</code>?</summary>
<p>Que pode ser acessado pela classe e suas subclasses.</p>
</details>

<details>
<summary>5. Como proteger propriedades da alteração externa?</summary>
<p>Usando <code>private</code> ou <code>getter/setter</code>.</p>
</details>

---

## 🔌 8. Interface

<details>
<summary>1. O que é uma interface?</summary>
<p>É um contrato que define propriedades e métodos que uma classe deve implementar.</p>
</details>

<details>
<summary>2. Como declarar uma interface?</summary>
<p><code>interface Pessoa { nome: string; falar(): void; }</code></p>
</details>

<details>
<summary>3. Como uma classe implementa uma interface?</summary>
<p><code>class Aluno implements Pessoa { ... }</code></p>
</details>

<details>
<summary>4. Interfaces podem ter propriedades opcionais?</summary>
<p>Sim, usando <code>?</code>. Ex: <code>idade?: number</code></p>
</details>

<details>
<summary>5. Interfaces podem herdar outras?</summary>
<p>Sim, com <code>extends</code>.</p>
</details>

---

## 🏗️ 9. Classes Abstratas

<details>
<summary>1. O que é uma classe abstrata?</summary>
<p>É uma classe que não pode ser instanciada e serve como base para outras classes.</p>
</details>

<details>
<summary>2. Como declarar uma classe abstrata?</summary>
<p><code>abstract class Pessoa { }</code></p>
</details>

<details>
<summary>3. Como declarar um método abstrato?</summary>
<p><code>abstract falar(): void;</code></p>
</details>

<details>
<summary>4. É obrigatório implementar métodos abstratos?</summary>
<p>Sim, na subclasse concreta.</p>
</details>

<details>
<summary>5. Posso ter métodos implementados em classes abstratas?</summary>
<p>Sim, além dos métodos abstratos, pode ter métodos normais.</p>
</details>

---

## 💠 10. Generics

<details>
<summary>1. O que são generics?</summary>
<p>São tipos parametrizados que permitem reutilização com diferentes tipos.</p>
</details>

<details>
<summary>2. Como declarar uma função genérica?</summary>
<p><code>function identidade&lt;T&gt;(valor: T): T { return valor; }</code></p>
</details>

<details>
<summary>3. Como limitar um generic?</summary>
<p><code>&lt;T extends AlgumaInterface&gt;</code></p>
</details>

<details>
<summary>4. Qual o benefício de generics?</summary>
<p>Reutilização de código com segurança de tipo.</p>
</details>

<


details>

<summary>5. Posso usar generics em classes?</summary>
<p>Sim. Ex: <code>class Caixa&lt;T&gt; { conteudo: T; }</code></p>
</details>

---

## ➕ 11. Sobrecarga de Método

<details>
<summary>1. TypeScript permite sobrecarga?</summary>
<p>Sim, com múltiplas assinaturas e uma implementação.</p>
</details>

<details>
<summary>2. Como se declara sobrecarga?</summary>
<p>
```ts<br>
function exemplo(a: number): void;<br>
function exemplo(a: string): void;<br>
function exemplo(a: any): void { console.log(a); }<br>
```
</p>
</details>

<details>
<summary>3. A implementação deve cobrir todos os casos?</summary>
<p>Sim.</p>
</details>

<details>
<summary>4. As assinaturas aparecem no JavaScript?</summary>
<p>Não, só a implementação final é transpilada.</p>
</details>

<details>
<summary>5. É possível usar sobrecarga em métodos de classes?</summary>
<p>Sim.</p>
</details>

---

## 📑 12. Enumeradores

<details>
<summary>1. O que é um enum?</summary>
<p>É uma forma de definir um conjunto nomeado de constantes.</p>
</details>

<details>
<summary>2. Como declarar um enum?</summary>
<p><code>enum Cor { Vermelho, Verde, Azul }</code></p>
</details>

<details>
<summary>3. Enums são numéricos por padrão?</summary>
<p>Sim, começam do 0 por padrão.</p>
</details>

<details>
<summary>4. É possível atribuir valores string aos enums?</summary>
<p>Sim, com <code>= "valor"</code></p>
</details>

<details>
<summary>5. Como acessar o valor de um enum?</summary>
<p><code>Cor.Vermelho</code></p>
</details>

