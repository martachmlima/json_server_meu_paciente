<h1 align="center">
Json Server - Eu Paciente
</h1>

<p align = "center">
Esta é uma fake API que permite que usuários se cadastrem, façam login e cadastrem consultas, medicamentos, vacinas e exames em seu perfil.
</p>

## **Endpoints**

A API tem um total de 9 endpoints.

Destes, 3 podem ser usados para cadastrar o usuário:

POST /register <br/>
POST /signup <br/>
POST /users <br/>

Dois podem ser usados para efetuar o login:

POST /login <br/>
POST /signin<br/>

Um para o usuário acessar, cadastrar e editar suas consultas:

GET /appointments <br/>
POST /appointments <br/>
PATCH /appointments <br/>
DELETE /appointments <br/>
(obs: apenas o dono do recurso pode acessar os dados do endpoint)

Um para o usuário acessar, cadastrar e editar seus medicamentos:

GET /medications <br/>
POST /medications <br/>
PATCH /medications <br/>
DELETE /medications <br/>
(obs: apenas o dono do recurso pode acessar os dados do endpoint)

Um para o usuário acessar, cadastrar e editar suas vacinas:

GET /vaccines <br/>
POST /vaccines <br/>
PATCH /vaccines <br/>
DELETE /vaccines <br/>
(obs: apenas o dono do recurso pode acessar os dados do endpoint)

Um para o usuário acessar, cadastrar e editar seus exames:

GET /exams <br/>
POST /exams <br/>
PATCH /exams <br/>
DELETE /exams <br/>
(obs: apenas o dono do recurso pode acessar os dados do endpoint)

O url base da API é https://api-eu-paciente.herokuapp.com/

## Rotas que não precisam de autenticação

<h2 align ='center'> Criação de usuário </h2>

`POST/register - FORMATO DA REQUISIÇÃO`

```json
{
  "email": "kenzinha@mail.com",
  "password": "123456",
  "name": "Kenzinha",
  "age": 25,
  "weight": 60,
  "height": 170,
  "gender": "female",
  "bloodtype": "A+"
}
```

OBS: apenas os campos email e password são obrigatórios.

Caso dê tudo certo, a resposta será assim:

`POST/register - FORMATO DA RESPOSTA - STATUS 201`

```json
{
  "accessToken": "eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJlbWFpbCI6ImtlbnppbmhhQG1haWwuY29tIiwiaWF0IjoxNjQzMTMyNDA1LCJleHAiOjE2NDMxMzYwMDUsInN1YiI6IjIifQ.bdleOWJDxSH5nefo94WvJPJBYjrmiyjw8i7LO705UYg",
  "user": {
    "email": "kenzinha@mail.com",
    "name": "Kenzinha",
    "age": 25,
    "weight": 60,
    "height": 170,
    "gender": "female",
    "bloodtype": "A+",
    "id": 2
  }
}
```

<h2 align ='center'> Possíveis erros </h2>

Caso algum campo vá em branco, dará o seguinte erro.

`POST/register - `
` FORMATO DA RESPOSTA - STATUS 400`

```json
{
  "status": "error",
  "message": "Email and password are required"
}
```

Email já cadastrado:

`POST/register - `
` FORMATO DA RESPOSTA - STATUS 400`

```json
{
  "status": "error",
  "message": "Email already exists"
}
```

<h2 align = "center"> Login </h2>

`POST/login - FORMATO DA REQUISIÇÃO`

```json
{
  "email": "kenzinha@mail.com",
  "password": "123456"
}
```

Caso dê tudo certo, a resposta será assim:

`POST/login - FORMATO DA RESPOSTA - STATUS 201`

```json
{
  "accessToken": "eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJlbWFpbCI6ImtlbnppbmhhQG1haWwuY29tIiwiaWF0IjoxNjQzMTMyNTQyLCJleHAiOjE2NDMxMzYxNDIsInN1YiI6IjIifQ.nbenHnrNpKxLEiwfS6TbgdDMHHx50nGYql7SdeFPZR0",
  "user": {
    "email": "kenzinha@mail.com",
    "name": "Kenzinha",
    "age": 25,
    "weight": 60,
    "height": 170,
    "gender": "female",
    "bloodtype": "A+",
    "id": 2
  }
}
```

<p>Nessa resposta temos o token de autenticação para as rotas em que ele é necessário: appointments, medications, vaccines, exams.</p>

## Rotas que necessitam de autorização

Rotas que necessitam de autorização deve ser informado no cabeçalho da requisição o campo "Authorization", dessa forma:

> Authorization: Bearer {token}

<p>Após o usuário estar logado, ele deve conseguir consultar, adicionar, deletar e editar consultas, medicações, vacinas e exames.</p>

<h2 align ='center'> Adicionar consultas </h2>

`POST/appointments/ - FORMATO DA REQUISIÇÃO`

```json
{
  "doctor": "Doutor Ciclano",
  "date": "01/03/2022",
  "time": "15h",
  "contact": 99999999999,
  "completed": false,
  "userId": 1
}
```

<h2 align ='center'> Editar consultas </h2>

`PATCH/appointments/appointment_id - FORMATO DA REQUISIÇÃO`

```json
{
  "completed": true
}
```

Todos os campos podem ser alterados, menos o userId e o id.

<h2 align ='center'> Deletar consulta </h2>

Requisição não necessita de body, apenas o id da consulta a ser deletada é passado por parâmetro.

`DELETE /appointments/appointment_id - FORMATO DA REQUISIÇÃO`

<h2 align ='center'> Buscar todas as consultas </h2>

Requisição não necessita de body.

`GET /appointments - FORMATO DA RESPOSTA - STATUS 200`

```json
[
  {
    "doctor": "Doutor Ciclano",
    "date": "01/03/2022",
    "time": "15h",
    "contact": 99999999999,
    "completed": false,
    "userId": 1,
    "id": 1
  }
]
```

<h2 align ='center'> Buscar consulta específica </h2>

Requisição não necessita de body.

`GET /appointments/appointment_id - FORMATO DA RESPOSTA - STATUS 200`

```json
{
  "doctor": "Doutor Ciclano",
  "date": "01/03/2022",
  "time": "15h",
  "contact": 99999999999,
  "completed": false,
  "userId": 1,
  "id": 1
}
```

<h2 align ='center'> Adicionar medicamentos </h2>

`POST/medications/ - FORMATO DA REQUISIÇÃO`

```json
{
  "name": "remédio 1",
  "frequency": "diário",
  "time": "12h45",
  "function": "diminuir pressão",
  "completed": false,
  "userId": 1
}
```

<h2 align ='center'> Editar medicamentos </h2>

`PATCH/medications/medication_id - FORMATO DA REQUISIÇÃO`

```json
{
  "completed": true
}
```

Todos os campos podem ser alterados, menos o userId e o id.

<h2 align ='center'> Deletar medicamentos </h2>

Requisição não necessita de body, apenas o id do medicamento a ser deletado é passado por parâmetro.

`DELETE /medications/medication_id - FORMATO DA REQUISIÇÃO`

<h2 align ='center'> Buscar todos os medicamentos </h2>

Requisição não necessita de body.

`GET /medications - FORMATO DA RESPOSTA - STATUS 200`

```json
[
  {
    "name": "remédio 1",
    "frequency": "diário",
    "time": "12h45",
    "function": "diminuir pressão",
    "completed": false,
    "userId": 1,
    "id": 2
  }
]
```

<h2 align ='center'> Buscar medicamento específico </h2>

Requisição não necessita de body.

`GET /medications/medication_id - FORMATO DA RESPOSTA - STATUS 200`

```json
{
  "name": "remédio 1",
  "frequency": "diário",
  "time": "12h45",
  "function": "diminuir pressão",
  "completed": false,
  "userId": 1,
  "id": 2
}
```

<h2 align ='center'> Adicionar vacinas </h2>

`POST/vaccines/ - FORMATO DA REQUISIÇÃO`

```json
{
  "type": "covid",
  "date": "01/03/2022",
  "nextshot": "01/03/2030",
  "completed": false,
  "userId": 1
}
```

<h2 align ='center'> Editar vacinas </h2>

`PATCH/vaccines/vaccine_id - FORMATO DA REQUISIÇÃO`

```json
{
  "completed": true
}
```

Todos os campos podem ser alterados, menos o userId e o id.

<h2 align ='center'> Deletar vacinas </h2>

Requisição não necessita de body, apenas o id da vacina a ser deletada é passado por parâmetro.

`DELETE /vaccines/vaccine_id - FORMATO DA REQUISIÇÃO`

<h2 align ='center'> Buscar todas as vacinas </h2>

Requisição não necessita de body.

`GET /vaccines - FORMATO DA RESPOSTA - STATUS 200`

```json
[
  {
    "type": "covid",
    "date": "01/03/2022",
    "nextshot": "01/03/2030",
    "completed": false,
    "userId": 1,
    "id": 1
  }
]
```

<h2 align ='center'> Buscar vacina específica </h2>

Requisição não necessita de body.

`GET /vaccines/vaccine_id - FORMATO DA RESPOSTA - STATUS 200`

```json
{
  "type": "covid",
  "date": "01/03/2022",
  "nextshot": "01/03/2030",
  "completed": false,
  "userId": 1,
  "id": 1
}
```

<h2 align ='center'> Adicionar exames </h2>

`POST/exams/ - FORMATO DA REQUISIÇÃO`

```json
{
  "type": "Raiox-x",
  "date": "01/03/2022",
  "link_to_image": "www.seila",
  "completed": false,
  "userId": 1
}
```

<h2 align ='center'> Editar exames </h2>

`PATCH/exams/exam_id - FORMATO DA REQUISIÇÃO`

```json
{
  "link_to_image": "www.seila2"
}
```

Todos os campos podem ser alterados, menos o userId e o id.

<h2 align ='center'> Deletar exames </h2>

Requisição não necessita de body, apenas o id do exame a ser deletado é passado por parâmetro.

`DELETE /exams/exam_id - FORMATO DA REQUISIÇÃO`

<h2 align ='center'> Buscar todos os exames </h2>

Requisição não necessita de body.

`GET /exams - FORMATO DA RESPOSTA - STATUS 200`

```json
[
  {
    "type": "Raiox-x",
    "date": "01/03/2022",
    "link_to_image": "www.seila",
    "completed": false,
    "userId": 1,
    "id": 1
  }
]
```

<h2 align ='center'> Buscar exame específico </h2>

Requisição não necessita de body.

`GET /exams/exam_id - FORMATO DA RESPOSTA - STATUS 200`

```json
{
  "type": "Raiox-x",
  "date": "01/03/2022",
  "link_to_image": "www.seila",
  "completed": false,
  "userId": 1,
  "id": 1
}
```
