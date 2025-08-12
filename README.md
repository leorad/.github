
# Eventos postMessage LEORAD

O LEO utiliza comunicação entre o parent e o iframe usando o método `window.postMessage`. Veja abaixo os principais eventos e exemplos prontos para copiar e colar:

---

## Como emitir eventos do parent para o iframe

```js
// Definir conteúdo no editor
iframe.contentWindow.postMessage({ action: 'setContent', data: '<p>Texto</p>' }, '*');

// Inserir conteúdo no cursor do editor
iframe.contentWindow.postMessage({ action: 'insertContent', data: 'Texto a inserir' }, '*');

// Solicitar o conteúdo atual do editor
iframe.contentWindow.postMessage({ action: 'getContent' }, '*');

// Indicar que o iframe terminou de carregar
iframe.contentWindow.postMessage({ action: 'loaded', data: true }, '*');
```

---

## Como escutar eventos

```js
window.addEventListener('message', function(event) {
  const { action, data } = event.data || {};
  if (action === 'getContent') {
    // Recebe o conteúdo do editor vindo do iframe e manda para o elemento #target
    document.getElementById('target').innerHTML = data;
  }
});
```

---

## Observações

- Sempre utilize o campo `action` para identificar o tipo de evento.
- O campo `data` carrega o conteúdo relevante para cada ação.
- Recomenda-se validar a origem (`event.origin`) para segurança em produção.
