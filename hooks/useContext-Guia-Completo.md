# 🌐 Guia Definitivo do `useContext` – React / React Native

---

## 📌 O que é `useContext`

`useContext` é um hook que permite **acessar valores compartilhados entre componentes** sem precisar passar props manualmente em cada nível.

```tsx
const value = useContext(MyContext)
```

- Funciona com um contexto criado via `React.createContext`
- Permite **propagação automática de valores** para qualquer componente descendente
- Excelente para temas, autenticação, configuração global, etc.

---

## 🧠 Por que usar `useContext`

Evita o famoso **prop drilling** — quando você precisa passar props por vários níveis só para um componente interno usar.

---

## ⚙️ Exemplo prático

### 1. Criando um contexto

```tsx
const ThemeContext = React.createContext('light')
```

### 2. Provedor de contexto

```tsx
<ThemeContext.Provider value="dark">
  <MyComponent />
</ThemeContext.Provider>
```

### 3. Consumindo com `useContext`

```tsx
const theme = useContext(ThemeContext)
```

---

## 🔁 Comportamento reativo

- Sempre que o valor do `Provider` muda, **todos os consumidores são re-renderizados**
- Comparação é feita por identidade (`===`), então valores **imutáveis/memoizados** são melhores

---

## ✅ Checklist de uso do `useContext`

- [ ] Preciso compartilhar um valor entre vários componentes?
- [ ] Quero evitar passar props manualmente por múltiplos níveis?
- [ ] Sei que todos os consumidores vão re-renderizar quando o valor mudar?
- [ ] Meu contexto não depende de performance ultra refinada (ou uso memo/context selector)?

---

## ⚠️ Cuidados

- Grandes objetos em `context` causam **re-renders em todos os consumidores**
- Não use para **valores que mudam frequentemente e impactam a performance**
- Prefira usar `useReducer + context` para valores mutáveis e centralizados

---

## 🧠 Dica avançada

- Combine com `useMemo` ao passar objetos:

```tsx
<SomeContext.Provider value={useMemo(() => ({ user, logout }), [user])}>
```

- Ou crie contextos separados para valores distintos (ex: um para tema, outro para auth)

---

## ❗ Anti-patterns

| Padrão                                | Correção                                     |
|----------------------------------------|-----------------------------------------------|
| Passar objetos novos em todo render    | Use `useMemo`                                 |
| Usar para estados que mudam o tempo todo | Prefira `useState` ou `useReducer` local     |
| Usar contexto para valores que poderiam ser props simples | Simplifique |

---

## 📚 Conclusão

`useContext` é essencial para:

✅ Compartilhar valores entre múltiplos níveis de componentes  
✅ Centralizar controle de temas, idiomas, auth, preferências  
✅ Reduzir complexidade e evitar props excessivos

Mas deve ser usado **com consciência de performance**, e combinado com boas práticas como **memoização** e **separação de responsabilidades**.

