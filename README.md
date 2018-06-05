# Express-Base

A base repository for any ExpressJS site.

## Installation

Download this repository and install all dependencies

```
git clone git@git.theidol.com:theidol/express-base.git
cd express-base
npm install
```

Please ensure you have Redis installed and running. This should be installed on your computer already by the infrastructure team.

## Environment Variables and Configuration

All configuration options for any application should be taking these settings from the environment. So you do not need to manually set these on the command line a tool called `dotenv` in used to load files form a `.env` file.

This file is **specific to you** and will more than likely contain usernames & passwords. *This should never be commited to Git*.

The following environment variables are used:

**PORT** exposed as `config.port`. This is the port your application will listen on when running. *Default is 3000*

**SECRET_KEY** exposed as `config.secretKey`. This is secret key used for sessions. This should never be leaked, it doesn't matter so much in non-public facing instances but can not be empty. *Default is "PleaseChangeMe"*

**LOG_FORMAT** exposed as `config.logFormat`. This value allows us to change the access log format on AWS so we can better diagnose issues.

**DB_URL** exposed as `config.dbURL`. The database connection URI to a MySQL/MariaDB database. This should be in the following format `mysql://username:password@hostname[:port]/databasename[?options]`.

**MAIL_URL** exposed as `config.mailURL`. The connection URI to an SMTP server. Should be in the following format `smtp[s]://username:password@hostname[:port]/[?options]`.

**REDIS_URL** exposed as `config.redisURL`. The connection URI to a Redis server/cluser. Should be in the following format `redis://:password@hostname[:port]/dbnumber[?options]`

**SENTRY_DSN** exposed as `config.sentryDSN`. Connection URI to Sentry for error logging. Should be in the format `https://publickey:privatekey@hostname/projectno`.

All environment variables should be converted to keys in the config object (`config.js`). No where else in your code should you read from the environment.

## Code Quality and Testing

### ESLint

The base system has our standard `.eslintrc.json` file. This will ensure all code passes our re-defined coding standard. This is a living, breathing standard and will evolve over time.

To run `eslint` on it's own:

```
npm run lint
```

This will highlight any places where the code does not follow the standard.

ESLint can also fix many of these problems on your behalf, to do this simply run

```
npm run lint:fix
```

### Mocha

The test framework Mocha is set up for you to use. Testing is simply making assertions about the result of a function or route dispatches given a certain input. Writing good tests is a subject to large to cover in a `README`, however you should structure your code in to discrete bodies of code which can easily be tested.

All the tests are stored in `/tests` (please see for examples). You can run the full test command (as will be done by Gitlab) with the following command:

```
npm test
```

This will inform you that all your tests pass and will give you a code coverage report (via `istanbul`) so you can see how much of your code is being exercised. The exact testing standard for *theidol.com* is not yet defined but code coverage **will** become a metric for how rigerous your code is.

`supertest` is also installed which allows you to test routes as if hitting the website. This is a large tool so please refer to documentation and the `tests/` directory for a quick run down.

### Databases

There is a project wide `mysql2/promise` connection pool. By simply requiring the `db.js` file in the project root you can then use that in all the ways outlined in [their Github page](https://github.com/sidorares/node-mysql2).

### Mail

There is a project wide smtp transport. Simply require in the `mailer.js` file and you can use the mailer as per the [Nodemailer website](https://nodemailer.com/about/)

### Updates

Express-base is just a starting point! It may be out of date (dependency wise) at times. Please make sure you use `npm outdated` to check that all packages are up to date
