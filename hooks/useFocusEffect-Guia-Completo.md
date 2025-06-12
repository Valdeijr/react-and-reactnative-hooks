# 🎯 Guia Definitivo do `useFocusEffect` – React Navigation

---

## 📌 O que é `useFocusEffect`

`useFocusEffect` é um hook do React Navigation que executa uma função **toda vez que a tela (screen) ganha foco**, e opcionalmente **limpa algo quando perde o foco**.

```tsx
useFocusEffect(
  useCallback(() => {
    // código executado ao focar a tela

    return () => {
      // código de cleanup ao desfocar
    }
  }, [deps])
)
```

É como `useEffect`, mas amarrado ao **ciclo de vida de navegação da tela** (não apenas à montagem do componente).

---

## 🚦 Diferença entre `useEffect` e `useFocusEffect`

| Característica          | `useEffect`             | `useFocusEffect`                     |
|-------------------------|-------------------------|--------------------------------------|
| Executa ao montar       | ✅                      | ✅ (se for a primeira vez em foco)   |
| Executa ao voltar foco  | ❌                      | ✅                                   |
| Executa ao desfocar     | ❌                      | ✅ (via retorno/cleanup)             |
| Amarrado à navegação    | ❌                      | ✅                                   |

---

## 🧠 Quando usar `useFocusEffect`

### ✅ Casos comuns

- Atualizar dados toda vez que a tela entra em foco
- Adicionar/remover listeners de forma segura (Bluetooth, Location, etc.)
- Resetar formulários, rolar para o topo
- Fechar modal se estiver aberto

---

## ⚠️ Comportamentos importantes

- Executa novamente sempre que a **tela ganhar foco**.
- O cleanup executa quando a tela **perde o foco**, mesmo que o componente não seja desmontado.
- Você **deve envolver a função com `useCallback`** – obrigatório para evitar bugs.

---

## 💡 Exemplo completo

```tsx
useFocusEffect(
  useCallback(() => {
    const sub = AppState.addEventListener('change', state => {
      if (state === 'active') {
        checkSomething()
      }
    })

    return () => sub.remove()
  }, [])
)
```

---

## ❗ Anti-patterns comuns

| Erro | Correção |
|------|----------|
| Passar função inline direto | Use `useCallback` para garantir estabilidade |
| Usar `useEffect` para lógica que depende de foco de tela | Substitua por `useFocusEffect` |
| Esperar que ele execute apenas uma vez | Lembre-se: ele roda a **cada foco** |

---

## ✅ Checklist de uso do `useFocusEffect`

- [ ] A lógica que estou executando precisa rodar toda vez que a tela ganha foco?
- [ ] Estou fazendo cleanup corretamente ao perder o foco?
- [ ] Usei `useCallback` para encapsular a função passada?
- [ ] Evitei criar objetos/funções instáveis como dependência?

---

## 🚀 Dicas de performance

- Combine com `useIsFocused()` se quiser lógica condicional dentro do componente.
- Combine com `queryClient.invalidateQueries()` se estiver usando React Query para buscar dados novamente ao focar.
- Evite lógica muito pesada dentro do callback direto – prefira chamar funções externas ou assíncronas.

---

## 📚 Conclusão

`useFocusEffect` é essencial em apps com React Navigation para lidar com:

✅ Atualizações baseadas no ciclo de foco  
✅ Limpeza de efeitos ao perder foco  
✅ Experiência de usuário fluida ao navegar

Use com `useCallback`, pense no foco como um evento de entrada/saída da tela, e não como montagem/desmontagem do componente.

