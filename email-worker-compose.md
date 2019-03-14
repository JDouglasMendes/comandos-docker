### docker-compose.yml  

version: '3'  
  services:  
    db:  
      image: postgres:9.6  
            
      

_docker-compose up -d (Deamon)_  
_docker-compose up exec db psql -U postgres -c '\l'(Olhando as tabela do postgress)_  
_docker-compose down (descendo o servidor que subiu em modo daemon)_  
