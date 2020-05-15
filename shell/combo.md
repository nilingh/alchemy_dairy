# Combo!



##### Task：Move all the ordinary files to ./ex2 excluding directories in working path

只把当前目录下所有的文件移动到./ex2/下，不移动当前目录中的其他目录（只移动普通文件）

Tips of `find`:

* `-maxdepth 1` limit search depth in the current directory, the default setting will find out sub-directory if  it exists

* `-type f` search the ordinary file

Tips of `xargs`

* `xargs -i` the outputs of a pipeline will be put out in sequence `-t` will print out the command before it is executed, so we can check the syntax correction

* `{}` the advantage of `xargs` is we can pick the position of our parameters, while the outcome of ordinary `|` pipeline can only be the input of succeeding command

P.S. -exec is similar to xargs(), my personal choice is xargs 

```bash
find ./ -maxdepth 1 -type f | xargs -i -t mv {} ./ex2/
# -maxdepth 1 限制查找深度在当前目录，默认会把子目录中的文件也找出来
# -type f 查找类型是普通文件，这个参数是本任务的关键
# xargs -i 管道符前的输出会被逐项输出 -t 将后续命令输出后再执行，可以检查语法
# {} xargs的优势是可以执行参数的位置，如果是|管道符就只能当作后续命令的输入
# 补充：-exec和xargs比较近似，以后尽量使用xargs
```

