# 🧷 Guia Definitivo do `useMountedRef` – Custom Hook (React)

---

## 📌 O que é `useMountedRef`

`useMountedRef` é um **hook personalizado** (não nativo do React) usado para saber **se o componente ainda está montado**.  
É extremamente útil para evitar chamadas a `setState()` ou `dispatch()` **depois que o componente já foi desmontado**, o que causaria **warnings ou memory leaks**.

```tsx
const isMounted = useMountedRef()
```

---

## ⚙️ Implementação típica

```tsx
import { useEffect, useRef } from 'react'

export function useMountedRef() {
  const mounted = useRef(false)

  useEffect(() => {
    mounted.current = true
    return () => {
      mounted.current = false
    }
  }, [])

  return mounted
}
```

---

## 🧠 Quando usar

- Em **chamadas assíncronas** (`fetch`, `axios`, etc.)
- Em **setTimeout/setInterval**
- Em **eventos canceláveis**
- Em **hooks customizados complexos**

---

## ✅ Exemplo de uso

```tsx
function MyComponent() {
  const [data, setData] = useState(null)
  const isMounted = useMountedRef()

  useEffect(() => {
    fetchData().then(res => {
      if (isMounted.current) {
        setData(res)
      }
    })
  }, [])
}
```

✅ Isso evita o famoso erro:

> Warning: Can't perform a React state update on an unmounted component

---

## ✅ Checklist de uso do `useMountedRef`

- [ ] Tenho uma função assíncrona dentro de `useEffect`?
- [ ] Existe a chance de o componente desmontar antes do `await` ou `.then`?
- [ ] Preciso condicionar o `setState` à existência do componente?

---

## ⚠️ Cuidados

- Não substitui um **cancelamento real** de requisição (ex: `AbortController`)
- Apenas evita `setState` em componentes desmontados — **não cancela a operação**
- Sempre combine com `try/catch` se estiver usando `await`

---

## ❗ Anti-patterns

| Padrão                                | Correção                                      |
|----------------------------------------|-----------------------------------------------|
| Ignorar que o componente pode desmontar | Use `useMountedRef` para proteger atualizações |
| Fazer `setState` direto no `.then()`   | Verifique `.current` antes de atualizar       |

---

## 📚 Conclusão

`useMountedRef` é um **guardião contra atualizações indevidas**:

✅ Evita bugs em async/await  
✅ Protege timers e efeitos retardados  
✅ Melhora robustez de hooks customizados e componentes complexos

Use sempre que estiver em território assíncrono, onde o tempo pode desmontar o seu componente!

