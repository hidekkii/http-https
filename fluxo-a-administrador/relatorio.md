# Relatório — Laboratório de Inspeção HTTP/HTTPS — Fluxo A (Administrador)

> **Como usar este template.** Preencha cada campo `[...]` com sua resposta e arraste as capturas de tela diretamente para os locais indicados. Preserve a formatação Markdown.
>
> **Escopo:** este fluxo inclui HTTP em texto claro, HTTPS sem decriptação e HTTPS com decriptação TLS pelo Fiddler Classic.

---

## Como anexar capturas de tela

1. Faça a captura de tela e salve como PNG.
2. No editor do GitHub ou GitHub.dev, posicione o cursor no local indicado.
3. Arraste o PNG para o editor. O GitHub inserirá uma linha `![image](...)`.

---

## Identificação

| Campo | Valor |
|---|---|
| Nome | Bruno Reis e Renan Hideki |
| RA | 240017 e 240823 |
| Disciplina | Redes de Computadores |
| Turma | A |
| Data | 15/05/2026 |
| Fluxo | **A — Aluno com privilégio de administrador** |
| SO utilizado | [Windows 10 / Windows 11] |
| Ferramenta de proxy | Fiddler Classic |
| Navegador(es) | Edge |
| Decriptação HTTPS habilitada? | Sim  |
| Certificado Fiddler instalado durante a atividade? | Sim |

---

## Atividade 1 — Primeira captura

### Captura

<!-- arraste a captura aqui: sessão de http://example.com com Request/Response Raw --><img width="1515" height="544" alt="1" src="https://github.com/user-attachments/assets/22a88d1d-eba2-4330-9194-69407a0dc8ae" />


**Request-line:**

```http
GET http://example.com/ HTTP/1.1
```

**Status-line:**

```http
HTTP/1.1 200 OK

```

**Cabeçalhos do request:**

| Cabeçalho | Função |
|---|---|
|Content-Type: | text/html |
| Transfer-Encoding: | chunked|
| [...] | [...] |

**Resposta:**

| Campo | Valor observado |
|---|---|
| `Content-Type` | [...] |
| `Content-Length` ou `Transfer-Encoding` | [...] |

---

## Atividade 2 — Anatomia de um GET

### Captura
<img width="1916" height="1078" alt="json" src="https://github.com/user-attachments/assets/335ac871-e52b-4433-91df-90184e144704" />



**Request-line completa:**

```http
GET https://http.aulasrede.com.br/get?aluno=renan&curso=redes HTTP/1.1![Uploading json.PNG…]()


```

**Cabeçalhos-chave:**

| Cabeçalho | Valor |
|---|---|
|Host: | http.aulasrede.com.br |
| User-Agent: | Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/142.0.0.0 Safari/537.36 Edg/142.0.0.0
 |
| Accept-Encoding: | gzip, deflate, br, zstd |

**Campos do JSON de resposta:**

```json
{
  {
  "args": {
    "aluno": [
      "renan"
    ],
    "curso": [
      "redes"
    ]
  },
  "headers": {
    "Accept": [
      "text/html,application/xhtml+xml,application/xml;q=0.9,image/avif,image/webp,image/apng,*/*;q=0.8,application/signed-exchange;v=b3;q=0.7"
    ],
"origin": "200.210.165.75:49351",

}
```

**Resposta curta:** o que o campo `origin` representa? O `User-Agent` retornado coincide com o enviado?

[resposta]

---Representa a origem da requisição, ou seja, o IP e a porta de rede de onde a solicitação saiu.
Sim. O User-Agent retornado coincide.

## Atividade 3 — POST e envio de formulário

### Captura

<img width="1920" height="1080" alt="post" src="https://github.com/user-attachments/assets/4fd57d8c-621e-4dec-bf47-27ef44d6d96a" />


**Request-line do POST:**

```http
POST https://http.aulasrede.com.br/post HTTP/1.1

```

| Cabeçalho | Valor |
|---|---|
| Content-Type: | application/x-www-form-urlencoded
|
| Content-Length: | 88|

**Corpo do request:**

```text
Host: http.aulasrede.com.br
Connection: keep-alive
Content-Length: 88
Cache-Control: max-age=0
sec-ch-ua: "Chromium";v="142", "Microsoft Edge";v="142", "Not_A Brand";v="99"
sec-ch-ua-mobile: ?0
sec-ch-ua-platform: "Windows"
Upgrade-Insecure-Requests: 1
User-Agent: Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/142.0.0.0 Safari/537.36 Edg/142.0.0.0
Origin: https://http.aulasrede.com.br
Content-Type: application/x-www-form-urlencoded
Accept: text/html,application/xhtml+xml,application/xml;q=0.9,image/avif,image/webp,image/apng,*/*;q=0.8,application/signed-exchange;v=b3;q=0.7
Sec-Fetch-Site: same-origin
Sec-Fetch-Mode: navigate
Sec-Fetch-User: ?1
Sec-Fetch-Dest: document
Referer: https://http.aulasrede.com.br/forms/post
Accept-Encoding: gzip, deflate, br, zstd
Accept-Language: pt-BR,pt;q=0.9,en;q=0.8,en-GB;q=0.7,en-US;q=0.6

nome=renan&disciplina=Redes&observacao=Teste+de+formul%C3%A1rio+HTTP.+&interesse=headers
```

**Campo `form` da resposta:**

```json

  "form": {
    "nome": [
      "renan"
    ],
    "disciplina": [
      "Redes"
    ],
    "observacao": [
      "Teste de formulário HTTP. "
    ],
    "interesse": [
      "headers"
    ]
  },

```

**Resposta curta:** qual formato codifica o corpo? Qual aba mostra literalmente os bytes enviados: `WebForms` ou `Raw`?

[resposta]

--- formato application/x-www-form-urlencoded. São mostrados na aba raw.

## Atividade 4 — Status codes

### Captura

<!-- arraste a captura aqui: lista do Fiddler com as quatro sessões -->

| # | Método | URL | Status-line | Tamanho/body |
|---|---|---|---|---|
| 1 | GET | `https://http.aulasrede.com.br/status/200` | HTTP/1.1 200 OK | 55|
| 2 | GET | `https://http.aulasrede.com.br/redirect-to?status_code=301&url=/get` | HTTP/1.1 200 OK | 1.584 |
| 3 | GET | `https://http.aulasrede.com.br/status/404` | HTTP/1.1 404 Not Found | 45 |
| 4 | GET | `https://http.aulasrede.com.br/status/500` | HTTP/1.1 500 Internal Server Error| 57 |

**Resposta curta:** no `301`, qual cabeçalho informa o destino do redirecionamento?

[resposta]

---GET https://http.aulasrede.com.br/get HTTP/1.1

## Atividade 5 — Cabeçalhos essenciais

### Captura

<img width="912" height="444" alt="mtcoisa" src="https://github.com/user-attachments/assets/40a416d0-2e23-4304-a831-e9b76281fb69" />


| Cabeçalho | Req/Resp | Valor capturado | Função |
|---|---|---|---|
| `Host` | http.aulasrede.com.br | [...] | [...] |
| `User-Agent` | [...] | [...] | [...] |
| `Accept` | [...] | [...] | [...] |
| `Content-Type` | [...] | [...] | [...] |
| `Content-Length` / `Transfer-Encoding` | [...] | [...] | [...] |
| `Content-Encoding` | [...] | [...] | [...] |
| `Set-Cookie` | [...] | [...] | [...] |
| `Cache-Control` | [...] | [...] | [...] |
| `Strict-Transport-Security` | [...] | [...] | [...] |

**Resposta curta:** qual é o papel de `Content-Encoding` e de `Strict-Transport-Security`?

[resposta]

---

## Atividade 6 — HTTP vs HTTPS

### Captura — HTTP puro

<!-- arraste a captura aqui: http://http.aulasrede.com.br/get com redirecionamento 301 para HTTPS -->

### Captura — HTTPS sem decriptação

<!-- arraste a captura aqui: https://http.aulasrede.com.br/get sem decriptação -->

### Captura — HTTPS com decriptação

<!-- arraste a captura aqui: https://http.aulasrede.com.br/get com decriptação -->

| Situação | O que ficou visível? | O que ficou oculto? |
|---|---|---|
| HTTP puro | [...] | [...] |
| HTTPS sem decriptação | [...] | [...] |
| HTTPS com decriptação | [...] | [...] |

**Resposta curta:** por que a decriptação HTTPS pelo Fiddler exige instalar um certificado raiz?

[resposta]

---

## Atividade 7 — Cookies e sessão

### Captura

<!-- arraste a captura aqui: sequência cookies/set e cookies -->

| # | URL | `Set-Cookie` recebido | `Cookie` enviado |
|---|---|---|---|
| 1 | `/cookies/set?...` | [...] | [...] |
| 2 | `/cookies` | [...] | [...] |
| 3 | `/cookies` após recarregar | [...] | [...] |

**Resposta curta:** `Set-Cookie` apareceu em toda requisição ou apenas quando o servidor definiu/atualizou cookies? Quais atributos foram observados?

[resposta]

---

## Atividade 8 — Manipulação simples com breakpoint *(Opcional)*

### Captura

<!-- arraste a captura aqui: breakpoint com User-Agent editado -->

**JSON de resposta:**

```json
{
  "user-agent": ["[valor observado]"]
}
```

**Resposta curta:** o que este teste mostra sobre o papel ativo de um proxy?

[resposta]

- [ ] Breakpoints desabilitados ao final

---

## Reflexão final (opcional)

[até 10 linhas]

---

## Encerramento — Higiene de segurança

### Captura antes da remoção

<!-- arraste aqui a captura do certmgr.msc mostrando DO_NOT_TRUST_FiddlerRoot presente -->

### Captura depois da remoção

<!-- arraste aqui a captura mostrando o certificado ausente -->

- [ ] `Decrypt HTTPS traffic` desabilitado no Fiddler
- [ ] Certificado `DO_NOT_TRUST_FiddlerRoot` removido do Windows
- [ ] Certificado `DO_NOT_TRUST_FiddlerRoot` removido do Firefox, se aplicável
- [ ] Fiddler fechado

**Por que esta etapa é importante?**

[resposta curta]

---

## Checklist de entrega

- [ ] Campos `[...]` substituídos
- [ ] Capturas inseridas
- [ ] Atividades 1 a 7 preenchidas; Atividade 8 preenchida se executada
- [ ] Encerramento com duas capturas concluído
- [ ] PDF gerado como `SOBRENOME_NOME_RA_LAB_HTTP_FLUXOA.pdf`
- [ ] PDF submetido no Microsoft Teams
