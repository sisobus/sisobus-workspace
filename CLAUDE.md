# sisobus-workspace

이 repo는 여러 서비스를 submodule로 관리하는 오케스트레이션 repo이다.
실제 서비스 코드는 이 repo에 작성하지 않는다.

## 핵심 규칙

1. 이 repo에서 직접 서비스 코드를 작성하지 않는다
2. submodule 디렉토리 안으로 이동해서 작업하지 않는다 — 큰 틀의 관리만 수행한다
3. 실제 서비스 개발은 해당 서비스 repo에서 별도 세션으로 진행한다
4. 각 서비스 repo에는 자체 CLAUDE.md가 존재하며, 서비스 고유 컨텍스트를 담당한다

## 신규 서비스 생성 절차

1. GitHub repo 생성
   ```bash
   gh repo create sisobus/<service-name> --private --description "<서비스 설명>"
   ```

2. submodule로 연결
   ```bash
   git submodule add git@github.com:sisobus/<service-name>.git <service-name>
   ```

3. 서비스 repo에 CLAUDE.md 생성 (아래 템플릿 사용)

4. 이 repo에 커밋
   ```bash
   git add .
   git commit -m "Add <service-name> submodule"
   git push
   ```

5. 아래 서비스 목록에 항목 추가

## 서비스 삭제 절차

1. submodule 제거
   ```bash
   git submodule deinit -f <service-name>
   git rm -f <service-name>
   rm -rf .git/modules/<service-name>
   ```

2. 이 repo에 커밋
   ```bash
   git commit -m "Remove <service-name> submodule"
   git push
   ```

3. 필요시 GitHub repo 삭제
   ```bash
   gh repo delete sisobus/<service-name> --yes
   ```

4. 아래 서비스 목록에서 항목 제거

## submodule 포인터 업데이트

서비스 repo에서 작업이 완료된 후, 이 repo에서 submodule 포인터를 최신으로 업데이트한다:

```bash
git submodule update --remote <service-name>
git add <service-name>
git commit -m "Update <service-name> submodule pointer"
git push
```

## 서비스 CLAUDE.md 템플릿

신규 서비스 repo에 생성할 CLAUDE.md 기본 구조:

```markdown
# <service-name>

## 개요
<이 서비스가 무엇인지, 왜 만들었는지>

## 기술 스택
<사용하는 언어, 프레임워크, 주요 라이브러리>

## 프로젝트 구조
<디렉토리 구조 설명>

## 개발 규칙
<코딩 컨벤션, 브랜치 전략, 커밋 메시지 규칙 등>

## 빌드 및 실행
<빌드, 테스트, 실행 명령어>

## 배포
<배포 방법, 환경 정보>
```

## 서비스 목록

| 서비스명 | 설명 | repo | 상태 |
|---------|------|------|------|
| (아직 없음) | | | |
