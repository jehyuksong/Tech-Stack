# Authentication-Study

### 보안,인증 공부를 단계별로 저장하기 위해서 만든 저장소

### Level 1 ~ Level 6 까지의 보안 수준을 정리했습니다.

---

### \> Level 1 - 인증

### \> Level 2 - 암호화

### \> Level 3 - 해싱

### \> Level 4 - 해싱 + 솔트 : Bcrypt

### \> Level 5 - 쿠키, 세션 : Passport

### \> Level 6 - OAuth(Open Authorisation) : 구글 계정으로 로그인

---

> 혹시 소스가 궁금하신 분을 위해서 [https://github.com/jehyuksong/Authentication-Study](https://github.com/jehyuksong/Authentication-Study) <<

### 프로젝트 완성작과는 다를 수가 있어서 각 Commit마다 코멘트로 레벨을 적어놨습니다.

### 레벨별로 정리된 완성 파일을 필요하시다면 참고해주세요!

---

# 인증, 암호화

-   개인 데이터를 저장하고 엑세스를 제한하기 위해서 필요하다.
-   다양한 수준의 보안이 있다.
-   서비스와 이용자들을 전부 위험에 빠뜨리고 서비스가 망할 수도 있을 만큼 치명적이고 중요하다.

---

# Level 1 - 아이디, 비밀번호 데이터베이스 저장

-   단순히 사용자의 계정을 만들고 이메일과 비밀번호를 저장하는 것이다.

```
app.post("/login", function (req, res) {
  const username = req.body.username;
  const password = req.body.password;

  User.findOne({ email: username }, function (err, foundUser) {
    if (err) {
      console.log(err);
    } else {
      if (foundUser.password === password) {
        res.render("secrets");
      }
    }
  });
});
```

-   이러한 방법으로 데이터베이스에 등록된 정보와 로그인하는 정보가 일치한다면 로그인이 되게끔 하는 기본적인 방법이다.
-   하지만 이 방법을 이용하면 데이터베이스에서 그대로 아이디와 비밀번호가 노출되게 된다. 보안이 매우 취약한 방법이라고 볼 수 있다.

---

# Level 2 - 암호화

-   무언가를 뒤섞고 바꾸는 것을 암호화라고 한다.
-   메시지를 뒤섞는 방법과 뒤섞인 메시지를 해제할 수 있는 키가 필요하다.

```
$ npm i mongoose-encryption          // 암호화 모듈을 설치한다.
$ const encrypt = require("mongoose-encryption");
```

```
const userSchema = new mongoose.Schema({
  email: String,
  password: String,
});
```

-   만든 데이터베이스 스키마를 `new mongoose.Schema()` 를 사용해서 새로운 몽구스 스키마 객체로 만든다.

```
// secret을 정의하고
const secret = "Thisisourlittlesecret.";

//userSchema 에 암호화 플러그인을 추가한다. password 만이 암호화 되게끔 설정한다.
userSchema.plugin(encrypt, { secret: secret, encryptedFields: ["password"] });
```

-   이제 새로운 이메일과 비밀번호를 등록하거나 로그인할 때 알아서 암호화되고 알아서 해독이 된다.  
    데이터베이스에서 확인할 때도 굉장히 복잡한 문구로 나오는 것을 볼 수 있다.  
    ex > `"_ct" : { "$binary" : "YRdE1yDBN15wQadhPU8X9c+Oshc/f72VzdgHIAPAQsmap9gs/UNTARtm8FwVOxPtmQ==", "$type" : "00" },` 이처럼 말이다.
-   하지만 이 또한 문제가 있다. 자바스크립트 코드를 확인하는 것은 어렵지가 않은데, `secret` 인 `Thisisourlittlesecert.` 을 확인한다면 설정한 모든 패스워드를 해독할 수가 있기 때문이다.

---

### 환경 변수를 사용하여 비밀을 유지하는 방법 - dotenv

```
$ npm i dotenv            // dotenv 모듈을 설치한다.
```

```
require("dotenv").config();           // 상수로 정의하지 않고 사용하는데
                                                                            // 이를 코드 가장 위에 놓는 것이 매우 중요하다.
```

```
// 루트 폴더에 .env 파일을 만들고 연다.
// 아까 위에서 저장했던
const secret = "Thisisourlittlesecret.";
// 이 부분을 서버파일에서 삭제하고 .env 안에 아래와 같이 수정해서 넣는다.
SECERT=Thisisourlittlesecret.
// 자바스크립트 파일이 아니기 때문에 const도 필요없고, 따옴표, 세미콜론도 필요없다.
// 또한 암묵적으로 = 사이에는 공백이 없게 쓰는 것이 룰이다.
// 마지막 . 은 코드의 일부이기 때문에 남겨둔다.
```

```
// 그리고 위에서 사용했던
userSchema.plugin(encrypt, { secret: secret, encryptedFields: ["password"] });
// 이 부분을 아래와 같이 수정한다.
userSchema.plugin(encrypt, { secret: process.env.SECRET, encryptedFields: ["password"] });
```

-   `.env` 안에 저장된 내용들을 사용할 때는 `process.env` 에 이어서 참조할 수 있다.
-   `.env` **파일은 공개되면 안되기 때문에** `.gitignore` **에 추가해주는 것이 매우 중요하다.**
-   **Github에는 `commit history`가 남기 때문에 처음 `commit`을 하기 전에 `암호화`해야 할 것들을 설정해주고 `.gitignore`까지 정리를 하고 올려야 한다.**

---

