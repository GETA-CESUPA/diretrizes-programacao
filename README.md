# Padronização de Códigos e Tecnologias do Grupo de Estudos em Tecnologia Assistiva (GETA)
Este documento é responsável por prover as informações relacionadas à padronização de quais tecnologias são usadas, e dentro delas as formatações padrões que são usadas para as mesmas.

## Tecnologias
A linguagem adotada pelo grupo é JavaScript, por simples motivos como: estar em constante crescimento, estar alinhada com o mercado, bibliotecas e frameworks em constante expansão e melhorias, além de ter uma curva de aprendizado fácil e descomplicada.
Os frameworks escolhidas como padrão para desenvolvimento foram:

### ReactJS e React Native
Gerenciado pelo Facebook, Instagram e uma grande comunidade de empresas e desenvolvedores, o React é um dos frameworks mais procurados. De acordo com a análise JavaScript, o React está sendo utilizado em sites como Walmart, Netflix e Airbnb.
Ele oferece websites com alto desempenho e escalabilidade. React garante até reusabilidade de código, permitindo aos desenvolvedores otimizar seu tempo na criação de códigos. Também otimiza o SEO da sua aplicação web. Embora o conceito de React ainda seja novo, ele está amadurecendo rapidamente, e o Facebook planeja continuar investindo nele.
Além disso, ele é simples por causa da sua abordagem por componentização, o ciclo de vida bem definido e o uso simplificado do JavaScript torna o React muito fácil de aprender. Tem alto suporte para data binding, ou seja, usa ligação de dados unidirecional e uma arquitetura de aplicação chamada Flux, que controla o fluxo de dados para os componentes por meio de um ponto de controlo – o dispatcher. É mais fácil depurar componentes independentes de grandes aplicações React.js.
Lembrando que são dois frameworks diferentes (apesar de muito similares), sendo um específico para web (ReactJS) e o outro para aplicações mobile (React Native) tanto para o sistema operacional Android e iOS.

### Node.js
É uma plataforma back-end construída em cima do motor de interpretação de Javascript do Chrome, chamado V8 que, por sua vez, foi construído utilizando C++, que permite executarmos scripts Javascript no lado do servidor.
Agora, de forma fácil, o NodeJS te permite utilizar Javascript do lado do servidor, assim você pode acessar bancos de dados, fornecer dados através de uma API ou realizar qualquer outra operação de linguagens back-end como PHP e Ruby.
É extremamente simples de ser usado, é possível rodar um servidor completamente funcional com apenas uma página de códigos. Existe DIVERSAS bibliotecas para expandir o uso e possibilitar com que o desenvolvedor foque apenas na regra de negócio da sua aplicação, e instalar libs de terceiros para reuso.

Exemplo da simplicidade de criar um servidor:
```javascript
  const express = require('express')
  const app = express()

  app.get('/', (req, res) => {
    res.send('Hello World')
  })

  app.listen(3000)
```
Com apenas 6 linhas de código é possível ter um servidor de pé com a ajuda da poderosíssima ferramenta [Express](https://github.com/expressjs/express) que da uma robusta interface para lidar com requisições HTTP sem precisar de muitas configurações.

## Padronização de Sintaxe
É a forma de lidar com a mesma estilização de um código dentro dos arquivos, e para isso temos várias bibliotecas em JavaScript para nos ajudar a criar um padrão para uma empresa, entre elas temos:

**ESLint**
É um linter - ferramentas que analisam o código-fonte para sinalizar erros de programação, bugs, erros estilísticos e construções suspeitas - que analisa o código para rapidamente achar problemas de padronizações e conserta automaticamente com algoritmos chamandos _find and replace_ para que você não precise lidar com erros de sintaxe manualmente.

**Prettier**
O Prettier aplica um estilo de código consistente (ou seja, a formatação do código que não afeta a árvore de sintaxe) em toda a sua base de código, porque desconsidera o estilo original, analisando-o e reimprimindo a sintaxe analisado com suas próprias regras que assumem o comprimento máximo da linha em conta, agrupando o código quando necessário.
Tem a possibilidade de uma alta integração com linters (como o próprio ESLint) com exemplos de:

| Depêndencia | Descrição |
| --- | --- |
| eslint-config-prettier | Desliga todas as regras que são desnecessárias ou podem conflitar com o Prettier. |
| eslint-plugin-prettier | É um plugin que adiciona uma regra que formata o conteúdo usando Prettier |

