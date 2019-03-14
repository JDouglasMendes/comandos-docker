### docker-compose.yml ###  

version: '3'  
  services:  
    db:  
      image: postgres:9.6  
      volumes:  
        - dados:/var/lib/postgressql/data  
        - \./scripts:/scripts
        - \./scripts/init.sql:/docker-entrypoint-initdb.d/init.sql
        
      

_docker-compose up -d (Deamon)_  
_docker-compose up exec db psql -U postgres -c '\l'(Olhando as tabela do postgress)_  
_docker-compose down (descendo o servidor que subiu em modo daemon)_  
_docker-compose ps (lista as execuções)_
_docker-compose exe db psql -U postgres -f /scripts/check.sql_


