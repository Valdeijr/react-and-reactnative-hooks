# 👁️ Guia Definitivo do `useIsFocused` – React Navigation

---

## 📌 O que é `useIsFocused`

`useIsFocused` é um hook do React Navigation que retorna um **booleano (`true` ou `false`)** indicando se a tela atual **está em foco**.

```tsx
const isFocused = useIsFocused()
```

- Retorna `true` quando a tela está visível e interativa para o usuário
- Retorna `false` quando a tela está montada, mas em background ou coberta por outra

---

## 🔄 Como funciona

| Situação do componente    | `useIsFocused()` retorna |
|---------------------------|---------------------------|
| Tela visível no stack     | `true`                    |
| Tela por trás de outra    | `false`                   |
| Tela desmontada           | — (não é chamado)         |

---

## 🧠 Quando usar `useIsFocused`

### ✅ Casos práticos

- Executar lógica condicional com base no foco **sem efeito colateral**
- Mostrar/ocultar conteúdo com base no foco
- Suspender timers ou updates quando a tela perde o foco
- Evitar execução prematura de efeitos em `useEffect`

---

## 💡 Exemplo de uso

```tsx
const isFocused = useIsFocused()

useEffect(() => {
  if (isFocused) {
    fetchData()
  }
}, [isFocused])
```

☑️ Aqui, `fetchData` só é executado se a tela estiver focada.

---

## 🚫 Atenção

- `useIsFocused()` **não substitui** `useFocusEffect`
  - Ele é **reativo, baseado em valor**
  - `useFocusEffect` é **imperativo, baseado em eventos**

---

## ✅ Checklist de uso do `useIsFocused`

- [ ] Estou usando `isFocused` dentro de `useEffect` para condicionar execução?
- [ ] Estou usando para **render condicional leve**, e não lógica pesada direta?
- [ ] Não estou esperando que ele substitua `useFocusEffect` para efeitos ou listeners?

---

## ⚠️ Anti-patterns

| Padrão                        | Correção                         |
|-------------------------------|----------------------------------|
| Lógica pesada fora de `useEffect` com `isFocused` | Envolver dentro de `useEffect` |
| Misturar com `useFocusEffect` sem propósito | Escolha um ou combine conscientemente |
| Usar como "gatilho" de evento | Prefira `useFocusEffect` para ações |

---

## 🧠 Dicas úteis

- Útil para **components deeply nested** que não controlam a navigation diretamente
- Pode ser combinado com `useCallback` e `useEffect` para ações refinadas
- Em `tab navigation`, é muito útil para detectar se a aba atual está ativa

---

## 📚 Conclusão

`useIsFocused` é uma ferramenta **reativa** para acompanhar a visibilidade de uma tela:

✅ Ideal para controle leve, flags, condicionais  
❌ Não substitui efeitos imperativos ou listeners

Combine com `useEffect` ou lógica de render para comportamento elegante e performático.

