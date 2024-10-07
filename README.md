# React + TypeScript + Vite

This template provides a minimal setup to get React working in Vite with HMR and some ESLint rules.

Currently, two official plugins are available:

- [@vitejs/plugin-react](https://github.com/vitejs/vite-plugin-react/blob/main/packages/plugin-react/README.md) uses [Babel](https://babeljs.io/) for Fast Refresh
- [@vitejs/plugin-react-swc](https://github.com/vitejs/vite-plugin-react-swc) uses [SWC](https://swc.rs/) for Fast Refresh

## Expanding the ESLint configuration

If you are developing a production application, we recommend updating the configuration to enable type aware lint rules:

- Configure the top-level `parserOptions` property like this:

```js
export default tseslint.config({
  languageOptions: {
    // other options...
    parserOptions: {
      project: ['./tsconfig.node.json', './tsconfig.app.json'],
      tsconfigRootDir: import.meta.dirname,
    },
  },
})
```

- Replace `tseslint.configs.recommended` to `tseslint.configs.recommendedTypeChecked` or `tseslint.configs.strictTypeChecked`
- Optionally add `...tseslint.configs.stylisticTypeChecked`
- Install [eslint-plugin-react](https://github.com/jsx-eslint/eslint-plugin-react) and update the config:

```js
// eslint.config.js
import react from 'eslint-plugin-react'

export default tseslint.config({
  // Set the react version
  settings: { react: { version: '18.3' } },
  plugins: {
    // Add the react plugin
    react,
  },
  rules: {
    // other rules...
    // Enable its recommended rules
    ...react.configs.recommended.rules,
    ...react.configs['jsx-runtime'].rules,
  },
})
```
## React Render

# Motivos para um componente renderizar?
- Hooks changed (mudou estado, contexto, reducer ...)
- Props changed (mudou propriedade)
- Parent rerendered (componente pai renderizou)

# Fluxo de renderização:
- O react recria o html da interface daquele componente
- Compara a versão do html recriado com a versão anterior
- Se mudou alguma coisa, ele reescreve o html na tela

# Memo: Component
- Hooks changed, Props changed (deep comparison)
- Comparar a versão anterior dos hooks e props
- Se mudou algo, ele vai permitir a nova renderização

# useMemo: Variables
- Um hook focado em performance que memoriza valores computados e reavalia esses valores caso uma de suas dependências seja alterada.

# useCallback:
- Um hook focado em performance que memoriza funções e as recria caso uma de suas dependências seja alterada.

# useContextSelector
- Evitar novas renderizações desnecessárias quando um valor não selecionado da Context API tenha sido alterado.

# Aprendemos:
- Usar o hook useCallback() para evitar que um função seja recriada em memória quando ela não
precisar ser recriada em memória.
- Vamos usar o memo() quando tivermos um componente muito complexo, com loops, condicionais e um
html muito grande.