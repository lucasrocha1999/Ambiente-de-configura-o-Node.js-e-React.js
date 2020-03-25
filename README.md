# VS-Code-Node.js-React.js--Configurando-o-Ambiente-de-Desenvolvimento

## Node.js + React.js Express + ES6 + ESLint + Prettier + EditorConfig

#### Para criar um novo em Node.js projeto basta executar:

`yarn init -y`

- **init:** essa instrução instrui o yarn a criar um arquivo Package.json, responsável por guardar algumas definições iniciais do projeto e a lista de dependências;
- **-y:** ativa confirmação silenciosa, ou seja, preencher todas as perguntas com a resposta padrão, deste modo não seremos questionados quanto as escolhas durante o processo de criação.

Agora iremos instalar nossas primeiras dependências de produção:

`yarn add express cors dotenv`

- **express:** micro-framework simples e flexível;

- **cors (cross-origin):** é uma especificação que define meios para que um recurso do servidor seja acessado remotamente via web/rede; Resumidamente, o cors permite que nossa aplicação seja acessada de um endereço externo;

- **dotenv:** é um módulo de dependência zero, responsável por carregar variáveis de ambiente de um arquivo .env em process.env.\*.

#### Para criar um novo em React.js projeto basta executar:

```
npx create-react-app my-app
cd my-app
npm start

```

#### Agora iremos adicionar as dependências de desenvolvimento do nosso projeto:

> Obs: As extensões do Eslint, Prettier eEditor Config devem estar instaladas no seu editor.

`yarn add eslint prettier eslint-config-prettier eslint-plugin-prettier sucrase nodemon -D`

- **eslint:** utilizado para análise de código estático e identificação de padrões problemáticos presentes no código;
- **sucrase:** responsável por fazer a transpilação do código, ou seja, traduzir as especificações mais recentes da linguagem, que ainda não são nativamente suportadas pelo Node.js para um padrão que o mesmo já suporte. Essa ferramenta é altamente recomendada para ambiente de desenvolvimento devido a sua abordagem de transpilação, porém, não é adequada para um ambiente de produção;
- **nodemon:** monitora o diretório e realiza restart automático do server sempre que um arquivo for alterado;
- **prettier:** formata o código de modo a manter um padrão estético, os plugins eslint-config-prettier e eslint-plugin-prettier cuidam de fazer a integração entre o ESLint e o Prettier (assunto já abordado no inicio deste post), de modo a promover correções automáticas no código sempre que o ESLint apontar uma erro, obviamente você pode incluir regras personalizadas ou ignorar as predefinidas que não te atenderem.
- **EditorConfig** garante que nosso código esteja formatado corretamente independentemente do editor ou do sistema operacional ou membro da equipe esteja trabalhando no código.

#### Feito isso, vamos configurar o ESLint. A instrução abaixo irá realizar o download de algumas outras dependências de desenvolvimento e gerar o arquivo de configuração .eslintrc.\* (a extensão final pode ser js, json ou yml, veremos isso mais adiante):

`yarn eslint --init`

### Node.js

Serão feitas uma série de perguntas, recomenda-se no **Node.js** dar as seguintes respostas:

`To check syntax and find problems`  
`JavaScript modules(import/export)`  
`None of these`  
`Browser`  
`Use a popular style guide`  
`Airbnb`  
`JSON`  
`Y`

A instalação terminou. Agora vamos as configurações…  
Modifique o arquivo **.eslintrc.json** para que este fique assim no **Node.js**:

```
{
  "env": {
    "es6": true,
    "node": true
  },
  "extends": [
    "eslint:recommended",
    "prettier"
  ],
  "globals": {
    "Atomics": "readonly",
    "SharedArrayBuffer": "readonly"
  },
  "parserOptions": {
    "ecmaVersion": 2018,
    "sourceType": "module"
  },
  "plugins": [
    "prettier"
  ],
  "rules": {
    "prettier/prettier": "error"
  }
}
```

### React.js

Serão feitas uma série de perguntas, recomenda-se no **React.js** dar as seguintes respostas:

`To check syntax, find problems, and enforce code style`  
`JavaScript modules(import/export)`  
`React`  
`Browser`  
`Use a popular style guide`  
`Airbnb`  
`JavaScript`  
`Y`

A instalação terminou. Agora vamos as configurações…  
Modifique o arquivo **.eslintrc.json** para que este fique assim no **React.js**:

```
// .eslintrc.js
module.exports = {
  env: {
    browser: true,
    es6: true
  },
  extends: ["airbnb", "prettier", "prettier/react"],
  globals: {
    Atomics: "readonly",
    SharedArrayBuffer: "readonly",
    __DEV__: 'readonly'
  },
  parser: "babel-eslint",
  parserOptions: {
    ecmaFeatures: {
      jsx: true
    },
    ecmaVersion: 2018,
    sourceType: "module"
  },
  plugins: ["react", "prettier"],
  rules: {
    "prettier/prettier": "error",
    "react/jsx-filename-extension": ["warn", { extensions: [".jsx", ".js"] }],
    "import/prefer-default-export": "off",
    "no-param-reassign": "off",
    "no-console": ["error", { allow: ["tron"] }]
  }
}
```

### Node.js e React.js

Na raiz do projeto crie o arquivo **.prettierrc** e adicione este conteúdo a ele:

```
{
  "semi": false,
  "singleQuote": true,
  "trailingComma": "es5"
}
```

As configurações acima representam uma escolha pessoal minha. Explicando:

- **semi:** imprima ponto e vírgula no final das instruções;
- **singleQuote:** usar aspas simples em vez de aspas duplas;
- **trailingComma:** imprima vírgulas à direita sempre que possível quando houver várias linhas. (Uma matriz de linha única nunca receberá vírgulas). Essa opção pode parecer um pouco sem sentido, porém, me ajuda bastante, as vezes acabo adicionando uma nova entrada na lista e esqueço de incluir a virgula após o item anterior, ao deixar sempre a lista multilinhas com uma virgula a direita, evito ser pego desprevenido.

Na raiz do projeto crie um arquivo chamado **.editorconfig** e no seu conteúdo escreva:

```
root = true
[*]
indent_style = space
indent_size = 2
end_of_line = lf
charset = utf-8
trim_trailing_whitespace = true
insert_final_newline = true
```

- O **root = true** indica que este é o arquivo inicial e global do EditorConfig.
- O **[*]** indica que as configurações valem para todos os tipos de arquivo.
- O **indend_style = space** indica que a identação deverá ser feita com espaços e não tabs.
- O **indent_size = 2** diz que para cada identação deve ser usado 2 espaços de tamanho.
- O **end_of_line = lf** regulariza o estilo de quebra de linha para qualquer sistema operacional.
- O **trim_trailing_whitespace = true** removerá os espaços em branco no final de cada linha.
- O **insert_final_newline = true** vai adicionar uma linha em branco no final de cada arquivo.

> Obs: Usando o react-create-app, não vamos precisar configurar o nodemon e o sucrase.

Por fim edite o arquivo package.json e inclua o bloco referente a tag "scripts". Veja um exemplo:

```
{
  "name": "teste",
  "version": "1.0.0",
  "main": "./src/index.js",
  "license": "MIT",
  "scripts" : {
    "dev": "nodemon --exec sucrase-node ./src/index.js"
  },
  "dependencies": {
//...
```

Terminamos ^^

Agora podemos executar no terminal a instrução:

`yarn dev` ou `yarn start`

### Dotenv Node.js

Na raiz do projeto crie um arquivo .env com o conteúdo:

`PORT=3000`

> Importante: Utilizamos este arquivo para centralizar configurações sensíveis, tais como, chaves de API, senhas e outros dados que não devem fazer parte do controle de versões, ou seja, é uma boa prática incluir este arquivo no .gitignore do seu projeto.

Crie um diretório src e dentro um arquivo índex.js, adicionando a este arquivo o conteúdo:

```
import 'dotenv/config'
import cors from 'cors'
import express from 'express'

const app = express()

// Permite acesso externo
app.use(cors())

// Desativa o X-Powered-By: Express
app.disable('x-powered-by')

// Criamos uma rota raiz com o texto Hello World!
app.get('/', (req, res) => {
  res.send('Hello World!')
})

// Passamos a porta onde o servidor ficará ouvindo
app.listen(process.env.PORT || 3000, () => {
  console.log(`Listening on port: ${process.env.PORT}`)
})
```

> Importante: utilizo app.disable('x-powered-by') para remover da resposta HTTP a referência de que o Express/Node compõem a lista de tecnologias utilizadas, isso irá afastar rotinas mais simples de varredura e ataques automatizados.

> Fontes:
>
> <https://medium.com/@fabiojanio/node-js-express-es6-eslint-sucrase-de-forma-simples-e-r%C3%A1pida-8467fcfae728>
>
> <https://medium.com/@jccamargo15/vs-code-e-react-configurando-editorconfig-e-eslint-6ffd15310fba>
>
> <https://henriquetavares.com/pt-br/setting-eslint-on-reactjs-and-react-native/>
