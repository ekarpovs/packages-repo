## Session storage 

A session storage for Nodejs applications with the @ekarpovs/auth-session.

<p>
  <a href="https://www.npmjs.com/package/@ekarpovs/session-storage-mongo" target="_blank">
    <img alt="Version" src="https://img.shields.io/npm/v/@ekarpovs/session-storage-mongo.svg">
  </a>
  <a href="https://github.com/ekarpovs/session-storage-mongo#readme" target="_blank">
    <img alt="Documentation" src="https://img.shields.io/badge/documentation-yes-brightgreen.svg" />
  </a>
  <a href="https://github.com/ekarpovs/session-storage-mongo/graphs/commit-activity" target="_blank">
    <img alt="Maintenance" src="https://img.shields.io/badge/Maintained%3F-yes-green.svg" />
  </a>
  <a href="https://github.com/ekarpovs/session-storage-mongo/blob/master/LICENSE" target="_blank">
    <img alt="License: MIT" src="https://img.shields.io/badge/License-MIT-yellow.svg" />
  </a>
</p>

### Installation
```bash
  npm install @ekarpovs/session-storage-mongo
```
### Usage
```
import { sessionStorage } from 'ekarpovs/session-storage-mongo';


const storage = sessionStorage(storageConfig);

// inject into auth-session
// authConfig.storage = { store: storage};

const storageConfig: StorageConfig = {
  uri: "",
  db: "",
  collection: "",
};


```
