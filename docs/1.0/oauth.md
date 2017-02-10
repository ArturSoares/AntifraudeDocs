---
layout: page-classic-sidebar-left
title: Autenticação
previous: /docs/1.0/roles
next: /docs/1.0/product
---
---

A API do Antifraude utiliza o protocolo padrão de mercado OAuth 2.0 para autorização de acesso a seus recursos. 

Este documento descreve o fluxo necessário para que aplicações **cliente** obtenham tokens de acesso válidos para uso na plataforma. Caso deseje mais informações sobre o protocolo OAuth 2.0, consulte [https://oauth.net/2/](https://oauth.net/2/){:target="_blank"}.  

## Fluxo para obtenção do token de acesso  
----------------------------------------------

* O token de acesso é obtido através do fluxo de autorização **Client Credentials**.



![Obtenção de Tokens de Acesso]({{ site.url }}/img/FluxoAntifraude.png){: .centerimg }{:title="Fluxo para obtenção do Token de Acesso "}

-- Fluxo de obtenção do Token de Acesso:

1. A *Aplicação Cliente*, informa à API do *Antifraud Gateway* suas credenciais.  

2. O *Antifraud Gateway* valida a credencial recebida. Se for válida, retorna o token de acesso para a *Aplicação Cliente*.  

-- Fluxo de Análise:

3. A *Aplicação Cliente* informa o token de acesso no cabeçalho da requisições HTTP de Análise de Fraude.   

4. Se o token de acesso for válido, a requisição é processada e a resposta de Análise é retornada *Aplicação Cliente*.



## Exemplo de requisição HTTP  
----------------------------------------------

### Cenário I: Obtenção de token de acesso  

* Para se autenticar com a API do Antifraude, é necessário que sejam previamente criadas as credenciais **user** e **password**, as quais deverão ser solicitadas à equipe de implantação da Braspag.

* Uma vez em posse dessas credenciais, será necessário "codificá-la" em  Base64, utilizando a convenção **"usuario:senha"**.
<br/>Exemplo:

    * User: braspagtestes Password:1q2w3e4r
    * String  a ser codificada em Base 64: **braspagtestes:1q2w3e4r**
    * Resultado: YnJhc3BhZ3Rlc3RlczoxcTJ3M2U0cg==

**REQUEST:**  

``` http
POST /accesstoken HTTP/1.1
Host: {antifraude endpoint}
Content-Type: application/x-www-form-urlencoded
Authorization: Basic {StringCodificadaEmBase64}
Cache-Control: no-cache

grant_type=client_credentials
```

**RESPONSE:**  

``` http
HTTP/1.1 200 OK
Content-Type: application/json;charset=UTF-8
```
``` json
{
  "access_token": "faSYkjfiod8ddJxFTU3vti_rQV9fGvMrBNn0ZIZDqrLadEPKTUjt6ZPJSnNHtvOoJ6KO6gakgeyXNmSxFYHx7Y_-OCf8zgzILTVzCN5G1WTBWOKZHt-RknkmQLOgA882pWhC1gtOIQoq2tFX6-1VhOqsSCrdI3cUa2HolbGkxZWZMTPOl4Jzuy6ejo_USCMBNPqzvinchS0M33Bi8PiWMYwdpAbvwAe_nhIKNGmsAG6s7PTgWc2RksG6DaX8exdjvlGE9CMADq5LeM4JJ-BguZoHAP3yDBVZpe_DzI3JOrAYv0yzToBllPIMmq6CY-V8GJmckWByOGooBKr6COkZ1R9NPg2bvruYEC3g8hzKloUG21CD5r_la-t-0FvGHHY-8L7cKGybLidIYtw5aWOUgO2Aq0YScEnj1byDAsY6ROMnnzLrywkqscsf5xJACJwBmmEggHRyTVMY1-oOzmH6B2GNtC621i2XQ-8U6KVx9qD0R4qdWRn__AFatL7miTthMfO_PO2HWdDX_xD0i0jqcw",
  "token_type": "bearer",
  "expires_in": 599
}
```
 
 * Na resposta é importante ressaltar o campo **expires_in**, com  o tempo de expiração to access_token em segundos.

### Como obter uma credencial de usuário?  

> Solicite uma credencial pelo e-mail [implantacao.operacoes@braspag.com.br](mailto:implantacao.operacoes@braspag.com.br)