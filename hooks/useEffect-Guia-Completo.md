# 🧠 Guia Definitivo do `useEffect` – React/React Native

---

## 🔷 1. O Que é o `useEffect`

O `useEffect` é um **hook de efeito colateral**. Ele serve para executar código **fora do ciclo normal de renderização**, como:

- Assinar eventos
- Buscar dados
- Manipular DOM (no React Web)
- Iniciar animações, timers etc.

```tsx
useEffect(() => {
  // efeito colateral
  return () => {
    // limpeza
  }
}, [deps])
```

---

## 🔁 2. Quando Ele Executa

| Dependências | Comportamento |
|--------------|----------------|
| `[]`         | Executa **uma vez** após o primeiro render |
| `[x, y]`     | Executa sempre que `x` ou `y` mudarem |
| omitido      | Executa após **todo render**, o que é perigoso |

🔺 **Importante:** No modo `StrictMode` (dev), `useEffect` executa duas vezes em sequência para detectar efeitos colaterais não seguros.

---

## 🧩 3. Problemas Comuns e Soluções

### ✅ Problema: Executa várias vezes sem motivo
**Causa:** dependências instáveis (como objetos/funções inline)

```tsx
useEffect(() => {
  doSomething()
}, [{ a: 1 }]) // erro! novo objeto a cada render
```

**Solução:** memorizar dependências com `useMemo`, `useCallback`, ou extrair para constantes.

---

### ✅ Problema: Timeout ou listener não limpo

```tsx
useEffect(() => {
  const timeout = setTimeout(() => { ... }, 1000)
}, [])
```

**Solução:**
```tsx
useEffect(() => {
  const timeout = setTimeout(() => { ... }, 1000)
  return () => clearTimeout(timeout)
}, [])
```

---

### ✅ Problema: Referência à variável antiga (closure stale)

```tsx
useEffect(() => {
  setInterval(() => {
    console.log(count) // pode estar "congelado"
  }, 1000)
}, [])
```

**Solução:**
```tsx
const countRef = useRef(count)
useEffect(() => {
  countRef.current = count
}, [count])
```

---

## ⚙️ 4. Como Organizar Efeitos Corretamente

### ✅ Separar efeitos com responsabilidades diferentes

```tsx
useEffect(() => {
  // inicia conexão WebSocket
}, [])

useEffect(() => {
  // atualiza UI quando mudar `status`
}, [status])
```

---

## 💡 5. Casos Reais e Boas Práticas

### 📲 Em React Native

```tsx
useEffect(() => {
  const sub = AppState.addEventListener('change', handleAppState)
  return () => sub.remove()
}, [])
```

Ideal para eventos de app foreground/background.

---

### 🌐 Fetch de dados

```tsx
useEffect(() => {
  let mounted = true
  const fetchData = async () => {
    const res = await fetch('...')
    if (mounted) setData(res)
  }
  fetchData()
  return () => { mounted = false }
}, [])
```

Protege contra `setState` em componente desmontado.

---

### 🧼 Cleanup de listeners

```tsx
useEffect(() => {
  const listener = event => console.log(event)
  window.addEventListener('resize', listener)
  return () => window.removeEventListener('resize', listener)
}, [])
```

---

## 🧠 6. `useEffect` x `useCallback` x `useMemo`

| Hook        | Para quê serve | Quando usar |
|-------------|----------------|-------------|
| `useEffect` | Lidar com efeitos colaterais | Fetch, eventos, timers |
| `useCallback` | Memorizar função para evitar recriação | Quando passa como prop ou dependência |
| `useMemo`   | Memorizar valores complexos | Evita cálculos ou dependências instáveis |

---

## 🔥 7. Anti-Patterns

| Anti-pattern | Correção |
|--------------|----------|
| `useEffect` com dependência ausente (`eslint-disable-next-line`) | Evite! Use `useCallback` ou reestruture a lógica |
| Efeito com múltiplas responsabilidades | Divida em vários `useEffect` |
| Objeto/função inline em dependências | Memorize com `useCallback`/`useMemo` |
| `useEffect` que só serve para inicializar estado | Prefira `useState(() => valorInicial)` |

---

## ✅ Checklist de Ouro

- [ ] O efeito está limpo com `return () => {...}`?
- [ ] As dependências estão corretas?
- [ ] Funções usadas no efeito são estáveis (`useCallback`)?
- [ ] O efeito precisa mesmo ser reexecutado?
- [ ] Há um `console.log` para testar se está executando mais vezes do que deveria?
- [ ] Se houver animações, timers ou listeners: estou limpando corretamente?
