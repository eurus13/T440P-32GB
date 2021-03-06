# T440P-32GB

Work on getting the Thinkpad T440P to boot with 32gb ram (16gb x 2) 

<sup></sup>

## NOTES:

* Haswell(HSW) mobile chips(CPU and Cache) are capable of addressing ore than 32GB<sup>[1]</sup>

* QM87 chipset also capable of addressing more than 16GB<sup>[2]</sup><sup>[3]</sup>

* HSW MRC Addressing Decoding functions were missing bitshift[1<<28] and row/col[11]<sup>[4]</sup> info for 8Gbit,16GB modules
  
 * CAP REG(Capabilities Register) lists HSW col_11 support, but it is not enabled [commented out "SUPPORT" flag] 
  
   ** CAP REG also has setting that allows 16GB modules (it was set by default, but may not be on other machines"
  
   ** CAP REG has ability to enable DDR3L<sup>[5]</sup> voltage at 1.3V rather than DDR3 1.5V,( did not enable, just noting)
  
   ** CAP Memory Controller (MC) is set at 32bit offset limit for physical addresses(bit setting - 0xe4), 
        there is note of 64bit capabilites(bit setting - 0xf4); seemingly as it stands anything above 
        4GB( 8,16, or 32GB) would mapped pages and not physically allocated and addressed memory. 

 

  Please Note(Gigbits vs Gigbytes)
  | TYPE| CONFIG |  DRAM WIDTH |  ROW  | COL  | RANKS |  RANK SIZE |  MODULE SIZE |    
  | ---  | ---    |     ---      |  ---  | ---  |  ---  |    ---     |    ---       |
  | DDR3 |  x8    |   4 Gbit     |   16  |  10  |   2   |   4 GB     |     8 GB     |
|**DDR3L** |  **x8**    |   **8 Gbit**     |   **16**  |  **11** |   **2**   |   **8 GB**     |      **16 GB** |

^Data gathereed from Micron/Corsair Specsheet(mm_ktf16c2gx64hz))  
              (stacked 4Gbit)



## Action:

I have changed the col addressing decompiled assembly files, but have not put them back into assembly or binary.

P.S. the docs folder is loaded with gathered info that makes reference to obscure codes and settings related to the MRC and MC 

[1]
[Intel Specsheet](https://ark.intel.com/content/www/us/en/ark/products/75117/intel-core-i7-4700mq-processor-6m-cache-up-to-3-40-ghz.html)

[2]
[T440P Product Ref/Spec Sheet](https://psref.lenovo.com/syspool/Sys/PDF/withdrawnbook/ThinkPad_T440p.pdf)

[3]
[Intel QM87 Datasheet](https://www.intel.com/content/www/us/en/products/docs/chipsets/8-series-chipset-pch-datasheet.html)

[4] Number of rows already exists since the 16Gb DDR3 since DDR3 x8 utilizes same row information

[5] DDR3L is dual voltage and can run at either DDR3 1.5v or DDR3 1.3v, it is not compatibale to run at LPDDR3 specs
