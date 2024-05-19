#### Grant a permission to a token

🔧 `grant` - grants a permission to a token.

##### Parameters

* 📦 `token` of type `str` - the token string;
* 📦 `now can` of type `str` - a new permission for a token;

<!-- or...
🚫 This instruction takes no parameters.
-->

##### Success message

```
✅  The permission has been granted.
```

##### Reports

1. The token does not exist
```
❌  An error occurred in Quark.

The context:  You tried to grant a token a permission;
The error:    The token does not exist;
What to do:   Create a token first;

Try following these steps:
    1.  Run `create token` and pass your permissions in `can` array;

Doesn't work? Ask a question!
https://github.com/quark-database/cloud/issues
```

2. The permission is already granted
```
❌  An error occurred in Quark.

The context:  You tried to grant a token a permission;
The error:    The token already can the permission '$permission$';
What to do:   May be you wanted to grant the other permission?;

Doesn't work? Ask a question!
https://github.com/quark-database/cloud/issues
```

##### Result

🚫 This instruction returns no result.