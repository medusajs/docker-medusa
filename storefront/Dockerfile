FROM node:latest

WORKDIR /app/storefront

COPY . .

RUN rm -rf node_modules

RUN apt-get update

RUN npm install -g npm@latest

RUN npm install -g gatsby-cli

RUN npm install sharp

RUN npm install --loglevel=error

ENTRYPOINT ["gatsby", "develop", "-H", "0.0.0.0", "-p", "8000" ]