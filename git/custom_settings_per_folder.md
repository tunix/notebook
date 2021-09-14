# Custom configuration per folder

Sometimes you may need to have different configurations for different paths. If you frequently commit code for your
public repos as well as your employer's, you must know the feeling when your e-mail address is incorrect inside your
commits. 😉

Thankfully, there is now a solution to this problem.

Append below block in your `~/.gitconfig.inc` to include a custom config for your employer repo configuration:

```
[includeIf "gitdir:~/Projects/employer/"]
    path = ~/.employer.gitconfig
```

Now create a configuration file (`~/.employer.gitconfig`) for your employer with your custom configuration:

```
[user]
    email = john.doe@employer.com
```
