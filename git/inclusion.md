# Easy git config management by inclusion

* Create an empty `~/.gitconfig.inc` file.
* In case you're tracking changes via git, this file should be ignored.
* Place all your custom configuration that you don't need to be tracked. (ex: only use credential helper on a certain
  machine)
* Place below piece of configuration at the end of your `~/.gitconfig` file:

```
[include]
    path = ~/.gitconfig.inc
```

This file should not cause any trouble even if it doesn't exist. Unfortunetely, git config cannot seem to use glob
patterns as of now for such inclusions.
