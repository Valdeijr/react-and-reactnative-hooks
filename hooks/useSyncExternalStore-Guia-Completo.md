# 🧩 Guia Definitivo do `useSyncExternalStore` – React 18+

---

## 📌 O que é `useSyncExternalStore`

`useSyncExternalStore` é um hook introduzido no React 18 para lidar com **leitura segura e assinada de stores externas**, com suporte total ao modo concorrente (`Concurrent Mode`).

```tsx
const snapshot = useSyncExternalStore(subscribe, getSnapshot, getServerSnapshot?)
```

Ele garante que o React leia o **valor mais atualizado** de uma fonte externa (store, observable, etc.) de forma consistente e segura.

---

## 🧠 Por que existe

Antes do React 18, era comum usar soluções como:

- `useEffect` + `useState` para assinar stores
- `useLayoutEffect` para garantir atualizações sincronizadas

Mas esses padrões falham no **modo concorrente**, onde inconsistências e flickers visuais podem ocorrer.

---

## 🔍 Parâmetros

```tsx
useSyncExternalStore(
  subscribe: (onStoreChange) => () => unsubscribe,
  getSnapshot: () => currentValue,
  getServerSnapshot?: () => currentValue (para SSR)
)
```

| Parâmetro           | Função                                 |
|---------------------|-----------------------------------------|
| `subscribe`         | Registra um listener para mudanças      |
| `getSnapshot`       | Retorna o valor atual da store          |
| `getServerSnapshot` | (SSR) Valor usado durante server render |

---

## ⚙️ Exemplo com `window.innerWidth`

```tsx
function useWindowWidth() {
  return useSyncExternalStore(
    (callback) => {
      window.addEventListener('resize', callback)
      return () => window.removeEventListener('resize', callback)
    },
    () => window.innerWidth
  )
}
```

---

## 🧠 Casos de uso típicos

- Integração com stores externas como:
  - Zustand
  - Redux (via adaptador)
  - Recoil, Jotai
- Acompanhamento de eventos globais:
  - `window.location`, `scrollY`, `mediaQuery`
- Sincronização com sistemas legados ou APIs de terceiros

---

## ✅ Checklist de uso do `useSyncExternalStore`

- [ ] Preciso integrar com um store **fora do React**?
- [ ] Quero garantir consistência mesmo em `Concurrent Mode`?
- [ ] Estou lidando com múltiplos listeners/observables fora do estado React?
- [ ] Quero que React **reaja automaticamente a mudanças externas**?

---

## 🔬 Benefícios técnicos

- **Evita problemas de renderizações inconsistentes**
- **Segurança garantida para SSR + CSR**
- Substitui soluções baseadas em `useEffect/useLayoutEffect` que eram frágeis
- Respeita a ordem e atomicidade das atualizações

---

## ❗ Anti-patterns

| Padrão                               | Correção                                     |
|--------------------------------------|-----------------------------------------------|
| Usar `useEffect` para ler valor externo sem assinar corretamente | Use `useSyncExternalStore` |
| Usar `useSyncExternalStore` para dados locais (useState serve) | Simplifique |
| Ignorar `getSnapshot` como fonte primária | `getSnapshot` deve refletir o valor atual corretamente |

---

## 📚 Conclusão

`useSyncExternalStore` é o hook definitivo para:

✅ Sincronizar React com fontes externas de forma consistente  
✅ Garantir compatibilidade com React 18+ e SSR  
✅ Evitar flickers, inconsistências ou assinaturas quebradas

Use quando seu estado **não está dentro do React**, mas precisa **influenciar a interface** de forma reativa e segura.

