---
title: First Post
tags: [ python, visa, oscilloscope ]
layout: post
---

## Stuff and Things

This is the **first** post. Here's a capture from my oscilloscope.

![](/images/rigol_capture.png)

Which was acquired with the following Python script.

```python
import pyvisa

RIGOL = 'USB0::6833::1230::DS1ZA191806168::0::INSTR'
FILE = "rigol_capture.png"

rm = pyvisa.ResourceManager()
rigol = rm.open_resource(RIGOL, write_termination='\n', read_termination='\n')
raw_buf = rigol.query_binary_values(':DISP:DATA? ON,0,PNG', datatype='B')

with open(FILE, "wb") as fp:
    fp.write(bytearray(raw_buf))

print("Screen saved to", FILE)

rigol.close()
```

## Links to Things

- DS1000Z_Programming Guide_EN.pdf (just google for it)
- [PyVISA](https://pyvisa.readthedocs.io/en/latest/)
- [Virtual Instrument Software Architecture](https://en.wikipedia.org/wiki/Virtual_instrument_software_architecture)
- [Standard Commands for Programmable Instruments](https://en.wikipedia.org/wiki/Standard_Commands_for_Programmable_Instruments)
