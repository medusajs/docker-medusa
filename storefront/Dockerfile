# ===== BASE STAGE =====

FROM node:17 as deps

WORKDIR /app/admin

COPY package*.json ./

RUN npm install

RUN npm install -g gatsby-cli

COPY . .

# ===== DEVELOPMENT STAGE =====

FROM deps as dev

ENV NODE_ENV=development

EXPOSE 7000

CMD [ "gatsby", "develop", "-H", "0.0.0.0",  "-p", "7000" ]

# ===== BUILDER STAGE =====

FROM deps as builder

ENV NODE_ENV=production

RUN npm run build

RUN npm install --production


# ===== NGINX STAGE =====

FROM nginx:alpine

COPY --from=builder /app/admin/public /usr/share/nginx/html