## 프론트 배포 방식 
### 1. s3 + cloudfront
- https://dev.classmethod.jp/articles/aws-cli-s3-cloudfront-kr/ <br/>
- buildspec.yml
```
version: 0.2

phases:
  build:
    commands:
      - npm cache verify
      - npm install
      - npm run staging
  post_build:
    commands:
      - |-
        if [ $CODEBUILD_BUILD_SUCCEEDING -eq 0 ]; then
          return -1
        fi
      - aws s3 rm --recursive s3://rectest.haezoom.com/
      - aws s3 sync dist s3://rectest.haezoom.com/ 
      - aws cloudfront create-invalidation --distribution-id ECW2Z33NKU12T  --paths "/*"

```
### 2. nginx + 정적컨텐츠 방식
