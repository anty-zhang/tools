# brew 基本命令

brew home 用浏览器打开brew的官方网站

brew search

# mac os x install

sudo /Users/xxx/soft/Install\ macOS\ Sierra.app/Contents/Resources/createinstallmedia  --volume /Volumes/UUI/ --applicationpath /Users/xxx/soft/Install\ macOS\ Sierra.app --nointeraction

# mac gdb异常解决
```bash
异常信息描述
(gdb) run
Starting program: /Users/xxx/work5/data_structure/tree/a.out
During startup program terminated with signal ?, Unknown signal.
解决
vim ~/.gdbinit
set startup-with-shell off

```