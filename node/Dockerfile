	# De onde deve ser pega a imagem e a versão. Nesse caso do repositório padrão do Docker, a imagem do node
FROM node:argon

	# Instalar nodemon
RUN npm install -g nodemon

	# Prover camada de cached para os módulos do Node
ADD package.json /tmp/package.json
RUN cd /tmp && npm install
RUN mkdir -p /src && cp -a /tmp/node_modules /src/

	# Definir diretório de trabalho
WORKDIR /src
ADD . /src

	# Expor porta 8080
EXPOSE  8080

	# Rodar o app usando nodemon
CMD ["nodemon", "/src/index.js"]