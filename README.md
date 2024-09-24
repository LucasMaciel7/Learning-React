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
├── package-lock.json #Dependencies
├── package.json # Package Manager
├── README.md 
└── tsconfig.json # TypeScript configuration file 

```

# Compoentes
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

Após criarmos nosso componentes nós chamamos ele dentro do nosso compoente Main em:

### /src/App.tsx

```tsx
import React from 'react';
import { Tweet } from './components/tweet';

export default function App(){
  return <div>
    <Tweet />
  </div>
  }
```

Depois de registrar nosso componente Tweet dentro do nosso componente Main, vamos chamar nosso componente main dentro de /src/index.tsx que acessa a div com id root em nosso arquivo html em public/index.html

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

