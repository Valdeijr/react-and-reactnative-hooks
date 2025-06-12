# 🧷 Guia Definitivo do `useRef` – React/React Native

---

## 🧠 O que é o `useRef`

`useRef` é um hook que cria um **objeto mutável** cuja `.current` persiste entre renderizações **sem causar re-render**.

```tsx
const myRef = useRef(initialValue)
```

- `myRef.current` mantém o valor persistente
- Não dispara renderizações ao mudar
- Ideal para armazenar valores mutáveis ou referências a DOM/elementos

---

## 🔧 Principais usos do `useRef`

### 1. Referenciar elementos DOM (Web)
```tsx
const inputRef = useRef(null)

useEffect(() => {
  inputRef.current.focus()
}, [])
```

### 2. Guardar valores entre renders
```tsx
const renderCount = useRef(0)
renderCount.current += 1
```

### 3. Evitar reexecução de efeitos (`flag de inicialização`)
```tsx
const initialized = useRef(false)
useEffect(() => {
  if (initialized.current) return
  initialized.current = true
  doSomethingOnce()
}, [])
```

### 4. Guardar funções atualizadas
```tsx
const callbackRef = useRef(() => {})
useEffect(() => {
  callbackRef.current = () => {
    console.log('função mais atual')
  }
}, [someState])
```

---

## ❗Diferença entre `useRef` e `useState`

| Característica           | `useRef`             | `useState`              |
|--------------------------|----------------------|--------------------------|
| Mantém valor entre renders | ✅                   | ✅                        |
| Causa re-render ao mudar | ❌                   | ✅                        |
| Ideal para valores mutáveis sem impacto visual | ✅ | ❌                    |
| Usado para refs de DOM   | ✅                   | ❌                        |

---

## ⚠️ Cuidados com `useRef`

- Mudanças em `.current` **não disparam renderizações**
- Se você mudar `.current` e espera que a UI reaja: **não vai acontecer**
- **Nunca use `.current` como dependência em `useEffect`**, pois ela não muda a referência do objeto, apenas seu conteúdo interno

---

## ✅ Checklist de uso do `useRef`

- [ ] Preciso persistir um valor entre renders **sem causar render**?
- [ ] Estou controlando um elemento DOM (apenas no React Web)?
- [ ] Estou usando como flag (ex: "já inicializei")?
- [ ] Estou armazenando uma função ou callback que muda?

---

## 🧠 Dicas avançadas

- Use `useRef` para evitar closures “congeladas” em `setTimeout`, `setInterval`, etc.
```tsx
const valueRef = useRef(value)
useEffect(() => {
  valueRef.current = value
}, [value])
```

- Com `React.forwardRef`, você pode passar refs personalizadas para componentes filhos.

---

## 🔥 Anti-patterns

| Padrão                   | Correção                      |
|--------------------------|-------------------------------|
| Usar `.current` para forçar re-render | Use `useState` |
| Usar como storage geral de estado | Reflita se deveria ser `useReducer` |
| Esperar que mudar `.current` atualize a tela | Isso não acontece |

---

## 📚 Conclusão

`useRef` é o canivete suíço da persistência em React:

✅ Armazena valores sem renderizar  
✅ Controla elementos (input, scroll, media)  
✅ Evita bugs com reexecuções ou closures stale

Mas **não use para tudo**. Se o valor precisa impactar a UI → use `useState`.

