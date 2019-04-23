# IN APPLICATION PROGRAMMING
this code implements a very simple version of a bootloader on chip with little differences, you can follow the documentation [here](https://www.st.com/content/ccc/resource/technical/document/application_note/51/5f/03/1e/bd/9b/45/be/CD00264342.pdf/files/CD00264342.pdf/jcr:content/translations/en.CD00264342.pdf) & [here](https://www.st.com/content/ccc/resource/technical/document/application_note/b9/9b/16/3a/12/1e/40/0c/CD00167594.pdf/files/CD00167594.pdf/jcr:content/translations/en.CD00167594.pdf)

## first starting with peripherals used in this code & it's configurations 
### RCC
* HSE-crstal/ceramic resonator 
* 25 MHZ input frequency
* no RCC interrupts

**please refer to .ioc file and look for clock configurations to set any clock you prefer also notice that UART have issues with selecting baud-rates with low clocks so keep your clock as high as possible which consumes more power please refer to datasheet to know more about baudrate error persentage with each clock avvailable**

### UART 
* 115200 baudrate -bit/sec which means 14400 byte/sec
* 8-databits
* 1-stop bit
* No-parity bits
![github-small](https://drive.google.com/drive/u/2/my-drive)
##Description
this code starts with configuring all clocks for used peripherals then send sentence to ESP **STARTFLASH** which will wait for it after reseting the STM and for blocking section uart will wait on buffer for about **4 secs** to receive **"OK"** to start flashing, otherwise it will jumb to firmware and for flashing it take length of the section that is going to be writen to flash then take data **252 bytes** each multiple of **4** then flashes them to memory **4-bytes by 4-bytes** then sends "OK" indicating successful operation and so on till finishing .bin file then sends **0x00** for data length to jump to **user code (Firmware)**.
Jump function itself checks if the first byte in which it will jumb contains the SP if not it will not do any thing
the data received from uart located in Stack which is 20K so the maximum length you can flash at a time is less than 20K also for that you have to change the length bytes to allow that size.
