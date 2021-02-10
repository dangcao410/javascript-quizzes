<div align="center">
  <img height="60" src="img/JavaScript-logo.png">
  <h1>JavaScript Quizzes</h1>
</div>

---

###### 1. Output là gì?

```javascript
function a() {
    console.log(this);
}
a.call(null);
```

- A: `null`
- B: `undefined`
- C: `window object`

<details><summary><b>Đáp án</b></summary>
<p>

#### Đáp án: C

`this context` trong JavaScript tùy theo ngữ cảnh lúc gọi hàm.

Chúng ta có thể thay đổi `this context` của hàm bằng cách dùng hàm `call`, với tham số đầu tiên trở thành `this` và các tham số tiếp theo là các params của hàm.
Vì vậy, khi gọi `a.call(window)` thì `this` trong hàm `a` chính là `window`.

Lưu ý, khi chúng ta truyền tham số đầu tiên vào hàm `call` là `null` hay `undefined` thì JavaScript sẽ tự động truyền `global object` vào hàm được gọi chứ không truyền `null` hay `undefined`.
Vì vậy, đoạn code trên sẽ in ra `object window` thay vì `null`.

</p>
</details>

---

###### 2. Output là gì?

```javascript
if (!("a" in window)) {
    var a = 1;
}

console.log(a);
```

- A: `undefined`
- B: 1
- C: Reference Error

<details><summary><b>Đáp án</b></summary>
<p>

#### Đáp án: A

Đoạn code này trông có vẻ đơn giản, nếu biến global `window` chưa có phần tử `a` thì định nghĩa biến `a`, gán cho nó bằng 1.
Bạn sẽ nghĩ kết quả là 1, nhưng không, đáp án đúng là `undefined`, điều gì đang xảy ra? Cùng đi qua 3 điểm dưới đây sẽ rõ.

Đầu tiên, tất cả các biến global được lưu trữ trong global object là `window` (ở browser). Khi chúng ta khai báo `var a = 1` điều đó đồng nghĩa với việc khai báo `window.a = 1`, và chúng ta có thể kiểm tra 1 biến có phải là global hay nằm trong object window hay không bằng cách `"variable-name in window"`.
Vậy sau khi khai báo var `a = 1` thì `"a" in window` cho kết quả `true`.

Thứ hai, JavaScript có cơ chế `hoisted`, tất cả các khai báo biến đều được đưa lên đầu của scope của nó. Ví dụ:

```javascript
console.log("a" in window);
var a;
```

Tuy biến `a` được khai báo dưới dòng `console` nhưng kết quả in ra là `true`, vì JavaScript engine sẽ lần lượt tìm tất cả các khai báo biến và chuyển chúng lên đầu của scope.
Vì thế đoạn code được thực thi có thể viết lại như sau:

```javascript
var a;
alert("a" in window);
```

Thứ ba là chỉ các khai báo biến mới được `hoisted`, còn các khởi tạo, gán giá trị cho biến thì không. Ví dụ:

```javascript
var a = 1;
```

thì chúng ta có 2 quá trình:

```javascript
var a;    //declaration
a = 1;    //initialization
```

Tóm lại, với sự hiểu biết của 3 khái niệm trên thì đoạn code ban đầu được thực thi như sau:

```javascript
var a;
if (!("a" in window)) {
    a = 1;
}
console.log(a);
```

và tất nhiên, kết quả là `undefined`.

</p>
</details>

---

###### 3. Output là gì?

```javascript
function b(x, y, a) {
    arguments[2] = 10;
    console.log(a);
}
b(1, 2, 3);
```

- A: 1
- B: 2
- C: 3
- D: 10

<details><summary><b>Đáp án</b></summary>
<p>

#### Đáp án: D

`arguments` là một object đặc biệt trong function của JavaScript, nó chứa các params của function và share chung bộ nhớ với chúng, vì thế khi thay đổi giá trị của `agruments` thì các params cũng được thay đổi theo.

</p>
</details>

---

###### 4. Output là gì?

```javascript
console.log(new String('hello') === String('hello'));
```

- A: true
- B: false
- C: TypeError

<details><summary><b>Đáp án</b></summary>
<p>

#### Đáp án: B

Khi gọi String constructor function với từ khóa `new` sẽ cho kết quả là một object, trong khi đó, không có từ khóa `new` kết quả sẽ là một primitive string, so sánh `===` giữa 2 kiểu dữ liệu khác nhau sẽ cho kết quả là `false`.

</p>
</details>

---

###### 5. Output là gì?

```javascript
console.log('1' -- '1');
```

- A: 0
- B: 2
- C: 11
- D: TypeError

<details><summary><b>Đáp án</b></summary>
<p>

#### Đáp án: D

Postfix Operator `--` chỉ thực hiện với biến, trong trường hợp này `'1'` không phải là biến nên sẽ gây ra lỗi `TypeError`.
Nếu đoạn code trên được viết thành `'1' - - '1'` (chú ý có space giữa 2 dấu `-`) thì sẽ cho kết quả là `2`.

</p>
</details>

---

###### 6. Output là gì?

```javascript
var foo = function bar() {
    console.log(foo === bar);
};
foo();
bar();
```

- A: true, true
- B: false, false
- C: true, ReferenceError
- D: false, ReferenceError

<details><summary><b>Đáp án</b></summary>
<p>

#### Đáp án: D

Chúng ta có thể khai báo `function expression` cùng với `named function` và dùng `named function` bên trong function đó để gọi tới chính nó.
Nhưng chúng ta không thể dùng `named function` bên ngoài được, điều đó có nghĩa khi gọi `bar()` sẽ gây ra lỗi `ReferenceError`.

</p>
</details>

---

###### 7. Output là gì?

```javascript
var myArr = ['foo', 'bar', 'baz'];
console.log('2' in myArr);
```

- A: ReferenceError
- B: true
- C: false

<details><summary><b>Đáp án</b></summary>
<p>

#### Đáp án: B

`in operator` sẽ kiểm tra 1 thuộc tính có phải là của object đó hay không, một array cũng là một object và có các thuộc tính index (`myArray[2] === myArray['2']`), vậy kết quả là `true`.

</p>
</details>

---

###### 8. Output là gì?

```javascript
var bar = 1,
    foo = {};

foo: {
    bar: 2;
    baz: ++bar;
};

console.log(foo.baz + foo.bar + bar);
```

- A: ReferenceError
- B: TypeError
- C: NaN
- D: 4
- E: 5

<details><summary><b>Đáp án</b></summary>
<p>

#### Đáp án: C

Trong JavaScript cũng có `labled statement` nên đoạn code trên không có lỗi gì đâu nhé.
Phần tử `baz` và `bar` không có trong object `foo` nên ta có thể viết lại như sau `undefined + undefined + 1` và cho kết quả là `NaN`.

</p>
</details>

---

###### 9. Output là gì?

```javascript
console.log([] + [] + 'foo'.split(''));
```

- A: f,o,o
- B: ["f", "o", "o"]
- C: TypeError
- D: [][]["f", "o", "o"]

<details><summary><b>Đáp án</b></summary>
<p>

#### Đáp án: A

Theo operator precedence, các lời gọi function sẽ có độ ưu tiên cao hơn operator `+`, vì vậy `'foo'.split('')` sẽ thực hiện trước.
Ta có thể viết lại như sau `[] + [] + ['f', 'o', 'o']`, JavaScript sẽ chuyển đổi array sang string trước khi `+` nên ta có kết quả là `f,o,o`.

</p>
</details>

---

###### 10. Output là gì?

```javascript
console.log(true + false > 2 + true);
```

- A: true
- B: false
- C: TypeError
- D: NaN

<details><summary><b>Đáp án</b></summary>
<p>

#### Đáp án: B

Operator `+` sẽ có độ ưu tiên cao hơn operator `>` vì thế `+` sẽ được thực hiện trước.
Khi `+` number với boolean hoặc 2 boolean với nhau, JavaScript sẽ chuyển đổi boolean về number, `true -> 1` và `false -> 0`, vì vậy ta có thể viết thành `1 + 0 > 2 + 1`, kết quả `1 > 3` là `false`.

</p>
</details>

---

###### 11. Output là gì?

```javascript
var arr = [];
arr[0]  = 'a';
arr[1]  = 'b';
arr.foo = 'c';
console.log(arr.length);
```

- A: 1
- B: 2
- C: 3
- D: undefined

<details><summary><b>Đáp án</b></summary>
<p>

#### Đáp án: B

Trong JavaScript Array, khi set một thuộc tính cho một array, nếu thuộc tính đó là một `valid array index` thì `length` của array đó sẽ được tính toán lại. Một thuộc tính `p` là `valid array index` khi và chỉ khi `ToString(ToUint32(p)) bằng p hoặc ToUint32(p)` và p không bằng  `2^32−1.`.
Khi đó, `0` và `1` sẽ thỏa mãn điều kiện còn `foo` thì không, vậy kết quả là `2`.

</p>
</details>

---

###### 12. Output là gì?

```javascript
function Dog(name) {
    this.name = name;
    this.speak = function() {
        return 'woof';
    };
}

const dog = new Dog('Pogo');

Dog.prototype.speak = function() {
    return 'arf';
};

console.log(dog.speak());
```

- A: woof
- B: arf

<details><summary><b>Đáp án</b></summary>
<p>

#### Đáp án: A

Khi gọi đến thuộc tính hay phương thức của một object, đầu tiên nó sẽ tìm trong object trước, nếu không tìm thấy, mới tiếp tục tìm trong Prototype của nó.

</p>
</details>

---

###### 13. Output là gì?

```javascript
const p1 = new Promise((resolve, reject) =>
    setTimeout(resolve, 100, 'Hello')
);

const p2 = new Promise((resolve, reject) =>
    setTimeout(resolve, 120, 'Goodbye')
);

const p3 = new Promise((resolve, reject) =>
    setTimeout(reject, 10, 'Oops!')
);

Promise.race([p1, p2, p3])
    .then(result => console.log(result))
    .catch(reason => console.log('Something went wrong...'));
```

- A: Hello
- B: Goodbye
- C: Oops!
- D: Something went wrong...

<details><summary><b>Đáp án</b></summary>
<p>

#### Đáp án: D

Promise.race() sẽ trả về kết quả của một Promise nào hoàn thành trước. Trong ví dụ trên, `p3` sẽ hoàn thành trước, nó sẽ gọi `reject` sau 10ms và sẽ rơi vào `catch`.

</p>
</details>

---

###### 14. Output là gì?

```javascript
const timer = a => {
    return new Promise(res =>
        setTimeout(() => {
            res(a);
        }, Math.random() * 100)
    );
};

const all = Promise.all([
    timer('first'),
    timer('second')
]).then(data => console.log(data));
```

- A: ["first", "second"]
- B: It is random

<details><summary><b>Đáp án</b></summary>
<p>

#### Đáp án: A

Promise.all không quan tâm đến thứ tự thời gian hoàn thành xong các Promise, nó sẽ chờ cho tất cả các Promise hoàn thành xong và kết quả của nó sẽ là một array với thứ tự giữ nguyên với thứ tự của tham số truyền vào.

</p>
</details>

---

###### 15. Output là gì?

```javascript
console.log(1 < 2 < 3);
console.log(3 > 2 > 1);
```

- A: true true
- B: true false
- C: false false
- D: undefined undefined

<details><summary><b>Đáp án</b></summary>
<p>

#### Đáp án: B

Các toán tử `<` và `>` có cùng độ ưu tiên và sẽ được thực hiện từ trái qua phải.

Dòng đầu tiên chúng ta có thể viết lại như sau `(1 < 2) < 3`, `1 < 2` được thực hiện trước và trả về `true`, sau đó thực hiện `true < 3`, khi so sánh với number, boolean sẽ được chuyển đổi sang number, `true` trở thành `1`, vậy `true < 3` cho kết quả `true`.

Ở dòng thứ hai `(3 > 2) > 1`, `(3 > 2)` cũng được thực hiện trước và trả về `true`, tuy nhiên sau đó `true > 1` sẽ được chuyển đổi thành `1 > 1` và cho kết quả `false`.

</p>
</details>

---

###### 16. Output là gì?

```javascript
const obj = {
    1: 1,
    2: 2,
    3: 3
};

console.log(Object.keys(obj), Object.values(obj));
```

- A: [1, 2, 3] ["1", "2", "3"]
- B: ["1", "2", "3"] [1, 2, 3]
- C: ["1", "2", "3"] ["1", "2", "3"]

<details><summary><b>Đáp án</b></summary>
<p>

#### Đáp án: B

`Object.keys` sẽ chuyển đổi keys của object sang string `['1', '2', '3']` và `Object.values` sẽ giữ nguyên values của object `[1, 2, 3]`.

</p>
</details>

---

###### 17. Output là gì?

```javascript
const a = {
    stringField: 'Joe',
    nestedField: { field: 'Nested' },
    functionField: () => 'aReturn'
};

const b = Object.assign({}, a);

b.stringField = 'Bob';
b.nestedField.field = 'Changed';
b.functionField = () => 'bReturn';

console.log(
    a.stringField,
    a.nestedField.field,
    a.functionField()
);
```

- A: Joe Nested aReturn
- B: Bob Changed bReturn
- C: Joe Changed aReturn
- D: Bob Nested bReturn

<details><summary><b>Đáp án</b></summary>
<p>

#### Đáp án: C

`b = Object.assign({},a);` sẽ thực hiện một `shallow copy` trên object `a`, bất kỳ thuộc tính nào của `b` là object đều tham chiếu đến cùng thuộc tính trong `a`.
Vì vậy khi chúng ta thay đổi nested field của `b`, thì nested field của `a` cũng thay đổi theo.

</p>
</details>

---

###### 18. Output là gì?

```javascript
const a = {
    stringField: 'Joe',
    numberField: 123,
    dateField: new Date('1995-12-17T03:24:00'),
    nestedField: { field: 'Nested' }
};

const b = JSON.parse(JSON.stringify(a));

console.log(
    a.stringField === b.stringField,
    a.numberField === b.numberField,
    a.dateField === b.dateField,
    a.nestedField.field === b.nestedField.field
);
```

- A: true true true true
- B: true true true false
- C: true true false true
- D: false false false false

<details><summary><b>Đáp án</b></summary>
<p>

#### Đáp án: C

`b = JSON.parse(JSON.stringify(a))` sẽ thực hiện deep copy trên object `a`.
Tất cả các thuộc tính là các kiểu dữ liệu nguyên thủy (Boolean, String, Number) sẽ được copy một cách chính xác, tuy nhiên đối với các thuộc tính có giá trị không phải là giá trị JSON (Date, undefined, Function, và không phải kiểu dữ liệu nguyên thủy) sẽ không được copy đúng.
Trong ví dụ trên, object Date sẽ được chuyển đổi sang string, chúng ta có thể xem thêm về `JSON.stringify` để hiểu rõ hơn.

</p>
</details>

---

###### 19. Output là gì?

```javascript
var x = 5;

(function() {
    console.log(x);
    var x = 10;
    console.log(x);
})();
```

- A: 5 10
- B: undefined 10
- C: 5 undefined
- D: undefined undefined

<details><summary><b>Đáp án</b></summary>
<p>

#### Đáp án: B

Biến `x` sẽ được `hoist` bên trong function, chúng ta có thể xem function được thực thi như sau:

```javascript
var x = 5;

(function() {
  var x;
  console.log(x);
  x = 10;
  console.log(x);
})();
```

</p>
</details>

---

###### 20. Output là gì?

```javascript
console.log(typeof Object, typeof Array, typeof Number);
```

- A: object array number
- B: object object number
- C: object object object
- D: function function function

<details><summary><b>Đáp án</b></summary>
<p>

#### Đáp án: D

Object, Array và Number đều là các Function Constructor, chúng dùng để tạo ra các object với từ khóa `new`.

</p>
</details>

---

###### 21. Output là gì?

```javascript
const output = `Soon we must all choose between what is ${
    [] ? 'right' : 'wrong'
} and what is ${(() => false)() ? 'difficult' : 'easy'}`;

console.log(output);
```

- A: Soon we must all choose between what is right and what is easy
- B: Soon we must all choose between what is right and what is difficult
- C: Soon we must all choose between what is wrong and what is easy
- D: Soon we must all choose between what is wrong and what is difficult

<details><summary><b>Đáp án</b></summary>
<p>

#### Đáp án: A

Trong JavaScript, mảng rỗng `[]` và function là `truthy`. Nhưng chú ý ở ví dụ trên, function này được thực thi và nó trả về `false`.

</p>
</details>

---

###### 22. Output là gì?

```javascript
(function() {
    console.log(1);
    setTimeout(function() {
        console.log(2);
    }, 1000);
    setTimeout(function() {
        console.log(3);
    }, 0);
    console.log(4);
})();
```

- A: 1, 2, 3, 4
- B: 4, 2, 1, 3
- C: 1, 4, 3, 2
- D: 4, 3, 2, 1

<details><summary><b>Đáp án</b></summary>
<p>

#### Đáp án: C

Rõ ràng `1` và `4` sẽ được in ra đầu tiên vì `console.log()` mà không có delay.
`2` sẽ được in ra sau `3` vì `2` bị delay 1 giây còn `3` bị delay sau 0 giây.
Có một điểm chú ý là vì sao `3` bị delay là 0 giây, nhưng lại được in ra sau `4`?
Vì `callback` trong `setTimeout` sẽ được đẩy vào `event queue` và nó chỉ được gọi sau khi `call stack` rỗng.
Nếu bạn chưa rõ các khái niệm này, đọc thêm về `JS concurrency model/event loop`.

</p>
</details>

---

###### 23. Output là gì?

```javascript
const foo = () => {
    return {
        foo: 'foo'
    }
}

const bar = () => {
    return
    {
        bar: 'bar'
    }
}

console.log(foo(), bar());
```

- A: { foo: "foo" } undefined
- B: undefined { bar: "bar" }
- C: undefined undefined

<details><summary><b>Đáp án</b></summary>
<p>

#### Đáp án: A

Mặc dù trông có vẻ hai function trong ví dụ trên hoàn toàn giống nhau. Nhưng JavaScript có một số quy tắc để tự động thêm vào dấu `;` (semicolon) sau một số câu lệnh, mà cụ thể ở đây là câu lệnh `return`.

Ở function `foo`, câu lệnh `return` và dấu `{` mở đầu một code block nằm trên cùng một dòng, vì vậy JavaScript chỉ thêm các dấu `;` vào sau các dấu `}` đóng code block:

```javascript
const foo = () => {
  return {
    foo: 'foo'
  };
};
```

Tuy nhiên, với function `bar` lại là một câu chuyện khác, câu lệnh `return` nằm riêng lẻ trên một dòng, vậy nên JavaScript sẽ tự động thêm dấu `;` vào sau câu lệnh `return` này:

```javascript
const bar = () => {
  return;
  {
    bar: 'bar';
  }
};
```

Nó làm cho function `bar` giờ có thể viết như thế này:

```javascript
const bar = () => {
  return;
};
```

</p>
</details>

---

###### 24. Output là gì?

```javascript
const a = { something: 1, someOtherThing: 2 };

const deleteSomething = input => {
    delete input.something;
    return input.something;
};

const result = deleteSomething(a);

console.log(result);
```

- A: 1
- B: An error is thrown
- C: undefined
- D: Something different is logged

<details><summary><b>Đáp án</b></summary>
<p>

#### Đáp án: C

Khi chúng ta truyền tham số vào một function là một kiểu dữ liệu tham chiếu (`reference types`) thì những thay đổi đối với tham số bên trong hàm sẽ thay đổi đến chính object chúng ta truyền vào.
Vì vậy khi xóa một thuộc tính của tham số `input` cũng chính là xóa luôn thuộc tính của object `a`.

</p>
</details>

---

###### 25. Output là gì?

```javascript
let b = '4';

console.log(b++ + 3, b);
```

- A: 44 4
- B: 8 5
- C: 7 5
- D: 43 5

<details><summary><b>Đáp án</b></summary>
<p>

#### Đáp án: D

Toán tử `++` (Postfix Increment) được ưu tiên hơn toán tử `+`, đầu tiên toán tử Postfix Increment sẽ chuyển đổi `b` từ string `'4'` sang number `4`, sau đó nó sẽ chờ phép toán `4 + 3` thực hiện xong mới thực hiện tăng `b` lên một đơn vị.

</p>
</details>

---

###### 26. Output là gì?

```javascript
const scrambled = {
    2: 'e',
    5: 'o',
    1: 'h',
    4: 'l',
    3: 'l'
};

const result = Object.values(scrambled).reduce(
    (agg, el) => agg + el,
    ''
);

console.log(result);
```

- A: hello
- B: eohll

<details><summary><b>Đáp án</b></summary>
<p>

#### Đáp án: A

Nếu key trong object là number thì `Object.values` sẽ sắp xếp lại các value theo thứ tự, với key không phải number thì thứ tự vẫn được giữ nguyên.

</p>
</details>

---

###### 27. Output là gì?

```javascript
const user = {
    name: 'lao Hac',
    age: 69,
    pet: {
        type: 'cho',
        name: 'vang'
    }
};

Object.freeze(user);

user.pet.name = 'shiba';

console.log(user.pet.name);
```

- A: shiba
- B: vang
- C: An error is thrown

<details><summary><b>Đáp án</b></summary>
<p>

#### Đáp án: A

Để tránh bất kỳ sự thay đổi nào trên các thuộc tính của một object, ta có thể dùng hàm `Object.freeze`, tuy nhiên hàm này chỉ có thể thực hiện `shallow freeze` trên object đó mà thôi, điều đó có nghĩa bất kỳ sự thay đổi nào trên các thuộc tính của object con đều được cho phép.
Trong ví dụ này, chúng ta không thể thay đổi `user.age`, nhưng không có vấn đề gì khi thay đổi `user.pet.name`.
Nếu chúng ta không muốn thay đổi bất kỳ thuộc tính nào của object, có thể dùng đệ quy `Object.freeze` cho các thuộc tính con hoặc dùng các chức năng `deep freeze` của các thư viện có sẵn.

</p>
</details>

---

###### 28. Output là gì?

```javascript
const n = 5;

console.log(1..n); // ?
```

- A: [1, 2, 3, 4, 5]
- B: undefined
- C: Syntax error

<details><summary><b>Đáp án</b></summary>
<p>

#### Đáp án: B

Khi muốn truy cập đến một thuộc tính hay method của một object ta có thể dùng dot notation (một dấu `.`), còn đối với number, ta có thể dùng hai dấu `.`, vì khi dùng một dấu `.` thì JavaScript sẽ bị nhầm lẫn với decimal number.
Trong trường hợp này, `1..n` sẽ truy cập đến thuộc tính `n` của number `1`, nó trả về `undefined`. Một ví dụ cụ thể là khi gọi `1..toString()` sẽ cho kết quả là `"1"`.

</p>
</details>

---

###### 29. Output là gì?

```javascript
const compare = a => a === a;

console.log(compare(null));
console.log(compare(undefined));
console.log(compare(NaN));
console.log(compare([NaN]));
```

- A: true true true true
- B: true false true true
- C: true true false true
- D: true true false false
- E: false false false false

<details><summary><b>Đáp án</b></summary>
<p>

#### Đáp án: C

Trong JavaScript, khi sử dụng Triple Equals (`===`) thì `null` và `undefined` chỉ cho kết quả `true` khi so sánh với chính nó, `NaN` thì luôn cho kết quả `false` khi so sánh với bất kỳ object nào, kể cả chính nó, còn `[NaN]` là một array bình thường chỉ chứa một phần tử là `NaN`.

</p>
</details>

---

###### 30. Output là gì?

```javascript
const notifications = 1;

console.log(
    `You have ${notifications} notification${notifications !==
    1 && 's'}`
);
```

- A: You have 1 notification
- B: You have 1 notifications
- C: You have 1 notificationfalse

<details><summary><b>Đáp án</b></summary>
<p>

#### Đáp án: C

Toán tử `&&` sẽ dừng và trả về kết quả `false` nếu gặp bất kỳ điều kiện nào sai, vì thế `notifications !== 1 && 's'` sẽ trả về `false`.
Nếu bạn muốn ví dụ trên chạy đúng như ý muốn, ta có thể dùng ternary operator: `notifications !== 1 ? 's' : ''`.

</p>
</details>

---

###### 31. Output là gì?

```javascript
const a = 0.1;
const b = 0.2;
const c = 0.3;

console.log(a + b === c);
```

- A: true
- B: false

<details><summary><b>Đáp án</b></summary>
<p>

#### Đáp án: B

Như chúng ta đã biết trong hệ thập phân, chúng ta không thể biểu diễn chính xác `1/3` dưới dạng dấu phẩy động (`floating-point`). Kết quả của `0.333 + 0.333 + 0.333` không thể nào bằng `1` được.

Tương tự, trong máy tính các số được biểu diễn dưới dạng nhị phân.
Đôi khi chúng chỉ biểu diễn được gần đúng số thực tế chứ không thể biểu diễn một các chính xác được, ví dụ như `0.1`, `0.2` hay `0.3`. Điều này dẫn đến các kết quả không mong muốn, trong trường hợp `0.1 + 0.2`, kết quả ta nhận được là `0.30000000000000004`.

</p>
</details>

---

###### 32. Output là gì?

```javascript
bar();

var bar;

function bar() {
    console.log('first');
}

bar = function() {
    console.log('second');
};

bar();

foo();

function foo() {
    console.log(1);
}

var foo = function() {
    console.log(2);
};

function foo() {
    console.log(3);
}

foo();
```

- A: second first 1 3
- B: first second 3 2
- C: second first 3 3
- D: first second 3 3

<details><summary><b>Đáp án</b></summary>
<p>

#### Đáp án: B

Cơ chế `hoisting` trong JavaScript được áp đụng khi khai báo biến (`variable declaration`) và khai báo function (`function declaration`), trừ khi gán một function cho biến (`function expression`).

Function declaration sẽ có độ ưu tiên hơn variable declaration khi `hoisting`, vì thế function `bar` sau khi `hoisted` sẽ giống thế này:

```javascript
function bar() {
  console.log('first');
}

bar(); // 'first'

bar = function() {
  console.log('second');
};

bar(); // 'second'
```

Trong trường hợp chúng ta có các khai báo trùng lặp (`duplication declaration`) hoặc gặp một phép gán (`assignment`) thì giá trị sẽ của biến hay function sẽ được thay thế, Vì vậy function `foo` sẽ giống thế này:

```javascript
function foo() {
  console.log(1);
}

function foo() {
  console.log(3);
}

foo(); // 3

foo = function() {
  console.log(2);
};

foo(); // 2
```

</p>
</details>

---

###### 33. Output là gì?

```javascript
console.log(fetch);
```

- A: The fetch function
- B: A reference error
- C: It depends

<details><summary><b>Đáp án</b></summary>
<p>

#### Đáp án: C

Tùy vào environment bạn chạy đoạn code trên mà kết quả sẽ khác nhau. Nếu chạy trên trình duyệt đã hổ trợ fetch thì kết quả là `the fetch function`, còn nếu chạy trên các trình duyệt cũ như `IE` hoặc trên môi trường `node`, chúng ta sẽ thấy lỗi `ReferenceError`.

</p>
</details>

---

###### 34. Output là gì?

```javascript
let a = new Date('2019,1,1').toLocaleDateString();
let b = new Date(2019, 1, 1).toLocaleDateString();
console.log(a, b);
```

- A: 1/1/2019 2/1/2019
- B: 1/1/2019 1/1/2019

<details><summary><b>Đáp án</b></summary>
<p>

#### Đáp án: A

Date Constructor `new Date()` trong JavaScript được dùng để tạo một date object, dựa vào tham số đầu vào mà sẽ cho các kết quả khác nhau.
Nếu tham số là một string, JavaScript sẽ tự động parse chuỗi string thành ngày tương ứng, trong trường hợp này `"2019,1,1"` được parse thành ngày `1/1/2019`, nếu tham số là ba numbers thì ố thứ nhất là năm, số thứ hai là tháng, số thứ ba là ngày, tuy nhiên cần chú ý, tháng ở đây được bắt đầu từ `0`, vậy truyền vào `1` có nghĩa là tháng `2`.

</p>
</details>

---

###### 35. Output là gì?

```javascript
function withVar() {
    const b = () => a;
    var a = 24;
    return b;
}

function withLet() {
    const b = () => a;
    let a = 24;
    return b;
}

function changingValue() {
    let a = 24;
    const b = () => a;
    a = 42;
    return b;
}

console.log(withVar()()); // ??
console.log(withLet()()); // ??
console.log(changingValue()()); // ??
```

- A: undefined Error 42
- B: 24 Error 24
- C: 24 24 42
- D: undefined Error 24
- E: 24 Error 42

<details><summary><b>Đáp án</b></summary>
<p>

#### Đáp án: C

`Closure` là khi một inner function có thể ghi nhớ và truy cập đến các thành phần ở scope của outer function, thậm chí outer function đã thực thi xong.
Ở trong ba ví dụ trên, thì function `b` vẫn ghi nhớ và truy cập đến biến `a` ở bên ngoài scope của nó, mặc dù các outer function đã được thực thi xong.

</p>
</details>

---

###### 36. Output là gì?

```javascript
let dog = {
    breed: 'Border Collie',
    sound: 'Wooh',
    getBreed: () => {
        return this.breed;
    },
    getSound: function() {
        return this.sound;
    }
};
console.log(dog.getBreed(), dog.getSound());
```

- A: Border Collie, Wooh
- B: Border Collie, undefined
- C: undefined, Wooh
- D: undefined, undefined

<details><summary><b>Đáp án</b></summary>
<p>

#### Đáp án: C

`this` trong một `Arrow functions` không được `bind` như trong một function bình thường mà `this` được thừa hưởng từ scope bên ngoài của nó (`lexical scoping`).
Đó là lý do tại sao `this` trong function `getBreed` không phải là object `dog` mà là global object, ở trình duyệt là window object, nên `this.breed` trả về `undefined`.

</p>
</details>

---

###### 37. Output là gì?

```javascript
const arr = [
    x => x * 1,
    x => x * 2,
    x => x * 3,
    x => x * 4
];

console.log(arr.reduce((agg, el) => agg + el(agg), 1));
```

- A: 1
- B: 60
- C: 100
- D: 120

<details><summary><b>Đáp án</b></summary>
<p>

#### Đáp án: D

Hàm `reduce` của array cho phép chúng ta truyền vào một giá trị ban đầu ở tham số thứ hai, trong trường hợp này là `1` và ta có các bước tính toán sau:

1 + 1 * 1 = 2
2 + 2 * 2 = 6
6 + 6 * 3 = 24
24 + 24 * 4 = 120

</p>
</details>

---

###### 38. Output là gì?

```javascript
function sayHi() {
    console.log(name);
    console.log(age);
    var name = 'name';
    let age = 1;
}

sayHi();
```

- A: name undefined
- B: name ReferenceError
- C: ReferenceError 1
- D: undefined ReferenceError

<details><summary><b>Đáp án</b></summary>
<p>

#### Đáp án: D

Trong JavaScript, khi một function được thực thi, sẽ trải qua hai giai đoạn.
Giai đoạn đầu tiên là `creation phase`, ở giai đoạn này, các biến khai báo trong function được cấp phát bộ nhớ và gán các giá trị mặc định, giai đoạn thứ hai là `execute phase`, giai đoạn này sẽ chạy từng dòng code trong function đó.

Sự khác biệt khi chúng ta khai báo biến giữa `var` và `let` là với biến được khai báo với `var` chúng sẽ được cấp phát bộ nhớ và gán giá trị mặc định là `undefined` ngay ở giai đoạn `creation phase`, vì thế, khi JavaScript chạy dòng `console.log(name)` sẽ in ra giá trị `undefined`.

Cơ chế này gọi là `hoisting` trong JavaScript.
Còn đối với biến được khai báo với `let`, chúng cũng được `hoisting` nhưng có hơi khác một chút với `var`.
Đó chính là trong giai đoạn `creation phase`, biến `let` cũng được cấp phát bộ nhớ nhưng không được gán giá trị mặc định, chúng ta không thể truy cập đến biến này trước khi chúng được gán một giá trị nào đó (`temporal dead zone`).
Vì vậy, khi `console.log(age)` trước khi `age` được gán giá trị, sẽ văng ra lỗi `ReferenceError`.

</p>
</details>

---

###### 39. Output là gì?

```javascript
const shape = {
    radius: 10,
    diameter() {
        return this.radius * 2;
    },
    perimeter: () => 2 * Math.PI * this.radius
};

console.log(shape.diameter());
console.log(shape.perimeter());
```

- A: 20 62.83185307179586
- B: 20 NaN
- C: 20 63
- D: NaN 63

<details><summary><b>Đáp án</b></summary>
<p>

#### Đáp án: B

Trong ví dụ trên, `diameter` là một function shorthand bình thường, còn `perimeter` là arrow function.

Khi tìm hiểu về this context trong JavaScript, với arrow function thì `this` được `auto binding` và `this` chính là scope bên ngoài chính function đó.
Điều đó có nghĩa là khi chúng ta gọi function `perimeter`, `this` bây giờ không phải là object `shape` mà là object global `window` (trong trình duyệt), window không có biến `radius` nên `this.radius` trả về `undefined`.

</p>
</details>

---

###### 40. Output là gì?

```javascript
function Person(firstName, lastName) {
    this.firstName = firstName;
    this.lastName = lastName;
}

const member = new Person('firstname', 'lastname');
Person.getFullName = function() {
    return `${this.firstName} ${this.lastName}`;
};

console.log(member.getFullName());
```

- A: TypeError
- B: SyntaxError
- C: firstname lastname
- D: undefined undefined

<details><summary><b>Đáp án</b></summary>
<p>

#### Đáp án: A

Khi tìm hiểu về prototype trong JavaScript, muốn thêm một function vào prototype và share cho tất cả các object dùng chung thì làm như sau:

```javascript
Person.prototype.getFullName = function() {
  return `${this.firstName} ${this.lastName}`;
};
```

</p>
</details>

---

###### 41. Output là gì?

```javascript
const a = {};
const b = { key: 'b' };
const c = { key: 'c' };

a[b] = 123;
a[c] = 456;

console.log(a[b]);
```

- A: 123
- B: 456
- C: undefined
- D: ReferenceError

<details><summary><b>Đáp án</b></summary>
<p>

#### Đáp án: B

Tất cả các keys của một object đểu được tự động chuyển thành string (trừ `Symbol`).

Khi một object chuyển sang string, nó có giá trị `"[object Object]"`, vậy `a[b] = 123` có thể viết thành `a["object Object"] = 123`, tương tự với `a[c] = 456` sẽ là `a["object Object"] = 456`.

</p>
</details>

---

###### 42. Output là gì?

```javascript
const obj = { a: 'one', b: 'two', a: 'three' };
console.log(obj);
```

- A: { a: "one", b: "two" }
- B: { b: "two", a: "three" }
- C: { a: "three", b: "two" }
- D: SyntaxError

<details><summary><b>Đáp án</b></summary>
<p>

#### Đáp án: C

Nếu bạn có một object với nhiều keys có cùng tên, thì chúng sẽ được đè lên nhau, giá trị chính là giá trị sau cùng nhưng thứ tự lại là thứ tự đầu tiên của key.

</p>
</details>

---

###### 43. Output là gì?

```javascript
const obj = { 1: 'a', 2: 'b', 3: 'c' };
const set = new Set([1, 2, 3, 4, 5]);

obj.hasOwnProperty('1');
obj.hasOwnProperty(1);
set.has('1');
set.has(1);
```

- A: false true false true
- B: false true true true
- C: true true false true
- D: true true true true

<details><summary><b>Đáp án</b></summary>
<p>

#### Đáp án: C

Tất cả các keys của một object đểu được tự động chuyển thành string (trừ `Symbol`). Vì thế `obj.hasOwnProperty('1')` cho kết quả `true`.

Nhưng điều đó không đúng với `Set`, set phân biệt giữa string và number nên `set.has('1')` sẽ trả về `false` còn `set.has(1)` trả về `true`.

</p>
</details>

---

###### 44. Output là gì?

```javascript
function sayHi() {
    return (() => 0)();
}

console.log(typeof sayHi());
```

- A: object
- B: number
- C: function
- D: undefined

<details><summary><b>Đáp án</b></summary>
<p>

#### Đáp án: B

`immediately invoked function (IIFE)` là hàm được gọi ngay lập tức lúc khai báo, có cú pháp như trong ví dụ trên `(() => 0)()`.
Ở đây hàm `sayHi` trả về một `IIFE` và nó được gọi ngay lập tức khi hàm `sayHi` được gọi, vì thế `sayHi()` sẽ trả về số `0` với type là `number`.

</p>
</details>

---

###### 45. Output là gì?

```javascript
function Person(firstName, lastName) {
    this.firstName = firstName;
    this.lastName = lastName;
}

const ti = new Person('cu', 'ti');
const teo = Person('cu', 'teo');

console.log(ti);
console.log(teo);
```

- A: Person { firstName: "cu", lastName: "ti" } undefined
- B: Person { firstName: "cu", lastName: "ti" } Person { firstName: "cu", lastName: "teo" }
- C: Person { firstName: "cu", lastName: "ti" } {}
- D: Person { firstName: "cu", lastName: "ti" } ReferenceError

<details><summary><b>Đáp án</b></summary>
<p>

#### Đáp án: A

Khi gọi một Function Constructor, `this` sẽ được tạo và trả về một cách ngầm định nếu chúng ta gọi bằng từ khóa `new`, nếu không `this` sẽ không được tạo và sẽ là global window object (trong trình duyệt).

</p>
</details>

---

###### 46. Output là gì?

```javascript
const person = { name: 'fullName' };

function sayHi(age) {
    return `${this.name} is ${age}`;
}

console.log(sayHi.call(person, 1));
console.log(sayHi.bind(person, 1));
```

- A: undefined is 1 fullName is 1
- B: function function
- C: fullName is 1 fullName is 1
- D: fullName is 1 function

<details><summary><b>Đáp án</b></summary>
<p>

#### Đáp án: D

Chúng ta đã biết cả hai hàm `call` và `bind` đều được dùng để thay đổi this context của hàm.

Tuy nhiên, với `call` thì hàm sẽ được gọi ngay lập tức, còn `bind` thì nó sẽ trả về một hàm mới với context mình truyền vào chứ không gọi ngay lúc đó.

</p>
</details>

---

###### 47. Output là gì?

```javascript
const map = ['a', 'b', 'c'].map.bind([1, 2, 3]);
map(el => console.log(el));
```

- A: 1 2 3
- B: a b c
- C: An error is thrown
- D: Something else

<details><summary><b>Đáp án</b></summary>
<p>

#### Đáp án: A

Hàm `bind` (tương tự cho `apply` và `call`) trong JavaScript cho phép chúng ta thay đổi ngữ cảnh của biến `this` (this context).
Trong trường hợp này, hàm `map` sau khi được `bind` sẽ có biến `this` là `[1, 2, 3]` chứ không phải là `['a', 'b', 'c']`.

</p>
</details>

---

###### 48. Output là gì?

```javascript
const arr1 = ['a', 'b', 'c'];
const arr2 = ['b', 'c', 'a'];

console.log(
    arr1.sort() === arr1,
    arr2.sort() == arr2,
    arr1.sort() === arr2.sort()
);
```

- A: true true true
- B: true true false
- C: false false false
- D: true false true

<details><summary><b>Đáp án</b></summary>
<p>

#### Đáp án: B

Hàm `sort` sẽ sắp xếp lại array và đồng thời trả về chính tham chiếu đến array đó.
Vì vậy `arr1.sort()` và `arr1` tham chiếu đến cùng một object trong bộ nhớ, điều này cũng đúng cho `arr2.sort()` và `arr2`.

Với `arr1.sort()` và `arr2.sort()` thì rõ ràng chúng tham chiếu đến hai object khác nhau trong bộ nhớ.

</p>
</details>

---

###### 49. Function dưới đây luôn luôn trả về phần tử lớn nhất trong array đúng không?

```javascript
function greatestNumberInArray(arr) {
    let greatest = 0;
    for (let i = 0; i < arr.length; i++) {
        if (greatest < arr[i]) {
            greatest = arr[i];
        }
    }
    return greatest;
}
```

- A: Đúng
- B: Không

<details><summary><b>Đáp án</b></summary>
<p>

#### Đáp án: B

Coi chừng bị lừa nhé, function trên chỉ đúng trong trường hợp các phần tử của mảng lớn hơn `0` mà thôi, còn nhỏ hơn `0` thì chắc là sai rồi, vì biến `greatest` được gán mặc định bằng `0` mà.

</p>
</details>

---

###### 50. Output là gì?

```javascript
let i = 0;

const arr = new Array(5);
arr.forEach(() => i++);

console.log(i);
```

- A: 5
- B: 4
- C: 1
- D: 0

<details><summary><b>Đáp án</b></summary>
<p>

#### Đáp án: D

Bạn nghĩ là `5` à, không, bạn nên xem lại cách hoạt động của Array constructor, khi truyền vào một tham số là number từ 0 đến (2^32 - 1), nó sẽ tạo ra một array chỉ có thuộc tính `length` là number vừa truyền vào chứ nó không chứa các phần tử nào (empty slots), array này còn được gọi là `sparse array`.
Vì array không chứa phần tử nào nên hàm `forEach` sẽ không được duyệt qua bất kỳ lần nào, vậy kết quả là `0`.

</p>
</details>

---

###### 51. Output là gì?

```javascript
const mySet = new Set([{ a: 1 }, { a: 1 }]);
const result = [...mySet];
console.log(result);
```

- A: [{a: 1}, {a: 1}]
- B: [{a: 1}]

<details><summary><b>Đáp án</b></summary>
<p>

#### Đáp án: A

`Set` được dùng để lưu trữ dữ liệu mà các phần tử trong `Set` là duy nhất (unique).
Tuy nhiên, nên chú ý với các trường hợp dữ liệu là kiểu dữ liệu tham chiếu, ở đây hai object `{ a: 1 } và { a: 1 }` có cùng thuộc tính và giá trị nhưng chúng là hai object hoàn toàn khác nhau và được lưu trong hai ô nhớ khác nhau.
Đó cũng là lý do mà `{ a: 1 } === { a: 1 }` cho kết quả `false`.

Trong trường hợp `Set` được tạo như sau: `obj = { a: 1 }, new Set([ obj, obj ])`, khi đó `Set` chỉ chứa một phần tử, vì hai object lúc này cùng tham chiếu đến một ô nhớ mà thôi.

</p>
</details>

---

###### 52. Output là gì?

```javascript
const url = 'quiz.dangcao410.com';
const { length: ln, [ln - 1]: domain = 'quiz' } = url
    .split('.')
    .filter(Boolean);
console.log(domain);
```

- A: "quiz"
- B: "dangcao410"
- C: "com"
- D: undefined
- E: An error is thrown

<details><summary><b>Đáp án</b></summary>
<p>

#### Đáp án: C

Đấu tiên gán quiz.dangcao410.com cho biến url.

```javascript
const url = 'quiz.dangcao410.com';
```

Với toán tử `=` (assignment) thì chúng ta quan tâm toán hạng bên phải trước (right side assignment):

```javascript
url.split('.').filter(Boolean);
```

`url.split('.')` sẽ cắt chuỗi `url` thành một array bởi dấu `.`: `['quiz', 'duthaho', 'com']`, sau đó array này sẽ gọi `filter(Boolean)`, đây là cách viết gọn từ: `filter(el => Boolean(el))`, bởi vì các phần tử trong array đều là string, chúng là `truthy` nên `Boolean(el)` luôn cho kết quả `true`, điều đó cũng có nghĩa sau khi `filter`, các phần tử trong array đều được giữ lại.

Đến đây thì ta có thể viết lại như sau:

```javascript
const { length: ln, [ln - 1]: domain = 'quiz' } = [
  'quiz',
  'dangcao410',
  'com'
];
```

Đây rõ ràng là cú pháp của `Object Destructing` trong `ES2015` vì array cũng là một object, chúng ta có thể truy cập các thuộc tính index và length từ array (`arr["0"], arr["length"]`).

Trong trường hợp này, chúng ta dùng aliasing để gán thuộc tính `length` cho một biến mới là `ln`.
Tiếp theo ta lại gán thuộc tính index thứ `ln - 1` cho biến có tên là `domain` với giá trị mặc định là `'quiz'`, có nghĩa là `domain` sẽ có giá trị là `'quiz'` nếu array không có thuộc tính index thứ `ln - 1` nào.

Ở đây, `length` được gán cho `ln`, có giá trị là `3`, suy ra `ln - 1` là `2`, và phần tử ở vị trí số `2` trong array là `com`. Vì vậy, câu trả lời là `com`.

</p>
</details>

---

###### 53. Output là gì?

```javascript
function ArrayBoolean() {
    if ([] == true && [1] == true) return [true, true];
    else if ([] == true && [1] == false) return [true, false];
    else if ([] == false && [1] == true) return [false, true];
    else return [false, false];
}
ArrayBoolean();
```

- A: [true, true]
- B: [true, false]
- C: [false, true]
- D: [false, false]

<details><summary><b>Đáp án</b></summary>
<p>

#### Đáp án: C

Trong JavaScript, các array (rỗng hoặc có phần tử) đều là `truthy`, tức là khi chúng ta kiểm tra với điều kiện `if ([]) { return true; }` sẽ cho kết quả là `true`.
Nhưng xin hãy chú ý khi chúng ta so sánh Double Equals (`==`) giữa array với boolean, JavaScript sẽ chuyển đổi dữ liệu trước khi so sánh (`Type Conversion`), khi đó `arr.toString()` sẽ được gọi `[].toString() = ""`, vì thế `[] == false` cho kết quả `true`.

</p>
</details>

---

###### 54. Output là gì?

```javascript
var a = [1, 2, 3];
var b = [1, 2, 3];
var c = '1,2,3';

console.log(a == c);
console.log(b == c);
console.log(a == b);
```

- A: true, true, false
- B: true, true, true
- C: true, false, false
- D: false, false false

<details><summary><b>Đáp án</b></summary>
<p>

#### Đáp án: A

Khi so sánh Double Equals (`==`) giữa array và string, cụ thể là `a` hoặc `b` với `c`, JavaScript sẽ tự động gọi `arr.toString()` để chuyển đổi array sang string trước khi so sánh, hai mảng `a` và `b` convert sang string sẽ là `'1,2,3'`, vì thế `a == c` và `b == c` cho kết quả `true`.

Khi so sánh Double Equals (`==`) hay Triple Equals (`===`) giữa các đối tượng là kiểu dữ liệu tham chiếu (`Reference Type`), như object, array, function, chúng ta không quan tâm đến giá trị mà đối tượng đang chứa, mà chỉ quan tâm đến chúng có cùng trỏ đến một địa chỉ ô nhớ hay không mà thôi.
Trong trường hợp này, `a` và `b` là hai array trỏ đến hai ô nhớ khác nhau, vì thế `a == b` cho kết quả `false`.

</p>
</details>

---

###### 55. Output là gì?

```javascript
var a = [9];
var b = [10];

console.log(a == 9);
console.log(b == 10);
console.log(a < b);
```

- A: true true true
- B: false false false
- C: true true false
- D: false false true

<details><summary><b>Đáp án</b></summary>
<p>

#### Đáp án: C

Khi so sánh Double Equals (`==`) giữa array và number, JavaScript sẽ chuyển đổi array sang number trước khi so sánh (`[9] -> 9` và `[10] -> 10`), vì thế `[9] == 9` và `[10] == 10` cho kết quả `true`.

Nhưng khi so sánh hai array với toán tử `<` hoặc `>`, lúc này array sẽ không được chuyển đổi sang number mà là sang string (`[9] -> "9"` và `[10] -> "10"`).
Khi so sánh hai string thì sẽ so sánh theo alphabet với từng ký tự một, vì thế `"9" < "10"` cho kết quả là `false` vì `"9" < "1"` là sai.

</p>
</details>

---

###### 56. Output là gì?

```javascript
const ar = [5, 1, 3, 7, 25];
const ar1 = ar;
console.log(ar1.sort());
([5, 25].indexOf(ar[1]) != -1 &&
    console.log(ar.reverse())) ||
(ar[3] == 25 && console.log(ar));
console.log(ar1);
```

- A: [1, 3, 5, 7, 25] [7, 5, 3, 25, 1] [1, 25, 3, 5, 7] [1, 25, 3, 5, 7]
- B: [1, 25, 3, 5, 7] [5,1,3,7,25]
- C: [1, 25, 3, 5, 7] [7, 5, 3, 25, 1] [7, 5, 3, 25, 1] [7, 5, 3, 25, 1]
- D: An error is thrown

<details><summary><b>Đáp án</b></summary>
<p>

#### Đáp án: C

`const ar1 = ar` có nghĩa `ar1` và `ar` cùng tham chiếu đến một array trong bộ nhớ.
`ar1.sort()` sẽ sắp xếp chính nó và `ar1` cũng sẽ thay đổi theo.

Bạn nên nhớ hàm sort của array sẽ chuyển đổi các phần tử sang string trước khi sắp xếp chúng theo alphabet, vậy dòng `console.log` đầu tiên là `[1, 25, 3, 5, 7]`.

Tiếp theo `[5, 25].indexOf(ar[1]) != -1` trả về `true` nên (`ar.reverse()`) sẽ được gọi. `ar.reverse()` sẽ sắp xếp arr theo chiều ngược lại, `ar` bây giờ sẽ là `[7, 5, 3, 25, 1]`, và được in ra ở `console.log` thứ hai.

`console.log` không trả về giá trị nào nên ta có thể viết lại như sau:

```javascript
undefined || (ar[3] == 25 && console.log(ar));
```

`undefined` là falsy, nên `ar[3] == 25` được gọi và kết quả là `true` vì phần tử thứ `3` của `ar` giờ là `25`, tiếp theo thì `console.log(ar)` thứ ba được in ra với kết quả là `[7, 5, 3, 25, 1]`.

Cuối cùng vì `ar1` và `ar` cùng tham chiếu đến một array nên dòng `console.log(ar1)` thứ tư cũng sẽ in ra (`[7, 5, 3, 25, 1]`).

</p>
</details>

---

###### 57. Cả hai cách `a` và `b` đều tạo ra object cùng thuộc tính và giá trị. Theo bạn thì phương án nào tốt hơn?

```javascript
const arr = [1, 2, 3];

const a = arr.reduce(
    (acc, el, i) => ({ ...acc, [el]: i }),
    {}
);

const b = {};
for (let i = 0; i < arr.length; i++) {
    b[arr[i]] = i;
}
```

- A: `a`
- B: `b`

<details><summary><b>Đáp án</b></summary>
<p>

#### Đáp án: B

Nhiều bạn nghĩ rằng đây là thời đại của ES2015 rồi, dùng `reduce` sẽ gọn và tối ưu hơn.
Nhưng hãy nhìn kỹ vào code, với phương án `b`, qua mỗi vòng lặp ta chỉ việc set một thuộc tính mới vào `b`, còn ở phương án `a`, với mỗi lần lặp, spread operator (`...`) sẽ tạo ra thêm một shallow copy của `acc` và sau đó mới set một thuộc tính mới, điều này rõ ràng làm tốn bộ nhớ và không tối ưu.

</p>
</details>
