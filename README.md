# CPUMicrocodes
Intel, AMD, VIA &amp; Freescale CPU Microcode Repositories

[CPU Microcode Repositories News Feed](https://twitter.com/platomaniac)

[CPU Microcode Repositories Discussion Topic](https://www.win-raid.com/t3355f47-Intel-AMD-VIA-amp-Freescale-CPU-Microcode-Repositories-Discussion.html)

[MC Extractor](https://github.com/platomav/MCExtractor)

[MC Extractor Discussion Topic](https://www.win-raid.com/t2199f47-MC-Extractor-Intel-AMD-VIA-amp-Freescale-Microcode-Extraction-Tool-Discussion.html)

This is a collection of every **Latest Production** Intel & AMD as well every VIA & Freescale CPU microcode we have found. You can use [MC Extractor](https://github.com/platomav/MCExtractor) to check instantly whether a microcode is already at the repository. Please report any microcodes which are missing from the [MC Extractor](https://github.com/platomav/MCExtractor) database at the [CPU Microcode Repositories Discussion Topic](https://www.win-raid.com/t3355f47-Intel-AMD-VIA-amp-Freescale-CPU-Microcode-Repositories-Discussion.html) instead of opening an issue here.

Collecting CPU microcodes is important for upgrading purposes, for creating universal tools that can help people understand what microcode they use, for research on how the general technology works, for developers with no vendor representative who want to work on a given platform etc.

**Disclaimer: All the microcodes below come only from official BIOS/UEFI updates, Intel/AMD Linux Microcode Updates, Linux Distributions, Windows Updates etc which were provided and made public by various manufacturers!**


All microcodes are checked by [MC Extractor](https://github.com/platomav/MCExtractor) to verify their health, size etc.

It is always advised to request and/or wait for your OEM/OS to release newer fixes. The microcodes are gathered and provided with the sole purpose of helping people who are out of other viable solutions. Thus, they can be extremely helpful to those who have major problems with their systems for which their manufacturer refuses to assist due to indifference and/or system age.


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
	- Examples: Intel 0x000906EB, AMD 0x00810F10 or VIA 0x00010690 or Freescale 0x8323.
- **Release** (Intel only)
	- Specifies the status of the microcode. This can be either Production (PRD) or Pre-Production (PRE)
	- `PRD` microcodes are to be valued higher than `PRE` due to stability
	- Only `PRD` are included in this repository.
- **Signature** (VIA and Freescale only)
	- Human readable CPUID and Update Revision
	- Example: "BJ_6FE_0205" or "MPC8569 QE Microcode Rel_B6900155".
- **PlatformID** (Intel only)
	- Provides information about the supported sockets (LGA775, LGA1366 etc) or platform types (Desktop, Mobile etc) depending on CPU generation
	- 8 bits in hexadecimal representation (bitmask)
	- When updating to another microcode, ensure that at least the same Platform IDs are supported. Example: changing from 0x1C (2,3,4) to 0x1D (0,2,3,4) is okay, due to the additionally included platform "0".
	- To not risk losing socket/platform support, avoid reducing the supported platforms. Example: avoid 0x1C to 0x18 due to the missing platform "2".
	- Note: in 2017 microcodes with CPUID 0x000906E9 & Platform ID 0x22 (1,5) were superseded by CPUID 0x000906E9 & Platform ID 0x2A (1,3,5) in order to add LGA2066 socket/HEDT platform type support at KBL(-X) CPUID.
- **Revision**
	- Microcode update revision counter. Newer revisions have higher numbers.
	- Only the latest microcodes of each CPUID are included in the repositories.
- **Date**
	- Date of its public release in ISO8601 (YYYY-MM-DD) format
- **Checksum**
	- Number for validity checks during deployment to manufacturers.
	- All Freescale and AMD microcodes with CPUID >= 0x00500F00 lack an official Checksum, thus [MC Extractor](https://github.com/platomav/MCExtractor) generates its own.