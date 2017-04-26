# OSH Park Eagle scripts

These scripts are to help Eagle users get orders in just a tad bit faster, and help keep things a bit more up to date.

Currently, our ownly supported tool is a simple "Upload PCB" button to help save some file browsing. We look forward to adding more capability to these scripts later.


## Installation (easy mode)

The simple way is to run our installer script. This consists of a few short steps. 

1. Download all the files here. 

2. Open Eagle, to the Schematic or Board layout window. 

3. Select `File`, then `Run ULP`. On the file select dialog, browse to the files and select `install.ulp`.

4. Should be all done! You'll new see a new ![](oshpark.png) button on your top toolbar. Click it to see cool stuff!

In the future, we'll be adding improvements to the script to add cool new feautures. The installer will help with upgrading.


## Installation (The hard way)

### Find your $EAGLEDIR directory

In Linux based systems, this directory is typically `~/.eagle/`

For Windows, this directory is typically `C:\Users\[username]\AppData\Roaming\CadSoft\EAGLE`. 

### Copy over the files

To get the image to display properly, copy the `oshpark.png` file to your `$EAGLEDIR/scr` directory.


Copy `oshpark.ulp` to `$EAGLEDIR/ulp/`

Copy `oshpark.png` to the `bin/` folder where Eagle is installed. This is unfortunately where Eagle looks for menu images. 

### Edit Eagle.scr

Next is some quick editing to `$EAGLEDIR/scr/eagle.scr`. This file is what Eagle uses for it's startup configuration, and consists of a few menu commands. This file consists of several sections, split up into sections for various work interfaces in Eagle.

```
BRD:
# configure the board layout editor

SCH:
# configure the schematic layout editor

LIB:
LBR:
DEV:
SYM:
PAC:
# configure various library menus
```

To add a button, we'll use the `MENU` command. This is most helpful under `BRD:`, but you can add it under `SCH:` if you want. 

The simplest method is to simply add the following line after any existing `MENU` lines. Doing so will overwrite any previous Menu commands.

```
MENU ' [oshpark.png]Oshpark{Upload PCB: Run oshpark.ulp;}'
```

If you have other `MENU` items want to use, you can add it to the existing line.

```
MENU 'Text1:action1;'\
     'Text2:action2;'\
     '[oshpark.png]Oshpark{Upload PCB: Run oshpark.ulp;}'\
     ;
```
Note that you must use a `\` at the end of each line, and each command or block must have a space between them (in this example, the spaces are at the start of the line). More complex examples can be found in the `src` dir in your Eagle installation.

### Test the button!

Click it! 

If everything worked properly, you should see a link to oshpark, where we've started processing the board!
