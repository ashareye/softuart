To use it   
====   
* put softuart.h & softuart.c into {your micropython's path}/esp8266/
* add "extern const mp_obj_type_t mp_softuart_type;"  to esp8266/modmachine.h   
* add "{ MP_ROM_QSTR(MP_QSTR_SOFTUART), MP_ROM_PTR(&mp_softuart_type) },"  to esp8266/modmachine.c after "{ MP_ROM_QSTR(MP_QSTR_UART...   
* add "softuart.c" to SRC_C of esp8266/Makefile   
* add "*softuart.o(.literal*, .text*)" to esp8266_common.ld after *machine_uart.o...   
* make it and flash to esp8266   
   
   
reset in micropython's REPL   
====   
```python
>>>from machine import SOFTUART;   
>>>s = SOFTUART(tx=14,rx=12,baudrate=115200)   # default tx=14,rx=12,baudrate=115200
>>>dir(s)  # show all method of softuart   
>>>s.put(0x0D)   
>>>s.write('abcdefg')   
>>>s.write(b'\x0D\xFF\xCC')   
>>>s.wait(10000)  	# wait rx for 10000us,default is 10000us 
>>>s.getcount()  	# rx buf available number   
>>>s.get()  		# pop a byte from rx buf, if none return 0   
>>>s.getall()  		# get all char available in rx buf, if None return None
>>>s.flush()  		# clear rx buf   
```