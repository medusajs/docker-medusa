FROM node:17.1.0 as base

WORKDIR /app/medusa

COPY package*.json .

RUN npm install -g @medusajs/medusa-cli@latest

COPY . .

# ===== DEVELOPMENT STAGE =====

FROM  base as dev

ENV NODE_ENV=development

RUN npm install

ENTRYPOINT ["./develop.sh", "develop"]

# ===== PRODUCTION STAGE =====

FROM base as prod

ENV NODE_ENV=production

RUN npm install --production

RUN npm run build

ENTRYPOINT [ "npm", "run", "start" ]
