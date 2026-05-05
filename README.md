# KnockIn
KnockIn 프로젝트입니다. 이 프로젝트는 서브모듈을 포함하고 있습니다.

## 🚀 프로젝트 초기 설정 (Project Setup)

이 프로젝트를 처음 세팅할 때 반드시 아래 순서대로 원격 저장소를 설정해야 합니다.

### 1. 프로젝트 클론 및 서브모듈 초기화
```bash
# 부모 레포 클론
git clone https://github.com/your-repo/KnockIn.git
cd KnockIn

# 서브모듈 초기화 및 업데이트
git submodule update --init --recursive
```

### 2. 서브모듈 원격 저장소(Upstream) 설정
서브모듈 내에서 원본 저장소(Upstream)의 소식을 듣기 위해 설정이 필요합니다.
```bash
cd back/11th-1team-BE

# Upstream 원격 저장소 추가
git remote rename origin upstream
git remote add origin {서브모듈 Origin Repo URL}

# 설정 확인
git remote -v
cd ../..
```

### 3. 보안 파일 해제 (git-crypt)
프로젝트 내의 암호화된 파일(설정값 등)을 사용하기 위해 `git-crypt` 잠금을 해제합니다.
```bash
# git-crypt가 설치된 환경에서 키 파일을 이용해 해제
git-crypt unlock {key path}
```

---

## 🛠 서브모듈 관리 가이드 (Submodule Guide)

이 프로젝트의 서브모듈은 `upstream`(원본)과 `origin`(내 포크) 두 개의 원격을 가집니다.

### 1. 원본(Upstream) 최신 코드 가져오기
**`git submodule update --remote`는 `origin`을 기준으로 동작하므로, 원본(`upstream`)의 최신 코드를 가져오려면 아래 방식을 권장합니다.**
```bash
# 1. 서브모듈 폴더로 이동
cd back/11th-1team-BE

# 2. 원본(Upstream)의 main 브랜치에서 pull
git pull upstream main

# 3. 내 포크(Origin)에도 반영 (필요 시)
git push origin main

cd ../..
```

### 2. 서브모듈 수정 및 반영 (Push)
서브모듈 내부에서 코드를 수정했을 때의 절차입니다.
1. **서브모듈 커밋/푸시:**
   ```bash
   cd back/11th-1team-BE
   git add .
   git commit -m "feat: 서브모듈 수정 내용"
   git push origin main
   ```
2. **부모 레포에서 포인터 업데이트:**
   ```bash
   cd ../..
   git add back/11th-1team-BE
   git commit -m "chore: update submodule reference"
   git push origin main
   ```

### 3. 권장 설정
```bash
# 부모 레포 pull 시 서브모듈 자동 업데이트 활성화
git config submodule.recurse true
```
