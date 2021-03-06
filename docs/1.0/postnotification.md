---
layout: page-classic-sidebar-left
title: Notificação de Mudança de Status
featimg: MapAntifraud.png
previous: /docs/1.0/analise
next: /docs/1.0/autenticacao
---
---

Serviço que envia um post de notificação ao cliente caso haja alguma alteração de status. 

* É necessário solicitar a Equipe de Implementação o cadastramento da URL de Mudança de Status.
Quando estimulada pelo servidor da Braspag, enviando o POST, a URL cadastrada para Retorno de
Mudança de Status, deverá retornar o código HTTP 200 (OK), indicando que a mensagem foi recebida e processada com sucesso pelo servidor da loja.

* Se a URL de mudança de status da loja for acessada pelo servidor da Braspag não exibir o código de
confirmação ou ocorrer uma falha na conexão, o servidor irá fazer mais 3 tentativas de envio.

* A URL de mudança de Status de Pagamento somente pode utilizar porta 80 (padrão para http) ou porta
443 (padrão para https). Recomendamos que a loja trabalhe sempre com SSL para esta url, ou seja, sempre HTTPS.

![Notificação de Mudança de Status]({{ site.url }}/img/PostNotification.png){: .centerimg }{:title="Notificação de Mudança de Status "}

#### `POST`{:.http-post} Notificação de Mudança de Status 
----------------------------------------------
Abaixo seguem os exemplos de mensagem que o servidor da Braspag enviará à URL cadastrada, e como deve ser a resposta enviada em caso de sucesso.


**REQUEST:**  

``` http
POST https://urlcadastrada.loja.com.br/Notification/ HTTP/1.1
Host: urlcadastrada.loja.com.br
Content-Type: application/json
```

``` json
{  
   "Id":"9004ba26-f1f1-e611-9400-005056970d6f",
   "OrderId":"4493d42c-8732-4b13-aadc-b07e89732c27",
   "OriginalDecision":"Review",
   "NewDecision":"Accept",
   "Reviewer":"Alberto Moreira da Silva",
   "ReviewerComments":"Transação Aceita Após Ligação para o Cliente",
   "Notes":null,
   "Queue":null,
   "Profile":null
}​​​
```

**RESPONSE:**  

``` http
HTTP/1.1 200 Ok
```