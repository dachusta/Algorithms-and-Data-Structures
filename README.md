# Algorithms-and-Data-Structures

## 1. Palindrome CheckerPassed

Return `true` if the given string is a palindrome. Otherwise, return `false`.

```javascript
function palindrome(str) {
  let word = str.toLowerCase().replace(/\s|\W|_/g,'');
  let reverseWord = word.split("").reverse().join("");
  return reverseWord === word;
}
palindrome("A man, a plan, a canal. Panama");
```



## 2. Roman Numeral ConverterPassed

Convert the given number into a roman numeral.

```javascript
function convertToRoman(num) {
  const numeral = {M:1000, CM:900, D:500, CD:400, C:100, XC:90, L:50, XL:40, X:10, IX:9, V:5, IV:4, I:1};
  let roman = '';
  for (let i in numeral ) {
    while ( num >= numeral[i] ) {
      roman += i;
      num -= numeral[i];
    }
  }
  return roman;
}
convertToRoman(2021);
```


## 3. Caesars Cipher

Function which takes a ROT13 encoded string as input and returns a decoded string.

```javascript
function rot13(str) {
  const arrStart = ['A', 'B', 'C', 'D', 'E', 'F', 'G', 'H', 'I', 'J', 'K', 'L', 'M'];
  const arrEnd = ['N', 'O', 'P', 'Q', 'R', 'S', 'T', 'U', 'V', 'W', 'X', 'Y', 'Z'];
  const toCipher = [];

  for (let i = 0; i < str.length; i++) {
    if (arrStart.indexOf(str[i]) > -1) {
      let index = arrStart.indexOf(str[i])
      toCipher.push(arrEnd[index])
    }
    else if (arrEnd.indexOf(str[i]) > -1) {
      let index = arrEnd.indexOf(str[i])
      toCipher.push(arrStart[index])
    }
    else toCipher.push(str[i])
  }
  return toCipher.join('');
}
rot13("SERR PBQR PNZC");
```



## 4. Telephone Number ValidatorPassed

Return `true` if the passed string looks like a valid RU phone number.

```javascript
function telephoneCheck(str) {
  let regexp = /^(((\+7)|8)[\- ]?)?((\(\d{3}\))|(\d{3}))[\- ]?\d{3}[\- ]?(\d{4})$/;
  return regexp.test(str);
 }
telephoneCheck("8(555)-555-5555");
```



## 5. Cash Register

Design a cash register drawer function `checkCashRegister()` that accepts purchase price as the first argument (`price`), payment as the second argument (`cash`), and cash-in-drawer (`cid`) as the third argument.
`cid` is a 2D array listing available currency.
The `checkCashRegister()` function should always return an object with a `status` key and a `change` key.
Return `{status: "INSUFFICIENT_FUNDS", change: []}` if cash-in-drawer is less than the change due, or if you cannot return the exact change.
Return `{status: "CLOSED", change: [...]}` with cash-in-drawer as the value for the key `change` if it is equal to the change due.
Otherwise, return `{status: "OPEN", change: [...]}`, with the change due in coins and bills, sorted in highest to lowest order, as the value of the `change` key.

```javascript
function checkCashRegister(price, cash, cid) {
  let change = {status: "OPEN", change: []};
  let due = 100 * (cash - price);
  let moneyValues = [1, 5, 10, 25, 100, 500, 1000, 2000, 10000];
  let availableFunds = 0;

  cid.forEach(e => availableFunds += e[1])
  if (availableFunds*100 === due) {
    change.status = "CLOSED";
    change.change = cid
    return change;
  }
  for (let i = cid.length - 1; i >= 0; i--){
    let amt = 0;
    while (moneyValues[i] <= due && cid[i][1] > 0 && due > 0){
      cid[i][1] -= moneyValues[i]/100;
      due -= moneyValues[i];
      amt += moneyValues[i]/100;
    }
    if (amt !== 0){
      change.change.push([cid[i][0], amt]);
    }
  }
  if (due !== 0){
    change.status = "INSUFFICIENT_FUNDS";
    change.change = [];
    return change;
  }
  for (let j = 0; j < cid.length; j++){
    if (cid[j][1] > 0){
      return change;
    }
  }
}
checkCashRegister(19.5, 20, [["PENNY", 0.5], ["NICKEL", 0], ["DIME", 0], ["QUARTER", 0], ["ONE", 0], ["FIVE", 0], ["TEN", 0], ["TWENTY", 0], ["ONE HUNDRED", 0]]) 
```
