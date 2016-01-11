### This snippet here uses [Fisher-Yates Shuffling](https://www.wikiwand.com/en/Fisher%E2%80%93Yates_shuffle) Algorithm to shuffle a given array.

```javascript
function shuffle(arr){
    var i,j,temp;
    for (i = arr.length - 1; i > 0; i--) {
        j = Math.floor(Math.random() * (i + 1));
        temp = arr[i];
        arr[i] = arr[j];
        arr[j] = temp;
    }
    return arr;
}
```
An example:

```javascript
a=[1,2,3,4,5,6,7,8];
b = shuffle(a);
console.log(b);
//[2, 7, 8, 6, 5, 3, 1, 4]
```

Also, it can be used as a function in Array.prototype like this:

```javascript
Array.prototype.shuffle = function(){
    var i,j,temp;
    for (i = this.length - 1; i > 0; i--) {
        j = Math.floor(Math.random() * (i + 1));
        temp = this[i];
        this[i] = this[j];
        this[j] = temp;
    }
    return this;
}
```

An example:

```javascript
a=[2, 7, 8, 6, 5, 3, 1, 4];
a.shuffle();
console.log(a);
//[6, 5, 7, 4, 1, 8, 2, 3]
```
