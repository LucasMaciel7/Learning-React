
# Todo-list-React

Directorys 
```bash
mysite/
├── node_modules/ # Dependencies
├── public/  # Static files 
│   └── index.html
├── src/ # Source code 
│   ├── App.tsx # Main component
│   └── index.tsx # Renders app.tsx
├── .gitignore
├── package-lock.json #Arquivo de controle de dependencias
├── package.json # Package Manager
├── README.md 
└── tsconfig.json # Arquivo de configuração do typescript

```

# 1. Componentes
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
# 2. Propiededades
Dentro do React conseguimos acessar ou passar propiedades para aquele  componente diretamente dentro da tag HTML passando `{}`
## Example
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

# 3. State
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






