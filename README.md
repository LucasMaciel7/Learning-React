# 🚀 Princípios React
Este repositório tem como objetivo 📘 **aprendizagem da biblioteca React** de JavaScript, e já vamos iniciar os estudos com a linguagem **TypeScript**, que adiciona suporte a tipagens ao JavaScript.

---

## 📜 **Autor**: Lucas Maciel
🔗 **[![GitHub](https://img.shields.io/badge/-GitHub-181717?style=flat&logo=github&logoColor=white)](https://github.com/LucasMaciel7)**  \
🔗 **[![LinkedIn](https://img.shields.io/badge/-LinkedIn-0A66C2?style=flat&logo=linkedin&logoColor=white)](https://linkedin.com/in/lucas-maciel7)**  \
🔗 **[![Email](https://img.shields.io/badge/-Email-D14836?style=flat&logo=gmail&logoColor=white)](mailto:lucasmacielcampos27@gmail.com)** \
🔗 **[![99Freelas](https://img.shields.io/badge/-99Freelas-00CBB5?style=flat&logo=99freelas&logoColor=white)](https://www.99freelas.com.br/user/LucasMaciel.7)**


---

## 🛠 Criando o app
```bash
npx create-react-app nome-do-seu-app --template typescript
```
## 📁 Estrutura de Diretórios:
```bash
mysite/
├── node_modules/ # 📦 Dependências
├── public/  # 🗂️ Arquivos estáticos
│   └── index.html
├── src/ # 🧑‍💻 Código-fonte
│   ├── App.tsx # Componente principal
│   └── index.tsx # Renderiza App.tsx
├── .gitignore
├── package-lock.json # Gerenciamento de dependências
├── package.json # Gerenciador de pacotes
├── README.md 
└── tsconfig.json # Configurações do TypeScript


```
# 🚀 Componentes
Dentro do React exibimos o nosso frontend através de componentes, são apenas funções JavaScript que retornam um HTML.
O Fluxo de trabalho se baseia em criar um componente em um arquivo TSX.
### /src/components/tweet.tsx
```tsx
export function Tweet(){
    return(
        <p>Tweet</p>
    )
}
```
Após criarmos nosso componente Tweet, nós o chamamos dentro do nosso componente principal (`App`) em `src/App.tsx`

### `/src/App.tsx`

```tsx
import React from 'react';
import { Tweet } from './components/tweet';

export default function App(){
  return <div>
    <Tweet />
  </div>
  }
```

Depois de registrar nosso componente Tweet dentro do nosso componente Main, vamos chamar nosso componente main dentro de /src/index.tsx que injeta nosso componente na div com id root em nosso arquivo html em 
### `public/index.html`

```tsx
import React, { StrictMode } from "react";
import { createRoot } from "react-dom/client";
import App from "./App";

const rootElement = document.getElementById("root");

if (rootElement) {
  const root = createRoot(rootElement);
  root.render(
    <StrictMode>
      <App />
    </StrictMode>
  );
} else {
  console.error("Elemento root não encontrado.");
}

```
# 🔧 Propriedades: são argumentos que passamos aos componentes
Dentro do React conseguimos acessar ou passar Propriedades para aquele  componente diretamente dentro da tag HTML passando `{}`
## Explicação
Ao utilizar TypeScript no React, definimos os tipos de propriedades que o componente pode receber. Isso garante maior segurança no código, facilitando o desenvolvimento com tipagens corretas
### `src/components/tweet.tsx`
```tsx
type tweetProps = {
    text: string;
}
```
No mesmo arquivo, criar o componente passando como parametro a propriedade que criamos
```tsx
export function Tweet(props: tweetProps){
    return(
        <p>{props.text}</p>
    )
}
```

Logo após chamar este componente no nosso main passando como parametro Text da nossa propriedade
### `/src/main.tsx`
```tsx
import React from 'react';
import { Tweet } from './components/tweet';

export default function App(){
  return <div>
    <Tweet text='Tweet 1 '/>
    <Tweet text='Tweet 2'/>
    <Tweet text='Tweet 3 '/>
  </div>
  }
```

## Output
![image](https://github.com/user-attachments/assets/8a7debf8-88e4-49bf-a2d4-a8b6e6d52832)

# 📊 Estado: Controla o comportamento e a renderização de componentes
O Estado ou `state`de um componente define como ele deve se comportar e renderizar um determinado momento e quando o estado muda o React acaba renderizando o componente para refletir a nova condição.
## Example
```tsx
import React from 'react';
import { useState } from 'react';
import { Tweet } from './components/tweet';

export default function App(){
  const [tweets, setTweets] = useState<string[]>([
        'Tweet 1',
        'Tweet 2',
        'Tweet 3'
  ])

 function  createTweet(){
      setTweets([...tweets, 'Tweet 5'])
  }
 
<button onClick={createTweet}>Adicionar Tweet</button>

  return (
  <div>
    {tweets.map(tweet => {
        return <Tweet text={tweet} />
     })}
  </div>
  );
  }
```

### Definição do estado
```tsx
const [tweets, setTweets] = useState<string[]>([
     'Tweet 1',
     'Tweet 2',
     'Tweet 3'
]);
```
Neste Bloco de codigo vamos estar criando uma variavel usa o metodo `useState`, que é uma função do React queu permite que adiconamos um estado ao componente.
O Metodo `useState`  recebe o valor inicial do estado que será um array de strings que se inicia com três strings.\
Neste bloco recebemos as variaveis
- `tweets`: Que armazena o valor atual do estado
- `setTwets`: Função que permite atualizar o estado


### Manipulação do estado
```tsx
function createTweet(){
   setTweets([...tweets, 'Tweet 5'])
}
```
Criamos agora uma função que vai chamar a função `setTweet` criada dentro do estado do componente.\
Esta função ficara responsavel por manipular o estado de nosso componente.

- `setTweets([...tweets, 'Tweet 5'])`
    - O operador `...` copia as informações de dentro de nosso array `tweets`
    - `'Tweet 5'` Adiciona ao final do array copiado o novo valor
 
### Renderização Baseada no estado
```tsx
{tweets.map(tweet => {
   return <Tweet text={tweet} />
 })}

```

Este bloco ele esta retornando o estado atual do componente, fazendo um for dentro do array tweet e retornando o tweet com seu determinado estado.

### Alteração do estado
```tsx
<button onClick={createTweet}>Adicionar Tweet</button>
```

Altera o estado a cada click chamando a função que criamos.


# 🎨 Estilização: Use CSS ou frameworks como TailwindCSS para customizar a aparência.
Dentro do Raeact podemos seguir o mesmo padrão de estilização convencional que ja conhecemos, como por exemplo o prório css
Somente criar um arquivo `.css`dentro de Src e importalo para dentro do seu app
### `src/app.css/`
```css
body{
    background-color: black;
}
```
Depois somente importalo dentro do seu app que irá renderizar a estilização
### `src/App.tsx`

```ts
import './app.css';
```

### Bibliotecas java Script de estilos
Com o uso frequente do java Script criou-se a necessidade de de poder estilizar componentes e paginas diretamento no arquivo `jsx` que o proprio React já disponibiliza.
```jsx
   <button 
      onClick={createTweet}
      style={{
        backgroundColor: 'blue',
        padding:'6px 10px',
        border: 0,
      }}>
      Adicionar Tweet
    </button>
```


Passando entre duas chaves `{{}}` conseguimos passar Propriedades css para aquele objeto\
Tirando isso o React tem suporte a outras bibliotecas de Estilização inline como tailwindcss ou bootstrap entre outros.\

# 🔀 Roteamento: Crie rotas para diferentes páginas dentro da aplicação
Roteamento dentro do React permite que nós tenhamos uma aplicação com varias paginas, para isso precisamos instalar primeiro sua dependencia.\
- Documentação da biblioteca: [React Router](https://reactrouter.com/en/main)

```zsh
pnpm add react-router-dom
```
Se estiver ultilizando TypeScript é recomendavel que que instale os tipos da biblioteca
```zsh
pnpm add -D @types/react-router-dom
```

Para exemplificar a explicação do roteamento do react, vamos criar um arquivo

### `src/pages/catalog.tsx`
Vamos criar o componente catalogo neste arquivo 
```tsx
export function Catalog(){
    return <h1>Catalog</h1>
}
```

Logo após vamos criar um arquivo chamado `routes.tsx` seu caminho será:
### `src/routes.tsx`
```tsx
import { Catalog } from "./pages/catalog"
import{
    BrowserRouter as Router,
    Route,
    Routes
} from "react-router-dom"

export function AppRoutes(){
    return(
        <Router>
            <Routes>
                <Route path="/catalog" element= {<Catalog />}></Route>
            </Routes>
        </Router>
    )
}
```
Primeiros importamos nosso componente `catalog` e logo após importamos as seguintes funções da biblioteca
- `BrowserRouter as Router`: Verifica as mudanças na url
- `Route`: Registra nossas rotas
- `Routes`: Engloba todas as route

`<Route path="/cart" element={<Cart />}></Route>` Aqui nós estamos passando qual será o caminho na URL com o `path` e depois mostramos qual componente queremos renderizar com o `Element`

Depois de tudo devemos chamar nosso componente `AppRoutes` dentro de nosso `App.tsx`

```tsx
export default function App(){
  return (
    <AppRoutes />
  )
```

E pronto, ao acessarmos: `http:localhost:3000/catalog`irá nos exibir nosso componente dentro de catalog.
## Output

```bash
<h2>Catalogo<h2/>
```

## 🎥 Material de acompanhamento

<div style="text-align: center;">
  <a href="https://www.youtube.com/watch?v=pDbcC-xSat4">
    <img src="https://img.youtube.com/vi/pDbcC-xSat4/0.jpg" alt="Iniciando no React.js em 2022" />
  </a>
</div>

Clique na imagem acima para assistir ao vídeo de acompanhamento no YouTube.




    






