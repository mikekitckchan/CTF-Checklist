## Introduction

- Before Python 3.7, we can simply set file permission using below code in Python:

```python
import os

target_dir = "path_to_my_working_dir/tmp_files/"
os.makedirs(target_dir, mode=0700)
```
- The above code should gives you a newly created folder with permission of 700. 

- However, in Python 3.7, when you check the permission, the file might appeared to be 777 instead. According to the documentation, the major reason is because os.makedir() honors the umask of current process. Thus, in python 3.7 onware, we need to set umask to 0 to change its chmod. For example: 

```python
import os
try:
    original_umask = os.umask(0)
    os.makedirs('full/path/to/new/directory', 0700)
finally:
    os.umask(original_umask)
```
