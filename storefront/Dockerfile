# ===== BASE STAGE =====

FROM node:17 as base

WORKDIR /app/admin

COPY package*.json ./

COPY . .

# ===== DEVELOPMENT STAGE =====

FROM base as dev

ENV NODE_ENV=development

RUN npm install

CMD [ "gatsby", "develop", "-H", "0.0.0.0",  "-p", "7000" ]

# ===== BUILDER STAGE =====

FROM base as builder

ENV NODE_ENV=production

RUN npm install --production

# ===== NGINX STAGE =====

FROM nginx:alpine

COPY --from=builder /app/admin/public /usr/share/nginx/html