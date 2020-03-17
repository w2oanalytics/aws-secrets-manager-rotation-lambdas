# To build:

- On local machine
  ```
  docker run -it --name pg-container lambci/lambda:build-python3.7 /bin/bash
  ```

- Inside container
  ```
  yum install -y postgresql96-devel
  exit
  ```

- On local machine
  ```
  docker commit pg-container lambci/lambda:build-python3.7
  sam build -u --skip-pull-image
  ```
## Note:
Typically running `sam build` will install all dependencies specified in `requirements.txt` without intervention. However, in our case this dependency `PyGreSQL` include native libs.
Also its installation requires `pg_config` command line tool. Hence we have above steps to roll a custom image first then ask `sam` to build inside this container.

# To publish to SAR:

```
sam package -t .aws-sam/build/template.yaml --s3-bucket <s3 build bucket> --s3-prefix sar/secrets-manager-postgres-rotation-single-user --output-template-file packaged.yml
sam publish -t packaged.yml
```