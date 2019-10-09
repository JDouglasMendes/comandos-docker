# comandos-docker #

## Comandos para Imagem ##

 __docker image__ - _comamdo base para gerenciamento de imagem_
 
 __docker image pull__ [NOME DA IMAGEM] - _faz download da imagem do docker hub_

__docker image ls__ - _lista todas as imagens_

__docker image rm__ [NOME DA TAG] - _remove uma imagem_

__docker image inspect__ [NOME DA TAG] - _mostra informações da imagem_

__docker image tag__ [TAG ORIGEM] [TAG DESTINO] - _cria uma nova imagem a partir de outra_

__docker image build__ - _comando para construir uma imagem_

__docker image push__ - _envia uma imagem ao registry ou docker hub_

__docker network ls__ - _lista as redes do container_

__docker network inspect__ _[bridge, nome, host]_ - _inspeciona uma rede_

### Links Uteis ###

[Docker Hub](https://hub.docker.com/search/?type=image) - Repositório de imagens.

### Passos para enviar uma imagem para o Docker Hub ###

_1ª)_ __docker image tag__ _[NOME DA TAG]_  _[NOME REGISTRO]/[NOME IMAGEM]:[VERSAO]_

_2ª)_ __docker login --username=__ _[NOME DO USUARIO]_

# Criando um build #

Criar um arquivo de nome _Dockerfile_ __(Deve ser sem extensão)__

FROM nginx:latest

RUN echo 'Hello world !' > /usr/share/nginx/html/index.html
  
_Comando para executar_

__docker image build -t [NOME DA TAG] .__

__docker container run -p 80:80 [NOME IMAGEM]__

### Rede ###

__docker container run -d --net none debian__ _container sem rede_

__docker container run d --net brigde debian__ _container com uma rede brigde_

__docker container run --name ws1 -p8080:80 nginx__ 
<blockquote>
  <p></p>
</blockquote> 

__docker container run --name ws3 -p8080:80 -v(pwd)/html:/usr/share/nginx/html -d nginx__

<blockquote>
  <p></p>
</blockquote> 

__docker container run -nome demonet -it microsoft/dotnet:2.1-sdk__
__dotnet new console__
__dotnet build__
__dotnet run__

__docker container star -it demonet__
<blockquote>
  <p></p>
</blockquote>

__docker container prune__
<blockquote>
  <p></p>
</blockquote>

__docker image rm [nome_imagem]__





