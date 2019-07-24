# Desafio Backend Barato Coletivo 2019

Oi! Quer fazer parte do nosso time **Barato Coletivo**? Se você deseja participar do nosso processo seletivo, siga as instruções desse desafio e nos mande sua resolução em um *pull request* nesse repositório do Github.


# Sobre o Barato
Somos uma empresa a 10 anos no mercado. O maior e-commerce de serviços e oportunidades do nordeste. Nosso grande desafio é continuar crescendo e acompanhando o mercado cada vez mais competitivo. 

## Nossa stack:
- Site: Laravel / Zend Framework / Code Igniter / MySQL
- Outras tecnologias utilizadas: Linux / Nodejs / Vuejs / MySQL / Postgresql / Docker / AWS


# Vagas disponíveis
 - Desenvolvedor Estágio Backend Frontend (Limite para envio do desafio: 10/08/2019)
 - Desenvolvedor CLT Backend (Jr/Pleno) (Limite para envio do desafio: 10/08/2019)


# Conhecimentos necessários para Frontend Pleno

Nesse desafio você deverá criar um novo serviço de disparo de emails para o Barato. O desafio consiste no seguinte:
Você deverá disponiblizar um endpoint da seguinte forma:


#### Primeiro Endpoint

`POST /seusistema/emails/queue`

Esse EndPoint deve receber um JSON via post da seguinte forma:

```json
{
    "template": "new-user",
    "from": "Barato Coletivo",
    "fromEmail": "disparo@barato.com",
    "subject": "Novo usuário",
    "vars": {
      "name": "Nome do usuario",
      "link": "https://www.barato.com.br/"
   }
  }
```

Então o email deverá ser adicionado a uma fila (Projete essa fila usando banco de dados MySQL).

Em seguida você deverá fazer uma rotina que dispara esses emails partindo de um serviço gratuito de sua preferência.
  - Você pode usar SendGrid, Mailjet ou até mesmo MailTrap para fazer o disparo.

No banco de dados deverá ser armazenado o status do email: queued, sended ou error.
Caso o disparo dê erro, você deverá adicionar um contador e fazer até 3 tentativas de envio, após a 3a tentativa mal sucedida, o status vira "failed" e o email não mais entrará na fila.

#### Segundo endpoint:

`POST /seusistema/emails/addTemplate`

Esse EndPoint deve receber um JSON via post da seguinte forma:

```json
{
    "name": "nomedonovotemplate",
    "defaultFrom": "Barato Coletivo",
    "defaultFromEmail": "disparo@barato.com",
    "defaultSubject": "Novo usuário",
    "html":"<html><body> {{nome}} {{link}}</body></html>"
  }
```

Nesse endpoint, você vai disponibilizar uma forma de criar templates.
Lembrando que {{variavel}} vira uma variável que deve ser substituída pelo conteúdo do campo "vars" do primeiro endpoint.

Você deve armazenar esse email da forma como achar melhor: Seja numa tabela no banco ou em um arquivo no projeto.
Caso eu envie um template com o mesmo nome de um já existente, o existente deve ser atualizado para os dados que estão vindo na requisição atual, ou seja, deve ser atualizado. O sistema deve fornecer um retorno informando a atualização ou o cadastro do novo template.

#### terceiro endpoint:

`GET /seusistema/emails/status/{ID}`

Esse EndPoint deve receber na URL o ID de um email previamente agendado, para saber o status desse email.

Deve retornar:

```json
{
    "status": "success",
    "statusEmail": "sended",
  }
```


```json
{
    "status": "success",
    "statusEmail": "queued",
  }
```


```json
{
    "status": "success",
    "statusEmail": "error",
    "attempts": 2 
  }
```
(Attemps) quantidade de tentativas que ainda serão feitas para o envio.

```json
{
    "status": "success",
    "statusEmail": "failed"
  }
```

#### Premissas do desafio
Forneça sempre mensagens de erro e sucesso no retorno das requisições.
O formato deve ser algo do tipo:

```json
{
  "status": "success",
  "message": "Template atualizado com sucesso"
}

```

```json
{
  "status": "success",
  "message": "Email agendado",
  "id": "iddoagendamento"
}
```


### Qual arquitetura usar

Fique a vontade para definir seu stack, seja em PHP / NodeJS ou a tecnologia de sua preferência.
Contudo, o resultado deve estar rodando no Docker com docker-compose configurado, ou seja:

O comando
`docker-compose up`
deverá ser o suficiente para que seu projeto esteja rodando e os endpoints funcionando na porta 8080 local.


 
### Como nos enviar a resolução

Adicione um Pull request com sua solução para o problema ou compacte um ZIP do seu código e envie para:
`joaoneto[a]baratocoletivo.com.br`
Não esqueça de criar um README com instruções de como fazer seu código funcionar.


### Diferenciais

- Testes unitários
- Dashboard admin simples apenas com a lista de emails agendados / enviados / erro
- Usar redis ou outro gerenciador de fila
- Usar Lumen / Laravel
- Autenticar a API 
