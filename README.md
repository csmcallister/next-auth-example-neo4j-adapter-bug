## Neo4jAdapter Bug Report

To reproduce the bug `Neo4jError: You cannot begin a transaction on a session with an open transaction; either run from within the transaction or use a different session`, follow these steps.

1. install deps
```
npm i
```

2. Create a `.env.local` for a Google (or likely any other) provider:

```ini
NEXTAUTH_SECRET=
AUTH_GOOGLE_ID=
AUTH_GOOGLE_SECRET=
```

3. Create a free neo4j db (or use Docker) and then configure the neo4j connection in `auth.ts`:

```typescript
const driver = neo4j.driver(
  "neo4j+s://<id>.databases.neo4j.io",
  neo4j.auth.basic("neo4j", "password")
)
```

4. Start a dev server with `npm run dev`, sign in, and then try to visit either `http://localhost:3000/server-example` or `http://localhost:3000/client-example`. Both will log the following error:

```
 ✓ Compiled /server-example in 279ms (1698 modules)
[auth][error] AdapterError: Read more at https://errors.authjs.dev#adaptererror
[auth][cause]: Neo4jError: You cannot begin a transaction on a session with an open transaction; either run from within the transaction or use a different session.
    at new Neo4jError (webpack-internal:///(rsc)/./node_modules/neo4j-driver-core/lib/error.js:74:16)
    at newError (webpack-internal:///(rsc)/./node_modules/neo4j-driver-core/lib/error.js:106:12)
    at Session._beginTransaction (webpack-internal:///(rsc)/./node_modules/neo4j-driver-core/lib/session.js:404:40)
    at eval (webpack-internal:///(rsc)/./node_modules/neo4j-driver-core/lib/session.js:531:26)
    at TransactionExecutor.eval (webpack-internal:///(rsc)/./node_modules/neo4j-driver-core/lib/internal/transaction-executor.js:280:37)
    at step (webpack-internal:///(rsc)/./node_modules/neo4j-driver-core/lib/internal/transaction-executor.js:117:23)
    at Object.eval [as next] (webpack-internal:///(rsc)/./node_modules/neo4j-driver-core/lib/internal/transaction-executor.js:58:20)
    at eval (webpack-internal:///(rsc)/./node_modules/neo4j-driver-core/lib/internal/transaction-executor.js:36:71)
    at new Promise (<anonymous>)
    at __awaiter (webpack-internal:///(rsc)/./node_modules/neo4j-driver-core/lib/internal/transaction-executor.js:18:12)
    at TransactionExecutor._executeTransactionInsidePromise (webpack-internal:///(rsc)/./node_modules/neo4j-driver-core/lib/internal/transaction-executor.js:268:16)
    at eval (webpack-internal:///(rsc)/./node_modules/neo4j-driver-core/lib/internal/transaction-executor.js:230:19)
    at new Promise (<anonymous>)
    at TransactionExecutor.execute (webpack-internal:///(rsc)/./node_modules/neo4j-driver-core/lib/internal/transaction-executor.js:229:16)
    at Session._runTransaction (webpack-internal:///(rsc)/./node_modules/neo4j-driver-core/lib/session.js:530:42)
    at Session.writeTransaction (webpack-internal:///(rsc)/./node_modules/neo4j-driver-core/lib/session.js:526:21)
    at write (webpack-internal:///(rsc)/./node_modules/@auth/neo4j-adapter/index.js:293:42)
    at getSessionAndUser (webpack-internal:///(rsc)/./node_modules/@auth/neo4j-adapter/index.js:203:34)
    at acc.<computed> (webpack-internal:///(rsc)/./node_modules/@auth/core/lib/init.js:170:30)
    at Module.session (webpack-internal:///(rsc)/./node_modules/@auth/core/lib/actions/session.js:84:36)
    at AuthInternal (webpack-internal:///(rsc)/./node_modules/@auth/core/lib/index.js:50:77)
    at async Auth (webpack-internal:///(rsc)/./node_modules/@auth/core/index.js:123:29)
    at async UserButton (webpack-internal:///(rsc)/./components/user-button.tsx:19:21)
[auth][details]: {}
[auth][error] SessionTokenError: Read more at https://errors.authjs.dev#sessiontokenerror
[auth][cause]: Neo4jError: You cannot begin a transaction on a session with an open transaction; either run from within the transaction or use a different session.
    at new Neo4jError (webpack-internal:///(rsc)/./node_modules/neo4j-driver-core/lib/error.js:74:16)
    at newError (webpack-internal:///(rsc)/./node_modules/neo4j-driver-core/lib/error.js:106:12)
    at Session._beginTransaction (webpack-internal:///(rsc)/./node_modules/neo4j-driver-core/lib/session.js:404:40)
    at eval (webpack-internal:///(rsc)/./node_modules/neo4j-driver-core/lib/session.js:531:26)
    at TransactionExecutor.eval (webpack-internal:///(rsc)/./node_modules/neo4j-driver-core/lib/internal/transaction-executor.js:280:37)
    at step (webpack-internal:///(rsc)/./node_modules/neo4j-driver-core/lib/internal/transaction-executor.js:117:23)
    at Object.eval [as next] (webpack-internal:///(rsc)/./node_modules/neo4j-driver-core/lib/internal/transaction-executor.js:58:20)
    at eval (webpack-internal:///(rsc)/./node_modules/neo4j-driver-core/lib/internal/transaction-executor.js:36:71)
    at new Promise (<anonymous>)
    at __awaiter (webpack-internal:///(rsc)/./node_modules/neo4j-driver-core/lib/internal/transaction-executor.js:18:12)
    at TransactionExecutor._executeTransactionInsidePromise (webpack-internal:///(rsc)/./node_modules/neo4j-driver-core/lib/internal/transaction-executor.js:268:16)
    at eval (webpack-internal:///(rsc)/./node_modules/neo4j-driver-core/lib/internal/transaction-executor.js:230:19)
    at new Promise (<anonymous>)
    at TransactionExecutor.execute (webpack-internal:///(rsc)/./node_modules/neo4j-driver-core/lib/internal/transaction-executor.js:229:16)
    at Session._runTransaction (webpack-internal:///(rsc)/./node_modules/neo4j-driver-core/lib/session.js:530:42)
    at Session.writeTransaction (webpack-internal:///(rsc)/./node_modules/neo4j-driver-core/lib/session.js:526:21)
    at write (webpack-internal:///(rsc)/./node_modules/@auth/neo4j-adapter/index.js:293:42)
    at getSessionAndUser (webpack-internal:///(rsc)/./node_modules/@auth/neo4j-adapter/index.js:203:34)
    at acc.<computed> (webpack-internal:///(rsc)/./node_modules/@auth/core/lib/init.js:170:30)
    at Module.session (webpack-internal:///(rsc)/./node_modules/@auth/core/lib/actions/session.js:84:36)
    at AuthInternal (webpack-internal:///(rsc)/./node_modules/@auth/core/lib/index.js:50:77)
    at async Auth (webpack-internal:///(rsc)/./node_modules/@auth/core/index.js:123:29)
    at async UserButton (webpack-internal:///(rsc)/./components/user-button.tsx:19:21)
[auth][details]: {}
```

>This is related to [#5849](https://github.com/nextauthjs/next-auth/issues/5849), but perhaps distinct because it's occurring with `@auth/neo4j-adapter` and `next-auth` 5 (beta). 

As you can see, `const session = await auth()` in `UserButton` is causing the error. This is because `const session = await auth()` is also called within `app/server-example/page.tsx` as well as `app/client-example/page.tsx`. Comment out either of those calls in the pages, so that there's just one `const session = await auth()` occurring, and the error disappears. Only problem is, I'd like to be able to call `const session = await auth()` in both `UserButton.tsx` as well as within my pages. As the error message states, there's an issue with the session lifecycle within the Neo4jAdapter. As the [neo4j docs](https://neo4j.com/docs/javascript-manual/current/transactions/) state, "Session creation is a lightweight operation, so sessions can be created and destroyed without significant cost. Always close sessions when you are done with them.".

I suspected the session wasn't being closed and then recreated since the adapter is passed in as `Neo4jAdapter(session)` instead of as `Neo4jAdapter(driver)`. Looking into `node_modules/@auth/neo4j-adapter/index.js`, I could see this is the case:

```typescript
export function Neo4jAdapter(session: Session): Adapter {
  const { read, write } = client(session)
  ...
```

Above, the session is passed to the `client` function, which manages the transactions. However, the session never gets closed. Editing the `.js` code locally, I was able to resolve the error by:

1. Making the driver the argument to Neo4jAdapter (i.e., `export function Neo4jAdapter(session)` becomes `export function Neo4jAdapter(driver)`)
2. Updating `auth.ts` to pass the driver to `Neo4jAdapter`: 

```typescript
export const config = {
  theme: {
    logo: "https://next-auth.js.org/img/logo/logo-sm.png",
  },
  adapter: Neo4jAdapter(driver)  // <--- here
```

3. Updating the client function to accept the driver instead of a session as its argument. That way we can create new lightweight sessions with each read/write transaction. I also ensured that the `read` and `write` functions close the session:

```javascript
function client(driver) {
    return {
        /** Reads values from the database */
        async read(statement, values) {
            const session = driver.session()
            try {
                const result = await session.executeRead((tx) => tx.run(statement, values));
                return format.from(result?.records[0]?.get(0)) ?? null;
            } finally {
                session.close();  // closing the session
            }
        },
        /**
         * Reads/writes values from/to the database.
         * Properties are available under `$data`
         */
        async write(statement, values) {
            const session = driver.session()
            try {
                const result = await session.executeWrite((tx) => tx.run(statement, { data: format.to(values) }));
                return format.from(result?.records[0]?.toObject());
            } finally {
                session.close();  // closing the session
            }
        },
    };
}
```

4. Scope down instantiation of the read/write functions within Neo4jAdapter, e.g.,

```javascript
export function Neo4jAdapter(driver) {
    // const { read, write } = client(session)  // move this down
    return {
        async createUser(data) {
            const { write } = client(driver)  // scope client (and session) instantiation to each adapter method
            const user = { ...data, id: crypto.randomUUID() };
            await write(`CREATE (u:User $data)`, user);
            return user;
        },
        async getUser(id) {
            const { read } = client(driver) // scope client (and session) instantiation to each adapter method
            return await read(`MATCH (u:User { id: $id }) RETURN u{.*}`, {
                id,
            });
        },
        ...
```

After doing the above and performing a `rm -rf .next`, the error message goes away and the demo app runs swimmingly.
