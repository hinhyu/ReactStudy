# 전개 연산자(Spread Operator)

## 전개 연산자?
전개 연산자는 ECMAScript6(2015)에서 새롭게 추가되었으며, 특정 객체 또는 배열의 값을 다른 객체, 배열로 복제하거나 옮길 때 사용. 연산자의 모양은 ... 으로 생김.

## 배열 조합
```javascript
const arr1 = [1,2,3];
const arr2 = [4,5,6];
const arr3 = [7,8,9];
const arrWrap = arr1.concat(arr2,arr3);

console.log(arrWrap);
// 결과값 : [1,2,3,4,5,6,7,8,9]
```
```javascript
const arr1 = [1,2,3];
const arr2 = [4,5,6];
const arr3 = [7,8,9];
const arrWrap = [...arr1,...arr2,...arr3];

console.log(arrWrap);
// 결과값 : [1,2,3,4,5,6,7,8,9]
```
```javascript
const arr1 = [1,2,3];
const arr2 = [4,5];
Array.prototype.push.apply(arr1,arr2);

console.log(arr1);
// 결과값 : [1,2,3,4,5]
```
```javascript
const arr1 = [1,2,3];
const arr2 = [4,5];
arr1.push(...arr2);

console.log(arrWrap);
// 결과값 : [1,2,3,4,5]
```

## 객체 조합
```javascript
const obj1 = {
    a:'A',
    b:'B'
};
const obj2 = {
    c:'C',
    d:'D'
};
const objWrap = {obj1,obj2};
console.log(objWrap);
```
```javascript
//결과값
{
    obj1:{
        a:'A',
        b:'B'
    },
    obj2:{
        c:'C',
        d:'D'
    }
}
```
### 객체 자체가 들어감
```javascript
const obj1 = {
    a:'A',
    b:'B'
};
const obj2 = {
    c:'C',
    d:'D'
};
const objWrap = {...obj1,...obj2};
console.log(objWrap);
```
```javascript
//결과값
{
    a:'A',
    b:'B',
    c:'C',
    d:'D'
}

```
### 객체 자체가 아닌 각각의 값이 할당 됨

## 기존 배열을 보전
```javascript
const arr1 = [1,2,3];
const arr2 = arr.reverse();

console.log(arr1); // [3,2,1]
console.log(arr2); // [3,2,1]
```
### 원본 배열까지 역순으로 변경됨
```javascript
const arr1 = [1,2,3];
const arr2 = [...arr1].reverse();

console.log(arr1); //[1,2,3]
console.log(arr2); //[3,2,1]
```
### 원본 배열을 유지