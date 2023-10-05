## Authorization definitions on MongoDb.

A npm package that provides access to authorization definitions for Node.js projects.  
The package is dedicated to be used with the @ekarpovs/authorization-checker package.  
Supports ACL - Access Control List and RBAC - Role Based Access Control methods. 

<p>
  <a href="https://www.npmjs.com/package/@ekarpovs/authorization-repo-mongo" target="_blank">
    <img alt="Version" src="https://img.shields.io/npm/v/@ekarpovs/authorization-repo-mongo.svg">
  </a>
  <a href="https://github.com/ekarpovs/authorization-repo-mongo#readme" target="_blank">
    <img alt="Documentation" src="https://img.shields.io/badge/documentation-yes-brightgreen.svg" />
  </a>
  <a href="https://github.com/ekarpovs/authorization-repo-mongo/graphs/commit-activity" target="_blank">
    <img alt="Maintenance" src="https://img.shields.io/badge/Maintained%3F-yes-green.svg" />
  </a>
  <a href="https://github.com/ekarpovs/authorization-repo-mongo/blob/master/LICENSE" target="_blank">
    <img alt="License: MIT" src="https://img.shields.io/badge/License-MIT-yellow.svg" />
  </a>
</p>

### Installation
```bash
  npm install @ekarpovs/authorization-repo-mongo
```

### Usage
```
import { ModelType, initRules, rulesRepository } from '@ekarpovs/authorization-repo-mongo';

If an application doesn't use a Rules Management feature do the following (once only):

Create authorization definitions - acl.json or rbac.json file.    

Add the file into the .gitignore.  

Populate the authorization definitions into the application DataBase:  
  initRules(ModelType.ACL, aclData);
or:  
  initRules(ModelType.RBAC, rbacData);

The authorization repository is ready to be used (injected into) by  
the @ekarpovs/authorization-checker package.  

```

