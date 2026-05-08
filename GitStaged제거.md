# 이미 원격 깃에 push된 파일 gitignore에 추가

- 이미 원격에 올라간 파일은 .gitignore에 추가만 해서는 추적이 멈추지 않는다.

1. gitignore에 추가
- 만약 test/ 폴더를 gitignore 설정하고 싶은데 이미 올라간 상태 (추적이 되어 있는 상태)
```
# .gitignore
test.txt
test/
```

2. 추적 제거
- cached : 실제 파일은 안 지우고, Git의 추적만 제거
``` bash
# 파일 제거
git rm --cached test.txt
# 폴더 제거
git rm -r --cached test/
```

3. commit push
``` bash
git commit -m "Remove ignored files from tracking"

git push
```