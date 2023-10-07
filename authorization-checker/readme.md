## Authorization checker.

A npm package that provides access control authorized routers for Node.js projects.  
The package is dedicated to be used with the @ekarpovs/authorization-repo-<database> packages. 
Supports ACL - Access Control List and RBAC - Role Based Access Control methods. 
Only authorization-repo-mongo is implemented at present.  

<p>
  <a href="https://www.npmjs.com/package/@ekarpovs/authorization-checker" target="_blank">
    <img alt="Version" src="https://img.shields.io/npm/v/@ekarpovs/authorization-checker.svg">
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
  npm install @ekarpovs/authorization-checker
```

### Pre-conditions:
```
  The package @ekarpovs/authorization-repo<database> has to be installed.  
  The User model (table) has to have **role: string** property.  
```

### Usage  
```
  import { authorization } from './authorization-checker';  

Init the rules repository  
  const rulesRepo = rulesRepository(ModelType.ACL);  
Init the authorization package  
  const isAuthorized = authorization({ rulesRepo }, { getUserData });  

The isAuthorized parameters: (permission: string, resource?: string) 

Protect an authorized router:  
  router.get(  
    '/test-acl',  
    checkAuthenticated,  
    isAuthorized('read', 'test-acl'),  
    (_req, res) => {  
      res.json({ message: 'You are authorized to access this resource' });  
    },  
  );  
  
router.get(  
  '/test-rbac',  
  checkAuthenticated,  
  isAuthorized('read'),  
  (_req, res) => {  
    res.json({ message: 'You are authorized to access this resource' });  
  },  
);  
```

