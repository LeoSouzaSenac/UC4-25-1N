# 🚀 O que é Sobrecarga de Métodos?

👉 **Sobrecarga de métodos** acontece quando **um mesmo método** (uma mesma função dentro da classe) pode ser chamado de **maneiras diferentes**.
Em **TypeScript**, às vezes queremos que **um mesmo método** de uma classe possa ser chamado de **formas diferentes**.
Por exemplo: você quer que o método `somar` funcione **com números** ou **com textos**, ou que o método `enviar` funcione **para uma pessoa** ou **para várias pessoas**.
Essa possibilidade é chamada de **sobrecarga de métodos**. Ou seja: você pode **dar mais de uma forma de usar** esse método, mudando o **tipo ou quantidade de parâmetros**.

---

# 📝 Por que isso existe?

Imagine que você tem uma **calculadora**.
Às vezes, você quer somar **números**, outras vezes quer somar **textos** (concatenar strings).
Não faria sentido criar 2 métodos diferentes, tipo `somarNumeros` e `somarTextos`.

➡️ Com **sobrecarga**, você usa o mesmo nome (`somar`) e o TypeScript entende o que fazer dependendo do tipo de dado.

---

# 🎯 Quando usamos?

* Quando queremos deixar o código **mais simples e natural**, evitando vários métodos diferentes.
* Quando uma mesma ação pode ser feita de **várias formas**.
* Quando queremos que a classe pareça mais **inteligente**: ela entende o que o usuário quis dizer pelo tipo de dado.

---

## 🔹 O que são assinaturas?

As **assinaturas** de um método são como **“contratos”** que dizem ao TypeScript **quais formas de chamar o método são válidas**.
Elas **não têm corpo** — ou seja, não dizem **como o método funciona**, apenas **como ele pode ser usado**.

Exemplo de assinaturas:

```ts
somar(a: number, b: number): number;   // assina que pode receber dois números
somar(a: string, b: string): string;   // assina que pode receber duas strings
```

➡️ Aqui você está dizendo: “o método `somar` pode ser chamado **com dois números** ou **com duas strings**”.

---

## 🔹 O que é a implementação real?

A **implementação real** é **uma única função** que vai conter **toda a lógica** do método, cobrindo **todas as assinaturas**.

Como cada assinatura pode ter parâmetros diferentes, geralmente usamos **`any`** ou **`unknown`** nos parâmetros da implementação e fazemos **checagens de tipo** ou de quantidade dentro do método:

```ts
somar(a: any, b: any): any {
  return a + b;  // aqui o TypeScript vai decidir o que fazer dependendo do tipo de 'a' e 'b'
}
```

➡️ O TypeScript usa as assinaturas para **validar a chamada** e o corpo da implementação para **executar a lógica real**.

---

## 🔹 Para que serve a separação entre assinaturas e implementação?

1. **Organização do código:** você mantém **uma única função**, mas que pode ser usada de **formas diferentes**.
2. **Validação pelo TypeScript:** ele garante que o método só será chamado de **formas que você definiu nas assinaturas**.
3. **Flexibilidade:** permite que **o mesmo método se comporte de maneiras diferentes**, sem precisar criar vários nomes de função.

---

## 🔹 Resumindo

* **Sobrecarga de métodos:** permite que um mesmo método tenha **mais de uma forma de uso**.
* **Assinaturas:** definem **como o método pode ser chamado** (tipo e quantidade de parâmetros).
* **Implementação real:** contém **a lógica do método**, cobrindo todas as assinaturas.
* Serve para **deixar o código mais limpo, organizado e natural**, permitindo que a classe entenda **diferentes formas de executar uma mesma ação**.

---



# 📌 Exemplo 1: Calculadora Simples

```typescript
class Calculadora {
  // --- Definindo as "formas" possíveis do método ---
  somar(a: number, b: number): number;
  somar(a: string, b: string): string;

  // --- Implementação real do método ---
  somar(a: any, b: any): any {
    return a + b;
  }
}

// 👇 Testando
const calc = new Calculadora();

console.log(calc.somar(10, 20));    // 30  (soma números)
console.log(calc.somar("Bom ", "dia")); // "Bom dia" (junta textos)
```

➡️ Aqui temos **um único método** `somar`, mas que aceita **números ou textos**.

---

# 📌 Exemplo 2: Mensagens (Chat)

Imagine que estamos criando um app de mensagens.

```typescript
class Mensageiro {
  // Pode mandar mensagem para uma pessoa
  enviar(destinatario: string, mensagem: string): void;
  // Ou pode mandar para várias pessoas ao mesmo tempo
  enviar(destinatarios: string[], mensagem: string): void;

  enviar(dest: any, mensagem: string): void {
    if (Array.isArray(dest)) {
      console.log("Enviando para vários:", dest.join(", "));
    } else {
      console.log("Enviando para:", dest);
    }
    console.log("Mensagem:", mensagem);
  }
}

// 👇 Testando
const m = new Mensageiro();

m.enviar("Ana", "Oi, tudo bem?");  
// Enviando para: Ana
// Mensagem: Oi, tudo bem?

m.enviar(["João", "Maria"], "Bom dia, galera!");
// Enviando para vários: João, Maria
// Mensagem: Bom dia, galera!
```

➡️ O mesmo método `enviar` funciona para **um único contato** ou **uma lista de contatos**.

---

# 📌 Exemplo 3: Desenhar Formas

Se você estiver criando algo tipo um joguinho ou programa gráfico:

```typescript
class Desenhista {
  // Pode desenhar um círculo passando só o raio
  desenhar(raio: number): void;
  // Ou pode desenhar um retângulo passando largura e altura
  desenhar(largura: number, altura: number): void;

  desenhar(a: number, b?: number): void {
    if (b === undefined) {
      console.log(`Desenhando um círculo de raio ${a}`);
    } else {
      console.log(`Desenhando um retângulo de ${a}x${b}`);
    }
  }
}

// 👇 Testando
const d = new Desenhista();

d.desenhar(10);       // Desenhando um círculo de raio 10
d.desenhar(20, 30);   // Desenhando um retângulo de 20x30
```

➡️ O mesmo método `desenhar` entende se é **círculo** ou **retângulo** pelo número de parâmetros.

---

# 🧠 Resumindo:

1. **Sobrecarga = um mesmo método com várias formas de uso.**
2. Serve para **deixar o código mais organizado e natural**.
3. Muito usado quando uma ação pode ser feita de **mais de um jeito**.
4. Em TypeScript, escrevemos as "formas possíveis" em cima (as assinaturas), e a implementação real embaixo.


---

# 🎯 O que dá pra mudar com sobrecarga de métodos?

Na prática, **sobrecarga é sobre variações nas “assinaturas” do método** (a forma como ele é chamado).
Você pode sobrecarregar em relação a:

---

## 1. 📌 **Quantidade de parâmetros**

➡️ O mesmo método pode aceitar **mais ou menos argumentos**.

```ts
class Mensageiro {
  // Só um destinatário
  enviar(destinatario: string, mensagem: string): void;
  // Vários destinatários
  enviar(destinatarios: string[], mensagem: string): void;

  enviar(dest: any, mensagem: string): void {
    if (Array.isArray(dest)) {
      console.log(`Enviando para vários: ${dest.join(", ")}`);
    } else {
      console.log(`Enviando para: ${dest}`);
    }
    console.log(`Mensagem: ${mensagem}`);
  }
}

const m = new Mensageiro();

// Chamando para 1 pessoa
m.enviar("Ana", "Oi, tudo bem?");

// Chamando para várias pessoas
m.enviar(["João", "Maria"], "Bom dia, pessoal!");
```

---

## 2. 📌 **Tipo dos parâmetros**

➡️ O mesmo método pode aceitar **tipos diferentes** para o mesmo parâmetro.

```ts
class Calculadora {
  somar(a: number, b: number): number;
  somar(a: string, b: string): string;

  somar(a: any, b: any): any {
    return a + b;
  }
}

const c = new Calculadora();
console.log(c.somar(10, 20));       // 30
console.log(c.somar("Bom ", "dia")) // "Bom dia"
```

---

## 3. 📌 **Combinação de tipos e quantidades**

➡️ Dá pra misturar as duas ideias.

```ts
class Desenhista {
 // Assinaturas (só diz ao TypeScript como pode ser chamado)
desenhar(raio: number): void;
desenhar(largura: number, altura: number): void;
desenhar(pontos: [number, number][]): void;

// Implementação real (uma só!)
desenhar(a: any, b?: any): void {  // <--- aqui usamos 'any' para cobrir todas as assinaturas
  if (typeof a === "number" && b === undefined) {
    console.log(`Círculo de raio ${a}`);
  } else if (typeof a === "number" && typeof b === "number") {
    console.log(`Retângulo ${a}x${b}`);
  } else {
    console.log(`Polígono com ${a.length} pontos`);
  }
}

const d = new Desenhista();
d.desenhar(10);
d.desenhar(20, 30);
d.desenhar([[0,0],[1,0],[1,1],[0,1]]);
```

---

## 4. 📌 **Tipo de retorno**

➡️ Dependendo da forma como é chamado, o método pode **retornar tipos diferentes**.

```ts
class Repositorio {
  buscar(id: number): string;
  buscar(nome: string): string[];

  buscar(arg: any): any {
    if (typeof arg === "number") {
      return "Usuário com id " + arg;
    } else {
      return ["Usuário1", "Usuário2"];
    }
  }
}

const r = new Repositorio();
const u = r.buscar(1);     // retorna string
const lista = r.buscar("a"); // retorna string[]
```

---

# 🚨 O que **NÃO** dá pra mudar com sobrecarga?

É importante os alunos saberem os limites:

1. ❌ Você **não pode mudar só o nome do parâmetro**. O compilador não liga para nomes, só para quantidade e tipo.

   ```ts
   metodo(a: string): void;
   metodo(b: string): void; // <-- duplicado, não funciona
   ```

2. ❌ Você **não pode mudar modificadores de acesso** (public, private, etc.) na sobrecarga.

   ```ts
   metodo(a: string): void;   // public
   private metodo(a: number): void; // inválido
   ```

3. ❌ Você não pode mudar só o **nome do método** e chamar de sobrecarga — isso já é outro método (normal, sem sobrecarga).

---

# 🧠 Resumindo

Com sobrecarga você pode mudar:

✅ **Quantidade de parâmetros**
✅ **Tipo dos parâmetros**
✅ **Combinação de tipos e quantidades**
✅ **Tipo de retorno** (dependendo da forma de chamada)



