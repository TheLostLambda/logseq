# Logseq

A privacy-first, open-source platform for knowledge sharing and management.

## Website

<https://logseq.com>

## Set up development environment

If you are on Windows, use the [Windows setup](#windows-setup).

### 1. Requirements

  - [Java & Clojure](https://clojure.org/guides/getting_started)

  - [PostgreSQL](https://www.postgresql.org/download/)

  - [Node.js](https://nodejs.org/en/)

### 2. Create a GitHub app

Follow the guide at <https://docs.github.com/en/free-pro-team@latest/developers/apps/creating-a-github-app>, where the user authorization "Callback URL" should be `http://localhost:3000/auth/github`.

Remember to download the `private-key.pem` which will be used for the next step.

### 3. Set up PostgreSQL

Make sure you have PostgreSQL running. You can check if it's running with `pg_ctl -D /usr/local/var/postgres status` and use `pg_ctl -D /usr/local/var/postgres start` to start it up. You'll also need to make a Logseq DB in PostgreSQL. Do that with `createdb logseq`.

### 4. Add environment variables

``` bash
export ENVIRONMENT="dev"
export JWT_SECRET="4fa183cf1d28460498b13330835e80ab"
export COOKIE_SECRET="10a42ca724e34f4db6086a772d787030"
export DATABASE_URL="postgres://localhost:5432/logseq"
export GITHUB_APP2_ID="78728"
export GITHUB_APP2_KEY="xxxxxxxxxxxxxxxxxxxx"
export GITHUB_APP2_SECRET="xxxxxxxxxxxxxxxxxxxx"
# Replace your-code-directory and your-app.private-key.pem with yours
export GITHUB_APP_PEM="/your-code-directory/your-app.private-key.pem"
export LOG_PATH="/tmp/logseq"
export PG_USERNAME="xxx"
export PG_PASSWORD="xxx"
```

### 5. Compile to JavaScript

``` bash
cd web
yarn
yarn watch
```

### 6. Start the Clojure server

1.  Download jar

    Go to <https://github.com/logseq/logseq-internal/releases>, download the `logseq.jar` and move it to the `resources` directory.

2.  Run jar

    ``` bash
    cd resources
    java -Duser.timezone=UTC -jar logseq.jar
    ```

### 7. Open the browser

Open <http://localhost:3000>.

## Windows setup

### 1. Required software

Install Clojure through scoop-clojure: <https://github.com/littleli/scoop-clojure>. You can also install [Node.js](https://nodejs.org/en/), [Yarn](https://yarnpkg.com/) and [PostgreSQL](https://www.postgresql.org/download/) through scoop if you want to.

### 2. Create a GitHub app

Follow [Step 2](#2-create-a-github-app) above if you want Logseq to connect to GitHub. If not, skip this section. The `GITHUB_APP_PEM` variable in the `run-windows.bat` needs to be set with the correct directory for your system.

### 3. Set up PostgreSQL

Make sure you have PostgreSQL running. You can check if it's running with `pg_ctl status` and use `pg_ctl start` to start it up. You'll also need to make a Logseq DB in PostgreSQL. Do that with `createdb logseq`.

### 4. Download the Clojure server

Go to <https://github.com/logseq/logseq-internal/releases>, download the `logseq.jar` and move into the root directory of repo.

### 5. Start Logseq

Run `start-windows.bat` which is located in the repo. This will open a second terminal that runs Logseq's backend server. To completely stop Logseq, you'll need to also close that second terminal that was opened.

`start-windows.bat` will try to start PostgreSQL for you if it's not already started.
