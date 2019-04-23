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

