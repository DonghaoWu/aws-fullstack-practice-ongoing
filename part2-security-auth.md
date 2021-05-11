# AWS Deployment (Part 2)

### `Key Word: User Authentication and Security.`

- #### Click here: [BACK TO NAVIGASTION](https://github.com/DonghaoWu/WebDev-tools-demo/blob/master/README.md)

## `Section: Backend.`

### `Summary`: In this documentation, we learn to encrypt and store password in database, also implement JWTs in Node.

### `Check Dependencies & Tools:`

- bcrypt
- @types/bcrypt
- jsonwebtoken
- @types/jsonwebtoken

------------------------------------------------------------

#### `本章背景: `
- 

------------------------------------------------------------

### <span id="2.0">`Brief Contents & codes position`</span>

- #### Click here: [BACK TO NAVIGASTION](https://github.com/DonghaoWu/WebDev-tools-demo/blob/master/README.md)

- [2.1 Outline.](#2.1)
- [2.2 Bcrypt password.](#2.2)
- [2.3 Implement JWT.](#2.3)
- [2.4 Deploying changes.](#2.4)

------------------------------------------------------------

### <span id="2.1">`Step1: Outline.`</span>

- #### Click here: [BACK TO CONTENT](#2.0)

    1. Install dependencies.

    2. Implement two methods:`generatePassword`/`comparePasswords`

    3. Implement one method:`generateJWT`, implement auth middleware method: `requireAuth`
        - add a new variable in .env file
        - import the new variable in config.js
    
    4. Deploy the changes.


### <span id="2.2">`Step2: Brypt methods.`</span>

- #### Click here: [BACK TO CONTENT](#2.0)

    1. Implement brypt methods.(`auth.router.ts`)

    ```ts
    import * as bcrypt from 'bcrypt';

    async function generatePassword(plainTextPassword: string): Promise<string> {
        const rounds = 10;
        const salt = await bcrypt.genSalt(rounds);
        const hash = await bcrypt.hash(plainTextPassword, salt);
        return hash;
    }

    async function comparePasswords(plainTextPassword: string, hash: string): Promise<boolean> {
        return await bcrypt.compare(plainTextPassword, hash);
    }
    ```

#### `Comment:`
1. In the register route, server will use `generatePassword` to encrypt the password then save it in database.

2. In the login route, server will use `comparePasswords` to decrypt the password then validate the password from database.

### <span id="2.3">`Step3: JWT methods.`</span>

- #### Click here: [BACK TO CONTENT](#2.0)

    1. Add a new variable in `.env` file

    ```json
    JWT_SECRET=your-secret
    ```

    2. Import the variable in `config.ts`

    ```js
    export const config = {
        "dev": {
            "username": process.env.POSTGRE_USERNAME,
            "password": process.env.POSTGRE_PASSWORD,
            "database": process.env.POSTGRE_DATABASE,
            "host": process.env.POSTGRE_HOST,
            "dialect": process.env.DIALECT,
            "aws_region": process.env.AWS_REGION,
            "aws_profile": process.env.AWS_PROFILE,
            "aws_media_bucket": process.env.AWS_MEDIA_BUCKET
        },
        "prod": {
            "username": "",
            "password": "",
            "database": "",
            "host": "",
            "dialect": "postgres"
        },
        "jwt": {
            "secret": process.env.JWT_SECRET
        }
    }
    ```

    3. Implement JWT method.(`auth.router.ts`)

    ```ts
    function generateJWT(user: User): string {
        return jwt.sign(user.toJSON(), config.jwt.secret)
    }
    ```

    4. Auth middleware function. (`auth.router.ts`)

    ```ts
    export function requireAuth(req: Request, res: Response, next: NextFunction) {
        if (!req.headers || !req.headers.authorization){
            return res.status(401).send({ message: 'No authorization headers.' });
        }

        const token_bearer = req.headers.authorization.split(' ');
        if(token_bearer.length != 2){
            return res.status(401).send({ message: 'Malformed token.' });
        }

        const token = token_bearer[1];

        return jwt.verify(token, config.jwt.secret, (err, decoded) => {
            if (err) {
                return res.status(500).send({ auth: false, message: 'Failed to authenticate.' });
            }
            return next();
        });
    }
    ```

#### `Comment:`
1. In the login/register route, server will send the token back to client after it is generated.

2. In some auth required routes, request will first go into auth middleware.
    
### <span id="2.4">`Step4: Deploying changes.`</span>

- #### Click here: [BACK TO CONTENT](#2.0)

    ```bash
    $ npm run build
    $ eb deploy
    ```

- #### Click here: [BACK TO CONTENT](#2.0)
- #### Click here: [BACK TO NAVIGASTION](https://github.com/DonghaoWu/WebDev-tools-demo/blob/master/README.md)