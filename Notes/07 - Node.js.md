# Node.js — Interview Preparation Guide

## Table of Contents

1. [Node.js Fundamentals](#nodejs-fundamentals)
2. [Event Loop & Internals](#event-loop-internals)
3. [Modules](#modules)
4. [npm](#npm)
5. [File System](#file-system)
6. [Buffers & Streams](#buffers-streams)
7. [Events](#events)
8. [Process & OS](#process-os)
9. [HTTP](#http)
10. [Express.js](#expressjs)
11. [REST APIs](#rest-apis)
12. [Authentication & Security](#authentication-security)
13. [Database](#database)

## Node.js Fundamentals
  
### 1. What is Node.js?  
**Answer:** Node.js is a JavaScript runtime built on Chrome's V8 engine that lets you run JavaScript outside the browser, mainly for server-side development.  
  
### 2. Why was Node.js created?  
**Answer:** It was created to build fast, scalable network applications using non-blocking I/O and an event-driven architecture.  
  
### 3. What are the advantages of Node.js?  
**Answer:** Fast execution, non-blocking I/O, scalable for concurrent requests, same language on frontend and backend, huge npm ecosystem.  
  
### 4. What are the limitations of Node.js?  
**Answer:** Not ideal for CPU-heavy tasks, callback complexity in older code, single main thread can be blocked by expensive computation.  
  
### 5. Where should you use Node.js?  
**Answer:** Real-time apps, APIs, streaming apps, chat apps, microservices, and I/O-heavy systems.  
  
### 6. Where should you avoid using Node.js?  
**Answer:** CPU-intensive apps like heavy image/video processing, ML workloads, or large synchronous computations unless offloaded.  
  
### 7. Is Node.js a programming language or a runtime?  
**Answer:** It is a runtime environment, not a programming language.  
  
### 8. What is the V8 Engine?  
**Answer:** V8 is Google's JavaScript engine that compiles JavaScript into machine code for fast execution.  
  
### 9. How does Node.js execute JavaScript?  
**Answer:** Node.js uses V8 to compile and run JavaScript, and uses libuv for async I/O and event loop handling.  
  
### 10. Explain the architecture of Node.js.  
**Answer:** Node.js uses a single-threaded event loop for JS execution, non-blocking I/O, and background worker threads via libuv for expensive async operations.  
  
---  
  
## Event Loop & Internals  
  
### 11. What is the Event Loop?  
**Answer:** The event loop is the mechanism that continuously checks the call stack and queues to execute asynchronous callbacks.  
  
### 12. Why is Node.js single-threaded?  
**Answer:** JavaScript execution in Node.js runs on one main thread to simplify concurrency, while I/O is handled in the background.  
  
### 13. How does Node.js handle multiple requests simultaneously?  
**Answer:** By using non-blocking I/O and delegating async operations to the OS or libuv thread pool.  
  
### 14. What is libuv?  
**Answer:** libuv is a C library that provides the event loop, async I/O, and thread pool support in Node.js.  
  
### 15. What is the Call Stack?  
**Answer:** It is the stack where function calls are executed in order.  
  
### 16. What is the Callback Queue?  
**Answer:** It stores completed async callback functions waiting to be pushed to the call stack.  
  
### 17. What is the Microtask Queue?  
**Answer:** It stores high-priority tasks like `Promise.then()` callbacks and `queueMicrotask()`.  
  
### 18. What is the difference between Microtasks and Macrotasks?  
**Answer:** Microtasks run before the next event loop phase; macrotasks like `setTimeout` run in later event loop phases.  
  
### 19. Explain the phases of the Event Loop.  
**Answer:** Timers, pending callbacks, idle/prepare, poll, check, close callbacks. Microtasks run between phases.  
  
### 20. What is the Poll phase?  
**Answer:** It handles incoming I/O events and executes related callbacks.  
  
### 21. What is the Check phase?  
**Answer:** It executes callbacks scheduled by `setImmediate()`.  
  
### 22. What is process.nextTick()?  
**Answer:** It schedules a callback to run immediately after the current operation, before the event loop continues.  
  
### 23. Difference between process.nextTick() and Promise.then()?  
**Answer:** `process.nextTick()` has higher priority and runs before promise microtasks in Node.js.  
  
### 24. Difference between process.nextTick() and setImmediate()?  
**Answer:** `process.nextTick()` runs before the event loop continues; `setImmediate()` runs in the check phase.  
  
### 25. Difference between setImmediate() and setTimeout()?  
**Answer:** `setImmediate()` runs in the check phase; `setTimeout(fn, 0)` runs in the timers phase, timing may vary.  
  
---  
  
## Modules  
  
### 26. What are modules in Node.js?  
**Answer:** Modules are reusable pieces of code split into separate files.  
  
### 27. What is CommonJS?  
**Answer:** CommonJS is Node.js’s traditional module system using `require()` and `module.exports`.  
  
### 28. What are ES Modules?  
**Answer:** ES Modules are the standard JavaScript module system using `import` and `export`.  
  
### 29. Difference between require() and import?  
**Answer:** `require()` is CommonJS and usually synchronous; `import` is ES Module syntax and is statically analyzable.  
  
### 30. Difference between exports and module.exports?  
**Answer:** `exports` is a reference to `module.exports`; reassigning `exports` breaks that reference.  
  
### 31. How does module caching work?  
**Answer:** Once a module is loaded, Node.js caches it, so repeated `require()` calls return the cached version.  
  
### 32. What is circular dependency?  
**Answer:** It happens when two modules depend on each other directly or indirectly, which can cause incomplete exports.  
  
### 33. How does Node.js resolve modules?  
**Answer:** It checks core modules first, then file paths, then `node_modules`, following resolution rules.  
  
---  
  
## npm  
  
### 34. What is npm?  
**Answer:** npm is Node.js’s package manager and registry for installing and managing dependencies.  
  
### 35. What is npx?  
**Answer:** `npx` runs packages directly without globally installing them.  
  
### 36. What is package.json?  
**Answer:** It is the project manifest containing metadata, scripts, dependencies, and config.  
  
### 37. What is package-lock.json?  
**Answer:** It locks exact dependency versions for consistent installs.  
  
### 38. Difference between dependencies and devDependencies?  
**Answer:** `dependencies` are needed in production; `devDependencies` are needed only during development.  
  
### 39. What is Semantic Versioning (SemVer)?  
**Answer:** Version format `MAJOR.MINOR.PATCH` where major = breaking changes, minor = features, patch = fixes.  
  
### 40. What are npm scripts?  
**Answer:** Custom commands defined in `package.json` under `scripts`.  
  
---  
  
## File System  
  
### 41. What is the fs module?  
**Answer:** The `fs` module provides file system operations like reading, writing, deleting, and watching files.  
  
### 42. Difference between synchronous and asynchronous file operations?  
**Answer:** Sync operations block execution; async operations do not block and use callbacks/promises.  
  
### 43. How do you read a file?  
**Answer:** Use `fs.readFile()`, `fs.promises.readFile()`, or streams for large files.  
  
### 44. How do you write a file?  
**Answer:** Use `fs.writeFile()`, `fs.promises.writeFile()`, or writable streams.  
  
### 45. How do you stream large files?  
**Answer:** Use `fs.createReadStream()` and optionally pipe it to a writable stream.  
  
---  
  
## Buffers & Streams  
  
### 46. What is Buffer?  
**Answer:** Buffer is a Node.js object for handling raw binary data.  
  
### 47. Why do we need Buffers?  
**Answer:** Because JavaScript traditionally handles text well, but binary data needs a dedicated structure.  
  
### 48. What are Streams?  
**Answer:** Streams process data in chunks instead of loading everything into memory at once.  
  
### 49. Types of Streams?  
**Answer:** Readable, Writable, Duplex, and Transform.  
  
### 50. What is pipe()?  
**Answer:** `pipe()` connects a readable stream to a writable stream.  
  
### 51. What is backpressure?  
**Answer:** Backpressure is the mechanism for controlling data flow when the receiver is slower than the sender.  
  
### 52. Difference between Buffer and Stream?  
**Answer:** Buffer holds the full chunk in memory; Stream processes data piece by piece.  
  
---  
  
## Events  
  
### 53. What is EventEmitter?  
**Answer:** It is a core Node.js class used to create and handle custom events.  
  
### 54. How do custom events work?  
**Answer:** You emit an event using `emit()` and listen using `on()` or `once()`.  
  
### 55. Difference between on() and once()?  
**Answer:** `on()` listens every time; `once()` listens only the first time.  
  
### 56. How do you remove an event listener?  
**Answer:** Use `off()` or `removeListener()`.  
  
---  
  
## Process & OS  
  
### 57. What is the process object?  
**Answer:** It is a global object that provides information and control over the current Node.js process.  
  
### 58. What is process.env?  
**Answer:** It contains environment variables.  
  
### 59. What is process.argv?  
**Answer:** It contains command-line arguments passed to the process.  
  
### 60. What is process.cwd()?  
**Answer:** It returns the current working directory from which the process was started.  
  
### 61. Difference between __dirname and process.cwd()?  
**Answer:** `__dirname` is the directory of the current file; `process.cwd()` is where the Node process was launched.  
  
---  
  
## HTTP  
  
### 62. How does the HTTP module work?  
**Answer:** It allows Node.js to create HTTP servers and clients using request-response handling.  
  
### 63. How do you create an HTTP server?  
**Answer:** Use `http.createServer((req, res) => {})` and call `listen()`.  
  
### 64. What is the request object?  
**Answer:** It contains incoming request data like method, headers, URL, and body stream.  
  
### 65. What is the response object?  
**Answer:** It is used to send headers, status code, and body back to the client.  
  
---  
  
## Express.js  
  
### 66. What is Express.js?  
**Answer:** Express is a minimal web framework built on Node.js for APIs and web apps.  
  
### 67. Why use Express over the HTTP module?  
**Answer:** It provides routing, middleware, easier request handling, and better developer productivity.  
  
### 68. What is middleware?  
**Answer:** Middleware is a function that runs during the request-response cycle and can modify req/res or pass control.  
  
### 69. Types of middleware?  
**Answer:** Application-level, router-level, error-handling, built-in, and third-party middleware.  
  
### 70. How does middleware execution work?  
**Answer:** Middleware runs in order, and each one calls `next()` to pass control.  
  
### 71. What is next()?  
**Answer:** It passes control to the next middleware or route handler.  
  
### 72. What is error-handling middleware?  
**Answer:** Middleware with four args: `(err, req, res, next)` used for centralized error handling.  
  
### 73. Difference between app.use() and app.get()?  
**Answer:** `app.use()` applies middleware to all methods; `app.get()` handles only GET requests for a route.  
  
### 74. What are route parameters?  
**Answer:** Dynamic URL parts like `/users/:id`.  
  
### 75. Difference between req.params, req.query, and req.body?  
**Answer:** `req.params` = route params, `req.query` = URL query string, `req.body` = request payload.  
  
---  
  
## REST APIs  
  
### 76. What is REST?  
**Answer:** REST is an architectural style for designing stateless resource-based APIs over HTTP.  
  
### 77. What are REST principles?  
**Answer:** Statelessness, client-server separation, cacheability, uniform interface, layered system, resource-based design.  
  
### 78. What are HTTP methods?  
**Answer:** GET, POST, PUT, PATCH, DELETE, and others like OPTIONS.  
  
### 79. Explain CRUD operations.  
**Answer:** Create, Read, Update, Delete — often mapped to POST, GET, PUT/PATCH, DELETE.  
  
### 80. Difference between PUT and PATCH?  
**Answer:** PUT usually replaces the full resource; PATCH partially updates it.  
  
### 81. What are HTTP status codes?  
**Answer:** Numeric codes indicating request result, like 200 OK, 201 Created, 400 Bad Request, 404 Not Found, 500 Server Error.  
  
### 82. How should REST APIs be designed?  
**Answer:** Use nouns for resources, proper HTTP methods, meaningful status codes, versioning, validation, and consistent responses.  
  
---  
  
## Authentication & Security  
  
### 83. Authentication vs Authorization?  
**Answer:** Authentication verifies who you are; authorization checks what you can access.  
  
### 84. What is JWT?  
**Answer:** JSON Web Token is a compact signed token used to carry user identity/claims.  
  
### 85. How does JWT authentication work?  
**Answer:** Server issues token after login, client sends it in requests, server verifies signature and claims.  
  
### 86. What is Refresh Token?  
**Answer:** A long-lived token used to obtain a new access token without forcing re-login.  
  
### 87. Why hash passwords?  
**Answer:** To avoid storing plain-text passwords and protect users if the database is leaked.  
  
### 88. Why use bcrypt?  
**Answer:** bcrypt is slow by design and includes salting, making brute-force attacks harder.  
  
### 89. What is CORS?  
**Answer:** Cross-Origin Resource Sharing controls which origins can access server resources.  
  
### 90. What is Helmet?  
**Answer:** Helmet is an Express middleware that sets secure HTTP headers.  
  
### 91. What is Rate Limiting?  
**Answer:** It restricts how many requests a client can make in a period to prevent abuse.  
  
### 92. What is CSRF?  
**Answer:** Cross-Site Request Forgery tricks a user’s browser into making unwanted authenticated requests.  
  
### 93. What is XSS?  
**Answer:** Cross-Site Scripting injects malicious scripts into web pages viewed by users.  
  
### 94. What is SQL Injection?  
**Answer:** It happens when untrusted input is inserted into SQL queries and alters query behavior.  
  
### 95. What is NoSQL Injection?  
**Answer:** Similar to SQL injection, but targets NoSQL queries by manipulating query objects or operators.  
  
---  
  
## Database  
  
### 96. SQL vs NoSQL?  
**Answer:** SQL databases are relational and structured; NoSQL databases are flexible and often better for unstructured or horizontally scaled data.  
  
### 97. Mongoose vs Prisma?  
**Answer:** Mongoose is ODM-focused for MongoDB; Prisma is a type-safe ORM supporting multiple databases.  
  
### 98. Connection Pooling?  
**Answer:** It reuses database connections instead of opening a new one for each request.  
  
### 99. Transactions in Node.js?  
**Answer:** Transactions group multiple DB operations so they either all succeed or all fail together.  
  
### 100. How would you structure a production-ready Node.js backend?  
**Answer:** Use layered architecture: routes, controllers, services, repositories, middleware, validation, auth, logging, env config, tests, monitoring, caching, queueing, and proper error handling.  
  
---  
  
# Bonus (Senior-Level) — Short Answers  
  
### Explain the complete lifecycle of a request in Node.js.  
**Answer:** Request reaches server, event loop accepts it, middleware/routes process it, async I/O is delegated, callback/microtask resumes execution, response is sent.  
  
### How would you optimize a slow Node.js application?  
**Answer:** Profile first, remove blocking code, optimize DB queries, add caching, use streams, paginate, compress, scale horizontally.  
  
### How do Worker Threads differ from the Event Loop?  
**Answer:** Event loop handles async coordination on the main thread; Worker Threads run CPU-heavy JS in parallel threads.  
  
### Cluster vs Worker Threads?  
**Answer:** Cluster creates multiple Node processes; Worker Threads create threads inside one process.  
  
### Child Process vs Worker Thread?  
**Answer:** Child process has separate memory/process; worker thread shares process memory more efficiently.  
  
### How does PM2 work internally?  
**Answer:** PM2 manages Node processes, supports clustering, restarts crashed apps, logs output, and helps with zero-downtime reloads.  
  
### How do you scale Node.js to millions of users?  
**Answer:** Use load balancers, clustering, stateless services, caching, queues, DB optimization, CDN, and horizontal scaling.  
  
### How do you prevent memory leaks?  
**Answer:** Avoid global state growth, clean listeners/timers, release unused references, monitor heap usage, and profile leaks.  
  
### Explain Streams internally.  
**Answer:** Streams use internal buffers and event-driven chunk processing with flow control and backpressure.  
  
### Explain Buffer internally.  
**Answer:** Buffer is built on raw binary memory allocation outside normal JS string handling for efficient byte operations.  
  
### How does libuv manage I/O?  
**Answer:** It uses the event loop, OS async APIs, and a thread pool for operations the OS cannot handle asynchronously.  
  
### Explain Node.js architecture in depth.  
**Answer:** JS runs on V8, async ops go through Node APIs to libuv/OS, callbacks return via event loop phases, with microtask handling between phases.  
  
### What happens internally when you call require()?  
**Answer:** Node resolves path, checks cache, loads file, wraps module in a function, executes it, and caches exports.  
  
### How does Node.js handle asynchronous I/O?  
**Answer:** It delegates I/O to the OS or libuv thread pool and runs the callback when the operation completes.  
  
### Design a scalable backend for a chat application.  
**Answer:** Use WebSockets, Redis pub/sub, stateless app servers, message store DB, auth, presence service, and horizontal scaling.  
  
### Design a scalable file upload service.  
**Answer:** Use presigned URLs, object storage, chunked uploads, background processing, metadata DB, virus scanning, and CDN delivery.  
  
### Design a URL shortener in Node.js.  
**Answer:** Generate unique short IDs, store mapping in DB, cache hot URLs, redirect fast, and track analytics asynchronously.  
  
### How would you implement rate limiting?  
**Answer:** Use Redis with fixed window, sliding window, or token bucket based on IP/user/token.  
  
### How would you implement caching with Redis?  
**Answer:** Cache frequent query results with TTL, invalidate on updates, and use cache-aside pattern.  
  
### How would you build a notification system using RabbitMQ?  
**Answer:** Publish notification events to queues, consume them with workers, retry failed jobs, and store delivery status.