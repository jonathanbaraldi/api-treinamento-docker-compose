# api-treinamento-docker-compose
Construção da API do treinamento para rodar com o Docker Compose

http://anandmanisankar.com/posts/docker-container-nginx-node-redis-example/


----------------------------------------------------------------
# 0) Container REDIS
	# docker build -t <your username>/redis .
	# docker run -d --name redis -p 6379:6379 <your username>/redis
	# docker run -d --name redis -p 6379:6379 jonathanbaraldi/redis

Com isso temos o container do Redis rodando na porta 6379.

Docker, in addition to creating the environment variables, also updates the host entries in /etc/hosts file. In fact, Docker documentation recommends using the host entries from etc/hosts instead of the environment variables because the variables are not automatically updated if the source container is restarted.

----------------------------------------------------------------
# 1) Container Nodejs	
Ir no diretório /node onde tem o Dockerfile da aplicação, e rodar o build.
	Fazendo a imagem
	# docker build -t <your username>/node .
	Rodando a imagem do node, fazendo a ligação com o container do Redis
	# docker run -d --name node -p 8080:8080 --link <your username>:redis <your username>/node
	# docker run -d --name node -p 8080:8080 --link redis:redis jonathanbaraldi/node

Com isso já temos a aplicação rodando, conectada no Redis

# 2) Container NGiNX 
Ir no diretório /nginx onde tem o Dockerfile da aplicação, e rodar o build.
	Fazendo a imagem
	# docker build -t <your username>/nginx .
	Criando o container do nginx a partir da imagem e fazendo a ligação com o container do Node
	# docker run -d --name nginx -p 80:80 --link <app running>:node <your username>/nginx
	#  docker run -d --name nginx -p 80:80 --link node:node jonathanbaraldi/nginx



