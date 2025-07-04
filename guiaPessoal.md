# 🧰 Setup Inicial de Projetos com Next.js + TypeScript

Este documento é um guia pessoal para iniciar projetos com **Next.js + TypeScript**, usando uma stack moderna e padronizada. A ideia é garantir consistência, clareza e velocidade ao começar novos repositórios.

---

## 🏗️ 1. Criação do Projeto com `pnpm`

### 🧾 Comando:

```bash
pnpm create next-app meu-projeto
```

Durante a criação, selecione as seguintes opções:

- **TypeScript** ✅
- **ESLint** ✅
- **Tailwind CSS** ✅
- **src/ directory** ✅
- **App Router (recommended)** ✅
- **Import alias (@/)** ✅
- **Turbopack** ✅

> **🟡 Não use --latest no comando acima!**  
> Isso evita instalar versões instáveis ou incompatíveis entre si.

---

## 📦 Por que usar pnpm?

`pnpm` é um gerenciador de pacotes mais eficiente que o npm e yarn. Ele economiza espaço e melhora a performance através de links simbólicos entre dependências comuns.

**Vantagens:**
- 🚀 Mais rápido na instalação
- 🧠 Compartilhamento inteligente de pacotes
- ✅ Integridade de dependências garantida
- 🧹 Menos espaço no disco

**Para instalar:**
```bash
npm install -g pnpm
```

---

## 🧠 Explicação das Tecnologias Selecionadas

### 🔹 TypeScript
Superset do JavaScript que adiciona tipagem estática. Traz segurança, autocompletar, refatoração segura e melhor documentação no código.

### 🔹 ESLint / Prettier
ESLint é uma ferramenta que analisa seu código e ajuda a manter boas práticas e estilo consistente, ajudando em:
- 🐛 Erros de Sintaxe: Detecta problemas que quebrariam o código;
- 📏 Padrões de Código: Garante consistência no estilo;
- ⚡ Boas Práticas: Sugere melhorias de performance e legibilidade;
- 🔒 Problemas de Segurança: Identifica padrões potencialmente perigosos. 

📦 Instalação
Se você seguiu o primeiro passo, o ESLint já foi instalado automaticamente com o Next.js. Caso precise instalar manualmente:

```bash
pnpm add -D eslint eslint-config-next @typescript-eslint/eslint-plugin @typescript-eslint/parser
```
🛠️ Comandos Úteis
```bash
# Verificar erros
pnpm lint

# Corrigir erros automaticamente
pnpm lint:fix

# Lint rigoroso (falha se houver warnings)
pnpm lint:strict

# Lint em arquivo específico
pnpm eslint src/components/Header.tsx
```


Já o Prettier é um formatador de código que: 
- 📐 Formatação Automática: Indentação, espaçamento, quebras de linha;
- 🎯 Consistência: Mesmo estilo em todo o projeto e equipe;
- ⚡ Produtividade: Não perde tempo formatando manualmente;
- 🤝 Zero Configuração: Funciona bem com configurações padrão.

📦 Instalação
```bash
pnpm add -D prettier eslint-config-prettier eslint-plugin-prettier prettier-plugin-tailwindcss
```
🔧 Configuração no `.prettierrc`

Crie o arquivo `.prettierrc` na raiz do projeto:
```json
{
  "trailingComma": "all",
  "semi": true,
  "printWidth": 80,
  "tabWidth": 2,
  "singleQuote": true,
  "jsxSingleQuote": true,
  "endOfLine": "auto",
  "plugins": ["prettier-plugin-tailwindcss"]
}
```
🔄 Integração ESLint + Prettier

Atualize o `.eslintrc.json` para integrar com o Prettier:

```js
{
    "extends": [
      "next/core-web-vitals",
      "next/typescript",
      "next",
      "prettier",
      "plugin:storybook/recommended"
    ]
  }
  
```
✅ Adicionar scripts no `package.json`

Adicione ou atualize os scripts no seu `package.json`:
```json
{
  "scripts": {
    "lint": "next lint",
    "lint:fix": "next lint --fix",
    "prettier": "prettier --write .",
    "prettier:check": "prettier --check .",
    "format": "prettier --write . && next lint --fix"
  }
}
```
📝 Criar arquivo `.prettierignore`

Crie um `.prettierignore` para excluir arquivos que não devem ser formatados:
```
node_modules
.next
out
dist
build
*.min.js
*.min.css
package-lock.json
yarn.lock
pnpm-lock.yaml
```

🧪 Testar se está funcionando

```bash
# Verificar se o ESLint está funcionando
pnpm lint

# Verificar se o Prettier está funcionando
pnpm prettier:check
```
🛠️ Comandos Úteis
- pnpm lint - Verifica problemas de linting
- pnpm prettier - Formata todos os arquivos
- pnpm format - Formata e corrige problemas de linting
- pnpm prettier:check - Verifica se os arquivos estão formatados corretamente



### 🔹 Tailwind CSS
Framework utilitário para estilização. Permite aplicar estilos diretamente no HTML/JSX com classes como `flex`, `p-4`, `bg-blue-500`, etc.
🎨 2. Configuração do Tailwind CSS

 📦 Instalação
Se você seguiu o passo anterior, o Tailwind já foi instalado automaticamente. Caso precise instalar manualmente:

```bash
pnpm add -D tailwindcss postcss autoprefixer
pnpm dlx tailwindcss init -p
```
### 🔹 src/ Directory
Organiza o projeto dentro da pasta `src/`, separando o código-fonte dos arquivos de configuração da raiz. Padrão mais limpo.

### 🔹 App Router
Novo sistema de roteamento do Next.js, baseado na pasta `app/` em vez de `pages/`. Mais flexível, com suporte a layouts aninhados, loading, error boundaries e Server Components.

### 🔹 Import alias (@/)
Permite importar arquivos usando caminhos curtos como:

```tsx
import { Header } from '@/components/Header';
```

Evita `../../../` e melhora a legibilidade.

**Configuração no tsconfig.json:**
```json
"paths": {
  "@/*": ["./src/*"]
}
```

### 🔹 Turbopack
Novo bundler experimental do Next.js (substituto futuro do Webpack). Muito mais rápido na build e no HMR (Hot Module Replacement).

---

## 🏗️ 2. StoryBook
O **Storybook** é uma ferramenta de desenvolvimento isolado de componentes. Ele permite documentar, testar visualmente e evoluir seus componentes de UI sem depender da aplicação completa.

### 📦 Instalação

Execute no terminal:

```bash
pnpm dlx storybook@8.3.0 init
```
🔹 Durante a instalação, selecione:
- React como framework;
- TypeScript como linguagem (detectado automaticamente se seu projeto usa);
- Responda Sim para adicionar exemplos;
- Responda Não para instalar outras libs (opcional);

### 🛠️ Ajustes pós-instalação (Next + Tailwind)

- Instale dependências de Tailwind para Storybook:
```bash

pnpm add -D tailwindcss postcss autoprefixer
```
- Crie ou edite o arquivo `preview.ts`:
```ts
import '../src/app/globals.css';

const preview = {
  parameters: {
    controls: {
      matchers: {
        color: /(background|color)$/i,
        date: /Date$/i,
      },
    },
  },
} as const;

export default preview;

```
- Edite o `main.ts` do Storybook para suportar alias `@/`:
```ts
// .storybook/main.ts

import type { StorybookConfig } from '@storybook/nextjs';
import path from 'path';

const config: StorybookConfig = {
  stories: ['../src/**/*.mdx', '../src/**/*.stories.@(js|jsx|mjs|ts|tsx)'],
  addons: [
    '@storybook/addon-onboarding',
    '@storybook/addon-links',
    '@storybook/addon-essentials',
    '@chromatic-com/storybook',
    '@storybook/addon-interactions',
  ],
  framework: {
    name: '@storybook/nextjs',
    options: {},
  },
  staticDirs: ['..\\public'],
  webpackFinal: async (config) => {
    if (config.resolve) {
      config.resolve.alias = {
        ...config.resolve.alias,
        '@': path.resolve(__dirname, '../src'),
      }; //Agora você pode usar importações como import { Button } from '@/components/Button' nas suas stories, igual como faz no Next.js.
    }
    return config;
  },
};

export default config;

```
### ▶️ Rodando o Storybook
```bash
pnpm storybook
```
Acesse em: http://localhost:6006

Para buildar para produção (por exemplo, publicar no GitHub Pages ou Vercel):

```bash
pnpm build-storybook
```

## 🏗️ 3. Integração continua 
### ⚙️  Habilitando CI com GitHub Actions
Este tópico mostra como configurar **Integração Contínua (CI)** usando o **GitHub Actions**, para verificar automaticamente seu código sempre que houver um push ou pull request.

---

## 📁 Estrutura básica

Crie a seguinte pasta e arquivo na raiz do seu projeto:
```
Meu-projeto/
├── .github/           
│     ├── workflows/   
│       ├── ci.yml//        
│     ├── pull_request_template  // criando um modelo específico de PR
```
## 🧾 Exemplo de workflow: ci.yml
```yaml
  name: Continuous Integration

on:
  push:
    branches:
      - main
  pull_request:
    branches:
      - main
      - develop

jobs:
  ci:
    runs-on: ubuntu-latest

    strategy:
      matrix:
        node-version: [22]

    steps:
      - name: Checkout repository
        uses: actions/checkout@v4

      - name: Install pnpm
        uses: pnpm/action-setup@v4
        with:
          version: 9

      - name: Setup Node.js ${{ matrix.node-version }}
        uses: actions/setup-node@v4
        with:
          node-version: ${{ matrix.node-version }}
          cache: 'pnpm'

      - name: Install dependencies
        run: pnpm install --frozen-lockfile

      - name: Check formatting
        run: pnpm run prettier:check

      - name: Lint code
        run: pnpm run lint

      - name: Type check
        run: pnpm run type-check

      - name: Build project
        run: pnpm run build

```
### 🧠 Scripts esperados no package.json

```json
{
  "scripts": {
    "format:fix": "prettier --write .",
    "lint": "eslint . --ext .ts,.tsx",
    "build": "next build"
  }
}
``` 

## 🏗️ 4. Estrutura Inicial Esperada

```
meu-projeto/
├── .storybook/
|    ├── main.ts         # Configuração base do Storybook
|    ├── preview.ts      # Importação de estilos globais (ex: Tailwind)
|    ├── tsconfig.json   # Alinhado com o do projeto principal
├── src/
│   ├── app/           # App Router (páginas e rotas)
│   ├── components/    # Componentes reutilizáveis
│   ├── styles/        # Estilos globais e Tailwind
│   └── lib/           # Funções utilitárias
├── public/
├── .eslintrc.json
├── .prettier.json
├── tsconfig.json
├── next.config.js
└── package.json
```
