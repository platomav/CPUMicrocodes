# CPUMicrocodes
Intel, AMD, VIA &amp; Freescale CPU Microcode Repositories

[CPU Microcode Repositories News Feed](https://twitter.com/platomaniac)

[CPU Microcode Repositories Discussion Topic](https://www.win-raid.com/t3355f47-Intel-AMD-VIA-amp-Freescale-CPU-Microcode-Repositories-Discussion.html)

[MC Extractor: Intel, AMD, VIA & Freescale Microcode Extraction Tool](https://github.com/platomav/MCExtractor)

[MC Extractor Discussion Topic](https://www.win-raid.com/t2199f47-MC-Extractor-Intel-AMD-VIA-amp-Freescale-Microcode-Extraction-Tool-Discussion.html)

This is a collection of every **Latest Production** Intel & AMD as well every VIA & Freescale CPU microcode we have found. You can use [MC Extractor](https://github.com/platomav/MCExtractor) to check instantly whether a microcode is already at the repository. Please report any microcodes which are missing from the [MC Extractor](https://github.com/platomav/MCExtractor) database at the [CPU Microcode Repositories Discussion Topic](https://www.win-raid.com/t3355f47-Intel-AMD-VIA-amp-Freescale-CPU-Microcode-Repositories-Discussion.html) instead of opening an issue here.

Collecting CPU microcodes is important for upgrading purposes, for creating universal tools that can help people understand what microcode they use, for research on how the general technology works, for developers with no vendor representative who want to work on a given platform etc.

**Disclaimer: All the microcodes below come only from official BIOS/UEFI updates, Intel/AMD Linux Microcode Updates, Linux Distributions, Windows Updates etc which were provided and made public by various manufacturers!**

All microcodes are checked by [MC Extractor](https://github.com/platomav/MCExtractor) to verify their health, size etc. Please check [MCE's README](https://github.com/platomav/MCExtractor/blob/master/README.md) to learn more of its features and capabilities.

It is generally advised to request and/or wait for your OEM/OS to release newer fixes. **Latest is not always better or tested.** Manufacturers and OS mainteners usually have some insider/confidential info from microcode vendors on what got changed/fixed at newer microcode releases so if they ship older microcodes, it could be that newer versions have not been thoroughly tested, have been retracted/downgraded by the microcode vendor or not contain anything important enough to warrant an update. The microcodes here are gathered and provided with the sole purpose of helping people who are out of other viable solutions. Thus, they can be extremely helpful to those who have major problems with their systems for which their manufacturer refuses to assist due to indifference and/or system age.

## File naming explanation

All microcodes at the repositories have some common attributes and are categorized based on them as follows:

	 cpu[CPUID]_plat[PlatformID]_ver[Revision]_[Date]_[Release]_[Checksum].bin

### Examples:

	Intel:     cpu906EB_plat02_ver0000007C_2017-12-03_PRD_5046D998.bin
	AMD:       cpu00800F11_ver08001129_2017-07-14_4F426450.bin
	VIA:       cpu10690_ver00000001_sig[BJ_10690.020]_2017-01-09_A8B24DC2.bin
	Freescale: soc8360_rev2.1_sig[Soft-UART]_3725F40B.bin

### Field descriptions

- **CPUID**
	- This value encodes info such as Family, Generation, Model and Stepping.
	- Examples: Intel 0x000906EB, AMD 0x00810F10, VIA 0x00010690, Freescale 0x8323.
- **PlatformID** (Intel only)
	- Provides information about the supported sockets (LGA775, LGA1366 etc) or platform types (Desktop, Mobile etc) depending on CPU generation.
	- Up to 8 supported IDs, encoded in Little Endian binary form (bitmask). For example, 0xC0 = 0b11000000 = 6,7 or 0x03 = 0b00000011 = 0,1 or 0x76 = 0b01110110 = 1,2,4,5,6.
	- When updating to another microcode, ensure that at least the same or more Platform IDs are supported. You can use [MC Extractor](https://github.com/platomav/MCExtractor) to check each Intel microcode's supported Platform IDs. For example, changing from 0x5C (2,3,4,6) to 0x5D (0,2,3,4,6) is okay, due to the additionally included platform "0".
	- To not risk losing socket/platform support, avoid reducing the supported platforms. For example, changing from 0x5C (2,3,4,6) to 0x58 (3,4,6) might not be okay due to the missing platform "2".
	- If you cannot find the exact CPUID & Platform ID combo at the repository, as the one you currently have, it might be because there is another microcode with the same CPUID but with more supported Platform IDs. For example, microcodes with CPUID 0x906E9 & Platform ID 0x22 (1,5) were superseded in 2017 by CPUID 0x906E9 & Platform ID 0x2A (1,3,5) in order to add LGA2066 socket/HEDT platform type support at KBL(-X) CPUID.
- **Signature** (VIA and Freescale only)
	- Human readable CPUID and Update Revision.
	- Example: "BJ_6FE_0205" or "MPC8569 QE Microcode Rel_B6900155".
- **Revision**
	- Microcode update revision counter. Increased when fixes are applied. For example, 0xA0B < 0xA0E.
	- For Intel & AMD, only the latest microcodes of each CPUID are included in the repositories.
- **Date**
	- Date of its public release in ISO8601 (YYYY-MM-DD) format. For example, 2018-01-02 or 2016-12-09.
- **Release/Type** (Intel only)
	- Specifies the status of the microcode. This can be either Production (PRD) or Pre-Production (PRE).
	- `PRD` microcodes are to be valued higher than `PRE` due to stability & testing.
	- Only `PRD` microcodes are included in this repository.
- **Checksum**
	- Number for validity checks during deployment to manufacturers.
	- All Freescale & AMD microcodes with CPUID >= 0x00500F00 lack an official Checksum, thus [MC Extractor](https://github.com/platomav/MCExtractor) generates its own.
