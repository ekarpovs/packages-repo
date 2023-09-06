## Simple Logger

A simple error handler for Nodejs applications.

<p>
  <a href="https://www.npmjs.com/package/@ekarpovs/simple-error-handler" target="_blank">
    <img alt="Version" src="https://img.shields.io/npm/v/@ekarpovs/simple-error-handler.svg">
  </a>
  <a href="https://github.com/ekarpovs/simple-error-handler#readme" target="_blank">
    <img alt="Documentation" src="https://img.shields.io/badge/documentation-yes-brightgreen.svg" />
  </a>
  <a href="https://github.com/ekarpovs/simple-error-handler/graphs/commit-activity" target="_blank">
    <img alt="Maintenance" src="https://img.shields.io/badge/Maintained%3F-yes-green.svg" />
  </a>
  <a href="https://github.com/ekarpovs/simple-error-handler/blob/master/LICENSE" target="_blank">
    <img alt="License: MIT" src="https://img.shields.io/badge/License-MIT-yellow.svg" />
  </a>
</p>

### Installation
```bash
  npm install @ekarpovs/simple-error-handler
```
### Usage
```
 - in an Application (index.ts):

    const app: Express = express();
    ...

    // after the last router
    app.use(errorHandler);

  - somewhere in a controller:

    export const getItem = async (req: Request, res: Response | any, next: NextFunction) => {
      ...
      if (!item) {
        throw new AppError({
          code: ResponseCode.NOT_FOUND,
          description: 'Item does not exist',
        });
      }
      return res.status(ResponseCode.OK).json(item);
    };
```
