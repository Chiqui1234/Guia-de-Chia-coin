Para comprobar el estado de algún dispositivo de almacenamiento (HDD, SSD, SSD NVME y otros con soporte para S.M.A.R.T), debés tener instalado **smartmontools**.

```bash
sudo apt install smartmontools -y
```

## Listar almacenamientos disponibles

Después, con el siguiente comando verás todo el almacenamiento presente en tu sistema Linux:

```bash
sudo fdisk -l
```

## Activar S.M.A.R.T (opcional

Puede suceder que *smartctl* indique que el acceso al chip S.M.A.R.T no sea posible desde Linux, pero puede probar activarse con:

```bash
smartctl -s on -a /dev/nombreDelDispositivo
```

## Acceder al S.M.A.R.T

Una vez que identifiques tu disco (en mi caso, es un NVME listado como /dev/nvme0n1p1), ejecutá smartctl de la siguiente forma:

```bash
sudo smartctl -a /dev/nombreDelDispositivo
```

El log (resumido) de mi NVME es el siguiente, lo dejo a modo de ejemplo:

```bash
 santiago@PC-PINNACLE1:~$ sudo smartctl -a /dev/nvme0n1p1                                          
smartctl 6.6 2017-11-05 r4594 [x86_64-linux-4.19.0-16-amd64] (local build)                            
Copyright (C) 2002-17, Bruce Allen, Christian Franke, www.smartmontools.org                           

=== START OF INFORMATION SECTION ===
Model Number:                       ADATA FALCON
Serial Number:                      2L022LAKN9XC
Firmware Version:                   V9002s69
PCI Vendor/Subsystem ID:            0x10ec
IEEE OUI Identifier:                0x00e04c
Controller ID:                      1
Number of Namespaces:               1
Namespace 1 Size/Capacity:          512.110.190.592 [512 GB]                                          
Namespace 1 Formatted LBA Size:     512
Local Time is:                      Tue May  4 20:53:05 2021 -03                                      
Firmware Updates (0x02):            1 Slot
Optional Admin Commands (0x0007):   Security Format Frmw_DL                                           
Optional NVM Commands (0x0014):     DS_Mngmt Sav/Sel_Feat                                             
Maximum Data Transfer Size:         32 Pages
Warning  Comp. Temp. Threshold:     115 Celsius
Critical Comp. Temp. Threshold:     120 Celsius

=== START OF SMART DATA SECTION ===
SMART overall-health self-assessment test result: PASSED                                              

SMART/Health Information (NVMe Log 0x02, NSID 0x1)
Critical Warning:                   0x00
Temperature:                        31 Celsius
Available Spare:                    100%
Available Spare Threshold:          32%
Percentage Used:                    0%
Data Units Read:                    1.646.749 [843 GB]                                                
Data Units Written:                 1.817.651 [930 GB]                                                
Host Read Commands:                 6.583.650
Host Write Commands:                7.234.343
Controller Busy Time:               0
Power Cycles:                       6
Power On Hours:                     4
Unsafe Shutdowns:                   1
Media and Data Integrity Errors:    0
Error Information Log Entries:      0
Warning  Comp. Temperature Time:    0
Critical Comp. Temperature Time:    0
```

¡Listo!
