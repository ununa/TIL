## 별 만들기 01
#### 코드
``` js
let _max = 4;

for(let i = 0; i <= _max; i++) {
  
  let star = '';
  
  for(let j = _max; j >= i; j--){
    //console.log(j)
    star += '*';
  }
  console.log(star);
}
```
#### 결과
```
***** 
**** 
*** 
** 
* 
```

## 별 만들기 02
#### 코드
``` js
let _max = 4;

for(let i = 0; i <= _max; i++) {
  
  let star = '';
  
  for (let k = 0; k <= i; k++){
    star += ' ';  
  }
  for(let j = _max; j >= i; j--){
    //console.log(j)
    star += '*';
  }
  console.log(star);
}

```
#### 결과
```
 ***** 
  **** 
   *** 
    ** 
     * 
```
