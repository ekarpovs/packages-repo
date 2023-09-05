## Simple Email Client

A simple logger for Nodejs applications.

<p>
  <a href="https://www.npmjs.com/package/@ekarpovs/simple-logger" target="_blank">
    <img alt="Version" src="https://img.shields.io/npm/v/@ekarpovs/simple-logger.svg">
  </a>
  <a href="https://github.com/ekarpovs/simple-logger#readme" target="_blank">
    <img alt="Documentation" src="https://img.shields.io/badge/documentation-yes-brightgreen.svg" />
  </a>
  <a href="https://github.com/ekarpovs/simple-logger/graphs/commit-activity" target="_blank">
    <img alt="Maintenance" src="https://img.shields.io/badge/Maintained%3F-yes-green.svg" />
  </a>
  <a href="https://github.com/ekarpovs/simple-logger/blob/master/LICENSE" target="_blank">
    <img alt="License: MIT" src="https://img.shields.io/badge/License-MIT-yellow.svg" />
  </a>
</p>

## For the Email Client users:
### Installation
Download the ekarpovs-simple-logger-0.0.0-development.tgz for you computer and  
from the root directory of you project run the command:
```bash
  npm install <abs path to the archive>/ekarpovs-simple-logger-0.0.0-development.tgz 
```
### Usage
```
import { LoggerOptions, initLogger, level } from '@ekarpovs/simple-logger';

// Initialization
const cfg: LoggerOptions = {
  loggerFileLocation: "logs/log.json",
  loggerFileMaxSize: "20m",
  loggerDatePattern: "yyyy-MM-dd.",
  loggerMaxFiles: "14d",
  loggerZippedArchive: true,
  loggerLevel: level.http,   
};

const logger = initLogger(cfg);

// Usage
logger.info("Test Info logger");
```
