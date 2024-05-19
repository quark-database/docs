#### Create a token

🔧 `create token` - creates an auth token.

##### Parameters

* 📦 `token` of type `str` - the token string;
* 📦 `can` of type `array of str` - the list of permissions;

<!-- or...
🚫 This instruction takes no parameters.
-->

##### Success message

```
✅  The token has been created.
```

##### Reports

1. Token already exists
```
❌  An error occurred in Quark.

The context:  You tried to create a token;
The error:    The token already exists;
What to do:   Change the token string;

Doesn't work? Ask a question!
https://github.com/quark-database/cloud/issues
```

##### Result

🚫 This instruction returns no result.
