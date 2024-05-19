#### Change the server port

🔧 `change cloud port to` - changes the cloud port.

##### Parameters

* 📦 `port` of type `int` - the new port of the cloud;

<!-- or...
🚫 This instruction takes no parameters.
-->

##### Success message

```
✅  The port has been changed.
```

##### Reports

1. The port is invalid.
```
❌  An error occurred in Quark.

The context:  You tried to change the port;
The error:    The port $port$ is invalid;
What to do:   Pick a port between 1 to 65535;

Doesn't work? Ask a question!
https://github.com/quark-database/cloud/issues
```

2. The port is already in use.
```
❌  An error occurred in Quark.

The context:  You tried to change the port;
The error:    The port $port$ is already in use;
What to do:   Pick a free port between 1 to 65535;

Doesn't work? Ask a question!
https://github.com/quark-database/cloud/issues
```

##### Result

🚫 This instruction returns no result.