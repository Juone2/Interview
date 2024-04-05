## 배포를 해봐야 하는 이유

- 배포 및 배포 후 기능 추가 같은 사후 관리가 없는 프로젝트 경험이면 그저 화면만 개발하는 퍼블리싱 개발자로 남을 것이란 느낌
- 배포를 하여 내가 만든 프로젝트를 사람들에게 보여주고 싶음
- 배포를 제대로 한 적이 한번도 없었기에 프로젝트 마무리를 제대로 못했다는 느낌이 마음 한 구석을 불편하게 함
- 더더욱이 기업에서 배포경험이 있는 개발자를 우대하기 때문
- 다른 비개발자와의 프로토타입 공유를 위해서라도 임시 배포는 필요

## CI / CD

> 개발 > 빌드 > 테스트 > 릴리즈 > 배포
> 

**CI/CD**는 `CI`는 한마디로 **빌드 및 테스트 자동화 과정**, `CD`는 **배포 자동화 과정**을 뜻합니다.

**CI - 지속적인 통합**으로, 새로운 코드가 작성되었을 때 주기적으로 빌드 및 테스트가 진행되면서 공유되는 `repository`에 `merge` 되는 것

**CD - 지속적인 배포(제공)**으로, CI단계를 거친 코드를 실제 운영 서버에 자동 배포 하는 것

<aside>
💻 개발, 빌드, 테스트, 배포까지 모든 단계를 자동화 하여 사용자에게 빠르게 배포하는 것

</aside>

## CI 단계

Github와 같은 협업툴을 사용하여 협업을 할 때 코드를 통합하고 빌드하고 테스트 하는 과정에서 빌드와 테스트를 자동으로 진행해줬을 때 장점

- 여러 개발자가 관련된 코드를 작업하여 발생하는 충돌 문제를 해결할 수 있다.
- 커밋 할 때 마다 빌드와 자동 테스트가 이루어져 잘못된 merge를 예방할 수 있다.
- 코드 검증에 들어가는 시간이 줄어들며, 개발 편의성이 좋아진다.

→ push, pr 요청 했을 때 코트 테스트 및 통합

## CD 단계에서,

### CI 단계가 다 끝났다면?

이 코드를 자동으로 배포하여 사용자는 항상 최신 버전의 서비스를 사용할 수 있게 된다. 

→ 배포를 자동화 함으로써 일일이 deploy하지 않아도 되며, 배포보다 개발에 집중할 수 있게 된다.

## Github action

### 1. github action workflow 파일 생성

프로젝트의 .github 폴더에 workflows라는 폴더를 만들고 yaml 파일 하나를 만든다.

!https://blog.kakaocdn.net/dn/kOZmc/btsb1PU8rmc/2j3GPqK3HbsLZrwNrar39k/img.png

### 2. front-build.yaml 내용

파일을 만든 후 해당 브랜치에 이 파일을 push

- code
    
    ```yaml
    name: Front Deployment
    
    # trigger가 되길 바라는 action을 입력합니다. push / pull_request가 있습니다.# 저는 develop 브랜치에 push가 되면 actions을 실행하도록 설정했습니다.on:
      push:
        branches:
          - develop
    
    # 위의 이벤트가 트리거되면 실행할 목록입니다.jobs:
      build:
        name: react build & deploy
    # runner가 실행될 환경을 지정합니다.runs-on: ubuntu-latest
    
    # name은 단계별로 실행되는 액션들의 설명을 담은 것으로, 나중에 github action에서 workflow에 표시됩니다.# uses 키워드로 Action을 불러올 수 있습니다.steps:
    
    # 레포지토리에 접근하여 CI서버로 코드를 내려받는 과정입니다.- name: checkout Github Action
            uses: actions/checkout@v3
    
    # workflow가 실행될 때 필요한 파일 중에서 거의 바뀌지 않는 파일들을 GitHub의 캐시에 올려놓고 CI 서버로 내려받습니다.# 프로젝트에서 자주 바뀌지 않는 수많은 패키지를 매번 다운받아 올리면 시간도 오래걸리고 네트워크 대역폭을 많이 사용하게됩니다.- name: Get npm cache directory
            id: npm-cache-dir
            run: |
              echo "::set-output name=dir::$(npm config get cache)"
          - uses: actions/cache@v3
            id: npm-cache
            with:
              path: ${{ steps.npm-cache-dir.outputs.dir }}
              key: ${{ runner.os }}-node-${{ hashFiles('**/package-lock.json') }}
              restore-keys: |
                ${{ runner.os }}-node-
    
          - name: install npm dependencies
            run: npm install
    
          - name: react build
            run: npm run build
    
    # aws에 접근하기 위한 권한을 받아옵니다.- name: Configure AWS credentials
            uses: aws-actions/configure-aws-credentials@v1
            with:
              aws-access-key-id: ${{ secrets.AWS_S3_ACCESS_KEY_ID }}
              aws-secret-access-key: ${{ secrets.AWS_S3_SECRET_ACCESS_KEY_ID }}
              aws-region: ap-northeast-2
    
    # S3에 build 파일을 올립니다.- name: Upload to S3
            env:
              BUCKET_NAME: ${{ secrets.AWS_S3_BUCKET_NAME}}
            run: |
              aws s3 sync \
                ./build s3://$BUCKET_NAME
    
    # cloudfront로 배포되는 파일은 기본설정 상 24시간동안 캐시가 유지됩니다.# 배포 후 S3에는 최신 정적리소스가 올라가있지만 엣지로케이션엔 이전 파일이 올라가있는 상태라는 의미입니다.# 바로 변화가 반영되길 바란다면 invalidation을 해주면 됩니다.# 해당 부분은 과금될 수 있으니 확인 후 사용하세요!- name: CloudFront Invalidation
            env:
              CLOUD_FRONT_ID: ${{ secrets.AWS_CLOUDFRONT_ID}}
            run: |
              aws cloudfront create-invalidation \
                --distribution-id $CLOUD_FRONT_ID --paths /*
    ```
    

### 3. github secret 세팅하기

프로젝트 repo에 Settings - Security - Secrets and variables - Actions로 들어가서 New repository secret을 누른다.

!https://blog.kakaocdn.net/dn/cnYLKv/btscvwGxgkK/Mfvgnzsk9wTWP9IG0fanF0/img.png

!https://blog.kakaocdn.net/dn/cUBEI2/btsb1RyO0L8/vDXW9yKj05yx9kYkMPjKX1/img.png

!https://blog.kakaocdn.net/dn/uuorc/btscyZOr7wN/93EBpCbcIOmszpZkvVyQQK/img.png

**AWS_S3_ACCESS_KEY_ID** : aws iam에서 발급받은 엑세스 키

**AWS_S3_SECRET_ACCESS_KEY_ID** : 엑세스 키를 발급받을 때 한번만 알려주는 secret

**AWS_S3_BUCKET_NAME** : S3 버킷 이름

**AWS_CLOUDFRONT_ID** : cloudfront Id

### 4. 확인하기

develop 브랜치에 푸시를 하면 github action이 작동하도록 설정 → develop브랜치에 push를 하고 repo Actions 탭에서 성공 여부를 확인 가능

!https://blog.kakaocdn.net/dn/du505N/btscfDfoUnF/kIKGBXMvIJpl9lrWWkBtYK/img.png