# REcon2025 - Exhuming EBC
## Back from the dead: Exhuming EBC   

This repo contains the slidedeck and PoCs presented at REcon 2025 for my talk "Back from the dead: Exhuming EBC"


 
## REcon2025 slidedeck          
### REcon2025 talk slidededeck is in the [REcon2024-slides-GOP-Complex](REcon2024-slides-GOP-Complex/) folder.            
 

## REcon2025 talk recording         
### REcon2025 talk recording video is available on Youtube here: [Recon 2025 - Back from the dead: Exhuming EBC](https://youtu.be/y2_3yuVc-wg?si=wIj2eNHnb-Nq1lM0)


## REcon2025 POC
## PoC will be made publicly available at some point in the future.  
The link for the POC will be added here when I make it public.

---         
# Talk description:
A spectre is haunting UEFI -- the spectre of EBC.
All the powers of old platform firmware landscapes have entered into a holy alliance to exorcise this spectre: lack of open-source (or any) compiler targeted for EBC, exceptional rarity of in-the-wild EBC binary samples, lack of any working/maintained debugging tools for EBC binaries, sparse and outdated documentation.

If EBC has been wholly exorcised though, why do I keep finding the EBCVM DXE driver in modern UEFI firmware images at a staggering rate?

Two things result from this fact:

In reconciling this apparent contradiction between a purported industry-wide UEFI exorcism and the persistent spectre of EBC, one arrives at two conclusions:

I. EBC is already acknowledged to be itself a power. Platform firmware supply chain vulnerabilities are a persistent and pervasive problem, and the continued use of outdated and deprecated components is a known path for successful exploits of this kind, particularly in UEFI. The EBCVM binary is present in a wide range of current UEFI firmware builds out there in the wild... and without the means of material EBC binaries to run, the EBCVM is a DXE driver collecting dust.
II. Someone ought to do something about that.

What's a malware witch to do?
How does one reverse engineer EBC binaries without available EBC-targeted tools? Or write an exploit in an assembly language with only a slim collection of fasm-targeted assembly source files for reference and no working debugger for EBC? Is thunking this season's hottest new sandbox escape technique??

This talk is the story of the long and arduous UEFI EBC xdev process, and presents the first UEFI exploits written in EBC/targeting the EBCVM as well as novel techniques in UEFI reverse engineering/exploit development. This talk is the continuation of the work showcased in my article in vx-underground Black Mass volume #3, scheduled for release in the upcoming month. Building upon the work from that research project, this talk is a deep dive into EBC, the internals of the EBCVM and exploring novel UEFI attack vectors/exploit chains that leverage the EBCVM. I will talk about the next stage of EBC xdev, including the following novel techniques that I developed for EBC vx
- compiling valid EBC binaries using a combination of open-source and custom tools
- debugging EBC binaries with qemu and gdb, without the use of the EBCDebugger DXE driver by targeting the EBCVM itself
- leveraging EBC and the EBCVM for UEFI malware including but not limited to PCI option ROM attacks, polymorphism, exploit primitives for SMM attack chains, and graphics.

Applicable to seasoned UEFI reverse engineers/exploit developers, and those interested in topics such as: reverse engineering binaries for an archaic/undocumented ISA, exploit development techniques relevant to VM/sandbox escapes, and much more.

This talk is the story of how I resurrected a nearly dead ISA in the UEFI spec, painstakingly wrote and debugged PoCs in EFI Byte Code, and cracked the secrets to developing platform-independent UEFI exploits with EBC.

EBC, or EFI Byte Code, is a platform agnostic intermediary language that leverages natural-indexing to automatically adjust its instruction width to either 32-bit or 64-bit dependent on the architecture of the host machine. It was designed as a specification for writing platform/architecture-agnostic PCI Option ROMs for UEFI firmware, with one of the goals being that IBV/OEMs could use EBC as a one-stop-shop for their PCI OpRom implementations.

The EFI Byte Code Virtual Machine (EBCVM) is a software virtual machine that runs in the UEFI pre-boot environment and is responsible for loading and executing EBC UEFI apps/drivers.

Despite EBC support being removed as a requirement of UEFI-compatible firmware not being a part of the official UEFI spec since approximately 2018, there is still a dedicated chapter for EBC and the EBCVM in the UEFI spec -- specifically Chapter 22. Moreover, while EBC binaries themselves are exceptionally rare in the wild, the EBCVM is still present in a wide range of current UEFI firmware builds.

This talk takes inspiration from a line in a Richard Siken poem: "I take the parts that I remember and stitch them back together to make a creature who will do what I say or love me back." It is the tale of a vx labor of love -- a UEFI reversing engineering/exploit development project with expansive scope and the goal of building PoCs for an entirely new category of UEFI exploits.

In Part 1, I will cover EBC fundamentals (registers, calling conventions, instruction format), internals of the EBCVM, existing protections for known EBC attack vectors (e.g. PCI OptionROM attacks). I will also introduce concepts relevant to novel exploits covered in Part 3; such concepts include SMM and existing SMM protections, DMA attacks and existing techniques targeting PCI-E peripherals.

In Part 2, I will cover challenges of the EBC UEFI xdev process, and the novel solutions that I developed including
- techniques for compiling valid EBC binaries using a combination of open-source and custom tools
- techniques for debugging EBC binaries with qemu and gdb, without the use of the EbcDebugger DXE driver
- techniques for leveraging the EBCVM for UEFI malware

In Part 3, I will cover results from my latest xdev research:
1. using my PoC -- the first EBC UEFI virus, a simple self-replicating UEFI app -- as a template for developing more complex, creative exploits.
2. Leveraging my new knowledge of EBC RE/xdev to write an EBC UEFI virus that performs graphics manipulation via the GOP (Graphics Output Protocol).
3. Explore uses of EBC and the EBCVM for novel UEFI malware development -- including but not limited to PCI option ROM attacks, polymorphism, exploit primitives for SMM attack chains, and graphics.
---

Hit me up with questions or feedback.

xoxo
ic3qu33n
