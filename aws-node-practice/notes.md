1. 本地连接 aws database，复制黏贴 database endpoint，放进。/src/config/config.ts 文件夹中 /password/username/database/host/dialect/。

2. 为什么可以直接连接 aws 数据库，因为在上一节当中已经实现了 aws 的连接 inbound rules。

<!-- up about connect db in app -->

<!-- down about connecting s3 in app -->

1. signedURL

2. AWS SDK: aws.ts

3. generates an aws signed url to retreive an item

4. generates an aws signed url to put an item

<!-- elastic beanstalk -->

1. IAM/Users/add permissions/attach existing policies directly/

2. EB CLI

```bash
$ eb init/app name/node.js/
$ 
```

    - .elasticbeanstalk/config.yml
    ```yml
    deploy:
        artifact: ./www/Archive.zip
    ```

3. scripts

    ```json

    ```

    ```bash
    $ npm run build
    $ eb create
    ```

4. eb console configure/elastic bean stalk/ configuration/software/environment properties/copy and paste environment variables/apply

    ```
    AWS_PROFILE:DEPLOYED
    ```

5. eb console configure/elasticbean stalk/ configuration/security/IAM instance profile/IAM/roles/attach s3 policy and udaram_s3_media_dev

6. 总结本章，建立 IAM，RDS，S3，然后在 app code 添加连接 .env，最后安装 elasticbean stalk 去 deploy。过程很值得总结。

<!-- salted hashed password -->

1. install bcypt

    ```bash
    $ npm i bcypt --save
    $ npm i --save-dev @types/bcrypt
    ```

2. using brypt to encrypt password.

3. bcrypt 的加密和解密都不需要自提供 secret，JWT 需要提供自带 secret。

4. changed

```js
jwt.sign(user.toJSON(), config.jwt.secret)
```

5. deploying changing

```bash
$ npm run build // www/Archive.zip
$ eb deploy
```

6. scaling and fixing/domain name/DNS/router 53/

```bash

```

<!-- front end -->

1. content delivery networks.

2. using cdns to serve our frontend

3. upload the static build to an S3 bucket which can be linked to a cloudFront distributiobn.

4. scaling up in elasticbean stalk/modify instances/

5. scaling out in elasticbean stalk/more servers % load balancer & auto-scaling groups/

6. capacity/load balancing/scaling triggers/

7. scaling out rds instances

8. automatic bug reporting

    - elasticbean stalk/health/
    - sentry website
    - couldFlare/datadog/cloudWatch
    - 

    