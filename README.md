# AMD Vega 56/64 Reset Patch

Due to the architecture of Vega 10 and the lack of appropriate reset code for its built-in PCIe switch, until said reset code exists one can disable PCIe resets for their Vega card by applying this patch.  There appears to be an actual reset patch in the works but no word since last year.  

Patch from `https://gist.github.com/numinit/1bbabff521e0451e5470d740e0eb82fd`  

## Ubuntu 18.04 LTS example:
### Download the latest full kernel release version ...example here is 4.20
```
wget https://github.com/torvalds/linux/archive/v4.20.zip
unzip v4.20.zip
```
### Clone this repo
```
git clone https://github.com/netsiphon/vega-reset.git
cd vega-reset/
patch -d ../linux-4.20 -p0 -i fix-vega-reset.patch
```
All hunks must succeed to proceed. If they don't look for the failed hunk and manually correct it if you can.  

### Replace configuration with your OS kernel configuration from /boot
_Please note that the make-custom-kernel script is set to generate 16 threads for the 1700/2700. Choose the appropriate number for an alternate model._
```
./make-custom-kernel ../linux-4.20 config-4.18.0-13-lowlatency

```
Restart to use the new kernel
