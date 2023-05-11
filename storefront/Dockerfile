#Dependencies
FROM node:18-alpine3.16 as deps
WORKDIR /app/storefront/
#   Copy storefront package package.json and yarn.lock from /storefront
COPY ./package.json .
COPY ./yarn.lock .
#   Install deps
RUN yarn install --frozen-lockfile

#Build
FROM node:18-alpine3.16 as runner
WORKDIR /app/storefront/
#   Copy cached node_modules from deps
COPY --from=deps /app/storefront/node_modules /app/storefront/node_modules
#   Copy app source code and monorepo root package.json
COPY ./storefront /app/storefront

#   Run the storefront in dev mode
ENTRYPOINT [ "yarn", "dev" ]