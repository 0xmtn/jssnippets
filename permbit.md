### Using bits and bitwise operators to manage permissions and a lot more.
 
When creating APIs, a permission space is often needed - permission you give to a developer, permission users set in their profiles. The examples and snippets below demonstrate how to check whether a user or developer has required permissions or not.

```javascript
var perms = {BASIC: 1,
             PUBCONTENT: 2,
             FOLLOWERLIST: 4,
             COMMENTS: 8,
             RELATIONSHIPS: 16,
             LIKES: 32};

function create_perm_bitmask(req_perms){
  var j, k, i=0, perms_len = perms.length;
  var asked_perms = [];
  for(j=0; j<perms_len; j++){
    asked_perms.push(0);
  }

  for(k in perms){
    asked_perms[i] = false;
    if(req_perms.hasOwnProperty(k)){
      asked_perms[i] = true;
    }
    i++;
  }  

  var nMask = 0, nFlag = 0, nLen = asked_perms.length > 32 ? 32 : asked_perms.length;
  for (nFlag; nFlag < nLen; nMask |= asked_perms[nFlag] << nFlag++);
  return nMask;
}

//Suppose that in order to get list of followers of a user along with user's personal info,  
//and likes, the required permission scope consists: 
//basic, follower_list and likes
//Instead of checking if one has it by string comparison:

var users_permissions = create_perm_bitmask({BASIC: true, 
                                             FOLLOWERLIST: true, 
                                             LIKES: true, 
                                             RELATIONSHIPS:true});
console.log(required_perm_scope); // 53
```


Now that user has a bitmask of permissions, you can do following:

```javascript
if(perms.BASIC & users_permissions){
    //User has this permission
    //Continue..
}

```

Or checking combination of perms:
```javascript
var comb = perms.FOLLOWERLIST | perms.PUBCONTENT;
if(users_permissions & comb){
    //User has either FOLLOWERLIST or PUBCONTENT
    //Continue..
}
```

Adding new permissions to user
```javascript
var new_perms = perms.PUBCONTENT | perms.COMMENTS;
users_permissions |= new_perms;
console.log(users_permissions); //63
```

Toggle a permission or set of permissions:
```javascript
var new_perms = perms.BASIC | perms.LIKES;
users_permissions ^ new_perms; // If user had BASIC, it is gone now. If didn't have, then now has. Same goes for LIKES too.
```

Toggle all permissoins:
```javascript
var toggled_user_permissions = ~users_permissions;
```

Revoke permissions:
```javascript
users_permissions &= ~(perms.FOLLOWERLIST);

//Using combinations:
var comb = ~(perms.FOLLOWERLIST | perms.LIKES); //~perms.FOLLOWERLIST & ~perms.LIKES
users_permissions &= comb; //User won't have the permissions FOLLOWERLIST and LIKES from now on.
```
  
