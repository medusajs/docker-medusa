<p align="center">
  <a href="https://www.medusa-commerce.com">
    <img alt="Medusa" src="https://user-images.githubusercontent.com/7554214/129161578-19b83dc8-fac5-4520-bd48-53cba676edd2.png" width="100" />
  </a>
</p>
<h1 align="center">
  Docker Medusa
</h1>
<p align="center">
This repo provides the basis for you to get started with a complete <a href="https://github.com/medusajs/medusa">Medusa</a> setup using docker compose. The complete setup includes: 
<ul>
  <li><b>`/backend`</b>: Your Medusa instance, located in the <i>backend</i> folder</li>
  <li><b>`/admin`</b>: Medusa Admin where you control all aspects of your store</li>
  <li><b>`/storefront`</b>: Storefront for your customers to shop</li>
</ul>

**This project is inteded for development only at this time.**

The files for both the <i>Medusa server</i> and the <i>Storefront</i> are loaded in Bind Mounts allowing you to change the server functionality and have the change be hot-reloaded onto your running containers.

 <!-- Follow the steps below to get ready. -->
</p>
<p align="center">
  <a href="https://github.com/medusajs/medusa/blob/master/LICENSE">
    <img src="https://img.shields.io/badge/license-MIT-blue.svg" alt="Medusa is released under the MIT license." />
  </a>
  <a href="https://github.com/medusajs/medusa/blob/master/CONTRIBUTING.md">
    <img src="https://img.shields.io/badge/PRs-welcome-brightgreen.svg?style=flat" alt="PRs welcome!" />
  </a>
  <a href="https://discord.gg/xpCwq3Kfn8">
    <img src="https://img.shields.io/badge/chat-on%20discord-7289DA.svg" alt="Discord Chat" />
  </a>
  <a href="https://twitter.com/intent/follow?screen_name=medusajs">
    <img src="https://img.shields.io/twitter/follow/medusajs.svg?label=Follow%20@medusajs" alt="Follow @medusajs" />
  </a>
</p>

---

## Setting up your Medusa

To set up Medusa in a development environment with Docker you should initially build the images since they are not published on dockerhub. This is accomplished by adding the `--build` flag as shown below:

```bash
docker compose up --build
```

Having already built the Docker images you can run docker compose without the `--build` flag.

```
docker compose up
```

Your local Medusa setup is now running with each of the services occupying the following ports:

<ul>
  <li><b>Medusa Server</b>: 9000
  <li><b>Medusa Admin</b>: 7000
  <li><b>Storefront</b>: 8000
  <li><b>postgres</b>: 5432
  <li><b>redis</b>: 6379
</ul>

_Note: If you change the dependencies of your projects by adding new packages you can simply rebuild that package with the same tag `test` and run `docker compose up` once again to update your environment._

### Seeding your Medusa store

To add seed data to your medusa store run this command in a seperate

```
docker exec medusa-server medusa seed -f ./data/seed.json
```

## Running Medusa with docker in production

This repository and each of the services contain dockerfiles for both development and production, named `Dockerfile` and `Dockerfile.prod` respectively. The `Dockerfile.prod` copies the local files from disk and builds a production ready image based on your local development progress. Your specific needs for a production like container might differ from the `Dockerfile.prod` but it should provide a template and an idea of the requirements for each of the basic services.

To run the services in a production state `docker compose` is simply run with the `docker-compose.production.yml` file as well as the basic `docker-compose.yml` file as seen below. If you wish to build the production ready images and then start them run `docker compose up` with the `--build` flag as described above.

```
docker compose up -f docker-compose.yml -f docker-compose.production.yml up
```

`docker-compose.production.yml` contains production relevant overrides to the services described in the `docker-compose.yml` development file.

## Try it out

```
curl -X GET localhost:9000/store/products | python -m json.tool
```

After the seed script has run you will have the following things in you database:

- a User with the email: admin@medusa-test.com and password: supersecret
- a Region called Default Region with the countries GB, DE, DK, SE, FR, ES, IT
- a Shipping Option called Standard Shipping which costs 10 EUR
- a Product called Cool Test Product with 4 Product Variants that all cost 19.50 EUR

Visit [docs.medusa-commerce.com](https://docs.medusa-comerce.com) for further guides.

<p>
  <a href="https://www.medusa-commerce.com">
    Website
  </a> 
  |
  <a href="https://medusajs.notion.site/medusajs/Medusa-Home-3485f8605d834a07949b17d1a9f7eafd">
    Notion Home
  </a>
  |
  <a href="https://twitter.com/intent/follow?screen_name=medusajs">
    Twitter
  </a>
  |
  <a href="https://docs.medusa-commerce.com">
    Docs
  </a>
</p>
