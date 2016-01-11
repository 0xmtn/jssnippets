Sometimes, for the sake of UI, it is a neccessity to have a full control over a fullname when displaying it.

```javascript
function abbrFullName(arr, args){
    return arr.map(function(elem, idx, arr){
        return idx != 0 && idx != arr.length-1 ? elem[0]+"." : 
            (args.name && idx==0) || (args.surname && idx==arr.length-1) ? elem[0]+"." : 
            elem;
    }).join(" ");
}
```
Examples:
```javascript
var fullname_str = "John Ronald Reuel Tolkien";
var fullname_word_list = fullname_str.split(" ");
abbrFullName(fullname_word_list, {name: false, surname: false}); // abbreviate only middle names
//John R. R. Tolkien
abbrFullName(fullname_word_list, {name: true, surname: false}); //abbreviate name too
//J. R. R. Tolkien
abbrFullName(fullname_word_list, {name: false, furname: true}); //abbreviate surname too
//John R. R. T.
abbrFullName(fullname_word_list, {name: true, surname: true}); //abbreviate name and surname too
//J. R. R. T.
```
