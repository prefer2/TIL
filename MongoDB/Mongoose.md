Mongoose는 릴레이션이 아니라 다큐먼트를 사용하기 때문에 ODM(Object Document Mapping)이라고 불린다. 스키마(Schema)를 통해 노드 서버 단에서 데이터를 필터링 할 수 있다. 또한 MySQL의 JOIN 기능도 populate이라는 메서드로 보완 할 수 있다. 

## 연결

```sql
const mongoose = require('mongoose');

// mongodb+srv:~ 형태의 주소를 process.env에 저장해 두었다
const DB = process.env.DATABASE.replace('<PASSWORD>', process.env.DATABASE_PASSWORD);
mongoose.connect(DB, {
    useNewUrlParser: true,
    useCreateIndex: true,
    useFindAndModify: false
}).then(() => console.log('DB connection sucessful!'));
```

## 스키마

```sql
const mongoose = require('mongoose');

const tourSchema = new mongoose.Schema({
    name: {
        type: String,
        required: [true, 'A tour must have a name'],
        unique: true
    },
    rating: {
        type: Number,
        default: 4.5
    },
    price: {
        type: Number,
        required: [true, 'A tour must have a price']
    }
});

const Tour = mongoose.model('Tour', tourSchema);
const testTour = new Tour({
    name: "The Forest Hiker",
    rating: 4.7,
    price: 497
})

//save instance to database
testTour.save().then(doc => {
    console.log(doc);
}).catch(err => {
    console.log(err)
});
```

Schema 생성자를 사용해서 스키마를 만든다. 이후 시퀼라이즈에서 모델을 정의하듯이 필드를 정의한다. 새로운 객체를 만들고 save()를 하여 저장한다.
