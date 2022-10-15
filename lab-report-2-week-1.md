# Week 1 Lab Report
## How to Remotely Connect to ieng6 (Tutorial)

### Step 1 - Installing VScode
![Image](Installing%20VScode.png)

The first step is to go to ![https://code.visualstudio.com/](https://code.visualstudio.com/) and download Visual Studio for your operating system (Windows, Mac, etc.). Then, you will need to follow any installation steps that are required to install Visual Studio. After that, you can simply create any file for now.


### Step 2 - Remotely Connecting
![Image](Remotely%20Connecting.png)

With that new file open, you can open the terminal by pressing "Terminal" at the very top of the application and "New Terminal." Once you've opened the terminal, you should type the command `$ ssh cs15lfa22mo@ieng6.ucsd.edu` replacing "mo" with your username. Find your username through entering your info at ![https://sdacs.ucsd.edu/~icc/index.php](https://sdacs.ucsd.edu/~icc/index.php) and your password through following the instructions on ![https://docs.google.com/document/d/1hs7CyQeh-MdUfM9uv99i8tqfneos6Y8bDU0uhn1wqho/edit](https://docs.google.com/document/d/1hs7CyQeh-MdUfM9uv99i8tqfneos6Y8bDU0uhn1wqho/edit).  Some messages will pop up, in which you can type "yes" and your password after when told so.

### Step 3 - Trying Some Commands
![Image](Trying%20Some%20Commands.png)

Now that you're connected to the remote server, there are a few special commands you can try:

* cd ~ : changes directory to home directory
* cd : used to change directories
* ls -lat : returns a list of files in the current directory
* ls -a : returns a list of all visible and hidden files in your current directory
* cp /home/linux/ieng6/cs15lfa22/public/hello.txt ~/ : copies hello.txt file
* cat /home/linux/ieng6/cs15lfa22/public/hello.txt : displays the contents of hello.txt file

I've tested these commands myself as shown in the screenshot. 

### Step 4 - Moving Files with scp
![Image](Moving%20Files%20with%20scp.png)

On this step, we'll be moving a file from your local computer to the remote server using a command called scp. First, I created a file called "WhereAmI.java" and compiled it using the javac and java commands. Then, I typed the command `$ scp WhereAmI.java cs15lfa22mo@ieng6.ucsd.edu:~/` which will send the "WhereAmI.java" file to the remote server. You can test this by logging back into the remote server and using the `$ ls` command to see that the file is in your home directory.

WhereAmI.java code:

```
class WhereAmI {
    public static void main(String[] args) {
      System.out.println(System.getProperty("os.name"));
      System.out.println(System.getProperty("user.name"));
      System.out.println(System.getProperty("user.home"));
      System.out.println(System.getProperty("user.dir"));
    }
  }
```

### Step 5 - Setting an SSH Key
![Image](SSH%20Keys.png))   

In order to setup an SSH Key, you need to type the command ssh-keygen into your terminal on your local computer client. Again, a few messages will appear, for which you can simply press enter for each one. After those messages, you should log back into your remote server using the ssh command and type the command `$ mkdir .ssh` into the terminal. Now, go back to your local computer client, and type the command `$ scp /Users/jadontran/.ssh/id_rsa.pub cs15lfa22mo@ieng6.ucsd.edu:~/.ssh/authorized_keys` to finish setting up your SSH key.

### Step 6 - Optimize Remote Running
![Image](Making%20Remote%20Running%20Even%20More%20Pleasant.png)

The last step is to create a combination of commands that will allow for the most efficient way of editing our "WhereAmI.java" file, sending it to the remote server, and running it all at once. The command that must be used for this is a condensement of three commands. I used ` scp WhereAmI.java cs15lfa22mo@ieng6.ucsd.edu:~/ ; ssh cs15lfa22mo@ieng6.ucsd.edu "javac WhereAmI.java" ; ssh cs15lfa22mo@ieng6.ucsd.edu "java WhereAmI"` which allowed me to do all three at once at the click of a button.