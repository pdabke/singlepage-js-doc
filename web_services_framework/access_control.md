# Access Control
SinglePage support role-based access control at the service level as well as method level. Roles allowed to access the methods are defined using the attribute ACL in your service. Perhaps the most common case is to require users to log in to access any method on the service. The following code will set this up. Special field "*" is used to specify access restriction on all methods and the empty array indicates that the user has to be logged in.
```javascript
const CalculatorService = {
  ACL: {
    "*": []
  },
        :
        :
```
To restrict access for all methods of your service to specific roles, set "*" attribute of the ACL to the array of allowable roles. Code below shows an example that restricts access to MODERATOR role.

```javascript
const CalculatorService = {
  ACL: {
    "*": ['MODERATOR']
  },
        :
        :
```
 >Users with ADMIN and SUPERADMIN roles will always have access to all methods regardless of the ACL specification.

Roles allowed to access individual methods can be specified via attribute with the method name on ACL. The code below will allow users with MODERATOR role to access all methods but only users with MODERATOR as well as PLATINUM roles will be able to access divide method.

```javascript
const CalculatorService = {
  ACL: {
    "*": ['MODERATOR'],
    "divide": ['PLATINUM']
  },
        :
        :
​```