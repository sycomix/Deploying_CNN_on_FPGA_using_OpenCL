# Deploying CNN on FPGA using OpenCL  
This is a project for 2017 Innovate FPGA design contest. We hope this project can somehow help those who want to accelerate CNN on resouce-limited embedded systems with FPGA using OpenCL. Origin project link: [*PR065*](http://www.innovatefpga.com/cgi-bin/innovate/teams.pl?Id=PR065).
## Prerequisites:  
- Board: Terasic [*DE10-Nano*](http://www.terasic.com.tw/cgi-bin/page/archive.pl?Language=English&CategoryNo=167&No=1046) with Cyclone V SoC-FPGA (800MHz Dual-core Cortex-A9 processor & 110K LEs FPGA)
- Software: Intel FPGA SDK for OpenCL 17.1  
## System diagram:  
![System diagram](https://github.com/Er1cZ/Deploying_CNN_on_FPGA_using_OpenCL/raw/master/pic/sys.PNG)
## To use:
- Copy 2 files in `/bin/v1.3` folder & `/src/common/synset_words.txt` to `/your_path` on the TF card for DE10-Nano with Terasic Offical OpenCL BSP image
- Set up UART connection between DE10-Nano and PC
- Login as root
- Type in commands:
  - `cd ~`
  - `source ./init_opencl.sh`
  - `cd /your_path/`
  - `aocl program /dev/acl0 squeezenet.aocx`
  - `chmod +x squeezenet`
  - `./squeezenet`  

Input image:  

<img src="https://github.com/Er1cZ/Deploying_CNN_on_FPGA_using_OpenCL/raw/master/pic/dog.jpg" width="400px"/> 

Result should be like this: 
```
SqueezeNet on FPGA start:
kernel version 1.3

conv1 takes: 68.119 ms
block1 takes: 117.038 ms
block2 takes: 157.159 ms
block3 takes: 250.102 ms
classifier takes: 399.102 ms
total: 991.522 ms

predicted label: n02106662 German shepherd, German shepherd dog, German police dog, alsatian

done
```  
Resource usage:  
```
+--------------------------------------------------------------------+
; Estimated Resource Usage Summary                                   ;
+----------------------------------------+---------------------------+
; Resource                               + Usage                     ;
+----------------------------------------+---------------------------+
; Logic utilization                      ;   102%                    ;
; ALUTs                                  ;   68%                     ;
; Dedicated logic registers              ;   40%                     ;
; Memory blocks                          ;   106%                    ;
; DSP blocks                             ;   58%                     ;
+----------------------------------------+---------------------------;  
```
This is a simple and relatively naive implement. We barely found any tutorials and suffered a lot from getting started on this topic. So we decide to make this project more like a getting started tutorial.  

**For more details, please read** [*A getting started tutorial on FPGA implement of CNN using OpenCL*](https://github.com/Er1cZ/Deploying_CNN_on_FPGA_using_OpenCL/blob/master/GettingStartedTutorial.md).
