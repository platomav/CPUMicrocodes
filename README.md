# CPUMicrocodes
Intel, AMD, VIA &amp; Freescale CPU Microcode Repositories

[CPU Microcode Repositories News Feed](https://twitter.com/platomaniac)

[CPU Microcode Repositories Discussion Topic](https://www.win-raid.com/t3355f47-Intel-AMD-VIA-amp-Freescale-CPU-Microcode-Repositories-Discussion.html)

[MC Extractor](https://github.com/platomav/MCExtractor)

[MC Extractor Discussion Topic](https://www.win-raid.com/t2199f47-MC-Extractor-Intel-AMD-VIA-amp-Freescale-Microcode-Extraction-Tool-Discussion.html)

This is a collection of every **Latest Production** Intel & AMD as well every VIA & Freescale CPU microcode we have found. You can use [MC Extractor](https://github.com/platomav/MCExtractor) to check instantly whether a microcode is already at the repository. Please report any microcodes which are missing from the [MC Extractor](https://github.com/platomav/MCExtractor) database at the [CPU Microcode Repositories Discussion Topic](https://www.win-raid.com/t3355f47-Intel-AMD-VIA-amp-Freescale-CPU-Microcode-Repositories-Discussion.html) instead of opening an issue here.

Collecting CPU microcodes is important for upgrading purposes, for creating universal tools that can help people understand what microcode they use, for research on how the general technology works, for developers with no vendor representative who want to work on a given platform etc.

**Disclaimer: All the microcodes below come only from official BIOS/UEFI updates, Intel/AMD Linux Microcode Updates, Linux Distributions, Windows Updates etc which were provided and made public by various manufacturers!** It is always advised to request and/or wait for your OEM/OS to release newer fixes. The microcodes are gathered and provided with the sole purpose of helping people who are out of other viable solutions. Thus, they can be extremely helpful to those who have major problems with their systems for which their manufacturer refuses to assist due to indifference and/or system age.

All microcodes at the repositories have some common attributes and are categorized based on them as follows:

- Every microcode targets a specific **CPUID** which encodes info such as Family, Generation, Model, Stepping etc. For example, Intel 0x000906EB or AMD 0x00810F10 or VIA 0x00010690 or Freescale 0x8323.
- Every microcode has an **Update Revision** which is increased when fixes are applied. For example, 0x00000A0B < 0x00000A0E. For Intel & AMD, **only the latest microcodes of each CPUID are included in the repositories.**
- Every Intel, AMD and VIA microcode has a **Date** which relates to its public release, in ISO8601 YYYY-MM-DD format. For example, 2018-01-02 or 2016-12-09.
- Every microcode includes a **Checksum** to check its validity during deployment to manufacturers. For example 0x1B3E0B0E. All Freescale and AMD microcodes with CPUID >= 0x00500F00 lack an official Checksum so [MC Extractor](https://github.com/platomav/MCExtractor) generates its own.
- Intel microcodes have a **Platform ID** field which encodes the supported CPU sockets/platform types, in binary form. For example, 0xC0 = 6,7 or 0x03 = 0,1 or 0x76 = 1,2,4,5,6.
- Intel microcode **Release/Type** state is distinguished between Production (PRD) and Pre-Production (PRE). **Only Production (PRD) microcodes are included in the repositories.**
- VIA and Freescale microcodes have a **Signature** which usually shows the CPUID and Update Revision, in human readable form. For example, "BJ_6FE_0205" or "MPC8569 QE Microcode Rel_B6900155".

There is a certain mentality which is followed in order to structure the microcode repositories properly:

- Every firmware filename follows the structure **cpu**CPUID_**plat**PlatformID(Intel)_**ver**UpdateRevision_Date_Release(Intel)_Checksum and has a .bin extension. For example: Intel cpu906EB_plat02_ver0000007C_2017-12-03_PRD_5046D998, AMD cpu00800F11_ver08001129_2017-07-14_4F426450 or VIA cpu10690_ver00000001_sig[BJ_10690.020]_2017-01-09_A8B24DC2 or Freescale soc8360_rev2.1_sig[Soft-UART]_3725F40B.
- All microcodes are checked by [MC Extractor](https://github.com/platomav/MCExtractor) to verify their health, size etc. Please check MCE's description to learn more of its features and capabilities.
- Due to the fact that there are too many CPU microcodes, everything is placed in one vendor-specific folder and the user is responsible for finding the proper CPUID and Platform ID they require.
- The update status of all Intel & AMD CPU microcodes (Last Yes/No) relies on their CPUID, Update Revision and Date.
- The update status of Intel microcodes additionally relies on their Release/Type, which is either Production (PRD) or Pre-Production (PRE). For example, a hypothetical microcode cpu206A6_plat12_ver00000028_2010-09-15_PRD is "Last Yes" compared to the "Last No" cpu206A6_plat12_ver00000022_2010-07-07_PRD but so is cpu206A6_plat12_ver00000028_2010-09-15_PRE. That's because, compared to the other two, it is Pre-Production and not Production. Please note that [MC Extractor](https://github.com/platomav/MCExtractor) can detect that as well and will show both as being "Last Yes" due to their difference in Release/Type, even if everything else is the same or in favor of one or the other.
- The Platform ID field of Intel microcodes can contain up to 8 supported sockets (LGA775, LGA1366 etc) or platform types (Desktop, Mobile etc), depending on the CPU generation, in encoded binary form (bitmask). The user needs to determine if their chosen microcode update has the same or more Platform IDs compared to the currently loaded CPU microcode from the BIOS or OS. You can use [MC Extractor](https://github.com/platomav/MCExtractor) to check each Intel microcode's supported Platform IDs. For example, if your current microcode has CPUID 0x00000F4A and Platform ID 0x5C (2,3,4,6) you can update to a newer microcode which has the same CPUID of 0x00000F4A but Platform ID 0x5D (0,2,3,4,6) since it additionally includes platform "0". On the other hand, you cannot update to a newer microcode with the same CPUID of 0x00000F4A but Platform ID 0x58 (3,4,6) as it doesn't include the original "2" and your socket/platform type might not be supported. Please note that [MC Extractor](https://github.com/platomav/MCExtractor) can detect that as well, so if you cannot find the exact CPUID & Platform ID combo at the repository, as the one you currently have, it might be because there is another microcode with the same CPUID but with more supported Platform IDs. For example, in 2017, microcodes with CPUID 0x000906E9 & Platform ID 0x22 (1,5) were succeeded by CPUID 0x000906E9 & Platform ID 0x2A (1,3,5) in order to add LGA2066 socket/HEDT platform type support at KBL(-X) CPUID.