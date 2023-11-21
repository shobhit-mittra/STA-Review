# Getting Started With OpenTimer :

The following are the steps that replicate my approach towards intializing and running the timing analysis on `OpenTimer`.

## Setting up the work environment :

After the installation of OpenTimer, locate the `ot-shell` in the `bin` directory in the installed OpenTimer directory as shown below. 

![](/images/theory/OpenTimer_dir.png)

After locating the `ot-shell` simply copy it to your `work` directory where the runs would be done. It is preferable to create a proper directory that contains all necessary directories and files for the static analysis runs. My personal `work` directory looks something like the image under :

![](/images/theory/my_work_dir)

Now that the environment is set we can proceed onto invoking the tool.

## Invoking OpenTimer :

To envoke the tool simply type the command below. 
```
./ot-shell 
```

In case the run is done on a separate directory then it is important to copy the full path to the ot-shell. Hence, it is recommended to copy the `ot-shell` executable file to a directory one needs to work in. After running the command, the user is prompted to the ot-shell that looks like the image under :

![](/images/theory/ot_shell_prompt.png)

Now that the tool is invoked, we are ready to perform STA.

> [!NOTE]
> A better approach to invoke the tool is to create an environment variable and use that variable to call the path to the ot-shell, that environment variable can have a simple name such as opentimer or run_ot.

<br/>

## Initial Flow OpenTimer tool :




