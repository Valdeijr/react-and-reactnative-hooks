# 🔁 Guia Definitivo do `useCallback` – React/React Native

---

## 🧠 O que é o `useCallback`

O `useCallback` é um hook que retorna uma **versão memoizada de uma função** que só muda se as dependências mudarem.

```tsx
const memoizedFn = useCallback(() => {
  // lógica
}, [dep1, dep2])
```

🔹 Ele é **essencial para evitar a recriação de funções** em renderizações subsequentes.

---

## 🎯 Quando usar `useCallback`

| Situação | Usar `useCallback`? | Por quê? |
|---------|----------------------|----------|
| Função passada para componente filho memoizado (`React.memo`) | ✅ Sim | Evita renders desnecessários |
| Função usada dentro de `useEffect`, `useMemo`, `useImperativeHandle` | ✅ Sim | Garante referência estável |
| Função usada apenas no render atual e não afeta filhos | ❌ Não | Otimização prematura |
| Em loops, `.map()` ou renderizações diretas | ❌ Não | Funções inline são ok se não forem dependência |

---

## 🧩 Exemplo prático

### 🔁 Sem `useCallback`

```tsx
const MyComponent = () => {
  const handleClick = () => {
    console.log('Clicked')
  }

  return <Child onClick={handleClick} />
}
```

🧨 Problema: `handleClick` é **recriada a cada render** → filho pode **rerenderizar desnecessariamente**.

---

### ✅ Com `useCallback`

```tsx
const handleClick = useCallback(() => {
  console.log('Clicked')
}, [])
```

🧠 Agora a função é estável e pode ser usada em `props`, `useEffect`, etc.

---

## ⚠️ Cuidado com dependências

```tsx
const handleClick = useCallback(() => {
  console.log(count)
}, [count])
```

- Sempre inclua no array de dependência **todas as variáveis usadas dentro do corpo** da função.
- Se não fizer isso, pode referenciar valores "congelados" (stale closures).

---

## 🔥 Anti-Patterns

| Padrão | Correção |
|--------|----------|
| Memorizar função que não é reutilizada | Remover `useCallback` |
| Usar `useCallback` com dependência instável (ex: objetos inline) | Estabilizar dependência com `useMemo` |
| Omitir dependência usada no corpo da função | Incluir no array de deps |

---

## 💡 Dicas de uso

- Combine com `React.memo`:
```tsx
const MemoizedChild = React.memo(({ onClick }) => {
  // render
})
```

- Combine com `useRef` se precisar evitar mudanças:
```tsx
const ref = useRef(() => {})
ref.current = useCallback(() => {
  // função atualizada
}, [])
```

---

## ✅ Checklist de uso do `useCallback`

- [ ] A função é usada fora do render imediato?
- [ ] A função é passada como `prop` para um componente memoizado?
- [ ] A função é usada em algum `useEffect`, `useMemo` ou hook personalizado?
- [ ] As dependências da função estão corretas?
- [ ] Evitei usar `useCallback` em funções triviais que não precisam de memoização?

---

## 📚 Conclusão

`useCallback` é uma **ferramenta de performance**, não de lógica. Use com sabedoria para:

✅ Evitar renders desnecessários  
✅ Garantir referências estáveis  
✅ Melhorar performance em grandes componentes

Mas **não use à toa**. Otimização prematura gera complexidade desnecessária.

