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
