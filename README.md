# 아카이브 API 문서

### BASE URL
`https://archiver.me/api`

---

### RateLimit

`50회/분`

| Header | Description |
|:---:|:---:|
| `X-RateLimit-Limit` | 사용 가능한 요청 횟수 |
| `X-RateLimit-Remaining` | 남은 요청 가능 횟수 | 

---

### 서버 정보 가져오기

`GET /guild/{id}`

##### 응답 예시
```
{
  "code": true,
  "data": {
        "category": ["봇, 게임"],
        "description": "<h3> HTML 방식으로 입력할 수 있어요!</h3>",
        "icon": "https://cdn.discordapp.com/icons/901745892418256906/ced3268f35d205e4ff6d750fe3ebb50a",
        "id": "901745892418256906",
        "member_count":22,
        "name":"test",
        "owner_discriminator":"4755",
        "owner_id":"406815674539835402",
        "owner_name":"Kisss",
        "owner_pfp":"https://cdn.discordapp.com/embed/avatars/0.png",
        "score":28.8
    }
}
```
#### 서버 정보 구조
| Name | Type | Description |
|:---:|:---:|:---:|
| `id` | `String` | 서버의 ID
| `name` | `String`  | 서버의 이름 |
| `icon` | `String`  | 서버의 아이콘 (없을 경우 "" 반환) |
| `score` | `Int`  | 서버의 점수 |
| `category` | `Array`  | 서버의 카테고리 목록 |
| `description` | `String`  | 서버의 설명 (HTML 형식)|
| `member_count` | `Int`  | 서버의 유저 수 |
| `owner_name` | `String`  | 서버 관리자의 이름 |
| `owner_id` | `String`  | 서버 관리자의 아이디 |
| `owner_discriminator` | `String`  | 서버 관리자의 태그 |
| `owner_pfp` | `String`  | 서버 관리자의 프로필 이미지|

---

### 봇 정보 가져오기

`GET /bot/{id}`

#### 응답 예시
```
{
"code":true,
    "data": {
        "db": {
            "_id":924284360562208800,
            "category":["봇"],
            "description":"<h1> HTML 형식으로 입력해주세요 </h1>",
            "flags":1,
            "homepage":"924284360562208809",
            "invite":"13212",
            "like":0,
            "owners":["406815674539835402"],
            "prefix":"123",
            "sortdescription":"924284360562208809",
            "status":0,
            "supportserver":"123123"
        },
        "owners": [
            {
                "accent_color":null,
                "avatar":null,
                "banner":null,
                "banner_color":null,
                "discriminator":"4755",
                "id":"406815674539835402",
                "public_flags":256,
                "username":"Kisss"
            }
        ],
        "user": {
            "accent_color":null,
            "avatar":null,
            "banner":null,
            "banner_color":null,
            "bot":true,
            "discriminator":"7680",
            "id":"924284360562208809",
            "public_flags":0,
            "username":"아카이브"
        }
   }
}
```


#### 봇 정보 구조
| Name | Type | Description |
|:---:|:---:|:---:|
| `db` | `Object` | 서버의 데이터 베이스 정보
| `owners` | `Array`  | 관리자들의 유저 데이터 |
| `user` | `Object`  | 봇의 유저정보 |

---
### 카테고리 검색하기

`GET /search?keyword={keyword}`

#### 응답 예시

```
{
"code":true,
    "data": [
        {
            "type":"bot",
            "db": {
                "_id": 924284360562208800,
                "category":["봇"],
                "description":"<h1> HTML 형식으로 입력해주세요 </h1>",
                "flags":1,
                "homepage":"https://archiver.me/",
                "invite":"https://discord.com/oauth2/authorize?client_id=924284360562208809&permissions=8&scope=bot%20applications.commands",
                "like":0,
                "owners":["406815674539835402"],
                "prefix":"!",
                "sortdescription":"아카이브의 웹사이트를 위한 봇 입니다",
                "status":0,
                "supportserver":"https://archiver.me/guild/925066763731886111/join"
            },
            "user":{
                "accent_color":null,
                "avatar":null,
                "banner":null,
                "banner_color":null,
                "bot":true,
                "discriminator":"7680",
                "id":"924284360562208809",
                "public_flags":0,
                "username":"아카이브"
            }
        },
        {
            "type":"guild"
            "guild":{
                "icon":"https://cdn.discordapp.com/icons/901745892418256906/ced3268f35d205e4ff6d750fe3ebb50a",
                "member_count":7,
                "name":"Archive",
                "owner_id":"406815674539835402",
                "owner_name":"Kisss",
                "owner_pfp":"https://cdn.discordapp.com/embed/avatars/0.png"
            },
            "id":"925066763731886111",
            "score":13.8,
            "timestamp":1640627276.69108
        }
    ]
}
```

#### 검색 구조

##### Type이 guild일경우
| Name | Type | Description |
|:---:|:---:|:---:|
| `guild` | `Object` | 서버의 데이터 베이스 정보
| `id` | `String`  | 서버의 ID |
| `score` | `Int`  | 서버의 점수 |
| `timestamp` | `Int`  | 서버의 등록일 |

##### Type이 bot일경우
| Name | Type | Description |
|:---:|:---:|:---:|
| `db` | `Object` | 서버의 데이터 베이스 정보
| `user` | `Object`  | 봇의 유저정보 |
