<br />
<p align="center">
  <a href="http://geta.tk">
    <img src="https://i.imgur.com/hXaAYMr.png" alt="Logo" width="450">
  </a>

  <h2 align="center">Padronização de Códigos e Tecnologias do GETA</h2>
</p>

## Tabela de conteúdo
- [Por que padronização é importante?](#por-que-padronização-é-importante)
- [Tecnologias](#tecnologias)
  - [Node.js](#node-js)
    - [Instalação](#instalação)
    - [Sucrase](#sucrase)
    - [Criando seu primeiro servidor](#criando-seu-primeiro-servidor)
    - [Nodemon](#nodemon)
    - [Rodando Node com Sucrase](#rodando-node-com-sucrase)
  - [ReactJS e React Native](#reactjs-e-react-native)
    - [Instalação](#instalação-1)
    - [Como criar um projeto?](#como-criar-um-projeto)
- [Visual Studio Code (VSCode)](#visual-studio-code-vscode)
- [Padronização de Sintaxe](#padronização-de-sintaxe)
  - [ESLint](#eslint)
  - [Prettier](#prettier)
  - [EditorConfig](#editorconfig)
  - [Como é feito a instalação disto tudo?](#como-é-feito-a-instalação-disto-tudo)
    - [Configuração do ESLint e Prettier](#configuração-do-eslint-e-prettier)
- [Estrutura de Arquivos](#estrutura-de-arquivos)
  - [Node.js](#nodejs-1)
  - [ReactJS e React Native](#reactjs-e-react-native-1)
- [Contribuições](#contribuições)
- [Autoria](#autoria)

---

## Por que padronização é importante?
Sem uma padronização, os desenvolvedores envolvidos acabam realizando tarefas como acreditam ser melhor, tornando o **ambiente caótico** pela falta de controle. Então quando o caos se instala, os devs demoram mais tempo para resolver problemas para desenvolver e também para corrigir erros, pois não há uma **diretriz única**, levando cada profissional a fazer da forma que acredita ser correta e quem arca com os custos destes desperdícios e fica com um legado caótico é o cliente solicitante do desenvolvimento.   

Com o ambiente padronizado e documentado, todos os desenvolvedores podem dar suporte a qualquer sistema, pois existirá um padrão de desenvolvimento. Podemos fazer uma analogia aos idiomas, nessa situação, todos da equipe falarão a mesma língua sem necessidade de traduções para compreender o que está escrito no código.

## Tecnologias
A linguagem adotada pelo grupo é JavaScript, por simples motivos como: estar em constante crescimento, estar alinhada com o mercado, bibliotecas e frameworks em constante expansão e melhorias, além de ter uma curva de aprendizado fácil e descomplicada.    

Os frameworks escolhidas como padrão para desenvolvimento foram:

### Node.js
É uma plataforma back-end construída em cima do motor de interpretação de Javascript do Chrome, chamado V8 que, que permite executarmos scripts Javascript no lado do servidor.  

Agora, de forma fácil, o NodeJS te permite utilizar Javascript do lado do servidor, assim você pode acessar bancos de dados, fornecer dados através de uma API ou realizar qualquer outra operação de linguagens back-end como PHP e Ruby.   

É extremamente simples de ser usado, é possível rodar um servidor completamente funcional com apenas uma página de códigos. Existe DIVERSAS bibliotecas para expandir o uso e possibilitar com que o desenvolvedor foque apenas na regra de negócio da sua aplicação, e instalar libs de terceiros para reuso.


#### Instalação dos pacotes
A instalação dessa plataforma é necessária tanto para a parte back-end quanto para a front-end (que será discutida logo no próximo tópico)
- Para Windows é bem simples, basta baixar o Node do link abaixo, já vem incluso nele o NPM (que é o Package Manager do Node)
  - [Node v12.13.0](https://nodejs.org/dist/v12.13.0/node-v12.13.0-x64.msi)
- Para Ubuntu/Debian, você pode rodar o seguinte comando: (talvez haja a necessidade de adicionar `sudo` no começo):
  - `apt-get install node`
  - `apt-get install npm`
  - Siga esta ordem, após isso você pode checar se a instalação foi um sucesso rodando os comandos:
    - `node -v`
      - Resposta esperada `v12.13.0`
    - `npm -v`
      - Resposta esperada `v6.9.0 (ou similar)`
- É recomendado que você instale outro package manager disponível para Node que tem uma estabilidade melhor, facilidade de uso maior e uma velocidade aprimorada, este é o `yarn`, você pode instalar ele usando o próprio `npm`:
  - `npm install -g yarn`
  - Agora você pode usar o `yarn` para instalar suas dependências ao invés do `npm`

---

#### Sucrase
O Sucrase é um compilador de JS/TS que substitui o Babel (_compilador padrão do JavaScript_), e os motivos para isso são 2: o Sucrase é **mais rápido** que o Babel por usar versões mais recentes e otimizadas do JavaScript, ao contrário do Babel que usa versões muito antigas, outro motivo seria que por ser uma versão mais recente do JavaScript, a sintaxe usada também é mais recente fazendo com que o código fique similar aos aliados na stack de JS (React JS e Native), isso faz com que a identificação com os diferentes frameworks seja mais fácil.   

O Babel usa a sintaxe de **CommonJS** que utiliza o modelo _require/exports_, já o Sucrase utiliza o mais recente nomeado de **EcmaScript modules** que utiliza _import/exports_. Para botar na prática, olhe este exemplo de como os dois são usados para um mesmo código
+ **CommonJS (Babel)**
```javascript
// routes.js
const { Router } = require('express');
const routes = new Router();
module.exports = routes;

// server.js
const express = require('express');
const app = express();
const routes = require('./routes');
app.use(routes);
app.listen(8080);
```
+ **EcmaScript modules (Sucrase)**
```javascript
// routes.js
import { Router } from 'express';
const routes = new Router();
export default routes;

// server.js
import express from 'express';
import routes from './routes';

const app = express();
app.use(routes);
app.listen(8080);
```
Bem simples, né? Para rodar um código usando sucrase existem umas configurações bem básicas de serem feitas, tanto para rodar em ambiente de desenvolvedor (ver na seção sobre [Nodemon](#nodemon)) quanto em ambiente de [produção](#rodando-em-produção).

---

#### Criando seu primeiro servidor
Crie uma pasta e dentro dela escreva `yarn init -y` e entre as configurações que pedir, após isso você pode criar um arquivo com nome qualquer, para este exemplo vou usar `server.js`.   

Junto disto eu vou adicionar a primeira depêndencia (e a mais importante em um projeto back-end no Node):   

```yarn add express```
em seguida é só escrever o seguinte código no seu `server.js`:    

```javascript
  import express from 'express'; // pega a dependencia que você acabou de instalar
  const app = express() // inicializa a dependencia

  app.get('/', (req, res) => { // seta uma rota onde se recebe um request e um response
    res.send('Hello World') // envia como resposta para quem acessar
  })

  app.listen(3000) // inicia o servidor
```
Com apenas 6 linhas de código é possível ter um servidor de pé com a ajuda da poderosíssima ferramenta [Express](https://github.com/expressjs/express) que da uma robusta interface para lidar com requisições HTTP sem precisar de muitas configurações.

Veja as seções de [Nodemon](#nodemon) e [Rodando Node com Sucrase](#rodando-node-com-sucrase) para aprender à rodar um servidor em Node usando esta sintaxe.

---

#### Nodemon
É uma dependência de desenvolvimento que vai monitorar por qualquer mudança no seu código-fonte e vai automaticamente reiniciar seu servidor para você já poder testar a mudança direto. Para ser instalado é bem simples, basta rodar
```sh
yarn add nodemon -D 
```

este `-D` indica que é para ser adicionado como um dependência de **desenvolvimento**, e para este ser usado junto com o  **Sucrase** é necessário fazer uma simples configuração, basta criar um arquivo na raiz do projeto com o nome de `nodemon.json` e inserir a seguinte configuração:
```json
{
  "execMap": {
    "js": "sucrase-node"
  }
}
```
Isto é necessário pois por padrão o Nodemon executa rodando o Babel como compilador, mas passando esta regra ele entende que o compilador que será usado para o projeto é o Sucrase.  

E agora, você pode adicionar no seu `package.json` a seção de scripts onde você irá inserir um scriptzinho para rodar o seu nodemon (isto não é necessário mas é indicado por usabilidade):
```json
{
  "scripts": {
    "dev": "nodemon src/server.js"
  },
}
```
E agora no seu terminal você pode rodar `yarn dev` e ele vai reconhecer *dev* como se fosse o comando de execução do nodemon `nodemon src/server.js`, isso facilita na hora de rodar o projeto (novamente, não é necessário, porém indicado). 

---

#### Rodando Node com Sucrase
Normalmente, você rodaria os projetos com Node (em produção) usando o comando `node src/server.js`, mas usando o compilador Sucrase isto muda um pouco, e iremos criar dois scripts (que nem fizemos no [Nodemon](#nodemon)), um será responsável por fazer o _build_ do código e transformar ele para __imports__ e o outro apenas para rodar o código buildado.  

Então, no arquivo `package.json`, iremos fazer mais umas adições na parte de **scripts**:
```json
{
  "scripts": {
      "build": "sucrase ./src -d ./dist --transforms imports",
      "start": "node dist/server.js"
  }
}
```

A ordem de execução é primeiro executar `yarn build` que fará toda a tradução do código usando sucrase, e salvando esta tradução numa nova pasta na raiz do projeto chamada _dist/_, após isso executar `yarn start` para rodar o `server.js` de dentro da pasta do **dist**, e pronto, seu código em Sucrase agora está rodando normalmente.

---

### ReactJS e React Native
Gerenciado pelo Facebook, Instagram e uma grande comunidade de empresas e desenvolvedores, o React é um dos frameworks mais procurados. De acordo com a análise JavaScript, o React está sendo utilizado em sites como Walmart, Netflix e Airbnb.    

Ele oferece websites com alto desempenho e escalabilidade. React garante até reusabilidade de código, permitindo aos desenvolvedores otimizar seu tempo na criação de códigos.    

Além disso, ele é simples por causa da sua abordagem por componentização, o ciclo de vida bem definido e o uso simplificado do JavaScript torna o React muito fácil de aprender. Tem alto suporte para data binding, ou seja, usa ligação de dados unidirecional e uma arquitetura de aplicação chamada Flux, que controla o fluxo de dados para os componentes por meio de um ponto de controlo – o dispatcher. É mais fácil depurar componentes independentes de grandes aplicações React.js.    

Lembrando que são dois frameworks diferentes (apesar de muito similares), sendo um específico para web (ReactJS) e o outro para aplicações mobile (React Native) tanto para o sistema operacional Android e iOS.

#### Instalação
- React Native
  - Usando `npm` rode o comando `npm install -g react-native-cli`
  - Usando `yarn` rode o comando `yarn add global react-native-cli`
- React.js
  - Este já vem instalado junto com a instalação do NPM

#### Como criar um projeto?
- React Native
  - Usando `npx (este é um package-runner que já vem junto da instalação do NPM)` rode `npx create-react-app <nome_do_projeto>`
- React.js
  - Usando `yarn` rode `yarn create react-app <nome_do_projeto>`

## Visual Studio Code (VSCode)
O [VSCode](https://github.com/microsoft/vscode) é um editor de código-fonte desenvolvido pela Microsoft para Windows, macOS e Linux. Ele inclui suporte para depuração, controle Git incorporado, realce de sintaxe, complementação inteligente de código, snippets e refatoração de código. Você pode baixa-lo [aqui](https://code.visualstudio.com/download).   
Nele há algumas configurações de preparação para as regras que vão entrar na próxima seção de [Padronização de Sintaxe](#padronização-de-sintaxe), a tabela abaixo mostra as extensões que estão disponíveis e que vão nos ajudar durante o desenvolvimento de todos os projetos de diferentes formas.

Extensão | Descrição | Utilidade | _Obrigatório_ 
--- | --- | --- | ---
**[ESLint](https://marketplace.visualstudio.com/items?itemName=dbaeumer.vscode-eslint)** | Integra o ESLint com o VSCode | Alta | _Sim_
**[Prettier](https://marketplace.visualstudio.com/items?itemName=esbenp.prettier-vscode)** | Formatador de código | Alta | _Sim_
**[EditorConfig](https://marketplace.visualstudio.com/items?itemName=EditorConfig.EditorConfig)** | Sobrescreve arquivos com configs achadas em um `.editorconfig` | Alta | _Sim_
**[Dracula Official](https://marketplace.visualstudio.com/items?itemName=dracula-theme.theme-dracula)** | Tema escuro para a IDE, _preferência do autor_ | Baixa | _Não_
**[Color Highlight](https://marketplace.visualstudio.com/items?itemName=naumovs.color-highlight)** | Da um preview das cores sejam elas em hex, rgba. | Alta | _Não_ 
**[vscode-icons](https://marketplace.visualstudio.com/items?itemName=vscode-icons-team.vscode-icons)** | Icones para o VSCode | Baixa | _Não_
**Rocketseat [React JS](https://marketplace.visualstudio.com/items?itemName=rocketseat.RocketseatReactJS) e [Native](https://marketplace.visualstudio.com/items?itemName=rocketseat.RocketseatReactNative)** | Atalhos para construção dos componentes | Média | _Não_
**[vscode-styled-components](https://marketplace.visualstudio.com/items?itemName=jpoissonnier.vscode-styled-components)** | Destaque de sintaxe para a biblioteca de **styled-components** | Média | _Não_

Além das extensões para melhor usabilidade da IDE, é possível no próprio VSCode fazer configurações de preferências de estilização, para saber mais sobre, visite a [documentação oficial](https://vscode.readthedocs.io/en/latest/getstarted/settings/) do VSCode para essas configurações. Caso você não se sinta com paciência para configurar à mão, você pode sempre usar a mesma config do autor, encontrada neste [gist](https://gist.github.com/brunodmsi/9443fa2fcef1cb215b043259c1311105).

## Padronização de Sintaxe
É a forma de lidar com a mesma estilização de um código dentro dos arquivos, e para isso temos várias bibliotecas em JavaScript para nos ajudar a criar um padrão para uma empresa, entre elas temos:

### ESLint  
É um linter - ferramentas que analisam o código-fonte para sinalizar erros de programação, bugs, erros estilísticos e construções suspeitas - que analisa o código para rapidamente achar problemas de padronizações e conserta automaticamente com algoritmos chamandos _find and replace_ para que você não precise lidar com erros de sintaxe manualmente.

Dependência | Descrição
--- | ---
**[eslint-config-airbnb](https://github.com/airbnb/javascript/tree/master/packages/eslint-config-airbnb)** | Este pacote fornece o .eslintrc do Airbnb como uma configuração compartilhada extensível
**[eslint-plugin-import](https://github.com/benmosher/eslint-plugin-import)** | Plugin do ESLint com regras para ajudar na validação de imports
**[eslint-plugin-jsx-a11y](https://github.com/evcohen/eslint-plugin-jsx-a11y)** | Verificador estático AST das regras do a11y em elementos JSX
**[eslint-plugin-react](https://github.com/yannickcr/eslint-plugin-react)** | Regras de linting do ESLint específicas do React
**[eslint-plugin-react-native](https://github.com/Intellicode/eslint-plugin-react-native)** | Regras de linting do ESLint específicas do React Native
**[eslint-import-resolver-babel-plugin-root-import](https://github.com/olalonde/eslint-import-resolver-babel-root-import)** | Um resolver da lib _babel-root-import_ para a lib _eslint-plugin-import_

---

### Prettier 
O Prettier aplica um estilo de código consistente (ou seja, a formatação do código que não afeta a árvore de sintaxe) em toda a sua base de código, porque desconsidera o estilo original, analisando-o e reimprimindo a sintaxe analisado com suas próprias regras que assumem o comprimento máximo da linha em conta, agrupando o código quando necessário.
Tem a possibilidade de uma alta integração com linters (como o próprio ESLint) com exemplos de:

| Depêndencia | Descrição |
| --- | --- |
| **[prettier](https://github.com/prettier/prettier)** | Repositório do próprio no Github |
| **[eslint-config-prettier](https://github.com/prettier/eslint-config-prettier)** | Desativa todas as regras que são desnecessárias ou que podem dar conflito com o Prettier |
| **[eslint-plugin-prettier](https://github.com/prettier/eslint-plugin-prettier)** | Roda o Prettier como uma regra do ESLint |

---

### EditorConfig
Para ser usada diretamente no VSCode, consta com algumas configurações que ajudam a manter uma consistência para múltiplos desenvolvedores trabalhando em um mesmo projeto independente da sua IDE. A configuração padrão usada pelos projetos do GETA são:

Configuração | Descrição | Valor usado
--- | --- | ---
**root** | Propriedade especial que deve ser especificado no topo de cada arquivo. | true
**indent_style** | Número usado para definir colunas e o nível de identação. | 2 
**indent_size** | Especifica em que formato a identação é feita, se é em "tab" ou "space". | space
**charset** | Controla a formatação de caractere. | utf-8
**trim_trailing_whitespace** | Remove espaços em branco precendendo a quebra de linhas. | true
**insert_final_newline** | Assegura que o arquivo termine com uma linha em branco a mais. | true

Veja [aqui](https://gist.github.com/brunodmsi/dab434892e77cebb4b76562edc27782e) o arquivo padrão do EditorConfig indicado pelo autor. Você pode ver também a página oficial do [EditorConfig](https://editorconfig.org/) para ver todas as opções disponíveis

---

### Como é feito a instalação disto tudo?
Para começar, você já deve ter instalado antes as seguintes extensões no VSCode: `ESLint, Prettier e EditorConfig`.  
Instale a seguinte dependência como uma de desenvolvimento usando `npm`:
```sh
npm install --save-dev eslint
```
ou você pode usar `yarn` (que é o mais recomendado por ser mais eficaz):
```
yarn add eslint -D
```

Após finalizada a instalação, você pode fazer a configuração, começando-a com o comando:
```sh
yarn eslint --init
```
Irá aparecer uma tela perguntando como você gostaria de usar o ESLint, e nesta você irá selecionar a última opção usando a seta do teclado, a última é a escolhida pois supre todas as nossas necessidades para fazer o ciclo completo de checar a sintaxe, achar os problemas e reforçar a estilização do código:
```sh
? How would you like to use ESLint?
  To check syntax only
  To check syntax and find problems
> To check syntax, find problems, and enforce code style
```
Pressione `ENTER` e selecione a primeira opção das próximas que aparecerem
```JavaScript modules (import/export)```

e é após esta entrada que vai depender para qual biblioteca você está configurando o **ESLint** 

para entrar na configuração execute o comando `yarn eslint --init`

#### Configuração do ESLint e Prettier
1. Na primeira pergunta sobre como usar o ESLint selecione `To check syntax, find problems, and enforce code style`;
2. Seleciona que usa os modulos nativos de JavaScript: `JavaScript modules (import/export)`;
3. Which framework does your project use? (Use as setas do teclado)
  - React.js e React Native
    + Selecione `React`
  - Node.js
    + Selecione `None of these`
4. Insira `N` para a pergunta se o projeto usa TypeScript;
5. Onde seu código roda? *(Use espaço para selecionar, setas para navegar e ENTER para confirmar)*
  - React.js 
    + Selecione `Browser`
  - Node.js
    + Selecione `Node`
  - React Native
    + Deixe os dois deselecionados e confirme
6. Selecione `Use a popular style guide` para definir o estilo do projeto;
7. Selecione o style guide do Airbnb (deve ser o primeiro);
8. E pro formato de arquivo de configuração do ESLint, selecione JavaScript;
9. Você vai ser perguntado se quer instalar os pacotes necessários, digite `Y ou S`\
10. Será então instalado todas as dependências necessárias, mas agora você precisará instalar algumas dependências a mais, para isso veja a seção do [Prettier](#prettier) e baixe as que estão referenciadas lá.
11. Você notará que existe na raiz do seu projeto um arquivo chamado `.eslintrc.js`, e nele você irá usar a mesma configuração que está contida neste [gist](https://gist.github.com/brunodmsi/eadd45469a02833ec91df17079999a1d)
12. Para manter a padronização mais fiel ainda, você pode criar na raiz do seu projeto um arquivo chamado `.prettierrc`, e dentro dele inserir este outro [gist](https://gist.github.com/brunodmsi/e78c1fdc0451c18a08a2207041f2e22a) para deixar as aspas simples e ativar a estilização das virgulas apenas em objetos, arrays, etc.

## Estrutura de Arquivos
Além de todas essas padronizações, também seguimos uma ordem de estruturação dos arquivos e pastas dentro dos projetos, ele varia um pouco de acordo com o framework que está usado para o desenvolvimento, mas a ideia permanece a mesma entre as mesmas.

### Node.js
```
├── src/
│   ├── app/
│   │   └── controllers
│   │   └── middlewares
│   │   └── models
│   ├── config/
│   ├── database/
│   │   └── migrations/
│   │   └── seeds/
│   │   └── index.js
│   ├── app.js
│   ├── routes.js
│   └── server.js
├── .editorconfig
├── .eslintrc.js
├── .gitignore
├── .env.example
├── .prettierrc
├── .sequelizerc
├── nodemon.json
├── package.json
└── README.md
```

O que significa?
+ **src** - Diretório contendo todos os arquivos da aplicação, é criado um diretório src para que o código da aplicação possa ser isolado em um diretório e facilmente portado para outros projetos, se necessário;
  + **app** - Diretório que tem todas as regras de negócio da nossa aplicação;
    + **controllers** - Diretório onde ficam os controladores da aplicação, é pura regra de negócio que vai controlar tudo o que precisa ser processado e retornado em uma requisição;
    + **middlewares** - Diretório onde é possível fazer mudanças nos objetos de solicitação e resposta, encerrar um ciclo ou chamar um próximo middleware na pilha chamando a função `next()`;
    + **models** -  Diretório onde está os modelos das tabelas do nosso banco de dados;
  + **config** - Diretório para guardar os arquivos de configuração da aplicação, por exemplo, a configuração do banco de dados ou de autenticação (incluido apenas os dados que serão usado);
  + **database** - Diretório onde está todas as configurações mais específicas do banco de dados;
    + **migrations** - Migrations é a pasta onde se tem todas as definições dos campos e tipos de cada tabela e coluna do banco de dados;
    + **seeds** - Seeds tem todas as configurações para automaticamente encher certas tabelas com alguma informação;
    + **index.js** - Relaciona os modelos (da pasta _models_) com o próprio banco de dados, inicializa cada um e inicializa suas relationships também;
  + **app.js** - Arquivo que contém todas as configurações básicas e essenciais para o Express;
  + **routes.js** - Arquivo que contém todas as rotas da aplicação e para onde elas apontam.
  + **server.js** - Arquivo que inicializa o servidor passando uma porta específica;
+ **package.json** - Diferente dos projetos comuns, esse arquivo tem as configurações necessárias para a publicação do Template no NPM, para saber mais sobre isso veja a seção abaixo.
+ **.eslintrc.js** - Arquivo de configuração do ESLint, é nele que são inseridas as regras e configurações de Linting do projeto, tal como a configuração do Resolver para o Babel Plugin Root Import e configuração da variável global __DEV__;
+ **.editorconfig** - Arquivo destinado à configuração do plugin Editor Config, que padroniza algumas configurações para o editor em diferentes ambientes;
+ **.gitignore** - Arquivo destinado à definir quais são os arquivos/pastas que serão ignorados pelo Git ao enviar um push;
+ **.nodemon.json** - Arquivo destinado à configuração do Sucrase com o Nodemon;
+ **.sequelizerc** - Arquivo destinado à configuração da localização das pastas que são usadas pelo [Sequelize](https://github.com/sequelize/sequelize);
+ **.prettierrc** - Arquivo destinado à configurações básicas de como o Prettier deve se comportar em relação à configurações específicas;
+ **.env.example** - Arquivo cópia do `.env` que é o arquivo responsável por guardar todas as variáveis ambientes da aplicação (como usuario e senha do banco de dados, DSN do Sentry, etc);
---

### ReactJS e React Native
```
├── public/
│   ├── index.html
├── src/
│   ├── assets/
│   ├── pages/
│   │   └── Main/
│   │       └── index.js
│   │       └── styles.js
│   ├── config/
│   │       └── ReactotronConfig.js
│   ├── components/
│   ├── routes/
│   ├── styles/
│   ├── store/
│   ├── services/
│   │   └── api.js
│   ├── App.js
│   ├── index.js
├── .editorconfig
├── .eslintrc.js
├── .gitignore
├── .env.example
├── jsconfig.json
├── .config-overrides
├── package.json
├── yarn.lock 
└── README.md
```
---

## Contribuições
Achou algum erro na documentação, ou gostaria de adicionar alguma informação para que fique mais completinho? Você é livre para dar o `git clone` na sua máquina, fazer essas alterações e fazer um push request para gente avaliar e você se tornar um contribuidor!

## Autoria
Documentação escrita e desenvolvida pelo integrante [Bruno De Masi](https://github.com/brunodmsi).