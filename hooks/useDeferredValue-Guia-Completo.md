# 🐢 Guia Definitivo do `useDeferredValue` – React 18+

---

## 📌 O que é `useDeferredValue`

`useDeferredValue` é um hook que permite **adiar a atualização de um valor** para **evitar travamentos durante renderizações pesadas**.

```tsx
const deferredValue = useDeferredValue(value)
```

- Ele retorna uma versão do `value` que **é mantida atrasada intencionalmente**.
- Útil para **manter a interface fluida**, especialmente com entradas rápidas como search.

---

## 🧠 Como funciona

O React **prioriza renderizações mais importantes** (como digitar no input) e **deixa o `deferredValue` ser atualizado depois**, sem travar a UI.

- Executa com **baixa prioridade**
- Se o valor muda muito rápido, o defer atrasa a propagação
- Ideal para **renderizações secundárias** (como listas filtradas)

---

## ⚙️ Exemplo prático

```tsx
const [query, setQuery] = useState('')
const deferredQuery = useDeferredValue(query)

const results = useMemo(() => {
  return expensiveSearch(deferredQuery)
}, [deferredQuery])
```

- O `query` muda rapidamente com o `onChange`
- O `deferredQuery` só atualiza com atraso
- `expensiveSearch` só executa após o atraso

---

## 🚦 Fluxo visual de prioridade

1. Usuário digita → `query` muda imediatamente
2. Tela permanece fluida
3. `deferredQuery` atualiza **depois**
4. A UI secundária (ex: lista) se atualiza sem travar

---

## ✅ Checklist de uso do `useDeferredValue`

- [ ] Tenho um estado que muda rapidamente com a interação do usuário?
- [ ] A renderização associada a esse valor é pesada ou causa lentidão?
- [ ] Quero desacoplar a UI principal de uma atualização mais custosa?

---

## ⚠️ Cuidados

- `useDeferredValue` **não cancela renderizações pesadas** — apenas as **adianta**
- É **reativo**, não imperativo: não serve para controlar o tempo exato de delay
- Ideal em conjunto com `useMemo`, `React.memo` e `Suspense` para máximo benefício

---

## 💡 Combina bem com

- `useTransition`: para marcar updates como não urgentes
- `useMemo`: para evitar recalcular com cada digitação
- `React.memo`: para evitar rerenderização de filhos baseados no valor adiado

---

## ❗ Anti-patterns

| Padrão                                | Correção                                      |
|----------------------------------------|-----------------------------------------------|
| Achar que o valor é sempre "atrasado"  | Ele é adiado **só quando necessário**         |
| Usar com valores triviais              | Não traz ganho, só complexidade               |
| Esperar controle total de timing       | Prefira `useTransition` se quiser mais controle |

---

## 📚 Conclusão

`useDeferredValue` é uma ferramenta de **controle de fluidez** da UI:

✅ Ideal para inputs rápidos e UIs com renderização custosa  
✅ Mantém a responsividade sem sacrificar interatividade  
❌ Não substitui controle manual ou debounce

Use quando precisar que a **UI reaja rápido, mas sem travar com atualizações pesadas**.

