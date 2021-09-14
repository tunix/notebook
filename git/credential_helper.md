# Using GNOME Keyring as git credential helper

Modern Linux distros now have `libsecret` installed as part of the desktop which provides new & standardized keyring
capabilities. On the other hand, the git credential helper bit is kind of missing. You'll need to compile it from source
and let git know about it by changing configuration.

* Install `libsecret-1-dev` package.
* Go to `/usr/share/doc/git/contrib/credential/libsecret`
* Compile from source:

```
sudo make --directory=/usr/share/doc/git/contrib/credential/libsecret
```

* Change configuration of git to let it know about the new helper:

```
git config \
    --file $HOME/.gitconfig.inc \
    credential.helper \
   /usr/share/doc/git/contrib/credential/libsecret/git-credential-libsecret
```
