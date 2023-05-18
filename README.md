## API Mockup 서버 구동
```bash
prism mock openapi.yml -p 4010
```

## API 병합
```bash
swagger-cli bundle openapi.yml -o openapi.trg.yml -t yaml
```

## API Test
portman -l openapi.trg.yml -b http://localhost:4010 -n true
```bash
portman --cliOptionsFile ./portman-cli-options.yml
```
