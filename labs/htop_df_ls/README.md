# Space management commands

There are two kinds of space that we use for data: 
1. memory (Random Access Memory - RAM):
	- temporarily store data / code for running programs
	- gets reset when process (running program) dies (execution completes) 
	- fast in operation
	- smaller in size when compared to storage space
2. storage space (hard disk or Solid State Drive - SSD): 
	- permanently store data in the form of files and folders
	- long term storage (that is, data is retained on reboot)
	- slow in operation
	- usually much larger than RAM

#### Why do you need to learn about space management commands?

You might encounter resource crunch problems this semester as you learn to deal with larger and larger datasets. These commands will be helpful for you to determine the correct course of action to recover memory / storage space.

## Running `htop` to keep track of memory

- Open `terminal` either via `jupyterlab` session or open SSH session using `terminal` / `powershell`. 
- If you want to view both command output and your `jupyterlab` session, I would recommend opening an SSH session and splitting your screen between your browser window and the terminal (see the second image in the below write up).
- Run `htop` on your terminal. The output should look something like this:
<img src="img/htop.png">

- `htop` shows the programs that are using the top of the resources (memory, CPU, etc.,). The "h" letter indicates that the output is in human readable format (that is, it does not display too many large numbers).
- On your VM, we have two CPUs (marked by 0 and 1 in `htop` output - see above image). They probably might be running on a single physical chip, but they are two CPU cores on the same chip. The bars and the indicate how much each of those CPUs are being used. You will see a low number if you don't have two many processes (running programs) currently executing on your VM. When I took this snapshot, my CPUs were almost idle. 
- Below the CPU usage, we see "Mem" usage. Total memory available is 1.93 G. G stands for Gigabyte (aproximately 1 billion bytes). It is interesting that we are using so much memory (835 M; M stands for Megabyte, approximately 1 million bytes) when the CPUs are sitting idly. 
	- If too much memory is being used, then your VM becomes slow
	- How do we get memory back? 1. reboot 2. figure out what process is taking up all that memory 
	- Let's focus on option 2 here.
	- Go to your `jupyterlab` session and click on the "stop" sign (see below image):
	- As you can see, after you open a notebook for running it keeps running in the background even though you close the tab associated with a notebook
	- Close one of those notebooks and go back and check your memory usage. 
<img src="img/free_memory_1.png">

	- Continue closing all of the notebooks. Observe how memory gets freed up as you close the notebooks.
<img src="img/free_memory_2.png">
<img src="img/free_memory_3.png">
- To stop `htop`, you need to enter `Ctrl + c` on your keyboard, which sends the kill signal. 

**Note: It is important for you to close / shutdown unused notebooks often, so that your VM doesn't slow down too much!**

## Running `df` to keep track of storage space

- Run `df` on your terminal. The output should look something like this:
<img src="img/df_output.png">

- The output shows the details of all storage devices like hard drive. 
- We are not going to learn details about each listing here. Instead let's focus on the disk usage of the current working directory.
- Recall that we can use `.` to specify current working directory.
- Run `df .` on your terminal. The output should look something like this (it might not match exactly):
<img src="img/df_output_2.png">

- Right now, I am using 23% of my storage space. It also displays the size in blocks, which is difficult for us to read. Let's use "-h" option, which will enable us to get human readable output.
- Run `df . -h` on your terminal. The output should look something like this (it might not match exactly):
<img src="img/df_output_3.png">

- This output is so much better to read. I have a total of 15G storage space, out of which I am currently using 3.2G.

## Running `ls` to find files to delete for clearing up storage space 

- Change into `labs/htop_df_ls/data` directory on your `terminal`. That is run `cd cs320-s23-projects/labs/htop_df_ls/data`.
- Then run `ls` command. The output should list all the files and directories. It doesn't show the associated details like size.
- Try running `ls -l` command. "-l" option shows a list format of output with additional details, including size. The size is still difficult for us to read. Are you able to think of some other option which will make the output more human readable?
- If you were thinking "-h", you got it. Try running `ls -lh`. The output should look something like this:
<img src="img/ls_lh_output.png">

- As you can see "wi.zip" is a large file (21 M). Let's say that for some reason you have two copies of it. Execute `cp wi.zip wi_2.zip` command and then try to execute `ls -lh` command. You should now see two "zip" files.
- How can we delete unnecessary files? Run `rm wi_2.zip` command. Be very careful when executing `rm` command. The delete action will be permanent.

## Reading data from `wi.zip`

- `wi.zip` is a large dataset which contains all the loan applications in WI for a year. Real-life dataset. You will be analyzing this for project P2.
- Next lecture, you will learn how to read data from zip file without uncompressing it.
- For now, let's learn how to uncompress it. 
- You should have already installed unzip. If for some reason you did not, then run `sudo apt-get install unzip` on your terminal. Enter "9" for the prompt.
- Run `unzip wi.zip` on your terminal. Then run `ls -lh` and observe that we now have a "wi.csv" (size: 177M).
- Observe that the decompressed / inflated / extracted version is much larger. 
- As an alternate to deleting files to free up storage space, we can compress files and directories, to save space.
- Keep your screen split between `terminal` and `jupyterlab`. It is a good idea to run `htop` while writing code to observe how much memory space we are using (consequences of running the code that we are writing).
- Go to `jupyterlab` session, navigate to `htop_df_ls` directory (the parent directory of `data` directory).
- Create a new notebook file and name it `lab2.ipynb`. Discuss steps with your group members as needed.
- Create a cell for import statements:
```python
import pandas as pd
import os
```
- In a new cell, read the data in `wi.csv` using `pandas`. Before you run this cell, run `htop` on terminal and observe how memory usage increases as we read this large data file (see below image).
```python
df = pd.read_csv(os.path.join("data", "wi.csv"))
```
<img src="img/wi_csv_1.png">
<img src="img/wi_csv_2.png">
<img src="img/wi_csv_3.png">

- Observe that when we read `wi.csv` data, we are using more memory than the file size (which was just 177M). We often need more memory space than storage space. This is because the data is being reformatted for us to efficiently analyse it, which causes additional overhead on memory usage.
- Before adding a new cell with the below code, discuss with your group: will this new line of code cause a memory spike and why or why not?
```python
df2 = df
```
- Recall that above line of code produces reference copy. That is, we do not create any new objects. So, we don't see a spike in memory usage. Discuss with your group: what kind of copy would create a memory spike? Try writing the code for it (not provided).
<img src="img/wi_csv_4.png">

- How can used memory be reclaimed inside a program? Garbage collector clears up memory that stores data which no longer has active references inside our program. In python, we can simply change variable assignments to a different object to eliminate the prior reference. Try inserting a new cell with the below lines of code and observe how memory usage drops.
```python
df = "some dummy string"
df2 = df
```
<img src="img/wi_csv_5.png">

- **IMPORTANT**: do not forget to close / shutdown `lab2.ipynb`, so that you get the used memory back.
- We will continue this example during Wednesday's lecture.
