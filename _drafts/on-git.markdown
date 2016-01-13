## History of Version Control
[http://ericsink.com/vcbe/html/history_of_version_control.html](http://ericsink.com/vcbe/html/history_of_version_control.html)

## Configuring Git

Specifity overwrites the config.

### System-level configuration
```
git config --system
# Stored in /etc/config or c:\Program Files(x86)\Git\etc\gitconfig
```

### User-level configuration

```
git config --global
# Stored in ~/.gitconfig or c:\Users\<NAME>\.gitconfig
```

### Respository-level configuration

```
git config
# Stored in .git/config in each repo
```

### Useful Commands

```
git config --global --list
git config --global user.name "Pere Pages"
git config --global user.email "hello@pearpages.com"
git config --unset core.autocrlf
```

