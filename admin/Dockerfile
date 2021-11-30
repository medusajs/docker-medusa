FROM node:latest

WORKDIR /app/admin

COPY . .

RUN rm -rf node_modules

RUN apt-get update

RUN npm install -g npm@latest

RUN npm install sharp

RUN npm install -g gatsby-cli

RUN npm install --loglevel=error

RUN npm run build &> /dev/null

CMD [ "gatsby", "develop", "-H", "0.0.0.0",  "-p", "7000" ]