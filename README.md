## Packages repo

### Temporary storage for npm packages
The repository contains archived packages in .tgz format (after the npm pack command),  
which are dedicated to local testing before publishing to the NPM repo.

#### Local testing with a node application:
 - Download the ekarpovs-{package-name}-0.0.0-development.tgz to a local computer,
 - Install the package from the root folder of an application with the command:
 ```bash
    npm install <abs path to the archive>/ekarpovs-{package-name}-0.0.0-development.tgz
 ``` 

 #### Usage of a package:
  See the corresponding README.md file.

### The infrastructure for a package development:
#### 1. The empty application [for test a package(s)](https://github.com/ekarpovs/node-typescript-package-tester);
	The project includes:
	 - all tools (for linting, building, testing, e.t.c.);
	 - scripts for running these tools;
#### 2. The empty [base package project](https://github.com/ekarpovs/npm-base-package).
	The project includes:
	 - all tools (for linting, building, testing, packaging, e.t.c.);
	 - scripts for running these tools;
	 - example of a test;
	 - README.md for developers;
	 - readme.md for the NPM repo;
	 - Git hooks for pre-commit (linting) and pre-push (testing);
	 - Github actions for build, test, and delivery of the package into the NPM repository.
#### 3. The Github repo for [storing packages dedicated to local testing](https://github.com/ekarpovs/packages-repo).
####  4. Postman.

### The development workflow:
#### 1. Prepare a code for packaging:
   - Define a feature that is dedicated to a package(s).
   - Copy the feature code to the test application (src folder).
   - Analyze the feature code and separate it from the application code.
   - Or may split the code into several parts (the future packages).
   - Leave the main part of the feature's code in the test application.
   - Test and change the code to do it like a package code.
#### 2. Prepare a project for the package:
   - Copy the empty base package from Github to a local machine (one copy for each package).
   - Rename the projects respectively.
#### 3. Build the package:
   - Move the code into the corresponding empty package repository.
   - Write tests for the package.
   - Test it.
   - Locally pack the code.
#### 4. Locally test the package:
   - Locally install the package in the test application.
   - Test the feature implemented as the package.
#### 5. Store the results:
   - Push the project into Github (create a remote repo for the package code).
   - Copy the .tgz and readme.md to the packages repo and push the commit.
### 6. The package is ready for a local testing in an application.

### 7. Publish the package into the Github from GitHub Package Registry after these tests.  
   - A package will be built and published automatically via CI/CD pipeline (Github Actions),
### 8. Installation from the from GitHub Package Registry:  
   - Go to: Settings -> Developer Settings -> Personal access tokens - Tokens(classic). 
   - Create Personal access token in your Github account for Download packages  
      from GitHub Package Registry with the permission - read:packages
   - Create .npmrc file in the root directory of your project with the content:  
```
      @ekarpovs:registry=https://npm.pkg.github.com  
      //npm.pkg.github.com/:_authToken=<YOUR_TOKEN>  
      npm.pkg.github.com/:always-auth: false  
```
   - Install a package with the command:  
```bash
npm i --save @ekarpovs/<package name>
```
