# api-treinamento-docker-compose
Construção da API do treinamento para rodar com o Docker Compose

-------------------------------------------------------
# 0) Ter o docker instalado

-------------------------------------------------------
# 1) Iniciar ambiente do Docker na máquina
	# docker-machine rm default
	# docker-machine create --driver virtualbox default
	# docker-machine env default
	# eval $(docker-machine env default)
Pegar o IP que é usado pela VM do Docker para rodar as aplicações

----------------------------------------------------------------
# 2) Container REDIS
	# docker build -t <your username>/redis .
	# docker run -d --name redis -p 6379:6379 <your username>/redis
	# docker run -d --name redis -p 6379:6379 jonathanbaraldi/redis

Com isso temos o container do Redis rodando na porta 6379.

----------------------------------------------------------------
# 3) Container Nodejs	
Ir no diretório /node onde tem o Dockerfile da aplicação, e rodar o build.
	Fazendo a imagem
	# docker build -t <your username>/node .
	
	Rodando a imagem do node, fazendo a ligação com o container do Redis
	# docker run -d --name node -p 8080:8080 --link <redis name>  <your username>/node
	# docker run -d --name node -p 8080:8080 --link redis jonathanbaraldi/node

Com isso já temos a aplicação rodando, conectada no Redis

# 4) Container NGiNX 
Ir no diretório /nginx onde tem o Dockerfile da aplicação, e rodar o build. Fazendo a imagem: 

	# docker build -t <your username>/nginx .

	Criando o container do nginx a partir da imagem e fazendo a ligação com o container do Node
	# docker run -d --name nginx -p 80:80 --link <app running>  <your username>/nginx
	# docker run -d --name nginx -p 80:80 --link node jonathanbaraldi/nginx


# 5) Docker Compose
Feito isso, colocando os containers para rodar, e interligando eles, podemos ver como funciona nossa aplicação que tem um contador de acessos.
Para rodar nosso docker-compose, precisamos remover todos os containers que estão rodando e ir na raiz do diretório para rodar.

	# docker-compose up
	# curl <ip>:80 
		----------------------------------
		This page has been viewed 29 times
		----------------------------------

E após isso acessar no IP:80, pegando usando

	# docker-machine env default
