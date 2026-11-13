# docker-delivery-tracker

[shlee322/delivery-tracker](https://github.com/shlee322/delivery-tracker) 소스코드를 빌드하여 GitHub Container Registry(GHCR)에 배포하는 저장소입니다.

- **이미지 경로**: `ghcr.io/badugisoft/delivery-tracker`
- **지원 플랫폼**: `linux/amd64`, `linux/arm64`
- **기본 포트**: `4000`

## 컨테이너 실행

### Docker CLI

```bash
docker pull ghcr.io/badugisoft/delivery-tracker:latest

docker run -d \
  --name delivery-tracker \
  --restart unless-stopped \
  -p 4000:4000 \
  ghcr.io/badugisoft/delivery-tracker:latest
```

### Docker Compose

```yaml
services:
  delivery-tracker:
    image: ghcr.io/badugisoft/delivery-tracker:latest
    container_name: delivery-tracker
    restart: unless-stopped
    ports:
      - "4000:4000"
```

## 빌드 및 업로드 방식 (GitHub Actions)

[docker-publish.yml](.github/workflows/docker-publish.yml) 워크플로우가 다음 조건에서 `shlee322/delivery-tracker`를 체크아웃하여 멀티 플랫폼 이미지를 빌드하고 GHCR에 푸시합니다.

- **자동 실행**: `main` 브랜치에 푸시될 때
- **수동 실행**: GitHub 저장소의 **Actions → Build and Publish Docker Image → Run workflow** 실행 (선택적으로 `upstream_ref`에 원본 저장소의 브랜치, 태그 또는 커밋 SHA 지정 가능, 기본값 `main`)

생성되는 이미지 태그:
- `latest`
- `sha-<short_sha>`
- `<YYYYMMDD>-<short_sha>`
