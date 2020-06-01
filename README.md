# Manually-booting-the-Linux-kernel-from-GRUB
BOOTING :
        In computing, booting (also known as a boot-up) is the initial set of operations that a computer system performs after being turned on. When the machine finishes it's Power-On Self-Test (POST), it will look for instructions on how to actually load your Operating System. In the case of a hard disk (which is most common), it will load the code found in the Master Boot Record (MBR), which will generally locate and load the operating system's "Boot Loader" into memory. In the case here, the boot loader is GRUB. The boot loader is then responsible for preping and starting the Operating System.

HOW DOES IT WORK :
        The GRand Unified Bootloader (GRUB) was initially developed as a boot loader for the GNU/Hurd project. There are two versions of GRUB in common use, though GRUB version 2 is now used by most distributions (and will be the focus here). GRUB will check it's configs for the location of the requested kernel and attempt to load (or strap) that image into memory. Once loaded, GRUB will pass parameters (if any) and transfer control to the kernel. The kernel will then load both the default configuration file and any other modules needed.
 
 SO HOW DO WE FIX IT WHEN THINGS GO WRONG:
        Manually booting your operating system from GRUB is actually pretty easy once you know what you need to do. Before trying to actually do anything with GRUB, you should examine what GRUB can actually see in your system. For starters, if you can see the GRUB prompt you know that the MBR is intact, and that GRUB has been properly loaded into memory. Great! Now let's poke around and see which disks may be visible to GRUB. You can start by using the ls command.
        
   grub> ls
   
All of our partitions are showing up here (yours may look slightly different, depending on how things are partitioned). Since it can see our boot volume, let's actually tell it to use that.

   grub>linux (hd0,6)/boot/vmlinuz root = /dev/sda6
   
Now we can tell it to load or kernel image. (Just note that you must put in the full filename of the image. You can use TAB completion here to help you, especially if you don't remember the name of the file.)

   grub>initrd (hd0,6)/boot/initrd
   
Next, we need to tell the kernel where it can find it's initialization RAM disk (initrd).

   grub>boot
   
Finally, you can go ahead and boot your system.
    
