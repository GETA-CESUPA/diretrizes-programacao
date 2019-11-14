# Padronização de Códigos e Tecnologias do Grupo de Estudos em Tecnologia Assistiva (GETA)
Este documento é responsável por prover as informações relacionadas à padronização de quais tecnologias são usadas, e dentro delas as formatações padrões que são usadas para as mesmas.

## Tabela de conteúdo
- Tecnologias [#tecnologias]
  - Node.js [#node-js]
    - Instalação [#instalação-node]
    - Criando seu primeiro servidor [#criando-seu-primeiro-servidor]
  - ReactJS e React Native [#reactjs-e-react-native]
    - Instalação [#instalação-react]
    - Como criar um projeto? [#como-criar-um-projeto]
- Padronização de Sintaxe [#padronização-de-sintaxe]
  - ESLint [#eslint]
  - Prettier [#prettier]
  - EditorConfig [#editorconfig]
  - Style Guide (Airbnb) [#style-guide-airbnb]
  - Como é feito a instalação disto tudo? [#como-é-feito-a-instalação-disto-tudo]

## Tecnologias
A linguagem adotada pelo grupo é JavaScript, por simples motivos como: estar em constante crescimento, estar alinhada com o mercado, bibliotecas e frameworks em constante expansão e melhorias, além de ter uma curva de aprendizado fácil e descomplicada.    

Os frameworks escolhidas como padrão para desenvolvimento foram:

### Node.js
É uma plataforma back-end construída em cima do motor de interpretação de Javascript do Chrome, chamado V8 que, que permite executarmos scripts Javascript no lado do servidor.  

Agora, de forma fácil, o NodeJS te permite utilizar Javascript do lado do servidor, assim você pode acessar bancos de dados, fornecer dados através de uma API ou realizar qualquer outra operação de linguagens back-end como PHP e Ruby.   

É extremamente simples de ser usado, é possível rodar um servidor completamente funcional com apenas uma página de códigos. Existe DIVERSAS bibliotecas para expandir o uso e possibilitar com que o desenvolvedor foque apenas na regra de negócio da sua aplicação, e instalar libs de terceiros para reuso.


### Instalação
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
  - Usando `npx (este é um package-runner que já vem junto da instalação do NPM` rode `npx create-react-app <nome_do_projeto>`
- React.js
  - Usando `yarn` rode `yarn create react-app <nome_do_projeto>`

---

## Padronização de Sintaxe
É a forma de lidar com a mesma estilização de um código dentro dos arquivos, e para isso temos várias bibliotecas em JavaScript para nos ajudar a criar um padrão para uma empresa, entre elas temos:

### ESLint  
É um linter - ferramentas que analisam o código-fonte para sinalizar erros de programação, bugs, erros estilísticos e construções suspeitas - que analisa o código para rapidamente achar problemas de padronizações e conserta automaticamente com algoritmos chamandos _find and replace_ para que você não precise lidar com erros de sintaxe manualmente.

---

### Prettier 
O Prettier aplica um estilo de código consistente (ou seja, a formatação do código que não afeta a árvore de sintaxe) em toda a sua base de código, porque desconsidera o estilo original, analisando-o e reimprimindo a sintaxe analisado com suas próprias regras que assumem o comprimento máximo da linha em conta, agrupando o código quando necessário.
Tem a possibilidade de uma alta integração com linters (como o próprio ESLint) com exemplos de:

| Depêndencia | Descrição |
| --- | --- |
| **[eslint-config-prettier](https://github.com/prettier/eslint-config-prettier)** | Desliga todas as regras que são desnecessárias ou podem conflitar com o Prettier. |
| **[eslint-plugin-prettier](https://github.com/prettier/eslint-plugin-prettier)** | É um plugin que adiciona uma regra que formata o conteúdo usando Prettier |

---

### EditorConfig
Para ser usada diretamente no VSCode, consta com algumas configurações que ajudam a manter uma consistência para múltiplos desenvolvedores trabalhando em um mesmo projeto independente da sua IDE. A configuração padrão usada pelos projetos do GETA são:

Configuração | Descrição
--- | ---
**root** | Propriedade especial que deve ser especificado no topo de cada arquivo. _Valor padrão: true_
**indent_style** | Número usado para definir colunas e o nível de identação. _Valor padrão: 2_
**indent_size** | Especifica em que formato a identação é feita, se é em "tab" ou "space". _Valor padrão: space_
**charset** | Controla a formatação de caractere. _Valor padrão: utf-8_
**trim_trailing_whitespace** | Remove espaços em branco precendendo a quebra de linhas. _Valor padrão: true_
**insert_final_newline** | Assegura que o arquivo termine com uma linha em branco a mais. _Valor padrão: true_

Veja [aqui](https://gist.github.com/brunodmsi/dab434892e77cebb4b76562edc27782e) o arquivo padrão do EditorConfig.

---

### Style Guide (Airbnb)
Esta é a parte final sobre a padronização de sintaxe, mas não menos importante. Style guides são sets de padrões de como os códigos devem ser escritos e organizados, e o Airbnb tem uns dos mais populares styles guides de JavaScript.

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

