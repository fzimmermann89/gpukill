zimmer08@PTB23:~$ sudo gpukill -h
Accessing GPU 1
GPU Kill v0.1, felix.zimmermann@ptb.de, BSD 2-Clause

Usage: sudo gpukill [-l| -p PID| -h]
  Shows a menu of processes running on the gpu your user got assigned
  Assignment is done by being a member of one of the gpu0, gpu1, etc groups
Options:
  l        list all processes on the assigned gpu without showing a menu
  k PID    kills the process with id PID if its running on your gpu

known Issues:
   - User can only be assigned to one group
   - Signal to be send is not configureable
   - Process that got send a kill signal will still be shown on the list


## List Processes
zimmer08@PTB23:~$ sudo gpukill -l
Accessing GPU 1
Running Processes:
12247 zimmer08  551 MiB python -c import torch;a=torch.zeros(10).cuda();import time;time.sleep(100)


## Kill one of these Processes
zimmer08@PTB23:~$ sudo gpukill -k 12247
Accessing GPU 1
Killed 12247 zimmer08  551 MiB python -c import torch;a=torch.zeros(10).cuda();import time;time.sleep(100)

## Alternative: Find Process ID using nvidia-smi and kill it using gpukill
zimmer08@PTB23:~$ nvidia-smi
[...]
+-------------------------------------------------------+
| Processes:                                            |
|  GPU   GI   CI        PID   Type   Process name       |
|        ID   ID                                        |        
|=======================================================|
|    1   N/A  N/A     12410      C   python             | 
+-------------------------------------------------------+
zimmer08@PTB23:~$ sudo gpukill -k 12410
Accessing GPU 1
Killed 12410 zimmer08  551 MiB python -c import torch;a=torch.zeros(10).cuda();import time;time.sleep(100)
