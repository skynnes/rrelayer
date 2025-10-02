# Railway

## Deploy an example project

<https://github.com/joshstevens19/rrelayer/tree/master/providers/railway>

1. Clone the relevant directory

  ```bash
  # this will clone the railway directory
  mkdir rrelayer-railway && cd rrelayer-railway
  git clone \
    --depth=1 \
    --no-checkout \
    --filter=tree:0 \
    https://github.com/joshstevens19/rrelayer .
  git sparse-checkout set --no-cone providers/railway .
  git checkout && cp -r providers/railway/* . && rm -rf providers
  ```

2. Initialize a new Railway project

  ```bash
  railway init --name rrelayer-example
  ```

3. Create a service and link it to the project

  ```bash
  railway up --detach
  railway link --name rrelayer-example --environment production
  ```

4. Create a Postgres database

  ```bash
  railway add --database postgres
  ```

5. Configure environment variables

  ```bash
  railway open
  ```

- then open the service "Variables" tab and click on "Add Variable Reference" and select `DATABASE_URL`,
- postfix `?sslmode=disable` to the end of the value. It should look like this: `${{Postgres.DATABASE_URL}}?sslmode=disable`,
- hit "Deploy" or Shift+Enter.

6. Create a domain to access the API

  ```bash
  railway domain
  ```

7. Redeploy the service

  ```bash
  railway up
  ```
