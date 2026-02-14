# IOP Memory Map

## Physical Memory
```
  KUSEG: 00000000h-7FFFFFFFh User segment
  KSEG0: 80000000h-9FFFFFFFh Kernel segment 0
  KSEG1: A0000000h-BFFFFFFFh Kernel segment 1
  
  Physical
  00000000h  2 MB     Main RAM (same as on PSX)
  1D000000h           SIF registers
  1F800000h  64 KB    Various I/O registers
  1F900000h  1 KB     SPU2 registers
  1FC00000h  4 MB     BIOS (rom0) - Same as EE BIOS
  
  FFFE0000h (KSEG2)   Cache control
```

## MMIO 
```
Subsystem Interface (SIF)

  1D000000h 4h     MSCOM - EE->IOP communication
  1D000010h 4h     SMCOM - IOP->EE communication
  1D000020h 4h     MSFLAG - EE->IOP flags
  1D000030h 4h     SMFLAG - IOP->EE flags
  1D000040h 4h     Control register

CDVD Drive

  1F402004h 1h     Current N command
  1F402005h 1h     N command status (R)
  1F402005h 1h     N command params (W)
  1F402006h 1h     Error
  1F402007h 1h     Send BREAK command
  1F402008h 1h     CDVD I_STAT - interrupt register
  1F40200Ah 1h     Drive status
  1F40200Fh 1h     Disk type
  1F402016h 1h     Current S command
  1F402017h 1h     S command status
  1F402018h 1h     S command params

Interrupt Control

  1F801070h 4h     I_STAT - Interrupt status
  1F801074h 4h     I_MASK - Interrupt mask
  1F801078h 1h     I_CTRL - Global interrupt disable

DMA registers

  1F80108xh        MDECin - channel 0
  1F80109xh        MDECout - channel 1
  1F8010Axh        SIF2 (GPU) - channel 2
  1F8010Bxh        CDVD - channel 3
  1F8010Cxh        SPU2 Core0 - channel 4
  1F8010Dxh        PIO - channel 5
  1F8010Exh        OTC - channel 6
  1F80150xh        SPU2 Core1 - channel 7
  1F80151xh        DEV9 - channel 8
  1F80152xh        SIF0 - channel 9
  1F80153xh        SIF1 - channel 10
  1F80154xh        SIO2in - channel 11
  1F80155xh        SIO2out - channel 12
  
  1F8010F0h 4h     DPCR - DMA priority control
  1F8010F4h 4h     DICR - DMA interrupt control
  1F801570h 4h     DPCR2 - DMA priority control 2
  1F801574h 4h     DICR2 - DMA priority control 2
  1F801578h 4h     DMACEN - DMA global enable
  1F80157Ch 4h     DMACINTEN - DMA global interrupt control

IOP Timers

  1F80110xh        Timer 0
  1F80111xh        Timer 1
  1F80112xh        Timer 2
  1F80148xh        Timer 3
  1F80149xh        Timer 4
  1F8014Axh        Timer 5

Serial Interface (SIO2)

  1F808200h 40h    SEND3 buffer
  1F808240h 20h    SEND1/2 buffers
  1F808260h 1h     In FIFO
  1F808264h 1h     Out FIFO
  1F808268h 4h     SIO2 control
  1F80826Ch 4h     RECV1
  1F808270h 4h     RECV2
  1F808274h 4h     RECV3

Sound Processing Unit (SPU2)

  1F900000h 180h   Core0 Voice 0-23 registers
  1F900190h 4h     Key ON 0/1
  1F900194h 4h     Key OFF 0/1
  1F90019Ah 2h     Core attributes
  1F90019Ch 4h     Interrupt address H/L
  1F9001A8h 4h     DMA transfer address H/L
  1F9001ACh 2h     Internal transfer FIFO
  1F9001B0h 2h     AutoDMA status
  1F9001C0h 120h   Core0 Voice 0-23 start/loop/next addresses
  1F900340h 4h     ENDX 0/1
  1F900344h 2h     Status register
  
  ... above addresses repeat for Core1 starting at 1F900400h ...
  
  1F900760h 2h     Master Volume Left
  1F900762h 2h     Master Volume Right
  1F900764h 2h     Effect Volume Left
  1F900766h 2h     Effect Volume Right
  1F900768h 2h     Core1 External Input Volume Left
  1F90076Ah 2h     Core1 External Input Volume Right
```
