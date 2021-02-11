# Satellite

![node-js-ci](https://github.com/Seneca-CDOT/satellite/workflows/node-js-ci/badge.svg)

A Microservice Framework for [Telescope](https://github.com/Seneca-CDOT/telescope).
Because Ray said we should try microservices!

Satellite creates an [Express.js](http://expressjs.com/) based server with
various common pieces already set up. Bring your own router and let us do the rest.

## Install

```
npm install --save @telescope/satellite
```

## Usage

```js
// Get the Satellite constructor and logger.  NOTE: `Router` is also exposed
// in case you need to create a sub-router: `const router = new Router();`
// The `Router` constructor is the same as using `new express.Router()`;
const { Satellite, logger } = require("@senecacdot/satellite");

// Define your microservice, providing some options (see below)
const service = new Satellite({ name: "my-service" });

// Add your routes to the service's router
service.router.get("/my-route", (req, res) => {
  res.json({ message: "hello world" });
});

// Start the service on the specified port
service.start(8888, () => {
  logger.info("Here we go!");
});
```

### `Satellite(options)`

- `name`: the name of the service, used in logging and performance monitoring (required).

- `apmServerUrl`: the URL to the Elastic APM server. If omitted, APM monitoring is disabled.

- `healthCheck`: an optional `function` returning a `Promise`, used to determine if the service is healthy. If no function is defined, a default one will be provided. The `healthCheck` function is what runs at the `/healthcheck` route by default.

- `cors`: the options to pass to the [cors](https://www.npmjs.com/package/cors) middleware. By default all options are turned on. Use `cors: false` to disable cors.

- `helmet`: the options to pass to the [helmet](https://www.npmjs.com/package/helmet) middleware. By default all options are turned on. Use `helmet: false` to disable helmet.
