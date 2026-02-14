# EE Memory Map

## Virtual/Physical Memory
```
  KUSEG: 00000000h-7FFFFFFFh User segment
  KSEG0: 80000000h-9FFFFFFFh Kernel segment 0
  KSEG1: A0000000h-BFFFFFFFh Kernel segment 1
  KSSEG: C0000000h-DFFFFFFFh Supervisor segment
  KSEG3: E0000000h-FFFFFFFFh Kernel segment 3
  
  Virtual    Physical
  00000000h  00000000h  32 MB    Main RAM (first 1 MB reserved for kernel)
  20000000h  00000000h  32 MB    Main RAM, uncached
  30100000h  00100000h  31 MB    Main RAM, uncached and accelerated
  10000000h  10000000h  64 KB    I/O registers
  11000000h  11000000h  4 KB     VU0 code memory
  11004000h  11004000h  4 KB     VU0 data memory
  11008000h  11008000h  16 KB    VU1 code memory
  1100C000h  1100C000h  16 KB    VU1 data memory
  12000000h  12000000h  8 KB     GS privileged registers
  1C000000h  1C000000h  2 MB     IOP RAM
  1FC00000h  1FC00000h  4 MB     BIOS, uncached (rom0)
  9FC00000h  1FC00000h  4 MB     BIOS, cached (rom09)
  BFC00000h  1FC00000h  4 MB     BIOS, uncached (rom0b)
  70000000h  ---------  16 KB    Scratchpad RAM (only accessible via virtual addressing)

EE RAM is reportedly expandable up to 256 MB. However, the maximum seen in practice is 128 MB, for special TOOL consoles.
```

## MMIO
```
EE Timers

  100000xxh        Timer 0
  100008xxh        Timer 1
  100010xxh        Timer 2
  100018xxh        Timer 3

Image Processing Unit (IPU)

  10002000h 8h     IPU Command
  10002010h 4h     IPU Control
  10002020h 4h     IPU bit pointer control
  10002030h 8h     Top of bitstream
  10007000h 10h    Out FIFO (read)
  10007010h 10h    In FIFO (write)

Graphics Interface (GIF)

  10003000h 4h     GIF_CTRL - Control register
  10003010h 4h     GIF_MODE - Mode setting
  10003020h 4h     GIF_STAT - Status
  10003040h 4h     GIF_TAG0 - Bits 0-31 of tag before
  10003050h 4h     GIF_TAG1 - Bits 32-63 of tag before
  10003060h 4h     GIF_TAG2 - Bits 64-95 of tag before
  10003070h 4h     GIF_TAG3 - Bits 96-127 of tag before
  10003080h 4h     GIF_CNT - Transfer status counter
  10003090h 4h     GIF_P3CNT - PATH3 transfer status counter
  100030A0h 4h     GIF_P3TAG - Bits 0-31 of PATH3 tag when interrupted
  10006000h 10h    GIF FIFO

DMA Controller (DMAC)

  100080xxh        VIF0 - channel 0
  100090xxh        VIF1 - channel 1
  1000A0xxh        GIF - channel 2
  1000B0xxh        IPU_FROM - channel 3
  1000B4xxh        IPU_TO - channel 4
  1000C0xxh        SIF0 - channel 5
  1000C4xxh        SIF1 - channel 6
  1000C8xxh        SIF2 - channel 7
  1000D0xxh        SPR_FROM - channel 8
  1000D4xxh        SPR_TO - channel 9
  1000E000h 4h     D_CTRL - DMAC control
  1000E010h 4h     D_STAT - DMAC interrupt status
  1000E020h 4h     D_PCR - DMAC priority control
  1000E030h 4h     D_SQWC - DMAC skip quadword
  1000E040h 4h     D_RBSR - DMAC ringbuffer size
  1000E050h 4h     D_RBOR - DMAC ringbuffer offset
  1000E060h 4h     D_STADR - DMAC stall address
  1000F520h 4h     D_ENABLER - DMAC disabled status
  1000F590h 4h     D_ENABLEW - DMAC disable

Interrupt Controller (INTC)

  1000F000h 4h     INTC_STAT - Interrupt status
  1000F010h 4h     INTC_MASK - Interrupt mask

Subsystem Interface (SIF)

  1000F200h 4h     MSCOM - EE->IOP communication
  1000F210h 4h     SMCOM - IOP->EE communication
  1000F220h 4h     MSFLAG - EE->IOP flags
  1000F230h 4h     SMFLAG - IOP->EE flags
  1000F240h 4h     Control register

Privileged GS registers

  12000000h 8h     PMODE - various PCRTC controls
  12000010h 8h     SMODE1
  12000020h 8h     SMODE2
  12000030h 8h     SRFSH
  12000040h 8h     SYNCH1
  12000050h 8h     SYNCH2
  12000060h 8h     SYNCV
  12000070h 8h     DISPFB1 - display buffer for output circuit 1
  12000080h 8h     DISPLAY1 - output circuit 1 control
  12000090h 8h     DISPFB2 - display buffer for output circuit 2
  120000A0h 8h     DISPLAY2 - output circuit 2 control
  120000B0h 8h     EXTBUF
  120000C0h 8h     EXTDATA
  120000D0h 8h     EXTWRITE
  120000E0h 8h     BGCOLOR - background color
  12001000h 8h     GS_CSR - control register
  12001010h 8h     GS_IMR - GS interrupt control
  12001040h 8h     BUSDIR - transfer direction
  12001080h 8h     SIGLBLID - signal

Misc registers

  1000F180h 1h     KPUTCHAR - Console output
  1000F430h 4h     MCH_DRD - RDRAM initialization
  1000F440h 4h     MCH_RICM


```

