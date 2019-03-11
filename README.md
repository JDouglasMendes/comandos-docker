# comandos-docker

## Comandos para Imagem

 __docker image__ - _comamdo base para gerenciamento de imagem_
 
 __docker image pull__ [NOME DA IMAGEM] - _faz download da imagem do docker hub_

__docker image ls__ _lista todas as imagens_

__docker image rm__[NOME DA TAG] _remove uma imagem_

__docker image inspect__ [NOME DA TAG] _mostra informações da imagem_

__docker image tag__ [TAG ORIGEM] [TAG DESTINO] _cria uma nova imagem a partir de outra_

__docker image build__ _comando para construir uma imagem_

__docker image push__ _envia uma imagem ao registry ou docker hub_

### Links Uteis

[Docker Hub](https://hub.docker.com/search/?type=image) - Repositório de imagens.



# Criando um build

Criar um arquivo de nome _Dockerfile_ __(Deve ser sem extensão)__

FROM nginx:latest

RUN echo '<h1>Hello world !<>/h1' > /usr/share/nginx/html/index.html
  
__Comando para executar__

__docker image build -t [NOME DA TAG] .__

__docker container run -p 80:80 [NOME IMAGEM]__
