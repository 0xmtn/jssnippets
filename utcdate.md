To create UTC timestamps in JS:

```javascript
function UTCDate(date){
    var utc_tmstmp = Date.UTC(date.getUTCFullYear(),
            date.getUTCMonth(),
            date.getUTCDate(),
            date.getUTCHours(),
            date.getUTCMinutes(),
            date.getUTCSeconds(),
            date.getUTCMilliseconds());
    return utc_tmstmp;
};
```
Examples:
```javascript

```
