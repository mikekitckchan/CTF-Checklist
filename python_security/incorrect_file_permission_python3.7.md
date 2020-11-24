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
    target_dir = "path_to_my_working_dir/tmp_files/"
    os.makedirs(target_dir, 0700)
finally:
    os.umask(original_umask)
```
## Impact

### Django CVE-2020-24583: Incorrect permissions on intermediate-level directories on Python 3.7+

- The subject has impacted many software that run Python. One of the recent CVE regarding this is a vuln found in Django.

- If you set below code in ```setting.py```:

```python
STATIC_ROOT = BASE_DIR / "static"
FILE_UPLOAD_DIRECTORY_PERMISSIONS = 0o700
```
- You would found that the "static" folder's permission would still be 777. It is because the FILE_UPLOAD_DIRECTORY_PERMISSIONS used os.makedirs to setup the permission. 

- It might lead to leakage of sensitive info to attackers.
