## Se você clonou esse projeto 
1. Rode o comando yarn add dentro da pasta.
2. Altere "name": "primeiro-projeto-node" dentro do arquivo package.json para o nome da sua aplicação. 
3. Para inicializar o servidor basta rodar o comando yarn dev:server

## Começando um projeto Node do zero

1. Criar uma nova pasta e rodar o comando yarn init -y
2. Criar pasta src e adicionar um arquivo server.ts dentro dela
3. Rodar os comandos para adicionar typescript e express
    - yarn add typescript -D
    - yarn add express
4. Criar arquivo tsconfig.json onde vai todas as configurações do typescript
    - yarn tsc —init
5. Se ficar com erro ao importar qualquer biblioteca, rodar o comando yarn add @types/nome-da-biblioteca -D
    - yarn add @types/express -D
6. Editar arquivo tsconfig.json nas linhas 15 e 16. Em rootDir vc coloca o diretório onde está o tyscript e em outDir o diretório onde será transpilado o typescript
    - "rootDir": "./src",
    - "outDir": "./dist",
7. Para transpilar typescript rodar o comando yarn tsc e para executar rodar comando node dist/server.js
8. Se for executar somente pelo typescript, ignore a linha 7, exclua a pasta dist e coloque as seguintes informações dentro do package.json

    ```jsx
    //rodar o comando yarn add ts-node-dev -D e fazer as configurações abaixo dentro do package.json
    "scripts": {
        "build": "tsc",
        "dev:server": "ts-node-dev --inspect --transpileOnly --ignore-watch node_modules src/server.ts"
      },
    ```

9. Para executar o programa, rodar yarn dev:server. Desta maneira o servidor será inicializado via typescript e não pelo JS.
10. Instalar editorconfig dentro do vscode e clicar com botão direito e adicionar arquivo .editorconfig
11. Rodar o comando yarn add eslint -D
12. Fazer as configurações abaixo para configurar o eslint
   <img src="https://s3.us-west-2.amazonaws.com/secure.notion-static.com/4ff00d9f-0c37-4c47-ac88-36913c09a0b9/Untitled.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Credential=AKIAT73L2G45O3KS52Y5%2F20200429%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20200429T172130Z&X-Amz-Expires=86400&X-Amz-Signature=1e46647e80ff050d852ddc746ccd0f78b5dab01a28f5019180e08cb56cb92364&X-Amz-SignedHeaders=host&response-content-disposition=filename%20%3D%22Untitled.png%22"/>

13. Rodar o comando yarn add -D @typescript-eslint/eslint-plugin@latest eslint-config-airbnb-base@latest eslint-plugin-import@^2.20.1 @typescript-eslint/parser@latest
14. Instalar esLint no vscode
15. Adicionar o seguinte trecho dentro do seu settings.json do vscode. Para acessar o settings.json digite ctrl + shift + P e digitar Json

    ```jsx
    "[javascript]": {
        "editor.codeActionsOnSave": {
          "source.fixAll.eslint": true,
        },
        "editor.defaultFormatter": "esbenp.prettier-vscode"
      },
      "[javascriptreact]": {
        "editor.codeActionsOnSave": {
          "source.fixAll.eslint": true,
        }
      },
      "[typescript]": {
        "editor.codeActionsOnSave": {
          "source.fixAll.eslint": true,
        },
        "editor.defaultFormatter": "esbenp.prettier-vscode"
      },
      "[typescriptreact]": {
        "editor.codeActionsOnSave": {
          "source.fixAll.eslint": true,
        }
      },
    ```

16. Criar pasta routes dentro do src e criar arquivo index.ts onde será armazenado todas as rotas. Dentro do index.ts configurar da seguinte maneira:

    ```jsx
    import { Router } from 'express';

    const routes = Router();

    routes.get('/', (request, response) => response.json({ message: 'Hello Pedro' }));

    export default routes;
    ```

17. Rodar o comando para instalar prettier yarn add prettier eslint-config-prettier eslint-plugin-prettier -D
18. Rodar o seguinte comando yarn add -D eslint-import-resolver-typescript para remover os erros de importação do typescript e copiar o código abaixo dentro do .eslintrc.json

    ```jsx
    {
      "env": {
        "es6": true,
        "node": true
      },
      "extends": [
        "airbnb-base",
        "plugin:@typescript-eslint/recommended",
        "prettier/@typescript-eslint",
        "plugin:prettier/recommended"
      ],
      "globals": {
        "Atomics": "readonly",
        "SharedArrayBuffer": "readonly"
      },
      "parser": "@typescript-eslint/parser",
      "parserOptions": {
        "ecmaVersion": 2018,
        "sourceType": "module"
      },
      "plugins": [
        "@typescript-eslint",
        "prettier"
      ],
      "rules": {
        "prettier/prettier": "error",
        "import/extensions": [
          "error",
          "ignorePackages",
          {
            "ts": "never"
          }
        ]
        }, "settings": {
          "import/resolver": {
            "typescript": {}
          }
        }
      }
    ```

19. Criar arquivo prettier.config.js na raiz do projeto e colocar o seguinte trecho dentro

    ```jsx
    module.exports = {
      singleQuote: true,
      trailingComma: 'all',
      arrowParens: 'avoid',
    };
    ```

20. Criar arquivo .eslintignore na raiz e adicionar o seguinte trecho

    ```jsx
    /*.js
    node_modules
    dist
    ```

21. Clicar no icone do debug do vscode e clique em adicionar JSON e substituir o código pelo seguinte:

    ```jsx
    {
      // Use IntelliSense to learn about possible attributes.
      // Hover to view descriptions of existing attributes.
      // For more information, visit: https://go.microsoft.com/fwlink/?linkid=830387
      "version": "0.2.0",
      "configurations": [
        {
          "type": "node",
          "request": "attach",
          "protocol": "inspector",
          "restart": true,
          "name": "Debug",
          "skipFiles": [
            "<node_internals>/**"
          ],
          "outFiles": [
            "${workspaceFolder}/**/*.js"
          ]
        }
      ]
    }
    ```

### index.ts

```jsx

import { Router } from 'express';

const routes = Router();

routes.get('/', (request, response) =>
  response.json({ message: 'Hello Pedro' }),
);

export default routes;
```

### server.ts

```jsx
/* eslint-disable no-console */
import express from 'express';
import routes from './routes';

const app = express();

app.use(routes);

app.listen(3333, () => {
  console.log('Server is running on port 3333');
});
```
