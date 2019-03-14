# Exemplo 
* Montando um ambiente para envio de e-mail com as seguntes imagens:
* {frontend, app, banco de dados, mensageriacom redis. 3 workes para ler a fila do redis}

### docker-compose.yml ###
```
version: '3'  
  services:  
    db:  
      image: postgres:9.6  
      volumes:  
        - dados:/var/lib/postgressql/data  
        - \./scripts:/scripts
        - \./scripts/init.sql:/docker-entrypoint-initdb.d/init.sql              
```

### Criação da tabela que onde será salvo os e-mails ###

* Esse deve ter o nome de "init.sql" para respeitar a convenção da imagem postgres.

```
create database email_sender;

\c email_sender

create table emails (
    id serial not null,
    data timestamp not null default current_timestamp,
    assunto varchar(100) not null,
    mensagem varchar(250) not null
);

```

```
\l
\c email_sender
\d emails
```

_docker-compose up -d (Deamon)_  
_docker-compose up exec db psql -U postgres -c '\l'(Olhando as tabela do postgress)_  
_docker-compose down (descendo o servidor que subiu em modo daemon)_  
_docker-compose ps (lista as execuções)_
_docker-compose exe db psql -U postgres -f /scripts/check.sql_


