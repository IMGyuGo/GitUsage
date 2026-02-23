1. SSH 키 각각 생성 (이건 CMD창에서 원하는 위치에 생성 - 로컬데이터 유출되면 안됨)
``` bash
ssh-keygen -t ed25519 -C "account1@email.com"
ssh-keygen -t ed25519 -C "account2@email.com"

ssh-keygen -t ed25519 -C "account1@email.com" -f [원하는 경로]
```
각각 파일명 : id_ed25519_account1, id_ed25519_account2
위 명령어로 파일 만들 시 passphrase 설정하라고 나오는데, 여기서 비밀번호 넣으면 안전해짐  
아래는 (바로 경로 지정법)

2. SSH config 설정
~/.ssh/config 파일 생성 또는 수정 (만약 기존 경로를 수정했을 경우 IdentifyFile 위치를 변경한 경로로 설정해주면 됨)
```
Host [별칭1]
  HostName github.com
  User git
  IdentityFile ~/.ssh/id_ed25519_account1

Host [별칭2]
  HostName github.com
  User git
  IdentityFile ~/.ssh/id_ed25519_account2

- 추가로 Port는 기본 22인데 443으로 설정
Host [별칭1]
  HostName github.com
  Port 443
  User git
  IdentityFile ~/.ssh/id_ed25519_account1
```

3. 각 GitHub 계정에 공개키 등록
```
cat ~/.ssh/id_ed25519_[별칭].pub
```
복사 -> GitHub -> SSH Keys 등록
계정2도 동일

4. 레포별로 remote 변경
```
git remote set-url origin git@[별칭1]:username/[레포이름].git
git remote set-url origin git@[별칭2]:username/[레포이름].git
```

5. 추가로 중요 - 레포마다 커밋 작성자 설정
```
git config user.name "account1"
git config user.email "account1@email.com"
```

# 참고
``` bash
ssh -T git@github.com
ssh -T [account1]
```
ssh git 계정 연결 테스트(쉘을 열지 않고 연결 테스트만 하겠다는 의미)
만약 git config user.name으로 연결을 해놓았으면 아래로 연결 테스트 가능