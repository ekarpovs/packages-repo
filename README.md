## Packages repo

### Temporary storage for npm packages
The repository contains archived packages in .tgz format (after the npm pack command),  
which are dedicated to local testing before publishing to the NPM repo.

#### Local testing with a node application:
 - Download the ekarpovs-{package-name}-0.0.0-development.tgz to a local computer,
 - Install the package from the root folder of an application with command:
 ```bash
    npm install <abs path to the archive>/ekarpovs-simple-logger-0.0.0-development.tgz
 ``` 

 #### Usage of a package:
  See the corresponding README.md file.