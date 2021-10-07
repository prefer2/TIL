## 데이터베이스 생성

`use [데이터베이스 이름]`

데이터베이스를 사용하려면 use 명령어를 사용한다. 만약, 그 이름을 가진 데이터베이스가 없다면 그 이름의 데이터베이스가 만들어진다.

`show dbs`

현재 생성되어 있는 db들을 보여준다

## INSERT

- `db.collection.insertOne()`
- `db.collection.insertMany()`

1개의 도큐먼트를 추가할때는 insertOne, 여러개의 도큐먼트를 추가할 때는 insertMany를 사용한다.

```sql
db.movies.insertMany([
   {
      title: "Jurassic World: Fallen Kingdom",
      genres: [ "Action", "Sci-Fi" ],
      runtime: 130,
      rated: "PG-13",
      year: 2018,
      directors: [ "J. A. Bayona" ],
      cast: [ "Chris Pratt", "Bryce Dallas Howard", "Rafe Spall" ],
      type: "movie"
    },
    {
      title: "Tag",
      genres: [ "Comedy", "Action" ],
      runtime: 105,
      rated: "R",
      year: 2018,
      directors: [ "Jeff Tomsic" ],
      cast: [ "Annabelle Wallis", "Jeremy Renner", "Jon Hamm" ],
      type: "movie"
    }
])
```

## QUERY

`db.collection.find()`

```sql
db.movies.find()
```

movies 도큐먼트에 있는 모든 값을 출력한다

```sql
db.movies.find( { "title": "Titanic" } )
```

title이 Titanic인 값들을 출력한다. SQL문에서 `SELECT * FROM movies WHERE title = "Titanic"` 와 같은 역할이다.

```sql
db.movies.find( { countries: "Mexico", "imdb.rating": { $gte: 7 } } )
db.movies.find( {
     year: 2010,
     $or: [ { "awards.wins": { $gte: 5 } }, { genres: "Drama" } ]
} )
```

AND문의 경우에는 ,로 연결하여 구할 수 있다. OR문은 $or 연산자를 사용하여 구한다.


## UPDATE

- `db.collection.updateOne()`
- `db.collection.updateMany()`
- `db.collection.replaceOne()`

1개의 도큐먼트를 수정할때는 updateOne, 여러개의 도큐먼트를 수정할 때는 updateMany를 사용한다. 도큐먼트를 대체할때는 replaceOne을 사용한다.

```sql
db.listingsAndReviews.updateMany(
  { security_deposit: { $lt: 100 } },
  {
    $set: { security_deposit: 100, minimum_nights: 1 }
  }
)
```

## DELETE

- `db.collection.deleteMany()`
- `db.collection.deleteOne()`

1개의 도큐먼트를 삭제할때는 deleteOne, 여러개의 도큐먼트를 삭제할 때는 deleteMany를 사용한다.

```sql
db.movies.deleteMany( { title: "Titanic" } )
```

## OPERATOR


|  명령어    |     의미                            |
|------------|-------------------------------------|
| $gt, $gte  | greater than, greater than or equal |
| $lt, $lte  | less than, less than or equal       |
| $eq        | equal                               |
| $ne        | not equal                           |
| $in        | in                                  |
| $ni        | not in                              |
| $and, $or  | and, or                             |
| $nor, $not | nor, not                            |

## 출처
https://docs.mongodb.com/mongodb-shell/crud/
