# Malware Analysis Report (Azaza-SBB)
The goal of this report is to provide actionable intelligence regarding threat actors and the malware or other tools they use for reconnaissance, delivery, exploitation, and so forth in order for security operations (SecOps) teams to be empowered to more quickly detect and respond to this specific threat. 

In the case of a victim of this malware, this analysis can be used to understand the impact of the malware (e.g., what damage it may have done, lateral movement, data exfiltration, credential gathering, etc.). We also share this intelligence back to
the community to assist other researchers in their analysis of the same malware.

This threat intelligence report is based on analysis from the GlobeCyber team in which we examine details of malware may known as “SBB”

# Table of Contents

- Reports
    - [Persian Version](persian.md)
- [Requirements](#Requirements)
- [Installation](#Installation)
- Resources
	- [Infected Excel File](resources/sbb.xlsx)
	- [Malware Fake Certificate](resources/cert.der)
	- [Powershell ( IE Fake Cert Register )](resources/ps.ps1)
	- [Powershell ( Firefox Fake Cert Register )](resources/psf.ps1)
	- [Extracted Malware ( Obfuscated Object )](malware_obfuscated.object)
	- [Extracted Malware ( Obfuscated JS )](malware_obfuscated.js)
	- [Extracted Malware ( Deobfuscated JS )](malware_deobfuscated.js)
	- [Extracted Malware ( Pretified JS )](malware_prettified.js)

### Requirements
- [Python 3](https://www.python.org/downloads/)
- [NodeJS](https://nodejs.org/en/download/current/)
- [Zipdump.py](assets/zipdump.py)
- [Maldoc.yara](assets/maldoc.yara)
- [BOX-JS](https://github.com/CapacitorSet/box-js)
- Decoders
	- [Add1](assets/decoder_add1.py)
	- [Rol1](assets/decoder_rol1.py)
	- [XOR1](assets/decoder_xor1.py)
### Installation

```bash
pip install yara-python
```
```bash
npm install box-js --global
```


# Disclaimer
This report is provided "as is" for informational purposes only, GlobeCyber does not provide any warranties of any kind regarding any information contained within.