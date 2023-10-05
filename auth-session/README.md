## Authentication with the session

An auth with the express session and the passport, - a solution for Nodejs applications.
Uses MongoDb as a session storage.

<p>
  <a href="https://www.npmjs.com/package/@ekarpovs/auth-session" target="_blank">
    <img alt="Version" src="https://img.shields.io/npm/v/@ekarpovs/auth-session.svg">
  </a>
  <a href="https://github.com/ekarpovs/auth-session#readme" target="_blank">
    <img alt="Documentation" src="https://img.shields.io/badge/documentation-yes-brightgreen.svg" />
  </a>
  <a href="https://github.com/ekarpovs/auth-session/graphs/commit-activity" target="_blank">
    <img alt="Maintenance" src="https://img.shields.io/badge/Maintained%3F-yes-green.svg" />
  </a>
  <a href="https://github.com/ekarpovs/auth-session/blob/master/LICENSE" target="_blank">
    <img alt="License: MIT" src="https://img.shields.io/badge/License-MIT-yellow.svg" />
  </a>
</p>

### Installation
```bash
  npm install @ekarpovs/auth-session (@ekarpovs/session-storage-mongo)
```
### Installation
```bash
  npm install @ekarpovs/auth-session
```
### Usage:
```
  import express, { Express } from 'express';

  import { 
    AuthConfig,
    BaseUser,
    CookieConfig,
    SessionConfig,
  } from '@ekarpovs/auth-session';
  
  // Optional:
  // import { StorageConfig, sessionStorage } from '@ekarpovs/session-storage';
  // import { EmailClient } from '@ekarpovs/simple-email-client';

  // Somewhere in an application
  const app: Express = express();


  // Configuration
  const cookieConfig: CookieConfig = {
    secure: "false",
    sameSite: "lax",
    httpOnly: "true",
    maxAge: "3600000",
  };

  const sessionConfig: SessionConfig = {
    name: "",
    secret: "",
    saveUninitialized: "false",
    cookie: cookieConfig,
    resave: "false"
  };

  const authConfig: AuthConfig = {
    app: app,
    storage: undefined,
    User: BaseUser,
    sessionConfig: sessionConfig,
  };

  // Optional: - inject session-storage
  const storageConfig: StorageConfig = {
    uri: "",
    db: "",
    collection: "",
  };

  // const storage = sessionStorage(storageConfig);
  // authConfig.storage = { store: storage};

  // Optional: inject simple-email-client
  const config = {
    name: "gmail",
    user: "<the-account-owner-email>",
    password: "<the-account-owner-password>"
  };

  const emailClient = new EmailClient(config);
  authConfig.emailer = emailClient;

  initAuth(authConfig);

```
### Extend BaseUser (example)
```
import { Schema } from "mongoose";

import { BaseUser } from "@ekarpovs/auth-session";


export interface UserInterface {
  isSuperAdmin: boolean;
  phone?: string;
}

const UserSchema = new Schema<UserInterface>({
  isSuperAdmin: {
    type: Boolean,
    required: true,
    default: false,
  },
  phone: {
    type: String,
    required: false,
  },
}, {collection: 'users'});

export const User = BaseUser.discriminator("user", UserSchema);
```

### Protected router (example)
```
import { Router } from "express";

import { checkAuthenticated } from "@ekarpovs/auth-session";
import {
  getAllUsers,
  getUserById,
} from "./controller";

const userRouter = Router();

userRouter.get("/", 
  checkAuthenticated,
  getAllUsers
);

userRouter.get(
  "/user",
  checkAuthenticated,
  getUserById
);

export default userRouter;
```

### API
```
  register:  
  	 url: https://{uri}/auth/register  
	 body: {  
	    "name": "",  
	    "email": "",  
	    "password": "",  
	}  
   
  login:  
  	 url: https://{uri}/auth/login  
	 body: {  
	    "email": "",  
	    "password": ""  
	}  

  logout:  
  	url: https://{uri}/auth/logout  
  change password:  
  	url: https://{uri}/auth/change-password  
	body: {  
	    "email":"",  
	    "password":"",  
	    "passwordNew":""  
	}  
  
  reset password request:  
   	url: https://{uri}/auth/reset-password-request  
   	body: {  
	    "email": ""  
	}  
  
  reset password:  
   	url: https://{uri}/auth/reset-password  
   	body: {  
	    "user": "",  
	    "token": "",  
	    "password": ""  
	}  
```
