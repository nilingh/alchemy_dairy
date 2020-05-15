##### Using a String element as a Variable name

[Python将字符串常量转化为变量方法总结](https://www.jb51.net/article/157955.htm)

1. `globals()`

   ```python
   list1 = ['A', 'B', 'C', 'D']
   for i in list1:
       globals()[i] = ['new']
   ```

   Print out `globals()` and finding out a dictionary.  `globals()[i]` 

   ```python
   {'__name__': '__main__', '__doc__': None, '__package__': None, '__loader__': <class '_frozen_importlib.BuiltinImporter'>, '__spec__': None, '__annotations__': {}, '__builtins__': <module 'builtins' (built-in)>, 'names': {...}, 'i': 'A', 'list1': ['A', 'B', 'C', 'D']}
   ```

   

2. `exec` and `eval`



