add "extern const mp_obj_type_t mp_softuart_type;"  to modmachine.h 
add "{ MP_ROM_QSTR(MP_QSTR_SOFTUART), MP_ROM_PTR(&mp_softuart_type) },"  to modmachine.c after "{ MP_ROM_QSTR(MP_QSTR_UART...
add "softuart.c" to SRC_C of esp8266/Makefile
add "*softuart.o(.literal*, .text*)" to esp8266_common.ld after *machine_uart.o...

then make it and reset in micropython's REPL 
	from machine import SOFTUART; 
	s = SOFTUART(tx=14,rx=12,baudrate=115200)
	dir(s)  # show all method of softuart 
	s.put(0x0D)
	s.write('abcdefg')
	s.write(b'\x0D\xFF\xCC')
	s.wait(10000)  # wait rx for 10000us
	s.available()  # rx buf available
	s.get()  # pop a byte from rx buf, if none return 0
	s.flush()  # clear rx buf
