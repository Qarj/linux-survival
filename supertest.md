# supertest

```ts
import nock from 'nock';
import request from 'supertest';
import { instaniateApp } from '../../app';

nock.emitter.on('no match', (req) => {
    console.log(`No match for request: ${req.method} ${req.path}`);
});

describe('some integration tests', () => {
    beforeEach(() => {
        nock.cleanAll();
        jest.clearAllMocks();
    });

    it('should test something', async () => {
        const searchIntercept = nock(searchUrl).post('').reply(200, searchResult);
        const detailIntercept = nock(detailEndpoint)
            .get(detailPath))
            .reply(200, detailsResult);

        const response = await request(instaniateApp()).post('/v1/endpoint').send(requestBody);

        expect(searchIntercept.isDone()).toBeTruthy();
        expect(detailIntercept.isDone()).toBeTruthy();

        expect(response.status).toEqual(200);

        const body = response.body;
        expect(body.observation).toMatch(/something/);

        expect(nock.pendingMocks()).toStrictEqual([]);
    });
});
```

Run your tests with the `DEBUG` environment variable set to `nock.*`:

```bash
DEBUG=nock.* npm test
```

**Intercept Network Requests at a Lower Level**: If you want to capture all HTTP requests regardless of whether they are mocked or not, you can use a module like `mitm` to intercept and log all network requests.

First, install the `mitm` library:

```bash
npm install mitm
```

Then, use it in your tests to intercept and log requests:

```javascript
const mitm = require('mitm')();

mitm.on('request', (req, res) => {
    console.log(`Made request to: ${req.method} ${req.url}`);
    res.statusCode = 500;
    res.end();
});
```

Remember to disable `mitm` after your tests to avoid affecting other tests:

```javascript
afterEach(() => {
    mitm.disable();
});
```
