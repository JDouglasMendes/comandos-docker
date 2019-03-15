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
    frontend:
      image: nginx:1.13  
      volumes:
        - ./web:/user/share/nginx/html
        - ./nginx/default.comf:/etc/nginx/conf.d/default.conf
      ports:
        - 80:80
    app:
      image: python:3.6
      volumes:
        - ./app:/app
      working_dir: ./app
      comand: bash ./app.sh
      ports:
       - 8080:8080
       
```

### Sevidor em python para envio do e-mail ###

```
import psycopg2
import redis
import json
import os
from bottle import Bottle, request


class Sender(Bottle):
    def __init__(self):
        super().__init__()
        self.route('/', method='POST', callback=self.send)
        
        redis_host = os.getenv('REDIS_HOST', 'queue')
        self.fila = redis.StrictRedis(host=redis_host, port=6379, db=0)

        db_host = os.getenv('DB_HOST', 'db')
        db_user = os.getenv('DB_USER', 'postgres')
        db_name = os.getenv('DB_NAME', 'sender')
        dsn = f'dbname={db_name} user={db_user} host={db_host}'
        self.conn = psycopg2.connect(dsn)
        
    def register_message(self, assunto, mensagem):
        SQL = 'INSERT INTO emails (assunto, mensagem) VALUES (%s, %s)'
        cur = self.conn.cursor()
        cur.execute(SQL, (assunto, mensagem))
        self.conn.commit()
        cur.close()

        msg = {'assunto': assunto, 'mensagem': mensagem}
        self.fila.rpush('sender', json.dumps(msg))

        print('Mensagem registrada !')

    def send(self):
        assunto = request.forms.get('assunto')
        mensagem = request.forms.get('mensagem')

        self.register_message(assunto, mensagem)
        return 'Mensagem enfileirada ! Assunto: {} Mensagem: {}'.format(
            assunto, mensagem
        )

if __name__ == '__main__':
    sender = Sender()
sender.run(host='0.0.0.0', port=8080, debug=True)
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

_docker-compose up -d (Daemon)_  
_docker-compose up exec db psql -U postgres -c '\l'(Olhando as tabela do postgress)_  
_docker-compose down (descendo o servidor)_  
_docker-compose ps (lista as execuções)_
_docker-compose exe db psql -U postgres -f /scripts/check.sql_
_docker-compose logs -f -t(mostra os logs)_ 



