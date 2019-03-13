 _Nome do Arquivo_ __docker-compose.yml__
 
    version: '3'  
       services:  
    db:    
      image: ongo 3.4      
    backend  
      imagem: node: 8.1      
      volumes:      
        -./backend:/backend
      ports:      
        bash - c "cd /backen && npm i && node app"        
    frontend:    
      image: nginx: 1.13      
      volumes:      
        - ./frontend:/usr/share/nginx/html        
      ports:      
        - 80:80        


<blockquote>
  <p>Comando para "subir" as imagens.</p>
  <p>docker-compose up</p>
</lockquote> 
