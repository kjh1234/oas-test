
## OpenAPI편집에 유용한 확장기능
#### (**)주요기능
OpenAPI (Swagger) Editor: UI Editor, **UI Preview(swagger, redoc), **간편실행
Redocly OpenAPI: **Editor Option($ref, inteliSense), **참조 미리보기
openapi-designer: UI Preview(swagger), Editor Option(inteliSense), **API 문서 병합  
YAML to JSON Converter: **YAML <-> JSON 변환(단점: 변경전 파일을 삭제함, 이름이 기존과 동일하게 고정)

## API 병합
```bash
swagger-cli bundle openapi.yml -o openapi.trg.yml -t yaml
```

## API Mockup 서버 구동 - backend 개발 전 frontend 개발용으로 사용
```bash
# 로컬 api 파일로 mockup 서버 구동
prism mock openapi.yml -p 4010

# 원격지 api 파일로 mockup 서버 구동
prism mock https://raw.githubusercontent.com/kjh1234/oas-test/0.2/openapi.trg.yml -p 4010

# API 정의서와 동작중인 API 서비스의 Spec이 동일한지 비교 - 유효하지 않을경우 콘솔에 Error를 표시함
prism proxy openapi.yml http://127.0.0.1:4010 -p 4020

# API 정의서와 동작중인 API 서비스의 Spec이 동일한지 비교 - 유효하지 않을경우 콘솔/Response에 Error를 표시함
prism proxy openapi.yml http://127.0.0.1:4010 -p 4020 --errors
```

## API 규격의 소스파일 자동생성
```bash
# 로컬 api 파일로 source generator
npx @openapitools/openapi-generator-cli generate -i openapi.trg.yml -g typescript-axios -o ts-axios

# 원격지 api 파일로 source generator
npx @openapitools/openapi-generator-cli generate -i https://raw.githubusercontent.com/kjh1234/oas-test/0.2/openapi.trg.yml -g typescript-axios -o ts-axios

# spring client feign source generator
npx @openapitools/openapi-generator-cli generate -i https://raw.githubusercontent.com/kjh1234/oas-test/0.2/openapi.trg.yml -g spring --library spring-cloud  -o /samples/client/oas-test/java
```

## API Test
```bash
# 기본 검증(통신상태/스키마)
portman -l openapi.trg.yml -b http://localhost:4010 -n true

# 테스트 케이스 설정으로 검증(통신상태/스키마/결과값/API제외 등)
portman --cliOptionsFile ./portman-cli-options.yml
```


### Json Data를 JSON/YAML Schema로 변형시키는 도구
https://redocly.com/tools/json-to-json-schema/
