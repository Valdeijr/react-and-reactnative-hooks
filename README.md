# 📘 Dominando React Hooks – Da Base ao Avançado

Este repositório contém uma coletânea aprofundada de guias técnicos sobre os principais React Hooks, incluindo hooks nativos, avançados e customizados. O objetivo é oferecer uma base sólida para desenvolvedores que desejam dominar o comportamento interno dos hooks com foco em **boas práticas, performance e clareza técnica**.


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


## 📂 Conteúdo do repositório

Arquivos `hooks/use[name]-Guia-Completo.md` com guias individuais para cada hook,conforme listado na tabela abaixo:

| Hook                     | Tipo                            | Status |
|--------------------------|----------------------------------|--------|
| `useState`               | Core                             | ✅     |
| `useEffect`              | Core                             | ✅     |
| `useCallback`            | Core                             | ✅     |
| `useMemo`                | Core                             | ✅     |
| `useRef`                 | Core                             | ✅     |
| `useLayoutEffect`        | Core                             | ✅     |
| `useReducer`             | Core                             | ✅     |
| `useContext`             | Core                             | ✅     |
| `useId`                  | Core (React 18+)                 | ✅     |
| `useImperativeHandle`    | Avançado                         | ✅     |
| `useTransition`          | Concurrent (React 18+)           | ✅     |
| `useDeferredValue`       | Concurrent (React 18+)           | ✅     |
| `useInsertionEffect`     | Avançado (React 18+)             | ✅     |
| `useSyncExternalStore`   | Avançado (gerência de estado ext)| ✅     |
| `useDebugValue`          | DevTools                         | ✅     |
| `useFocusEffect`         | React Navigation                 | ✅     |
| `useIsFocused`           | React Navigation                 | ✅     |
| `useContextSelector`     | Experimental/Custom (Zustand, etc.) | ✅  |
| `useEvent`               | Experimental (React Canary)      | ✅     |
| `useCallbackRef`         | Custom Hook Pattern              | ✅     |
| `useMountedRef`          | Custom Hook                      | ✅     |
| `usePrevious`            | Custom Hook                      | ✅     |

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