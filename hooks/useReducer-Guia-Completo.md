# ⚙️ Guia Definitivo do `useReducer` – React / React Native

---

## 📌 O que é `useReducer`

`useReducer` é um hook que oferece uma **alternativa ao `useState`** para gerenciar estado complexo, baseado em **redução de ações**.

```tsx
const [state, dispatch] = useReducer(reducer, initialState)
```

- O estado é atualizado por meio de ações
- A lógica de transição fica **fora do componente**
- Ideal para **múltiplas ações** ou **transições previsíveis**

---

## 🔁 Conceito de reducer

Um reducer é uma função pura:

```tsx
function reducer(state, action) {
  switch (action.type) {
    case 'increment':
      return { count: state.count + 1 }
    case 'reset':
      return { count: 0 }
    default:
      return state
  }
}
```

Você despacha ações assim:

```tsx
dispatch({ type: 'increment' })
```

---

## 🧠 Quando usar `useReducer` em vez de `useState`

| Situação                                | Preferência           |
|----------------------------------------|------------------------|
| Vários campos de estado relacionados   | ✅ `useReducer`        |
| Múltiplas formas de atualizar estado   | ✅ `useReducer`        |
| Estados simples e isolados             | ✅ `useState`          |
| Precisa de histórico ou undo/redo      | ✅ `useReducer`        |

---

## 🧩 Exemplo prático

```tsx
const initialState = { count: 0 }

function reducer(state, action) {
  switch (action.type) {
    case 'increment':
      return { count: state.count + 1 }
    case 'decrement':
      return { count: state.count - 1 }
    case 'reset':
      return initialState
    default:
      return state
  }
}

const [state, dispatch] = useReducer(reducer, initialState)
```

---

## 🧰 Exemplo com payloads

```tsx
dispatch({ type: 'setName', payload: 'Einstein' })

function reducer(state, action) {
  switch (action.type) {
    case 'setName':
      return { ...state, name: action.payload }
    ...
  }
}
```

---

## ✅ Checklist de uso do `useReducer`

- [ ] O estado tem **vários subcampos** ou valores interdependentes?
- [ ] Você precisa de uma lógica clara para atualizar diferentes tipos de estado?
- [ ] Há múltiplas ações que modificam o mesmo estado?
- [ ] Você quer mover a lógica de atualização para **fora do componente**?

---

## 🔬 Vantagens técnicas

- Melhor **organização de lógica** de estado complexa
- Possibilita **composição e testes unitários da lógica de reducer**
- Mais próximo de conceitos de `Redux` (bom para quem migra)

---

## ⚠️ Anti-patterns

| Padrão                          | Correção                           |
|----------------------------------|-------------------------------------|
| Usar `useReducer` com apenas um campo trivial | Use `useState`                     |
| Criar reducers que dependem de efeitos colaterais | Reducer deve ser **puro**         |
| Atualizar estado fora do `dispatch` | Use apenas via `dispatch()`       |

---

## 🧠 Dica avançada

Você pode **lazy-inicializar** com uma função:

```tsx
const [state, dispatch] = useReducer(reducer, undefined, () => {
  return { count: getInitialCountFromLocalStorage() }
})
```

E pode combinar com `useContext` para criar **global state leve** sem Redux.

---

## 📚 Conclusão

`useReducer` é um hook de **gestão estruturada de estado**:

✅ Ideal para lógica complexa, agrupamento de updates, previsibilidade  
✅ Testável e mais escalável que `useState` em muitos casos  
❌ Mais verboso — não compensa para estados simples

Use quando precisar de **clareza, previsibilidade e escalabilidade** na atualização de estado.

