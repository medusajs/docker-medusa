FROM node:17.1.0 as deps

WORKDIR /app/medusa

COPY package*.json .

RUN npm install -g @medusajs/medusa-cli@latest

COPY . .

RUN npm install

# ===== DEVELOPMENT STAGE =====

FROM deps as dev

ENV NODE_ENV=development

ENTRYPOINT ["./develop.sh", "develop"]

# ===== PRODUCTION BUILDER STAGE =====

FROM deps as builder

ENV NODE_ENV=production

RUN npm run build

# ===== PRODUCTION RUNNER STAGE =====

FROM node:17.1.0-alpine

ENV NODE_ENV=production

COPY --from=builder /app/medusa/dist ./dist

RUN npm install --production

EXPOSE 9000

CMD [ "npm", "run", "start" ]
