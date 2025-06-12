# 🧠 Guia Definitivo do `useMemo` – React/React Native

---

## 🔍 O que é `useMemo`

`useMemo` é um hook que **memoriza (cacheia) o resultado de uma função de forma síncrona**, evitando que ela seja reexecutada desnecessariamente a cada render.

```tsx
const memoizedValue = useMemo(() => computeExpensiveValue(a, b), [a, b])
```

Ele só reexecuta a função quando alguma dependência muda. Em todos os outros renders, ele retorna **o valor previamente computado**.

---

## ⚙️ O que o `useMemo` **não é**

- ❌ Ele **não** torna sua função mais rápida
- ❌ Ele **não** adia a execução (não é lazy eval fora do render)
- ✅ Ele **impede a reexecução** de funções caras **quando os inputs não mudaram**

---

## 📈 Casos de uso reais

### 1. Cálculos pesados que dependem de props/estado
```tsx
const sortedItems = useMemo(() => {
  return items.sort((a, b) => a.value - b.value)
}, [items])
```

### 2. Evitar recriar objetos ou arrays a cada render
```tsx
const config = useMemo(() => ({
  theme: darkMode ? 'dark' : 'light',
}), [darkMode])
```

Evita bugs em componentes que recebem `config` como prop e só devem atualizar se ele realmente mudar.

### 3. Evitar reexecução de dependências em `useEffect`, `useCallback`, `React.memo`, etc.

---

## 🧠 Comparativo: `useMemo` vs `useCallback`

| Hook       | Retorna...     | Ideal para... |
|------------|----------------|----------------|
| `useMemo`  | um **valor memoizado** | Objetos, arrays, resultados de funções |
| `useCallback` | uma **função memoizada** | Funções passadas como prop ou usadas em deps |

---

## 🔬 Detalhes técnicos

- `useMemo(fn, deps)` executa `fn()` **durante a renderização**
- O valor **é recalculado apenas se qualquer dependência em `deps` mudar**
- Internamente usa **referência de igualdade** (`===`) para detectar mudanças
- Se `deps` for ausente ou instável, o memo perde o propósito

---

## 🔥 Anti-patterns

| Padrão                          | Correção                              |
|----------------------------------|----------------------------------------|
| `useMemo` com função leve/trivial | Remover – o custo do memo > benefício |
| Dependência instável (ex: objeto inline) | Estabilize com `useMemo` externo       |
| Função retorna novo objeto/array sem motivo | Memorize com `useMemo`                |

---

## ✅ Checklist de uso do `useMemo`

- [ ] A função é computacionalmente cara?
- [ ] O valor é usado em props, efeitos ou deps que exigem estabilidade?
- [ ] O objeto retornado é passado para componente memoizado (`React.memo`)?
- [ ] Evitei usar `useMemo` em retornos triviais como strings ou números?
- [ ] As dependências são estáveis e completas?

---

## ⚠️ Dicas avançadas

- `useMemo` **é útil quando o valor memoizado evita rerenderizações custosas** ou evita **reexecuções de efeitos** em filhos.
- Em listas renderizadas, pode reduzir o custo de ordenação, filtragem ou transformação.
- Combinado com `React.memo`, `useMemo` ajuda a evitar “renders fantasmas” em listas grandes.

---

## ❗ Cuidado: o memo **também ocupa memória**

- Cada memoização consome **heap**
- **Abuso de `useMemo` pode reduzir performance**, não melhorar

---

## 📚 Conclusão

`useMemo` é uma ferramenta **de controle de performance fina**:

✅ Evita recomputações pesadas  
✅ Estabiliza objetos em dependências  
✅ Evita renders desnecessários por referência nova

Mas **não use sem necessidade**. Se o cálculo é leve ou o valor não está sendo passado para filhos/dependências: **remova o memo**.

