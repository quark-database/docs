#### Revoke a permission from a token

🔧 `revoke from` - revokes a permission from a token.

##### Parameters

* 📦 `token` of type `str` - the token string;
* 📦 `now cannot` of type `str` - the revoking permission;

<!-- or...
🚫 This instruction takes no parameters.
-->

##### Success message

```
✅  The permission has been revoked.
```

##### Reports

1. The token does not exist
```
❌  An error occurred in Quark.

The context:  You tried to revoke a permission from a token;
The error:    The token does not exist;
What to do:   Create a token first;

Try following these steps:
    1.  Run `create token` with the token;

Doesn't work? Ask a question!
https://github.com/quark-database/cloud/issues
```

2. The permission does not exist
```
❌  An error occurred in Quark.

The context:  You tried to revoke a permission from a token;
The error:    The token does not have the permission '$permission$';
What to do:   May be you wanted to revoke the other permission?;

Doesn't work? Ask a question!
https://github.com/quark-database/cloud/issues
```

##### Result

🚫 This instruction returns no result.