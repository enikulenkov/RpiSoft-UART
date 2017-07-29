RpiSoft-UART
============

This driver will create a software-based serial port/UART using any GPIO pin, similiar to `/dev/tty*` devices, with some unique features.

### Features
* Works with <a href="http://en.wikipedia.org/wiki/Minicom">Minicom</a>
* Works with `cat` and `echo` commands
* 256 bytes RX buffer (read the data whenever you want, no data lost!)
* 256 bytes TX buffer (no need to send each byte separately, send the whole array once!)
* RX buffer cleared automatically after a read operation (Ex: `cat`)
* TX buffer cleared automatically after a write operation (Ex: `echo`)
* No pooling needed
* Loopback mode
* Runtime changeable parameters (GPIO pins, baudrate and loopback mode)

## Advanced
Just don't send more than 256 bytes at once and all must be ok, 256 is enough for most applications, but if you need more just change in the source code.

### Understanding the RX buffer
The driver have a 256 bytes RX buffer. This mean you can receive up to 256 bytes at once and they will be stored, without loss, if more bytes are received the buffer will be cleared and start store again. Any read operation at 'data' entry, will clear the buffer (Ex: `cat`). The buffer have only effect without the use of a software like `minicom` (because have it's own buffer, and due the pooling, keep the buffer clear).

### Understanding the TX buffer
The driver have a 256 bytes TX buffer. This mean you can send up to 256 bytes at once and they will be stored and transmitted until the last byte, clearing the buffer automatically. If more bytes than the buffer capacity is written, the buffer will clear and start store again. Any write operation at 'data' entry, will start the transmission (Ex: `echo`). The buffer have only effect without the use of a software like `minicom` (because transmit each byte separately, using just one byte of the TX buffer at time).

## License
GPLv2 License, details <a href="https://github.com/themrleon/RpiSoft-UART/blob/master/LICENSE">HERE</a>.
