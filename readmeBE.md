# Backend Lincar
Este guia considera o uso do Lubuntu 19.04, mas este serve para qualquer versão atual do Ubuntu.
Nesse README há dois tutoriais: o primeiro de como [iniciar o projeto do zero](#tutorial-para-criação-do-ambiente-de-desenvolvimento-do-zero) e o segundo de [como rodar o projeto já existente](#tutorial-para-executar-o-projeto-desse-git).

## Tutorial para criação do ambiente de desenvolvimento do zero
Nesta seção será mostrado como criar o ambiente de desenvolvimento do zero para o firebase que é o backend que estamos utilizado. Será utilizado TypeScript no exemplo.
### Instalação das dependências globais
Em primeiro lugar é necessário instalar o NodeJS, para isso utilizaremos o versionador do Node chamado NVM.
Para isso:
```bash
sudo wget -qO- https://raw.githubusercontent.com/nvm-sh/nvm/v0.35.0/install.sh | bash
```
Após a execução do script feche e abra o terminal. Verifique o nvm foi instalado corretamente.
Depois, execute o comando abaixo para instalar o NodeJS utilizado nesse projeto:
```bash
nvm install 10.16.3
```
Pronto, NodeJS e o NVM estarão instalados em sua máquina juntamente com o gerenciador de pacote NPM.
Em seguida será necessário instalar as depêndencias do firebase.
```bash
npm install -g firebase-tools
```
### Criação de um novo projeto
Depois de instalado as dependências iremos criar um novo projeto firebase.
O comando abaixo deve ser executado primeiramente para o firebase se conectar com sua conta Google Developer.
```bash
firebase login
```
E depois criamos o projeto com:
```bash
firebase init
```
Selecione a opção *Functions* com espaço depois aperte enter para continuar. Na próxima tela selecione *Use an existing project* e escolhar o projeto que deseja adicionar linkar ao seu diretório. Selecione TypeScript. Negue a utilização do TSLint como parser, pois utilizaremos o ESLint. Concorde com *Y* as próximas perguntas. O CLI irá instalar as dependências e pronto você tem um novo projeto firebase em sua máquina. :smile:

### Configurar os tests e cross-env
Para instalar as ferramentas de testes e ambiente, execute:
```bash
npm install -D jest @types/jest cross-env
```
Após a instalar execute:
```bash
npx jest --init
```
Digite *Y* e selecione com enter -> *node* -> *N* -> *N*
O jest estará instalado após esses passos.

No arquivo *tsconfig.json* dentro de functions faça:
```javascript
//tsconfig.json
{
  // ...
  "compilerOptions": {
    // ...
    "types": ["jest"],
    //...
  }
  /...
}
```
No arquivo *jest.config.js* faça:
```javascript
//jest.config.js
module.exports = { 
  // ...
  moduleFileExtensions: [
    "js",
    "ts",
    "tsx",
    "node"
  ],
  testRegex: "(/__tests__/.*|\\.(test|spec))\\.(ts|tsx|js)$",
  transform: {
    ".(ts|tsx)": "ts-jest"
  },
  //...
}
```
### Configuração do ESLint
Para configurar o ESLint precisaremos rodar os seguintes comandos dentro da pasta *functions* do projeto.
```bash
npm install --save-dev eslint @typescript-eslint/parser @typescript-eslint/eslint-plugin
```
Após a instalação das dependências, rode:
```bash
npx eslint --init
```
Selecione com enter *To check syntax, find problems, and enforce code style* -> *JavaScript modules (import/export)* -> *None of these* -> *Y* -> Desmarque todas opções com space -> *Use a popular style guide* -> *Standard (https://github.com/standard/standard)* -> *JavaScript* -> Selecione *Y* para instalar as novas dependências

Após a instalação das dependências abra o arquivo *.eeslintrc.js* adiciona na key *extends* o plugin:
```javascript
//.eslintrc.js
module.exports = {
    //...
    env: {
      //...
      node:true,
      jest:true
      // ...
    },
    //...
    extends: [
        "plugin:@typescript-eslint/recommended",
        //...
    ]
    //...
}
```
O arquivo por completo deve ficar parecedio com isso:
```javascript
//.eslintrc.js
module.exports = {
  env: {
    es6: true,
    node:true,
    jest:true
  },
  extends: [
    'plugin:@typescript-eslint/recommended',
    'standard'
  ],
  globals: {
    Atomics: 'readonly',
    SharedArrayBuffer: 'readonly'
  },
  parser: '@typescript-eslint/parser',
  parserOptions: {
    ecmaVersion: 2018,
    sourceType: 'module'
  },
  plugins: [
    '@typescript-eslint'
  ],
  rules: {
  }
}
```
Pronto o eslint já está configurado para Typescript

### Configuração do Prettier (Opcional)
O prettier é um corretor de texto automático para typescript, para instalar faça:
```bash
npm install -D eslint-config-prettier eslint-plugin-prettier prettier
```
Após isso vá no arquivo *.eslintrc.js* e coloque:
```javascript
module.exports = {
  //...
  extends: [
    //...
    'prettier/@typescript-eslint'
    //...
  ],
  // ...
}
```
### Para configurar o VSCode (opcional)
Para configurar o ESLint no VSCode pressione *CTRL+,* vá no canto superior esquerdo e vá no ícone que tem escrito *Open Settings* irá abrir o arquivo *settings.json* do VSCode, nele adicione as linhas abaixo.
```json
//settings.json
{
    // ...
    "eslint.autoFixOnSave": true,
    "eslint.validate": [
        {"language": "typescript","autoFix": true},
        {"language": "typescriptreact","autoFix": true}
    ]
    //...
}
```
Pronto agora o Visual Studio Code está configurado para o ESLint.

_É RECOMENDADO_ instalar as extensões Prettier e ESLint no VSCode. Basta apertar *CTRL+SHIFT+X* e pesquisar por essas extensões e instalar.

## Tutorial para executar o projeto desse git
Depois de instalado as [dependências globais](#instalação-das-dependências-globais) iremos instalar as depêndencias desse projeto.
É necessário realizar o login no firebase.
```bash
firebase login
```
Depois deve ser aberto a pasta functions e executar:
```bash
npm install
```
Após a execução do comando será instalado as dependências do projeto e estará pronto para rodar.

## Registrar credenciais
Para utilizar todos os serviços do Google Cloud localmente é necessário você criar as credenciais do projeto ou já usar uma existente. Para isso siga as etapas:
* Abra o [painel de contas de serviço](https://console.cloud.google.com/iam-admin/serviceaccounts) do Console do Google Cloud.
* Verifique se a conta de serviço padrão do App Engine está selecionada e use o menu de opções à direita para selecionar Criar chave.
* Quando solicitado, selecione JSON para o tipo de chave e clique em Criar.
* Ao baixar o arquivo coloque ele na raiz desse projeto
* Na raiz do projeto defina suas credenciais padrão do Google para apontar para a chave salva:
```bash
export GOOGLE_APPLICATION_CREDENTIALS="`pwd`/<NOME-DO-ARQUIVO>.json"
firebase emulators:start
```
