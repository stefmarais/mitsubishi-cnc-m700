# mitsubishi-cnc-m700
Python sample for communication with Mitsubishi Electric CNC M700 series using EZSocket.

It works by using COM object in Windows environment.

Please use as a hint when implementing in your own environment.

# Implementation function
-Reading and writing values ​​to D and M devices
-Acquisition of information such as NC status, tool number and rotation speed
-Directory search and file operations in NC (read / write / delete)

# Reference information

## The following Mitsubishi CNC communication software development kit is required in a Windows environment.
http://www.mitsubishielectric.co.jp/fa/download/software/detailsearch.do?mode=software&kisyu=/cnc&shiryoid=0000000030&lang=1&select=0&softid=1&infostatus=3_11_2&viewradio=0&viewstatus=&viewpos=

### Mitsubishi CNC Communication Software FCSB1224W000 Reference Manual
http://www.mitsubishielectric.co.jp/fa/document/others/cnc/ib-1501208/IB-1501208.pdf

### How to pass a VARIANT type argument from Python to COM
http://docs.activestate.com/activepython/3.4/pywin32/html/com/win32com/HTML/variant.html
https://mail.python.org/pipermail/python-win32/2012-October/012575.html

### pythoncom.VT_VARIANT type list
http://nullege.com/codes/search/pythoncom.VT_VARIANT


# How to use

```
from m700 import M700

# Open connection
m700 = M700.get_connection ('192.168.1.10:683') #683 is the default port for Mitsubishi M70 CNC controllers

# Get information in NC
m700.get_drive_infomation ()
m700.get_run_status ()
m700.get_alarm ()

# Operation on D device
m700.write_dev ('M900', 1)
m700.read_dev ('M900') #-> 1

# Operations on M device
m700.write_dev ('D200', 10)
m700.read_dev ('D200') #-> 10

# Manipulate machining program files (read / write / delete)
drivenm = m700.get_drive_infomation ()
m700.write_file (drivenm + '\ PRG \ USER \ __ TEST __. txt', b'TEST_WRITE ')
m700.read_file (drivenm + '\ PRG \ USER \ __ TEST __. txt')
m700.delete_file (drivenm + '\ PRG \ USER \ __ TEST __. txt')

# Close connection
m700.close ()
```
[TODO] 
* Update tests to include changes made
* Complete translations
