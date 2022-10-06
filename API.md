# API / 기능명세

## 1. 메인페이지

`**상품 관련**`

### 1) 목록 조회 + 검색 (GET)

<aside>
📌 example[.](http://domain.com/product/${ID}/reviews?offset)com/product/list?q=${queryString}&page=${page}&size=${size}

</aside>



- 요청

```
- 검색어
- 0부터 시작하는 페이지 번호
- 페이지 크기
```

- 반환

```json
[
   {
      "id":1,
      "picThumbnail":".../...png",
      "name":"레모나",
      "vendor":"일동제약",
      "price":3000,
      "reviewer":30,
      "checklists":[
         {
            "id":1,
            "num":2
         }
      ]
   }
]
```

## 2. 상품 조회 페이지

### 1) 상품 데이터 조회 (GET)

<aside>
📌 example.com/product/detail/${ID}

</aside>

- 요청

```
- 상품 번호
```

- 반환

```json
{
   "id":1,
   "pic_url":".../...png",
   "name":"레모나",
   "vendor":"일동제약",
   "price":3000,
   "deliveryFee":0,
   "originalURL":"https://...",
   "reviewer":30,
   "checklists":[
      {
         "id":1,
         "num":2
      },
      {
         "id":2,
         "num":2
      }
   ]
}
```

### 2) 상품 체크리스트 조회 (GET)

<aside>
📌 example.com/product/checklist/${ID}

</aside>

- 요청

```
- 상품 번호
```

- 반환

```json
{
   "id":1,
   "checklists":[
      {
         "id":1,
         "num":2
      },
      {
         "id":2,
         "num":2
      }
   ]
}
```

- 체크리스트

```kotlin
1. 증거 불충분
2. 애매모호한 주장
3. 거짓말
4. 부적절한 인증 라벨
```

---

`**리뷰 관련**`

### 2) 리뷰 조회 (GET)

<aside>
📌 example.com/review/list/${ID}?page=${page}&size=${size}

</aside>

- 요청

```
- 상품 번호
- 0부터 시작하는 페이지 번호
- 페이지 크기
```

- 반환

```json
[
   {
      "id":1,
      "content":"좋아요",
      "checkTypes":[
         1,
         2,
         3
      ]
   }
]
```

### 3) 리뷰 작성 (POST)

<aside>
📌 example.com/review/write

</aside>

- 요청

```
- 상품 번호 (**productId** : Int)
- 닉네임 (**nickname** : String) (나중에 교체)
- 내용 (**content** : String)
- 체크리스트 해당 여부 <- [1, 2 ...] (**checkTypes** : List<Int>)
```

- 반환

```json
{"id": 1}
```

### 4) 리뷰 삭제 (DELETE) - 미구현

<aside>
📌 example.com/review/delete

</aside>

- 요청

```
- 닉네임 (**nickname** : String) (나중에 교체)
```

- 반환

```json
{"id": 1}
```

---

## 5) 체크리스트 조회 (GET)

<aside>
📌 example.com/checklists

</aside>

- 요청

```
- 상품 ID
```

- 반환

```json
[
   {
      "id":1,
      "name":"증거 불충분"
   },
   {
      "id":2,
      "name":"애매모호한 주장"
   },
   {
      "id":3,
      "name":"거짓말"
   },
   {
      "id":4,
      "name":"부적절한 인증 라벨"
   }
]
```

- ID 별 체크리스트 종류

```
1. 증거 불충분
2. 애매모호한 주장
3. 거짓말
4. 부적절한 인증 라벨
```
  
## 6) 예외 처리
  
  
- HTTP 에러 코드 200, 400, 404, 500
- 응답
```json
  {"message": ""}
```
