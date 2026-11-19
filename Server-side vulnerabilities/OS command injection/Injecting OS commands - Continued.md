# Exploiting the Vulnerability with Command Separators

Because the application implements no defences against OS command injection, an attacker can inject shell command separators to break out of the intended command arguments and execute arbitrary commands.

For example, submitting the following payload into the `productID` parameter:

```
& echo aiwefwlguh &
```

Causes the server to construct and execute the following full shell command:

```
stockreport.pl & echo aiwefwlguh & 29
```

Here, the `&` character acts as a **shell command separator**, instructing the operating system to execute three separate commands sequentially, one after another.

## Understanding the Server Response

When the server executes the injected command, the HTTP response returns the combined output of all three commands:

```
Error - productID was not provided
aiwefwlguh
29: command not found
```

Each line of output confirms a distinct step in the execution flow:

- **`Error - productID was not provided`**: The original `stockreport.pl` script ran with no arguments because the `&` terminated the first command early, causing the script to return a missing-argument error.

- **`aiwefwlguh`**: Our injected `echo` command executed successfully and printed our unique test string into the output.

- **`29: command not found`**: Everything after the second `&` (`29`, which was originally the `storeID` argument) was interpreted by the shell as a standalone command, triggering a "command not found" error.

## Why Trailing Command Separators Matter

Placing an additional command separator (`&`) after your injected command is a crucial technique:

- **Isolating Your Payload**: It cleanly separates your injected command from any remaining arguments or flags that follow the injection point in the server's command template (such as `29` in this example).

- **Preventing Syntax Errors**: Without the trailing &, the shell would treat `29` as an argument passed directly into your injected command (e.g., `echo aiwefwlguh 29` or `whoami 29`), which could cause commands that do not accept extra arguments to fail.
