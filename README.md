# Padronização de Códigos e Tecnologias do Grupo de Estudos em Tecnologia Assistiva (GETA)
Este documento é responsável por prover as informações relacionadas à padronização de quais tecnologias são usadas, e dentro delas as formatações padrões que são usadas para as mesmas.

## Tabela de conteúdo
- [Tecnologias](#tecnologias)
  - [Node.js](#node-js)
    - [Instalação](#instalação)
    - [Criando seu primeiro servidor](#criando-seu-primeiro-servidor)
  - [ReactJS e React Native](#reactjs-e-react-native)
    - [Instalação](#instalação-1)
    - [Como criar um projeto?](#como-criar-um-projeto)
- [Padronização de Sintaxe](#padronização-de-sintaxe)
  - [ESLint](#eslint)
  - [Prettier](#prettier)
  - [EditorConfig](#editorconfig)
  - [Como é feito a instalação disto tudo?](#como-é-feito-a-instalação-disto-tudo)
    - [Configuração do ESLint](#configuração-do-eslint)

---

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

#### Criando seu primeiro servidor
Crie uma pasta e dentro dela escreva `yarn init -y` e entre as configurações que pedir, após isso você pode criar um arquivo com nome qualquer, para este exemplo vou usar `server.js`.   

Junto disto eu vou adicionar a primeira depêndencia (e a mais importante em um projeto back-end no Node):   

```yarn add express```
em seguida é só escrever o seguinte código no seu `server.js`:    

```javascript
  const express = require('express') // pega a dependencia que você acabou de instalar
  const app = express() // inicializa a dependencia

  app.get('/', (req, res) => { // seta uma rota onde se recebe um request e um response
    res.send('Hello World') // envia como resposta para quem acessar
  })

  app.listen(3000) // inicia o servidor
```
Com apenas 6 linhas de código é possível ter um servidor de pé com a ajuda da poderosíssima ferramenta [Express](https://github.com/expressjs/express) que da uma robusta interface para lidar com requisições HTTP sem precisar de muitas configurações.

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

---

## Padronização de Sintaxe
É a forma de lidar com a mesma estilização de um código dentro dos arquivos, e para isso temos várias bibliotecas em JavaScript para nos ajudar a criar um padrão para uma empresa, entre elas temos:

### ESLint  
É um linter - ferramentas que analisam o código-fonte para sinalizar erros de programação, bugs, erros estilísticos e construções suspeitas - que analisa o código para rapidamente achar problemas de padronizações e conserta automaticamente com algoritmos chamandos _find and replace_ para que você não precise lidar com erros de sintaxe manualmente.

Dependência | Descrição
--- | ---
[eslint-config-airbnb](https://github.com/airbnb/javascript/tree/master/packages/eslint-config-airbnb) | Este pacote fornece o .eslintrc do Airbnb como uma configuração compartilhada extensível
[eslint-plugin-import](https://github.com/benmosher/eslint-plugin-import) | Plugin do ESLint com regras para ajudar na validação de imports
[eslint-plugin-jsx-a11y](https://github.com/evcohen/eslint-plugin-jsx-a11y) | Verificador estático AST das regras do a11y em elementos JSX
[eslint-plugin-react](https://github.com/yannickcr/eslint-plugin-react) | Regras de linting do ESLint específicas do React
[eslint-plugin-react-native](https://github.com/Intellicode/eslint-plugin-react-native) | Regras de linting do ESLint específicas do React Native
[eslint-import-resolver-babel-plugin-root-import](https://github.com/olalonde/eslint-import-resolver-babel-root-import) | Um resolver da lib _babel-root-import_ para a lib _eslint-plugin-import_

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
**charset** | Controla a formatação de caractere. _Valor padrão: utf-8_
**trim_trailing_whitespace** | Remove espaços em branco precendendo a quebra de linhas. | true
**insert_final_newline** | Assegura que o arquivo termine com uma linha em branco a mais. | true

Veja [aqui](https://gist.github.com/brunodmsi/dab434892e77cebb4b76562edc27782e) o arquivo padrão do EditorConfig.

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

#### Configuração do ESLint
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

9. Você vai ser perguntado se quer instalar os pacotes necessários, digite `Y ou S`

10. Será então instalado todas as dependências necessárias, mas agora você precisará instalar algumas dependências a mais, para isso veja a seção do [Prettier](#prettier) e baixe as que estão referenciadas lá.

11. Você notará que existe na raiz do seu projeto um arquivo chamado `.eslintrc.js`, e nele você irá usar a mesma configuração que está contida neste [gist](https://gist.github.com/brunodmsi/eadd45469a02833ec91df17079999a1d)

12. Para manter a padronização mais fiel ainda, você pode criar na raiz do seu projeto um arquivo chamado `.prettierrc`, e dentro dele inserir este outro [gist](https://gist.github.com/brunodmsi/e78c1fdc0451c18a08a2207041f2e22a) para deixar as aspas simples e ativar a estilização das virgulas apenas em objetos, arrays, etc.