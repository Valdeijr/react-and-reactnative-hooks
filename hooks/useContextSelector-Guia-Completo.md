# 🎯 Guia Definitivo do `useContextSelector` – React Otimizado

---

## 📌 O que é `useContextSelector`

`useContextSelector` é uma proposta e/ou implementação customizada (não oficial no React Core) para permitir que **componentes consumam apenas parte de um contexto**, **evitando re-renderizações desnecessárias**.

> Esse padrão é comum em bibliotecas como **Zustand**, **Recoil**, ou implementações com `use-context-selector` (da comunidade React).

---

## 🎯 Problema que resolve

O `useContext` tradicional **re-renderiza todo consumidor** quando **qualquer parte** do valor do contexto muda.

Isso é ineficiente quando você só precisa de **uma chave específica do contexto**, mas o provedor muda outros valores.

---

## 💡 Exemplo com `use-context-selector`

```tsx
import {
  createContext,
  useContextSelector
} from 'use-context-selector'

const MyContext = createContext({ name: '', age: 0 })

function NameComponent() {
  const name = useContextSelector(MyContext, ctx => ctx.name)
  return <Text>{name}</Text>
}
```

✅ O componente só será re-renderizado **quando `name` mudar** – não `age`.

---

## 🧠 Quando usar

- Em contextos grandes (auth, configs, settings, estado global)
- Quando a performance importa (UI interativa, tabelas, dashboards)
- Quando `useContext` tradicional está causando re-renders em cascata

---

## 🧪 Comparativo: `useContext` vs `useContextSelector`

| Característica           | `useContext`         | `useContextSelector`              |
|--------------------------|----------------------|-----------------------------------|
| Atualiza em qualquer mudança | ✅ Sim             | ❌ Só se a parte usada mudar       |
| Performance granular     | ❌                  | ✅ Alta                            |
| APIs modernas/libraries  | ✅ Padrão React       | 🔁 Com lib externa ou manual      |

---

## ✅ Checklist de uso do `useContextSelector`

- [ ] Tenho um contexto com múltiplas chaves/objetos complexos?
- [ ] Quero garantir que um componente **reaja apenas a parte relevante**?
- [ ] Estou notando re-renders desnecessários com `useContext`?
- [ ] Posso usar bibliotecas como `use-context-selector` ou Zustand?

---

## ⚠️ Cuidados

- Não é parte da API nativa do React (por enquanto)
- Precisa de biblioteca ou implementação personalizada (`use-context-selector`, Zustand, Jotai...)
- Depende de como o contexto é construído: precisa ser **estável e bem projetado**

---

## 🔧 Alternativas nativas parciais

- Dividir contexto em múltiplos providers (`<ThemeProvider>`, `<UserProvider>`)
- Combinar `useMemo` no provedor para evitar recriação do objeto

---

## 📚 Conclusão

`useContextSelector` é a evolução natural do `useContext`:

✅ Mais granular  
✅ Mais performático  
✅ Evita re-renderizações globais

Se você tem **contextos grandes e componentes sensíveis à performance**, esse padrão é essencial. Use via libs como `use-context-selector`, Zustand ou Jotai — até que o React o torne oficial.

