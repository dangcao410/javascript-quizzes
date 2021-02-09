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
