<h1 align="center">FINANCE</h1>

<p align="center">
  <b>FINANCE is a simple yet powerful, self-hosted personal finance tracking web app with the ability to parse SMS transactions and generate very useful insights about your money. It's also powered by ChatGPT!</b>
</p>


## 🛠 Features

1. [x] Self-hosted - full control over your data privacy 
2. [x] Parse SMS bank transactions
3. [x] Powerful AI model - FinanceGPT 🔥 - [DEMO](https://www.youtube.com/watch?v=QFM2nqv1eJY&ab_channel=SaleemHadad)
4. [x] Detailed analysis of income and expenses
5. [x] Detailed monthly report of income and expenses - [see example](https://github.com/saleem-hadad/finance/pull/4)

## 🎮 Demo

Try the app with [live demo](https://finance-demo.saleem.dev/).

## ▶️ Installation 

> Docker Installation

1. Method one (recommended)
   
```bash
git clone https://github.com/JessyLedama/RopiaAi && cd RopiaAi

make build # build the docker image
make run # the same as docker-compose up -d

# wait for a few seconds to allow the DB to finish the setup then run
make install # only for the first time
```

<details>
<summary>2. Method two (using docker-compose public hosted docker image)</summary>

First, create a `docker-compose.yml` file
```yml
version: '3'
services:
    app:
        image: 'salee2m1/finance:1.9.0'
        ports:
            - "80:80"
        networks:
            - finance
        depends_on:
            - mysql
        environment:
            OPENAI_API_KEY: 'YOUR_OPENAI_API_KEY'
    mysql:
        image: 'mysql/mysql-server:8.0'
        ports:
            - '3306:3306'
        environment:
            MYSQL_ROOT_PASSWORD: 'root'
            MYSQL_ROOT_HOST: "%"
            MYSQL_DATABASE: 'finance'
            MYSQL_USER: 'finance'
            MYSQL_PASSWORD: 'finance'
            MYSQL_ALLOW_EMPTY_PASSWORD: 1
        volumes:
            - 'financemysql:/var/lib/mysql'
        networks:
            - finance
        healthcheck:
            test: ["CMD", "mysqladmin", "ping", "-proot"]
            retries: 3
            timeout: 5s
networks:
    finance:
        driver: bridge
volumes:
    financemysql:
        driver: local
```

Then, inside the same directory run

```bash
docker-compose up -d
# wait for a few seconds to run the DB then run
docker-compose run app php artisan migrate
docker-compose run app php artisan finance:install
```

</details>

Once done, visit the app on `http://localhost`

Read [full documentation](https://finance-demo.saleem.dev/docs)


## Project Visualization

![Visualization of this repo](./diagram.svg)

## 🪚 Built with

1. Laravel
2. Inertia & ReactJs
3. GraphQL
4. MySQL
5. Docker

## 🔖 License

This project is licensed under the MIT License - see the [LICENSE.md](https://github.com/JessyLedama/RopiaAi/blob/main/LICENSE) file for details.
