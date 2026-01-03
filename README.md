# KYEOL App GitOps

Saleor 앱 배포용 GitOps 레포지토리입니다.

## 디렉토리 구조

```
kyeol-app-gitops/
├── apps/
│   └── saleor/
│       ├── base/                # 기본 매니페스트
│       └── overlays/            # 환경별 오버레이
│           ├── dev/             # DEV 환경 (Phase-1)
│           ├── stage/           # STAGE (템플릿)
│           └── prod/            # PROD (템플릿)
└── argocd/
    └── applications/            # ArgoCD Application 정의
```

## 배포 방법

### Kustomize 직접 적용

```bash
kubectl apply -k apps/saleor/overlays/dev/
```

### ArgoCD를 통한 배포

```bash
kubectl apply -f argocd/applications/saleor-dev.yaml
```

## 필수 설정 교체

배포 전 다음 값을 실제 값으로 교체하세요:

1. **ECR 이미지 URL**: `827913617839.dkr.ecr.ap-northeast-1.amazonaws.com/...`
2. **ACM 인증서 ARN**: `arn:aws:acm:ap-northeast-1:827913617839:certificate/...`
3. **GitHub 레포 URL**: `https://github.com/Jungbin7/...`

## 도메인 설정

| 환경 | 메인 도메인 | API 도메인 |
|------|---------------|-------------|
| DEV | `dev.mgz-g2-u3.shop` | `dev-api.mgz-g2-u3.shop` |
| STAGE | `stage.mgz-g2-u3.shop` | `stage-api.mgz-g2-u3.shop` |
| PROD | `mgz-g2-u3.shop` | `api.mgz-g2-u3.shop` |
