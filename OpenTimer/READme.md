# Getting Started With OpenTimer :

The following are the steps that replicate my approach towards intializing and running the timing analysis on `OpenTimer`.

## Setting up the work environment :

After the installation of OpenTimer, locate the `ot-shell` in the `bin` directory in the installed OpenTimer directory as shown below. 

![](/images/theory/OpenTimer_dir.png)

After locating the `ot-shell` simply copy it to your `work` directory where the runs would be done. It is preferable to create a proper directory that contains all necessary directories and files for the static analysis runs. My personal `work` directory looks something like the image under :

![](/images/theory/my_work_dir.png)

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

## Initial Flow of OpenTimer tool :

To perform a basic timing analysis, the three underlined set of files are required :

- Verilog File : Describes the design of the circuit in HDL. Extension : .v
- SDC : Synopsys Design Constraint file contains the constraints that the design is desired to meet. An SDC is written in tcl language. Extension : .sdc
- Lib : The .lib contains the cell-definition and parameters (nominal conditions, luts , cell functionality, timing information).

> [!NOTE]
> The verilog file must contain the cell instances present in the .lib file and the pins of the modules should be properly mapped to the pins of the cells in the library file. Failure to do so may cause an error while reading the verilog file in the tool.

To run the opentimer use the following commands in the ot-shell in the following order:

```
read_celllib <path_to_lib>
```
This command reads the library given in the path.

```
read_verilog <path_to_verilog> 
```
This command reads the verilog given in the path.

```
read_sdc <path_to_sdc>
```
This command reads the sdc given in the path.





