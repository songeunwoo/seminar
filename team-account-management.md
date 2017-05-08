# Team public account password management

팀 프로젝트 내부에서 사용하는 부가 서비스의 계정들이 점차 늘어남에 따라 해당 계정들을 안전하게 공유하는 방법에 대해 소개합니다.

## pass 개념 및 사용준비

pass는 [GNU Privacy Guard (GnuPG or GPG)](https://en.wikipedia.org/wiki/GNU_Privacy_Guard) 기반의 패스워드 관리툴로 [PGP(Pretty Good Privacy)](https://en.wikipedia.org/wiki/Pretty_Good_Privacy)  오픈소스 구현판입니다. pass에서 사용된 암호화 방식의 대략적인 흐름도를 살펴보자면 아래와 같습니다.

보통 암호화를 하면 비밀번호가 생각나기 마련인데 이 암호화의 비밀번호는 암호화할때 쓰는 암호와 복호화할때 쓰는 암호가 같습니다. (이런 암호화 방식을 대칭키 암호화라 합니다.)

하지만 GPG에서 사용하는 [RSA](https://en.wikipedia.org/wiki/RSA_(cryptosystem) 방식은 다릅니다. RSA는 암호(이하 키)가 2개입니다. 어떤 키로 암호화하면 다른 키로만 복호화할 수 있습니다. 여기서 다른 사람에게 키를 공개해야 합니다. 왜나고요? 열쇠없이 자물쇠를 열 수는 없잖아요. 여기서 다른 사람에게 공개하는 키는 공개키라 칭하고, 자신만이 가지는 키는 개인키라 칭합니다.

공개키로 암호화하면 개인키로만 복호화할 수 있습니다. 개인키로 암호화하면 공개키로만 복호화할 수 있습니다. 개인키는 오직 그 자신만이 가지고 있기에 개인키로 암호화 했다는 것은 개인이 직접 암호화 했다는 것을 의미합니다. 보는 사람은 공개키를 이용하여 복호화하면 됩니다.

그리고 보내는 사람이 받는 사람의 공개키로 암호화하면 개인키를 가지고 있는 받는 사람만이 복호화하여 볼 수 있습니다. 주로 자신의 메일을 암호화 하는 데 사용하며, 2015년 6월 기준으로 페이스북에서 이걸 이용해서 비밀번호 재설정 링크 같은 민감한 정보를 암호화해 보낸다 합니다.


### pass 설치

이제 사용을 해보기 위해 설치하는 방법을 따라가 보자. 필자는 환경이 Mac이므로 Mac 기준으로 진행함을 참고 바란다.

```
$ brew install pass
$ echo "source /usr/local/etc/bash_completion.d/password-store" >> ~/.bash_profile
```

![](assets/account-1.png)

### gpg key 생성

우선 무엇을 하든 키가 필요할테니 gpg key를 만들어 줍니다. gpg는 비대칭키 방식의 암호화를 사용할 수 있는 오픈 소스 툴입니다.

```
# 키 생성
$ gpg2 --gen-key

# 키 확인
$ gpg2 --list-keys
```

![](assets/account-2.png)

여기에서 gpg-id 는 22C857138D5BEB460CF20DFFF68AB0160A5ACECF 입니다.

### pass 활성화

gpg-id를 이용하여 pass를 활성화 시킵니다.

```
$ pass init 22C857138D5BEB460CF20DFFF68AB0160A5ACECF
```

![](assets/account-3.png)

gpg-id로 pass를 시작하면 pass는 앞으로 해당 gpg-id의 공개 키를 이용해서 모든 비밀번호를 암호화합니다. ‘~/.password-store/’ 디렉토리가 생성되었으며 이곳에 암호화된 비밀번호를 ‘.gpg’ 파일로 저장한다. 이제 pass를 이용해서 비밀번호를 관리할 수 있습니다.


## pass 사용하기

이제부터는 pass를 사용하는 방법에 대해서 알아보겠습니다.

### 비밀번호 저장

test@test.com 메일의 비밀번호를 저장하는 예입니다.

```
$ pass insert email/test@test.com

$ Enter password for email/test@test.com:
$ Retype password for email/test@test.com:
```

![](assets/account-4.png)

email 디렉토리 밑에 test@test.com 계정의 비밀번호가 저장되었으며, pass 명령으로 해당 계정을 호출하면 비밀번호가 출력됩니다.

```
$ pass email/test@test.com
pasta!@#

$ pass -c email/test@test.com
Copied email/test@test.com to clipboard. Will clear in 45 seconds.
```

비밀번호 이외에 여러줄의 텍스트 정보 입력시에는 ```-m```을 이용하면 됩니다.

```
$ pass insert -m geunwoo-credit-card

Enter contents of geunwoo-credit-card and press Ctrl+D when finished:

9291-1212-2323-4444
name: GEUNWOO SON
number: 1234-1232-1231-1233
cvv: 099

$ pass
Password Store
├── email
│   └── test@test.com
├── geunwoo-credit-card
└── geunwoo-for-microsite

$ pass geunwoo-credit-card
9291-1212-2323-4444
name: GEUNWOO SON
number: 1234-1232-1231-1233
cvv: 099
```

### 비밀번호 생성

새 계정을 만들때부터 pass를 이용하여 비밀번호 생성이 가능하다.

![](assets/account-5.png)

## git으로 pass 관리하기

이제 주 목적인 pass를 이용하여 git을 사용하는 방법을 알아보겠습니다.
 ‘~/.password-store/’ 를 git으로 관리하면 되겠지만 pass에서는 자체 명렁어를 제공합니다.

```
$ pass git init
Initialized empty Git repository in /Users/NAVER/.password-store/.git/
[master (root-commit) b2b63b8] Add current contents of password store.
 4 files changed, 1 insertion(+)
 create mode 100644 .gpg-id
 create mode 100644 email/test@test.com.gpg
 create mode 100644 geunwoo-credit-card.gpg
 create mode 100644 geunwoo-for-microsite.gpg
[master 828a16f] Configure git repository for gpg file diff.
 1 file changed, 1 insertion(+)
 create mode 100644 .gitattributes
```

![](assets/account-6.png)

일단 git과 연결되면, pass의 정보가 바뀔 때마다 커밋이 자동으로 이루어집니다. ```pass git push, pass git pull``` 등을 사용해서 업데이트 및 푸쉬를 합니다.


## 팀원과 공유하기

![](assets/account-key.png)(출처: https://commons.wikimedia.org/wiki/File:Orange_blue_public_key_cryptography_en.svg)

블록체인

### 공개 키 공유하기


### 공개 키 가져오기


### 새로운 동료와 공유하기


### 서로 다른 보안 수준 반영하기


### 개인 비밀번호 관리하기


## .pem 파일 관리



출처: http://boxnwhis.kr/2017/04/27/how_to_manage_passwords_for_your_team.html
