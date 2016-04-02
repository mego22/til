# Read a plist
```
defaults read /Library/Preferences/com.apple.CrashReporter
```

# Write a value to a plist
```
sudo defaults write /Library/Preferences/com.apple.CrashReporter SomeKey -bool TRUE
sudo defaults write /Library/Preferences/com.apple.CrashReporter SomeKey -string "somevalue"
```

# Delete
```
sudo defaults delete /Library/Preferences/com.apple.CrashReporter SomeKey
```
