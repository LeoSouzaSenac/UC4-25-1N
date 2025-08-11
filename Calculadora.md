## 🧪 **Exercício Prático: Calculadora com Menu em TypeScript**

### 🎯 Objetivo:

Criar um pequeno sistema de calculadora em TypeScript utilizando:

* Estrutura de repetição `while`
* Estrutura de seleção `switch`
* Criação e uso de **funções externas**
* Leitura de dados pelo terminal com `readline-sync`

---

### 📝 Descrição:

Você deve criar uma **calculadora interativa** no terminal. Ela deve exibir um menu com as seguintes opções:

```
=== CALCULADORA ===
1 - Somar
2 - Subtrair
3 - Multiplicar
4 - Dividir
5 - Sair
```

O usuário poderá escolher a operação desejada, digitar dois números, e ver o resultado da operação.

O programa **deve continuar exibindo o menu** até que o usuário escolha a opção **5 - Sair**.

---

### 📌 Requisitos obrigatórios:

1. Crie **uma função separada para cada operação matemática**:

   * `somar()`
   * `subtrair()`
   * `multiplicar()`
   * `dividir()`

2. As funções devem ser definidas **fora do laço e fora do `switch`**, e **devem ser chamadas dentro do `switch`**.

3. O programa deve utilizar um laço `while` para exibir o menu repetidamente até a opção de sair ser escolhida.

4. Use o pacote `readline-sync` para ler os dados digitados pelo usuário no terminal.

   > 💡 **Dica**: Para instalar a biblioteca, use o comando:
   > `npm install readline-sync`

5. Converta as entradas do usuário para o tipo **`number`** antes de usá-las nas operações.

   > 💡 **Dica**: Use a função `Number()` para converter strings em números:
   >
   > ```ts
   > const numero = Number(readline.question("Digite um número: "));
   > ```

6. Adicione uma verificação para impedir divisão por zero.

7. Ao final de cada operação, exiba o resultado para o usuário.
