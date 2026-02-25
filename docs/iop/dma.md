# DMA 

### DMA Control Register Summary
| Register | Address | Access  | Description |
|---|---|---|---|
| DPCR1     | 0x1F8010F0 | RW | Priority/Enable (channels 1 - 6) |
| DPCR2     | 0x1F801570 | RW | Priority/Enable (channels 7 - 12) |
| DICR1     | 0x1F8010F4 | RW | Interrupt control (1) |
| DICR2     | 0x1F801574 | RW | Interrupt control (2) |
| DMACEN    | 0x1F801578 | RW | Global DMA enable switch |
| DMACINTEN | 0x1F80157C | RW | Global DMA Interrupt control |


## DMA Channels
| Channel | Base Address | Description |
|---|---|---|
| 0  | 0x1F801080 | MDEC (in)    |
| 1  | 0x1F801090 | MDEC (out)   |
| 2  | 0x1F8010A0 | SIF2/PGIF    |
| 3  | 0x1F8010B0 | CDVD         |
| 4  | 0x1F8010C0 | SPU (core 0) |
| 5  | 0x1F8010D0 | PIO          |
| 6  | 0x1F8010E0 | OTC          |
| 7  | 0x1F801500 | SPU (core 1) |
| 8  | 0x1F801510 | DEV9         |
| 9  | 0x1F801520 | SIF0         |
| 10 | 0x1F801530 | SIF1         |
| 11 | 0x1F801540 | SIO2 (in)    |
| 12 | 0x1F801550 | SIO2 (out)   |

### DMA Channel Register Summary
| Register  | Address  |  Access | Description |
|---|---|---|---|
| MADR | 0x0 | RW | Current RAM address |
| BCR  | 0x4 | RW | Block size  |
| CHCR | 0x8 | RW | Channel control register  |
| TADR | 0xc | RW | Tag address |
