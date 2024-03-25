# Relatório sobre o Uso do k6 para Testes de Carga e Requisições HTTP

## Introdução

O **k6** é uma ferramenta de código aberto utilizada para execução de testes de carga e performance. Neste relatório, o uso do k6 para realizar requisições HTTP, destacando os conceitos aprendidos e a sua aplicação prática.

## Requisições HTTP

Um dos passos fundamentais na criação de testes de carga é a definição das requisições HTTP que serão utilizadas para avaliar o sistema. O k6 facilita a realização dessas requisições através de métodos específicos, tais como `get()` e `post()`, permitindo simular o comportamento de usuários acessando um sistema via protocolo HTTP.

### Exemplo de Requisição GET

Um exemplo simples de uma requisição GET utilizando k6 seria o seguinte:

```javascript
import http from 'k6/http';

export default function () {
  http.get('http://test.k6.io');
}
```

### Exemplo de Requisição POST

Para uma requisição POST que envolve autenticação em um serviço ou site, podemos utilizar o seguinte código:

```javascript
import http from 'k6/http';

export default function () {
  const url = 'http://test.k6.io/login';
  const payload = JSON.stringify({
    email: 'aaa',
    password: 'bbb',
  });

  const params = {
    headers: {
      'Content-Type': 'application/json',
    },
  };

  http.post(url, payload, params);
}
```

### Métodos Disponíveis

O módulo `http` do k6 oferece uma variedade de métodos para lidar com requisições HTTP:

- `batch()`
- `del()`
- `get()`
- `head()`
- `options()`
- `patch()`
- `post()`
- `put()`
- `request()`

Esses métodos permitem realizar diferentes tipos de requisições HTTP, adequando-se às necessidades específicas de cada teste.

## Tags de Requisição HTTP

O k6 automaticamente aplica tags às requisições HTTP, facilitando a organização e análise dos resultados obtidos durante os testes de carga. Algumas das tags disponíveis incluem:

- `expected_response`
- `group`
- `name`
- `method`
- `scenario`
- `status`
- `url`

Estas tags fornecem informações importantes sobre cada requisição, como o método utilizado, o status da resposta e a URL requisitada.

## Agrupamento de URLs

O k6 permite agrupar URLs sob uma única tag, o que pode ser útil para testes que envolvam URLs dinâmicas. Por exemplo, podemos utilizar o seguinte código para agrupar requisições a diferentes URLs em uma única métrica:

```javascript
import http from 'k6/http';

export default function () {
  for (let id = 1; id <= 100; id++) {
    http.get(`http://example.com/posts/${id}`, {
      tags: { name: 'PostsItemURL' },
    });
  }
}
```

Dessa forma, todas as requisições são agrupadas sob a tag `name: 'PostsItemURL'`, facilitando a análise dos resultados.
