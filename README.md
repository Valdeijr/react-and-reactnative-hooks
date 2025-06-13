# 📘 Dominando React Hooks – Da Base ao Avançado

Este repositório contém uma coletânea aprofundada de guias técnicos sobre os principais React Hooks, incluindo hooks nativos, avançados e customizados. O objetivo é oferecer uma base sólida para desenvolvedores que desejam dominar o comportamento interno dos hooks com foco em **boas práticas, performance e clareza técnica**.

## 📂 Conteúdo do repositório

Arquivos `hooks/use[name]-Guia-Completo.md` com guias individuais para cada hook,conforme listado na tabela abaixo:

| Hook                     | Tipo                            | Status | Links |
|--------------------------|----------------------------------|--------|-------|
| `useState`               | Core                             | ✅     | [Link](https://github.com/Valdeijr/react-and-reactnative-hooks/blob/main/hooks/useState-Guia-Completo.md) |
| `useEffect`              | Core                             | ✅     | [Link](https://github.com/Valdeijr/react-and-reactnative-hooks/blob/main/hooks/useEffect-Guia-Completo.md) |
| `useCallback`            | Core                             | ✅     | [Link](https://github.com/Valdeijr/react-and-reactnative-hooks/blob/main/hooks/useCallback-Guia-Completo.md) |
| `useMemo`                | Core                             | ✅     | [Link](https://github.com/Valdeijr/react-and-reactnative-hooks/blob/main/hooks/useMemo-Guia-Completo.md) |
| `useRef`                 | Core                             | ✅     | [Link](https://github.com/Valdeijr/react-and-reactnative-hooks/blob/main/hooks/useRef-Guia-Completo.md) |
| `useLayoutEffect`        | Core                             | ✅     | [Link](https://github.com/Valdeijr/react-and-reactnative-hooks/blob/main/hooks/useLayoutEffect-Guia-Completo.md) |
| `useReducer`             | Core                             | ✅     | [Link](https://github.com/Valdeijr/react-and-reactnative-hooks/blob/main/hooks/useReducer-Guia-Completo.md) |
| `useContext`             | Core                             | ✅     | [Link](https://github.com/Valdeijr/react-and-reactnative-hooks/blob/main/hooks/useContext-Guia-Completo.md) |
| `useId`                  | Core (React 18+)                 | ✅     | [Link](https://github.com/Valdeijr/react-and-reactnative-hooks/blob/main/hooks/useId-Guia-Completo.md) |
| `useImperativeHandle`    | Avançado                         | ✅     | [Link](https://github.com/Valdeijr/react-and-reactnative-hooks/blob/main/hooks/useImperativeHandle-Guia-Completo.md) |
| `useTransition`          | Concurrent (React 18+)           | ✅     | [Link](https://github.com/Valdeijr/react-and-reactnative-hooks/blob/main/hooks/useTransition-Guia-Completo.md) |
| `useDeferredValue`       | Concurrent (React 18+)           | ✅     | [Link](https://github.com/Valdeijr/react-and-reactnative-hooks/blob/main/hooks/useDeferredValue-Guia-Completo.md) |
| `useInsertionEffect`     | Avançado (React 18+)             | ✅     | [Link](https://github.com/Valdeijr/react-and-reactnative-hooks/blob/main/hooks/useInsertionEffect-Guia-Completo.md) |
| `useSyncExternalStore`   | Avançado (gerência de estado ext)| ✅     | [Link](https://github.com/Valdeijr/react-and-reactnative-hooks/blob/main/hooks/useSyncExternalStore-Guia-Completo.md) |
| `useDebugValue`          | DevTools                         | ✅     | [Link](https://github.com/Valdeijr/react-and-reactnative-hooks/blob/main/hooks/useDebugValue-Guia-Completo.md) |
| `useFocusEffect`         | React Navigation                 | ✅     | [Link](https://github.com/Valdeijr/react-and-reactnative-hooks/blob/main/hooks/useFocusEffect-Guia-Completo.md) |
| `useIsFocused`           | React Navigation                 | ✅     | [Link](https://github.com/Valdeijr/react-and-reactnative-hooks/blob/main/hooks/useIsFocused-Guia-Completo.md) |
| `useContextSelector`     | Experimental/Custom (Zustand, etc.) | ✅  | [Link](https://github.com/Valdeijr/react-and-reactnative-hooks/blob/main/hooks/useContextSelector-Guia-Completo.md) |
| `useEvent`               | Experimental (React Canary)      | ✅     | [Link](https://github.com/Valdeijr/react-and-reactnative-hooks/blob/main/hooks/useEvent-Guia-Completo.md) |
| `useCallbackRef`         | Custom Hook Pattern              | ✅     | [Link](https://github.com/Valdeijr/react-and-reactnative-hooks/blob/main/hooks/useCallbackRef-Guia-Completo.md) |
| `useMountedRef`          | Custom Hook                      | ✅     | [Link](https://github.com/Valdeijr/react-and-reactnative-hooks/blob/main/hooks/useMountedRef-Guia-Completo.md) |
| `usePrevious`            | Custom Hook                      | ✅     | [Link](https://github.com/Valdeijr/react-and-reactnative-hooks/blob/main/hooks/usePrevious-Guia-Completo.md) |

## 🧭 Estrutura sugerida para estudo

### 🧱 Parte I – Fundamentos Essenciais
1. `useState` – Estado funcional
2. `useEffect` – Efeitos colaterais e sincronização externa
3. `useRef` – Persistência silenciosa entre renders
4. `useLayoutEffect` – Controle visual antes da pintura
5. `useContext` – Compartilhamento de estado entre componentes
6. `useReducer` – Estado complexo e previsível
7. `useId` – Geração segura de IDs em SSR

### 🚀 Parte II – Otimizações e Performance
8. `useCallback` – Funções estáveis entre renders
9. `useMemo` – Valores computados com performance
10. `useImperativeHandle` – APIs imperativas com encapsulamento
11. `useDeferredValue` – Interface fluida com valores atrasados
12. `useTransition` – Priorização de atualizações
13. `useSyncExternalStore` – Leitura segura de estados externos

### 🧠 Parte III – Hooks Customizados e Padrões Avançados
14. `usePrevious` – Rastreando valores anteriores
15. `useMountedRef` – Segurança contra updates em componentes desmontados
16. `useCallbackRef` – Closures sempre atualizadas
17. `useDebugValue` – Visibilidade nos DevTools
18. `useInsertionEffect` – Injeção de estilos sem flicker
19. `useContextSelector` – Granularidade em contextos pesados

### 📱 Parte IV – Hooks para React Native e Navigation
20. `useFocusEffect` – Efeitos ao focar a tela
21. `useIsFocused` – Monitoramento do foco da tela


## ✨ Objetivo

> Estudar React não precisa ser por tentativa e erro.  
> Compreender a fundo os hooks é dominar o ciclo de vida do seu componente,  
> evitar bugs silenciosos e construir apps mais performáticos.

<!-- ## 📬 Sugestões

- Utilize o `ReactHooks-eBook.md` para leitura linear
- Leia os guias individuais como referência ou estudo dirigido
- Copie os exemplos para testar no seu ambiente
- Melhore sua base contribuindo com novos padrões e exemplos -->

--- 

**Bons estudos! 🚀**