# SIO2

The Playstation 2 uses SPI to talk to memory cards and controller port peripherals, SIO2 is the controller in charge of this task.

Because the transmit and receive pins are pulled high on the board, reads from an empty slot will return 0xff.


### SIO2 Register Summary

| Register  | Address  | Access  | Description  |
|---|---|---|---|
| SIO2_MEM_FIFO_TX |  0x1f808000 |  RW  |  256 byte transmit FIFO |
| SIO2_MEM_FIFO_RX |  0x1f808100 |  RW  |  256 byte receive FIFO |
| SIO2_REG_CMD_QUEUE |  0x1f808200 |  RW  |  16 entry command queue |
| SIO2_REG_PORT0_CTRL0 |	0x1f808240	| RW | Controller 0 |
| SIO2_REG_PORT0_CTRL1 |	0x1f808244	| RW | Controller 0  |
| SIO2_REG_PORT1_CTRL0 |	0x1f808248	| RW | Controller 1  |
| SIO2_REG_PORT1_CTRL1 |	0x1f80824c	| RW | Controller 1  |
| SIO2_REG_PORT2_CTRL0 |	0x1f808250	| RW | Memory card 0 |
| SIO2_REG_PORT2_CTRL1 |	0x1f808254	| RW | Memory card 0 |
| SIO2_REG_PORT3_CTRL0 |	0x1f808258	| RW | Memory card 1 |
| SIO2_REG_PORT3_CTRL1 |	0x1f80825c	| RW | Memory card 1 |
| SIO2_REG_TX | 0x1f808260 | W | 8/16/32-bit transmit |
| SIO2_REG_RX | 0x1f808264 | R | 8/16/32-bit receive |
| SIO2_REG_CTRL | 0x1f808268 | RW | Control register |
| SIO2_REG_CMD_STAT | 0x1f80826c | R | Command status |
| SIO2_REG_PORT_STAT | 0x1f808270 | R | Port status |
| SIO2_REG_FIFO_STAT | 0x1f808274 | R | FIFO status |
| SIO2_REG_FIFO_TX | 0x1f808278 | RW | TX FIFO head and tail position |
| SIO2_REG_FIFO_RX | 0x1f80827c | RW | RX FIFO head and tail position |
| SIO2_REG_IRQ_STAT | 0x1f808280 | RW | Interrupt status |
| SIO2_REG_REMOTE_CTRL | 0x1f808284 | RW | For IOP rev >= 0x23 |

------------------------
## SIO2 Register Definitions

### Transmit Memory (SIO2_MEM_FIFO_TX) & Receive Memory (SIO2_MEM_FIFO_RX)
Storage for the contents of the TX/RX FIFO's is viewable at address 0x1f808000.

### Command Queue (SIO2_REG_CMD_QUEUE)
A 16 entry queue of commands to be executed.

Each entry is cleared to zero by the controller on reset.

wavedrom (
    {reg: [
        {bits: 2,  name: 'port', rotate: -90},
        {bits: 1,  name: 'pause', rotate: -90},
        {bits: 1},
        {bits: 1,  name: 'tx_dma', rotate: -90},
        {bits: 1,  name: 'rx_dma', rotate: -90},
        {bits: 2,  name: 'cfg'},
        {bits: 9,  name: 'tx_size'},
        {bits: 1},
        {bits: 9,  name: 'rx_size'},
        {bits: 3},
        {bits: 1,  name: 'clk_div', rotate: -90},
        {bits: 1,  name: 'ackwait', rotate: -90},
    ], config:{lanes: 1, vspace: 90}}
)

| Bits  | Name | Description |
|---|---|---|
| [31]    |   |   |
| [30]    | clk_div | Selects which divider from PORT_CTRL0 to use. | 
| [26:18] | rx_size  | Number of bytes to read into the RX FIFO  |
| [16:8]  | tx_size  | Number of bytes to read into the TX FIFO  |
| [7:6]   |   |   |
| [5]     |   |   |
| [4]     |   |   |
| [2]     | Pause | Pause after executing, resumed by CTRL RESUME |
| [1:0]   | Port  | Destination peripheral port |


A command with TX and RX size both at zero terminates the sequence of commands.


### Port Control 0 (SIO2_REG_PORT[0-3]_CTRL0)
wavedrom (
    {reg: [
    {bits: 8,  name: 'att_inactive'},
    {bits: 8,  name: 'att_active'},
    {bits: 8,  name: 'baud_div0'},
    {bits: 8,  name: 'baud_div1'},
    ], config:{}}
)

### Port Control 1 (SIO2_REG_PORT[0-3]_CTRL1)
wavedrom (
    {reg: [
    {bits: 16, name: 'sck_active'},
    {bits: 8,  name: 'sck_inactive'},
    {bits: 1},
    {bits: 1,  name: 'mode', rotate: -90},
    {bits: 6},
    ], config:{vspace: 70}}
)

### Transmit (SIO2_REG_TX) & Receive (SIO2_REG_RX)

### Control register (SIO2_REG_CTRL)
wavedrom (
    {reg: [
    {bits: 1, name: 'start', rotate: -90},
    {bits: 1,  name: 'resume', rotate: -90},
    {bits: 1,  name: 'reset', rotate: -90},
    {bits: 1,  name: 'reset_fifo', rotate: -90},
    {bits: 1,  name: 'timeout_en', rotate: -90},
    {bits: 1,  name: 'error_cont', rotate: -90},
    {bits: 1},
    {bits: 1},
    {bits: 1,  name: 'err_irq', rotate: -90},
    {bits: 1,  name: 'tx_irq', rotate: -90},
    {bits: 20},
    {bits: 1,  name: 'ps1'},
    {bits: 1,  name: 'dir'},
    ], config:{vspace:100}}
)

With error_cnt set the controller ignores errors and executes all commands regardless.


### Command status (SIO2_REG_CMD_STAT)
wavedrom (
    {reg: [
    {bits: 4},
    {bits: 1,  name: 'need_tx', rotate: -90},
    {bits: 1,  name: 'need_rx', rotate: -90},
    {bits: 2},
    {bits: 4,  name: 'index'},
    {bits: 1,  name: 'ready', rotate: -90},
    {bits: 1,  name: 'error', rotate: -90},
    {bits: 1,  name: 'flow_err', rotate: -90},
    {bits: 1,  name: 'ack_miss', rotate: -90},
    {bits: 16,  name: 'queue_errors'},
    ], config:{vspace:90}}
)

### Port status (SIO2_REG_PORT_STAT)
These correspond directly to pins on the IOP. Only the SAS[0-1] traces are connected to the controller ports, and only on fat PS2's, these are all supposedly tied high on later hardware.

wavedrom (
    {reg: [
    {bits: 1,  name: 'CDC0', rotate: -90},
    {bits: 1,  name: 'CDC1', rotate: -90},
    {bits: 1,  name: 'CDC2', rotate: -90},
    {bits: 1,  name: 'CDC3', rotate: -90},
    {bits: 1,  name: 'SAS0', rotate: -90},
    {bits: 1,  name: 'SAS1', rotate: -90},
    {bits: 1,  name: 'SAS2', rotate: -90},
    {bits: 1,  name: 'SAS3', rotate: -90},
    {bits: 24},
    ], config:{vspace:100}}
)

### FIFO status (SIO2_REG_FIFO_STAT)
wavedrom (
{   reg: [
    {bits: 9, name: 'tx_size'},
    {bits: 1},
    {bits: 1,  name: 'tx_full', rotate: -90},
    {bits: 1,  name: 'tx_empty', rotate: -90},
    {bits: 4},
    {bits: 9,  name: 'rx_size'},
    {bits: 1},
    {bits: 1,  name: 'rx_full', rotate: -90},
    {bits: 1,  name: 'rx_empty', rotate: -90},
    {bits: 4},
    ], config:{vspace:90}}
)

### FIFO position (SIO2_REG_FIFO[TX|RX])
wavedrom (
    {reg: [
    {bits: 8, name: 'head'},
    {bits: 8},
    {bits: 8,  name: 'tail'},
    {bits: 8},
    ], config:{}}
)

### Interrupt status (SIO2_REG_IRQ_STAT)
Set to clear.

Controller reset does not clear these bits.

wavedrom (
    {reg: [
    {bits: 1, name: 'tx', rotate: -90},
    {bits: 1,  name: 'error', rotate: -90},
    {bits: 30},
    ], config:{vspace:90}}
)
