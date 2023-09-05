## Http Logger

A Http logger for Nodejs applications.

<p>
  <a href="https://www.npmjs.com/package/@ekarpovs/http-logger" target="_blank">
    <img alt="Version" src="https://img.shields.io/npm/v/@ekarpovs/http-logger.svg">
  </a>
  <a href="https://github.com/ekarpovs/http-logger#readme" target="_blank">
    <img alt="Documentation" src="https://img.shields.io/badge/documentation-yes-brightgreen.svg" />
  </a>
  <a href="https://github.com/ekarpovs/http-logger/graphs/commit-activity" target="_blank">
    <img alt="Maintenance" src="https://img.shields.io/badge/Maintained%3F-yes-green.svg" />
  </a>
  <a href="https://github.com/ekarpovs/http-logger/blob/master/LICENSE" target="_blank">
    <img alt="License: MIT" src="https://img.shields.io/badge/License-MIT-yellow.svg" />
  </a>
</p>

### Installation
Download the [ekarpovs-http-logger-0.0.0-development.tgz](https://github.com/ekarpovs/pakages-repo/http-logger) to your computer and  
from the root directory of you project run the command:
```bash
  npm install <abs path to the archive>/ekarpovs-http-logger-0.0.0-development.tgz 
```
### Usage
```
import { LoggerFormatter, initHttpLogger } from '@ekarpovs/http-logger';

// Initialization
const cfg: LoggerFormatter = {
  token: ':remote-addr :method :url :status :res[content-length] - :response-time ms'
};

const HttpLogger = initHttpLogger(cfg);

// Usage
app.use(httpLogger);
```

// Define message format string (this is the default one).
// The message format is made from tokens, and each token is
// defined inside the Morgan library.
// ":method :url :status :res[content-length] - :response-time ms",
// ":remote-addr :method :url :status :res[content-length] - :response-time ms",
// ":remote-addr - :remote-user [:date[clf]] ':method :url HTTP/:http-version' :status :res[content-length] ':referrer' ':user-agent",
// It is possible to create a custom token.
