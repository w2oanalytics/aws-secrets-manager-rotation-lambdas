To publish to SAR:
```
sam package --template-file ./template.yml --s3-bucket <s3 build bucket> --s3-prefix sar/secrets-manager-postgres-rotation-single-user --output-template-file packaged.yml
sam publish --template packaged.yml
```