### 1. `.gitignore` 파일에 제외 규칙 추가

우선 `.gitignore`에 제외하려는 폴더를 추가하세요.

`example/*`

---

### 2. Git에서 캐시 제거

이미 추적되고 있는 폴더와 파일을 Git의 캐시에서 제거해야 합니다. 터미널에서 다음 명령어를 실행하세요:

`git rm -r --cached example/`

이 명령은 `example/` 폴더를 Git의 추적 대상에서 제거하지만, 실제 파일은 로컬에 그대로 남아 있습니다.

---

### 3. 변경 사항 커밋

이제 제거된 상태를 Git에 반영합니다:

`git commit -m "Remove example folder from tracking"`

---

### 4. 원격 저장소에 푸시

변경 사항을 원격 저장소로 푸시하세요:

`git push origin 브랜치이름`