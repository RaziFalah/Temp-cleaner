# Temp-cleaner
Clean temp and %temp% unneeded files. This program works on windows-based operating systems only! might be useful on linux systems running Wine but i would recommend to manually clean the environment.



<h1>Download app as .exe file <a href="https://github.com/RaziFalah/Temp-cleaner/releases/tag/v1.0.1" targe="_blank">here</a></h1>




used moudles:

```
import ctypes, sys
import os as do
from time import sleep
import getpass
```

App 

```
import ctypes, sys
import os as do
from time import sleep
import getpass


def is_admin():
    try:
        return ctypes.windll.shell32.IsUserAnAdmin()
    except:
        return False

if is_admin():
    print("Cleaning temp...")
    import os, shutil
    folder = "C:\Windows\Temp"
    for filename in os.listdir(folder):
        file_path = os.path.join(folder, filename)
        try:
            if os.path.isfile(file_path) or os.path.islink(file_path):
                os.unlink(file_path)
            elif os.path.isdir(file_path):
                shutil.rmtree(file_path)
        except Exception as e:
            print('Failed to delete %s. Reason: %s' % (file_path, e))
    print("Successfuly cleand temp!!")
    do.system("color 4")
    print("Cleaning %temp%...")
    import os, shutil
    user = getpass.getuser()
    folder = f"C:/Users/{user}/AppData/Local/Temp"
    for filename in os.listdir(folder):
        file_path = os.path.join(folder, filename)
        try:
            if os.path.isfile(file_path) or os.path.islink(file_path):
                os.unlink(file_path)
            elif os.path.isdir(file_path):
                shutil.rmtree(file_path)
        except Exception as e:
            print('Failed to delete %s. Reason: %s' % (file_path, e))
            sleep(10)
else:
    ctypes.windll.shell32.ShellExecuteW(None, "runas", sys.executable, " ".join(sys.argv), None, 1)

do.system("color a")
print("Temp and %temp has been cleard successfuly!")
```
