###### 1. Output là gì?

```javascript
function a() {
    console.log(this);
}
a.call(null);
```

- A: null
- B: undefined
- C: window object

<details><summary><b>Answer</b></summary>
<p>

#### Answer: C

`this context` trong JavaScript tùy theo ngữ cảnh lúc gọi hàm.

Chúng ta có thể thay đổi `this context` của hàm bằng cách dùng hàm `call`, với tham số đầu tiên trở thành `this` và các tham số tiếp theo là các params của hàm.
Vì vậy, khi gọi `a.call(window)` thì `this` trong hàm `a` chính là `window`.

Lưu ý, khi chúng ta truyền tham số đầu tiên vào hàm `call` là `null` hay `undefined` thì JavaScript sẽ tự động truyền `global object` vào hàm được gọi chứ không truyền `null` hay `undefined`.
Vì vậy, đoạn code trên sẽ in ra `object window` thay vì `null`.

</p>
</details>

---

###### 2. What's the output?

```javascript
function Name(a, b) {
  this.a = a;
  this.b = b;
}

const me = Name("Vuong", "Nguyen");

console.log(!(a.length - window.a.length));
```

- A: `undefined`
- B: `NaN`
- C: `true`
- D: `false`

<details><summary><b>Answer</b></summary>
<p>

#### Answer: C

We get true in the console. The tricky part is when we create an object from the constructor function Name but we DO NOT USE `new` keywork. That makes the variable `a` global one and get the value "Vuong". Remember that it is actually a property of the global object `window` (in the browser) or `global` in the nodejs.

We then get `a.length` ~ 5 and `window.a.length` ~ 5 which return 0. !0 returns true.

Imagine what would happen when we create the instance `me` with the `new` keywork. That is an interesting inquire!

</p>
</details>

---

###### 3. What's the output?

```javascript
const x = function (...x) {
  let k = (typeof x).length;
  let y = () => "freetut".length;
  let z = { y: y };

  return k - z.y();
};

console.log(Boolean(x()));
```

- A: `true`
- B: 1
- C: -1
- D: `false`

<details><summary><b>Answer</b></summary>
<p>

#### Answer: A

The spread operator `...x` might help us obtain the parameter in the function in the form of array. Yet, in Javascript the typeof array return "object" rather than "array". It is totally odd if you are coming from PHP.

That is said, we now have the length of the string `object` which returns 6. z.y() simply returns the length of the string 'freetut' (7).

Be aware that the function x() (in the form of `function express` or `anonymous function` (if you are coming from PHP) return -1 when being called and when converted to bool with `Boolean(-1)` return true instead of false. Noted that `Boolean(0)` return false.

</p>
</details>

---

###### 4. What's the output?

```javascript
(function js(x) {
  const y = (j) => j * x;

  console.log(y(s()));

  function s() {
    return j();
  }

  function j() {
    return x ** x;
  }
})(3);
```

- A: `undefined`
- B: 18
- C: 81
- D: 12

<details><summary><b>Answer</b></summary>
<p>

#### Answer: C

The function `js()` can be automatically executed without calling it and known as IIFE (Immediately Invoked Function Expression). Noted the parameter `x` of the function `js` is actuallly passed with the value 3.

The value return of the function is y(s())), meaning calling three other functions `y()`, `s()` and `j()` because the function `s()` returns `j()`.

j() returns 3^3 = 27 so that s() returns 27.

y(s()) means y(27) which returns 27\*3 = 81.

Note that we can call `declare function` BEFORE the function is actually declared but not with `expression function`.

</p>
</details>

---

###### 5. What's the output?

```javascript
var tip = 100;

(function () {
  console.log("I have $" + husband());

  function wife() {
    return tip * 2;
  }

  function husband() {
    return wife() / 2;
  }

  var tip = 10;
})();
```

- A: "I have \$10";
- B: "I have \$100";
- C: "I have \$50";
- D: "I have \$NaN";

<details><summary><b>Answer</b></summary>
<p>

#### Answer: D

We have here an IIFE (Immediately Invoked Function Expression). It means we do not have to call it but it will be excuted automatically when declared. The flow is as: husband() returns wife()/2 and wife() returns tip\*2.

We might think that tip = 100 because it is a global variable when declaring with `var` keyword. However, it is actually `undefined` because we also have `var tip = 10` INSIDE the function. As the variable `tip` is hoisted with default value `undefined`, the final result would be D. We know that `undefined` returns NaN when we try to divide to 2 or multiple with 2.

If we do not re-declare `var tip = 10;` at the end of the function, we will definately get B.

JS is fun, right?

</p>
</details>
