#### Redefine permissions for a token

🔧 `redefine permissions for` - revokes all existing permissions from a token and sets a new list of permissions for it.

##### Parameters

* 📦 `token` of type `str` - the token string;

<!-- or...
🚫 This instruction takes no parameters.
-->

##### Success message

```
✅  The permissions have been redefined.
```

##### Reports

1. The token does not exist
```
❌  An error occurred in Quark.

The context:  You tried to redefine permissions for a token;
The error:    The token does not exist;
What to do:   Create a token first;

Try following these steps:
    1.  Run `create token` and pass your permissions in `can` array;

Doesn't work? Ask a question!
https://github.com/quark-database/cloud/issues
```

##### Result

🚫 This instruction returns no result.
