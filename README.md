# Simple Bootloader

>[!NOTE]
>Originally, I this project was to help me learn Assembly and it was a pretty cool way of learning
>
>Take this as a "DO NOT INGEST" sign on toxic waste.
>
>This is in no way meant to replace your EFI System of your Bootloader.
>
>Replacing your EFI System Partition with this will most likely brick your motherboard.
>
>So, if you value your laptop or PC, please don't replace your Bootloader with this one.
>
>If you wanna replace your bootloader and patch the IME or PHP in your CPU, try [Coreboot](https://coreboot.org/) or [Libreboot](https://libreboot.org/)
>
>If you wanna replace your bootloader with this, by making this READTHIS.md, I absolve myself over all responsibility.
>
>This software is provided as-is without any liability. For More Info check the [MIT LICENSE](https://opensource.org/license/mit)
 

This is a tiny, fully working "bootloader" for x86 IBM-PC computers, which basically does nothing more than print some text to the screen.
Mostly a learning tool, I made it to help learn kernel and low-level hardware programming.

# Description

When a computer boots up, the job of getting from nothing to a functioning operating system involves a number of steps. The first thing that happens on an x86 PC is the operation of the BIOS. We'll eschew the discussion of the intricacies of how the BIOS works, but here's what you need to know. When you turn your computer on, the processor immediately looks at physical address 0xFFFFFFF0 for the BIOS code, which is generally on some read-only piece of ROM somewhere in your computer. The BIOS then POSTs, and searches for acceptable boot media. The BIOS accepts some medium as an acceptable boot device if its boot sector, the first 512 bytes of the disk are readable and end in the exact bytes 0x55AA, which constitutes the boot signature for the medium. If the BIOS deems some drive bootable, then it loads the first 512 bytes of the drive into memory address 0x007C00, and transfers program control to this address with a jump instruction to the processor.

Most modern BIOS programs are pretty robust, for example, if the BIOS recognizes several drives with appropriate boot sectors, it will boot from the one with the highest pre-assigned priority; which is exactly why most computers default to booting from USB rather than hard disk if a bootable USB drive is inserted on boot.

Typically, the role of the boot sector code is to load a larger, "real" operating system stored somewhere else on non-volatile memory. In actuality, this is a multi-step process. For example, Master Boot Record, or MBR, is a very common (though now becoming more and more deprecated) boot sector standard for partioned storage devices. Since the boot sector may contain a maximum of 512 bytes of data, an MBR bootloader often simply does the job of passing control to a different, larger bootloader stored somewhere else on disk, whose job in turn is to actually load the operating system (chain-loading). Right now, though, we won't concern ourselves with all this; the goal here isn't to write an operating system (saving that one for another post), but just to get the computer to spit something out onto the screen of our choosing.

It's boring stuff. If you just want to see it in action though, just run

     bochs -f bochsrc.txt

which runs bochs with the correct config file.
