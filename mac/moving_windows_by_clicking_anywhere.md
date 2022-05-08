# Moving a macOS window by clicking anywhere on it
Moving a macOS window by clicking anywhere on it (like on Linux) is possible. This behaviour can be enabled with the following command:

```
defaults write -g NSWindowShouldDragOnGesture -bool true
```

(logout may be necessary)

To drag a window, simply click on `CMD` + `Ctrl` and any part of the window.

The following command can be used to disable it:

```
defaults delete -g NSWindowShouldDragOnGesture
```

