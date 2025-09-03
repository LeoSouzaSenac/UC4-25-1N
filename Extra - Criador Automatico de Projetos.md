# Criando um Script para Gerar Projetos TypeScript Automaticamente

Que tal aprender um pouco sobre automatização, usando Typescript? Vamos aplicar alguns conceitos que aprendemos em aula para criar um projeto que cria **automaticamente** outros projetos, com tudo já configurado!
O projeto que vamos aprender a criar gera projetos prontos com:

* Estrutura de pastas (`src`, `dist`)
* `tsconfig.json` com configuração inicial
* `package.json` atualizado com scripts `build` e `start`
* Arquivo inicial `index.ts`

---

## Objetivo do Script

O script:

1. Pergunta o nome do projeto ao usuário.
2. Cria uma pasta para o projeto **uma pasta acima da atual**.
3. Inicializa o projeto com `npm init -y`.
4. Instala o TypeScript como dependência de desenvolvimento.
5. Cria `tsconfig.json` com as opções recomendadas.
6. Atualiza `package.json` com scripts úteis.
7. Cria a pasta `src` e um arquivo `index.ts` inicial.

* Crie um projeto de nome `projeto-automatico`, e siga todo o passo a passo para criá-lo, como sempre fazemos.

Instale estas dependências nele:

```bash
# Instala TypeScript como dependência de desenvolvimento
npm install typescript --save-dev

# Instala tipos do Node.js para o TypeScript
npm install @types/node --save-dev

# Instala readline-sync para capturar input do usuário
npm install readline-sync

# (Opcional, mas recomendado) Tipagem do readline-sync
npm install @types/readline-sync --save-dev

```

---

## 2. Bibliotecas

Antes de começarmos a escrever o script, é importante entender quais bibliotecas iremos utilizar e para que cada uma serve.

### 1. `fs` (File System)
- Biblioteca nativa do Node.js.
- Permite criar, ler, escrever e deletar arquivos e pastas.
- Funções principais usadas no script:
  - `fs.mkdirSync(path, options)` → cria uma pasta.  
    - `path`: string com o caminho da pasta.  
    - `options.recursive`: se `true`, cria pastas intermediárias (pastas que ficam antes de chegar na pasta final) caso não existam.  
  
  - `fs.writeFileSync(path, data)` → cria ou sobrescreve arquivos.  
    - `path`: caminho do arquivo.  
    - `data`: conteúdo do arquivo (string).  

  - `fs.readFileSync(path, encoding)` → lê o conteúdo de um arquivo.  
    - `path`: caminho do arquivo.  
    - `encoding`: ex. `"utf-8"`.    "utf-8" faz com que o conteúdo seja retornado como texto legível e não como código binário.
    - Retorna uma string com o conteúdo do arquivo.

### 2. `child_process` (`execSync`)
- Biblioteca nativa do Node.js para executar comandos do terminal.  
- Função usada no script:
  - `execSync(command, options)` → executa um comando de forma síncrona.  
    - `command`: string com o comando do terminal, ex: `"npm init -y"`.  
    - `options.stdio`: `"inherit"` para mostrar a saída diretamente no terminal.  
    
- Permite rodar comandos como `npm install`, `tsc`, ou qualquer comando do sistema.

### 3. `path`
- Biblioteca nativa do Node.js para manipulação de caminhos de arquivos.  
- Função usada:
  - `path.join(...paths: string[])` → junta várias strings de caminho de forma segura, usando o separador correto do sistema operacional (`/` ou `\`).  
  - Retorno: string com o caminho completo.

### 4. `readline-sync`
- Biblioteca externa para ler input do usuário.  
- Função usada:
  - `readlineSync.question(prompt)` → mostra o prompt no terminal e retorna o que o usuário digitou como string.
- Permite que o script pergunte o nome do projeto antes de criar pastas e arquivos.


## Interfaces que vamos utilizar neste script

Para organizar melhor o código e garantir que o TypeScript entenda os tipos de cada objeto, **precisamos criar duas interfaces**:

1. **TsConfig**  
   - Representa a estrutura do arquivo `tsconfig.json`.  
   - Define os tipos das opções do compilador, pastas incluídas e excluídas.

2. **PackageJson**  
   - Representa a estrutura do arquivo `package.json`.  
   - Define os tipos de propriedades como `name`, `version` e `scripts`.

### Boas práticas
- É considerado **boa prática** separar cada interface em arquivos diferentes, especialmente em projetos maiores.  
- Por exemplo:
  - `interfaces/TsConfig.ts` → contém apenas a interface `TsConfig`.  
  - `interfaces/PackageJson.ts` → contém apenas a interface `PackageJson`.  
- Isso deixa o código mais organizado e facilita a manutenção.


```ts
// Interface para tipar o tsconfig.json
export interface TsConfig {
  compilerOptions: {
    target: string;           // Versão JS alvo
    module: string;           // Tipo de módulo
    outDir: string;           // Pasta de saída do JS compilado
    rootDir: string;          // Pasta raiz dos arquivos TS
    strict: boolean;          // Ativa checagem de tipos rigorosa
    moduleResolution: string; // Como resolver módulos
    esModuleInterop: boolean; // Permite import fs from "fs"
  };
  include: string[];           // Quais pastas/arquivos incluir
  exclude: string[];           // Quais pastas/arquivos excluir
}
```

```ts
// Interface para tipar o package.json
export interface PackageJson {
  name?: string;               // Nome do pacote
  version?: string;            // Versão
  description?: string;        // Descrição
  main?: string;               // Arquivo principal
  scripts: {                   // Scripts npm
    test: string;
    build: string;
    start: string;
  };
  keywords?: string[];
  author?: string;
  license?: string;
  [key: string]: unknown;      // Permite outros campos extras
}

```
---

## Criando a Função Principal do Script

Vamos criar a função que será responsável por **criar o projeto TypeScript**.  
Por enquanto deixe ela vazia. Já vamos preenchê-la em seguida, passo a passo.

```ts
// Função principal que irá criar o projeto
function createTsProject(): void {
  // Código será adicionado aqui nos próximos passos
}
````

---

### Chamando a função

No final do arquivo, devemos **executar a função** para que o script realmente rode quando for iniciado:

```ts
// Chama a função principal
createTsProject();
```

* Assim, sempre que o script for executado, ele iniciará pela função `createTsProject`.

---


## Agora, preste atenção: todo código a partir de agora vai dentro da função principal

A partir deste ponto, **todo o código que cria pastas, arquivos e configura o projeto** será colocado dentro da função `createTsProject()` que criamos anteriormente.

---

### Passo 1: Perguntar o nome do projeto

Dentro da função, a primeira coisa que vamos fazer é solicitar ao usuário que digite o nome do projeto:

```ts
// Passo 1: Pergunta o nome do projeto
const projectName: string = readlineSync.question("Digite o nome do projeto: ");

// Validação simples: não pode ser vazio
if (!projectName) {
  console.log("❌ Nome do projeto não pode ser vazio!");
  return; // encerra a função se o usuário não digitou nada
}
````

#### Explicação:

* `readlineSync.question(prompt)`

  * Mostra a mensagem (`prompt`) no terminal.
  * Retorna o que o usuário digitou como **string**.

* `if (!projectName)`

  * Verifica se o usuário não digitou nada.
  * Se estiver vazio, mostra mensagem de erro e **encerra a função** com `return`.

* Dessa forma, garantimos que **sempre teremos um nome válido** para criar a pasta do projeto.
* 

---

### Passo 2: Definir o caminho da pasta do projeto

Depois de pegar o nome do projeto, precisamos criar a pasta onde ele será salvo.  
Neste script, vamos criar a pasta **uma pasta acima** da pasta atual.

```ts
// Caminho da pasta que será criada "uma acima" da pasta atual
const projectPath: string = path.join("..", projectName);
````

#### Explicação:

* `path.join(...paths: string[])`

  * Junta várias partes de um caminho de forma **segura**, respeitando o sistema operacional.
  * No Windows, ele usa `\` como separador, e no Linux/macOS, usa `/`.

* `".."` indica a **pasta acima** da pasta atual.

* `projectName` é o nome que o usuário digitou.

* Exemplo:

  * Pasta atual: `C:/Users/Aluno/projetos`
  * Nome do projeto digitado: `MeuProjeto`
  * `path.join("..", projectName)` resulta em:

    ```
    C:/Users/Aluno/MeuProjeto
    ```
  * Ou, no Linux/macOS:

    ```
    /home/aluno/MeuProjeto
    ```
* Ou seja, o path.join vai colocar ".." e também "/" junto do nome do projeto, criando uma pasta "acima" de onde o projeto deste script está
* Essa variável `projectPath` será usada para criar a pasta e mudar o diretório do script.

---

### Passo 3: Criar a pasta do projeto

Agora que já temos o caminho completo, vamos criar a pasta onde o projeto será armazenado.

```ts
// Cria a pasta do projeto, recursive:true garante criação de pastas intermediárias
fs.mkdirSync(projectPath, { recursive: true });
````

#### Explicação:

* `fs.mkdirSync(path, options)`

  * Cria uma pasta no caminho especificado.
  * `path`: caminho completo da pasta (`projectPath`).
  * `options.recursive: true`:

    * Se existirem pastas no caminho que ainda não existem, elas serão criadas automaticamente.
    * Essas pastas são chamadas de **pastas intermediárias**.
    * Sem `recursive: true`, o comando daria erro se alguma pasta do caminho não existisse.

* Exemplo:

  * `projectPath = "../MeuProjeto/src"`
  * Se `"../MeuProjeto"` não existir, o Node vai criar essa pasta também antes de criar `src`.

* Essa função **não retorna nada**, mas lança erro se não puder criar a pasta (por exemplo, por falta de permissão).

---

### Passo 4: Entrar na pasta criada

Depois de criar a pasta do projeto, precisamos **mudar o diretório atual** para dentro dela, para que todos os comandos seguintes sejam executados no lugar certo.

```ts
// Entra na pasta criada
process.chdir(projectPath);

console.log("Inicializando o projeto...");
````

#### Explicação:

* `process.chdir(path)`

  * Muda o **diretório de trabalho atual** do Node.js para o caminho especificado.
  * Todos os comandos futuros que criam arquivos ou executam scripts serão feitos dentro desta pasta.

---

### Passo 5: Inicializar o npm e instalar TypeScript

Agora vamos preparar o projeto para ser um projeto Node/TypeScript, criando o `package.json` e instalando o TypeScript.

```ts
// Inicializa npm (cria package.json padrão)
execSync("npm init -y", { stdio: "inherit" });

// Instala TypeScript 
execSync("npm install typescript", { stdio: "inherit" });
````

#### Explicação:

1. `execSync(command, options)`

   * Executa um comando do terminal **de forma síncrona** (o script espera o comando terminar antes de continuar).
   * `command`: string com o comando a ser executado, por exemplo `"npm init -y"`.
   * `options.stdio: "inherit"`: mostra a saída do comando diretamente no terminal.

2. `"npm init -y"`

   * Inicializa um projeto Node.js, criando um **package.json padrão** com valores default.
   * `-y` significa **responder “sim” para todas as perguntas automaticamente**.

3. `"npm install typescript"`

   * Instala o TypeScript como dependência do projeto.
   * Após isso, podemos usar o comando `tsc` para compilar arquivos `.ts` em `.js`.

> Observação: se você quiser instalar o TypeScript como dependência de desenvolvimento, pode usar `npm install typescript --save-dev`. É um pacote que você **só precisa enquanto programa**.  
Não é necessário quando o projeto já está pronto para rodar.

---

### Passo 6: Criar o tsconfig.json

O `tsconfig.json` diz ao TypeScript **como compilar o projeto**.  
Vamos criar um objeto com as configurações desejadas.

> Observação: O objeto `tsConfig` segue a **interface `TsConfig` que criamos anteriormente**.  
Isso garante que todas as propriedades estejam corretas e ajuda o TypeScript a detectar erros se algum campo estiver errado.


```ts
// Cria o tsconfig.json com as configurações desejadas
const tsConfig: TsConfig = {
  compilerOptions: {
    target: "ES6",            // gera JavaScript compatível com ES6
    module: "commonjs",       // usa módulos do Node.js
    outDir: "./dist",         // pasta onde o JS compilado será salvo
    rootDir: "./src",         // pasta onde estão os arquivos TS
    strict: true,             // ativa verificação rigorosa de tipos
    moduleResolution: "Node", // resolve módulos como o Node faz
    esModuleInterop: true     // permite import fs from 'fs'
  },
  include: ["src"],           // inclui a pasta src na compilação
  exclude: ["node_modules"]   // ignora a pasta node_modules
};
````

#### Explicação simples:

* `compilerOptions` → opções que definem **como o TypeScript gera o JavaScript**.
* `include` → quais pastas/arquivos o TypeScript deve compilar.
* `exclude` → quais pastas/arquivos o TypeScript deve **ignorar**.

---

### Passo 7: Salvar o tsconfig.json

Depois de criar o objeto `tsConfig`, precisamos escrever ele em um arquivo `tsconfig.json` dentro da pasta do projeto.

```ts
fs.writeFileSync("tsconfig.json", JSON.stringify(tsConfig, null, 2));
````

#### Explicação:

* `fs.writeFileSync(path, data)`

  * Cria ou sobrescreve um arquivo no caminho que especificamos antes (`path`).
  * Neste método (lembre-se que ele é um método que já vem com a biblioteca, pronto para usar) `data` deve ser **uma string**, então usamos `JSON.stringify` para converter o objeto em texto.

* `JSON.stringify(obj, null, 2)`

  * Converte o objeto JavaScript (`obj`) em uma string no formato JSON.
  * `null` → não usamos função de replacer.
  * `2` → adiciona **indentação de 2 espaços**, deixando o arquivo legível.

* **JSON**

  * É um formato de **texto que representa objetos** com chaves e valores, parecido com um objeto JavaScript.
  * Permite que diferentes programas leiam a mesma configuração (vários programas diferentes, em várias linguagens, entendem ele).
  * Exemplo:

```json
{
  "compilerOptions": {
    "target": "ES6"
  }
}
```

> Observação: O arquivo segue a **interface `TsConfig` que criamos anteriormente**, garantindo que todas as propriedades estejam corretas.

---

### Passo 8: Ler o package.json criado pelo npm

Quando rodamos `npm init -y`, o Node cria um arquivo `package.json` com algumas informações padrão.  
Para **editar esse arquivo** e adicionar nossos scripts, precisamos **ler o conteúdo e transformar em um objeto**.

```ts
// Lê o package.json criado pelo npm init
const packageJsonRaw: string = fs.readFileSync("package.json", "utf-8");

// Converte o texto JSON em um objeto JavaScript/TypeScript
const packageJson: PackageJson = JSON.parse(packageJsonRaw);
````

#### Explicação:

1. `fs.readFileSync(path, encoding)`

   * Lê o conteúdo de um arquivo.
   * `path`: caminho do arquivo (`"package.json"`).
   * `encoding: "utf-8"`: faz com que o conteúdo seja retornado como **texto legível**, e não como bytes.

2. `packageJsonRaw`

   * Contém todo o conteúdo do `package.json` como **string** (texto).

3. `JSON.parse(string)`

   * Converte o **texto JSON** em um **objeto JavaScript/TypeScript** que podemos manipular.

> Resumindo: primeiro lemos o arquivo como texto, depois transformamos esse texto em objeto para poder mexer nos campos.


---

### Passo 9: Adicionar scripts no package.json

Depois de transformar o `package.json` em objeto, podemos **adicionar scripts** para facilitar a compilação e execução do projeto.

```ts
// Adiciona scripts desejados
packageJson.scripts = {
  test: 'echo "Error: no test specified" && exit 1', // script de teste padrão
  build: "tsc",                                     // compila TS -> JS
  start: "tsc && node dist/index.js"               // compila e roda o JS gerado
};
````

#### Explicação:

* `test` → comando padrão de teste do npm. Aqui apenas imprime erro porque ainda não temos testes.
* `build` → roda o TypeScript Compiler (`tsc`) para gerar os arquivos JavaScript na pasta `dist`.
* `start` → primeiro compila o TypeScript (`tsc`), depois executa o arquivo principal (`node dist/index.js`).

---

### Passo 10: Salvar o package.json atualizado

Depois de adicionar os scripts, precisamos **escrever o objeto de volta no arquivo**:

```ts
fs.writeFileSync("package.json", JSON.stringify(packageJson, null, 2));
```

* Converte o objeto `packageJson` para **JSON formatado** com indentação de 2 espaços.
* Sobrescreve o `package.json` existente com as novas configurações.

---

### Passo 11: Criar a pasta src

A pasta `src` será onde colocaremos todos os arquivos TypeScript do projeto.

```ts
fs.mkdirSync("src");
```

* Cria a pasta `src` dentro do projeto.
* É aqui que os alunos vão escrever seus arquivos `.ts`.

---

### Passo 12: Criar um arquivo inicial index.ts

Para testar se tudo está funcionando, criamos um arquivo inicial com um **Hello World**.

```ts
fs.writeFileSync("src/index.ts", `console.log("Hello TypeScript!");`);
```

* Cria `index.ts` dentro de `src`.
* Conteúdo: `console.log("Hello TypeScript!")` para imprimir no terminal.

---

### Passo 13: Mensagem de sucesso

Por fim, mostramos uma mensagem no terminal com instruções de como começar a usar o projeto:

```ts
console.log(`\n✅ Projeto "${projectName}" criado com sucesso em "${projectPath}"`);
console.log("👉 Para começar:");
console.log(`cd ../${projectName}`);
console.log("npm run build");
console.log("npm start");
```

* Mostra que o projeto foi criado corretamente.
* Explica ao usuário como entrar na pasta, compilar e rodar o projeto.











