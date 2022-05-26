# Installation guide for Windows #


    
## 1. Prerequisites ##

Install 7-zip, FFMPEG, Anaconda, JDK8, git

You can also follow this [tutorial](https://github.com/Microsoft/malmo/blob/master/doc/install_windows_manual.md) to install dependencies. 

Note that newer JDK versions may not work.


## 2. Install malmo using Anaconda ##

Since malmo might not work on newest Python version, it is recommended that you create a virtual environment with a different Python installed.

Open Anaconda Prompt, run:
```
conda create -n malmo37 python=3.7

conda activate malmo37

pip install malmo
```
### Installing malmo official release ###


Create or change into a working directory where you would like Malmo to be installed, run:
```
python

import malmo.minecraftbootstrap

malmo.minecraftbootstrap.download()
```

The command will create a new directory called MalmoPlatform containing the Malmo GitHub project in your current working directory.

If you get `FileNotFoundError: [WinError 2] The system cannot find the file specified`, please make sure that your environment variable PATH contains your git installation path (git\bin and git\cmd).

### Installing specific malmo version ###

If you wish to install the specific malmo version for this project, please open the file in envs/malmo37/Lib/site-packages/malmo/minecraftbootstrap, change Line 58 from
```
subprocess.check_call(["git", "clone", "-b", branch, "https://github.com/Microsoft/malmo.git" , malmo_install_dir])
```
to
```
subprocess.check_call(["git", "clone", "https://github.com/chemgymrl/block_malmo", malmo_install_dir])
```
Then do the same as installing official malmo release mentioned above.

## 3. Launch Minecraft ##

Set up the MALMO_XSD_PATH environment variable to point to the MalmoPlatform/Schemas directory. 

Change the current directory to MalmoPlatform’s parent folder then run:

```
python

import malmo.minecraftbootstrap

malmo.minecraftbootstrap.launch_minecraft()
```

Remember you need to launch Minecraft first before running other scripts.


## 4. Common problems ##

```
ModuleNotFoundError: No module named 'MalmoPython'
```
Solution: Instead of using `import MalmoPython`, use `from malmo import MalmoPython`

```
ImportError: DLL load failed: The specified module could not be found.
```
Solution: This might happen when executing `from malmo import MalmoPython`. You can add zlib.dll to C:/Windows/System32, or try an older version, i.e. Python 3.6 with malmo 0.36.0
```
TypeError: Descriptors cannot not be created directly.
If this call came from a _pb2.py file, your generated code is out of date and must be regenerated with protoc >= 3.19.0.
```
Solution:  `pip install protobuf==3.20.1`
