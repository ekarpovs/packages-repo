## Authentication with session v-0.0.1

A auth with express session and passport, - a solution for Nodejs applications.

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
  npm install @ekarpovs/auth-session
```
### Usage:
```
  import express, { Express } from 'express';

import {
  AuthConfig,
  CookieConfig,
  initAuth,
  SessionConfig,
} from '@ekarpovs/auth-session';
import { StorageConfig, sessionStorage } from '@ekarpovs/session-storage-mongo';
// Optional:
import { EmailClient } from '@ekarpovs/simple-email-client';
import { LoggerOptions, initLogger } from '@ekarpovs/simple-logger';
import { errorHandler } from '@ekarpovs/simple-error-handler';

import { setupUserRouter, User } from './users';

  // Somewhere in an application
  const app: Express = express();


  // Configuration
// Authentication
const cookieConfig: CookieConfig = {
  secure: process.env.COOKIE_SECURE,
  sameSite: process.env.COOKIE_SAME_SITE,
  httpOnly: process.env.COOKIE_HTTP_ONLY,
  maxAge: process.env.COOKIE_MAX_AGE,
};

const sessionConfig: SessionConfig = {
  name: process.env.SESSION_NAME,
  secret: process.env.SESSION_SECRET,
  saveUninitialized: process.env.SESSION_SAVE_UNINITIALIZED,
  cookie: cookieConfig,
  resave: process.env.SESSION_RESAVE,
};

const authConfig: AuthConfig = {
  app: app,
  storage: undefined,
  User: User,
  sessionConfig: sessionConfig,
};

// Optional: - inject session-storage
const storageConfig: StorageConfig = {
  uri: process.env.SESSION_STORAGE_URI,
  db: process.env.SESSION_STORAGE_DB,
  collection: process.env.SESSION_STORAGE_COLLECTION,
};
const storage = sessionStorage(storageConfig);
authConfig.storage = { store: storage };

// Optional: inject simple-email-client and (or) simple-logger
authConfig.emailer = emailClient;
authConfig.logger = logger;

const { authRouter, isAuthenticated } = initAuth(authConfig);

const router = Router();
router.use('/auth', authRouter);
router.use(
  '/users',
  setupUserRouter({ isAuthenticated }),
);

...


```
### Extend BaseUser (example)
```
import { Schema } from "mongoose";

import { BaseUser } from "@ekarpovs/auth-session";


export interface UserInterface {
  role: string; // if an authorization will be used
  phone?: string;
}

const UserSchema = new Schema<UserInterface>({
  role: { // if authorization will be used
    type: string,
    required: true,
    default: 'guest',
  },
  phone: {
    type: String,
    required: false,
  },
}, {collection: 'users'});

export const User = BaseUser.discriminator("user", UserSchema);
```

### Protected router (example of an implementation)
```
import { Router } from 'express';

import { setupUserController } from './controller';

export const setupUserRouter = ({ isAuthenticated }) => {
  const cnt = setupUserController({ logger });
  const router = Router();
  router.get(
    '/',
    isAuthenticated,
    cnt.getAllUsers,
  );
  router.get(
    '/user',
    isAuthenticated,
    cnt.getUserById,
  );
  return router;
};
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