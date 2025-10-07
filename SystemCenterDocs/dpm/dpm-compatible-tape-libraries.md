---
description: This article describes tape libraries compatible with DPM.
ms.topic: concept-article
ms.service: system-center
keywords:
ms.date: 05/05/2025
ms.update-cycle: 180-days
title: System Center DPM Compatible Tape Libraries
ms.subservice: data-protection-manager
ms.assetid: 69cab349-9e1d-46f7-b722-6b612dae9498
author: Jeronika-MS
ms.author: v-gajeronika
ms.custom: engagement-fy23, updateFrequency.5, engagement-fy24
---

# System Center DPM Compatible Tape Libraries

::: moniker range="sc-dpm-2016"

Data Protection Manager (DPM) in System Center 2012 R2, 2016 and 2019 can be deployed using tape-based backup for data protected by the DPM server. A tape library or standalone tape drive can be connected to DPM servers. For more information, see [Planning the Tape Libraries Configuration](/previous-versions/system-center/data-protection-manager-2010/ff399733(v=technet.10)). The following tables summarize tape libraries that are compatible with DPM in System Center 2012 R2, 2016 and 2019.

::: moniker-end

::: moniker range="sc-dpm-2019"

Data Protection Manager (DPM) in System Center 2016 and 2019 can be deployed using tape-based backup for data protected by the DPM server. A tape library or standalone tape drive can be connected to DPM servers. For more information, see [Planning the Tape Libraries Configuration](/previous-versions/system-center/data-protection-manager-2010/ff399733(v=technet.10)). The following tables summarize tape libraries that are compatible with DPM in System Center 2016 and 2019.

::: moniker-end

::: moniker range="sc-dpm-2022"

Data Protection Manager (DPM) in System Center 2019 and 2022 can be deployed using tape-based backup for data protected by the DPM server. A tape library or standalone tape drive can be connected to DPM servers. For more information, see [Planning the Tape Libraries Configuration](/previous-versions/system-center/data-protection-manager-2010/ff399733(v=technet.10)). The following tables summarize tape libraries that are compatible with DPM in System Center 2019 and 2022.

::: moniker-end

::: moniker range="<=sc-dpm-2019"

> [!NOTE]
> DPM supports only the tape libraries that are connected using a single path and not the tape libraries connected using the multi-path software.
>
> Tape libraries configured with a virtual Fibre Channel adapter are only supported when using certified tape library hardware on the following configurations:
> - System Center Data Protection Manager 2012 R2 U3 (or later) running on Windows 2012 R2 (or later).
> - System Center Data Protection Manager 2016 running on Windows Server 2012 R2 (or later).
> - System Center Data Protection Manager 2019 running on Windows Server 2016 and Windows Server 2019.

::: moniker-end

::: moniker range="sc-dpm-2022"

> [!NOTE]
> DPM supports only the tape libraries that are connected using a single path and not the tape libraries connected using the multi-path software.
>
> Tape libraries configured with a virtual Fibre Channel adapter are only supported when using certified tape library hardware on the following configurations:
> - System Center Data Protection Manager 2019 running on Windows Server 2016 and Windows Server 2019.
> - System Center Data Protection Manager 2022 running on Windows Server 2019 and Windows Server 2022.

::: moniker-end

::: moniker range="sc-dpm-2025"

> [!NOTE]
> DPM supports only the tape libraries that are connected using a single path and not the tape libraries connected using the multi-path software.
> 
> Tape libraries configured with a virtual Fibre Channel adapter are only supported when using certified tape library hardware on the following configurations:
> - System Center Data Protection Manager 2022 running on Windows Server 2019 and Windows Server 2022.
> - System Center Data Protection Manager 2025 running on Windows Server 2022 and Windows Server 2025.

::: moniker-end

## Support Matrix

::: moniker range="<=sc-dpm-2019"

|Windows Server versions| DPM 2012 R2 | DPM 2016 | DPM 2019 | DPM 2022 |
| --- | --- | --- | --- | --- |
| Windows Server 2012 R2 |  Y |  Y |  N | N |
| Windows Server 2016    |  Y |  Y |  Y | N |
| Windows Server 2019    |  N |  N |  Y | Y |
| Windows Server 2022    |  N |  N |  Y | Y |

::: moniker-end

::: moniker range="sc-dpm-2022"

|Windows Server versions| DPM 2019 | DPM 2022 |
| --- | --- | --- |
| Windows Server 2019    | Y | Y |
| Windows Server 2022    | Y | Y |

::: moniker-end

::: moniker range="sc-dpm-2025"

|Windows Server versions| DPM 2022 | DPM 2025 |
| --- | --- | --- |
| Windows Server 2022    | Y | Y |
| Windows Server 2025    | Y | Y |

::: moniker-end

## BDT

| Library Model Name | Operating System | Changer Driver Version | Library Firmware Revision | Other Libraries in Test | Tape Drive Type | Tape Driver Version | Tape Drive Firmware Revision |
| --- | --- | --- | --- | --- | --- | --- | --- |
| FlexStor II 1U |   | 5.2.3790.7, 06/06/2009, signed | 2.4 | 2U, 4U, 8U | HP LTO5 HH FC | 1.0.6.3, 10/07/2010, signed | Y23B |
| FlexStor II 1U |   | 5.2.3790.7, 06/06/2009, signed | 2.4 | 2U, 4U, 8U | HP LTO5 HH SAS | 1.0.6.3, 10/07/2010, signed | Z21B |
| FlexStor II 4U |   | 5.2.3790.7, 06/06/2009, signed | 4.70/3.00e | 2U, 8U | HP LTO5 FH SAS | 1.0.6.1, 05/14/2009, signed | X22B |
| FlexStor II 4U |   | 5.2.3790.7, 06/06/2009, signed | 4.70/3.00e | 2U, 8U | HP LTO5 FH FC | 1.0.6.3, 10/07/2010, signed | I5BB |
| FlexStor II 4U |   | 5.2.3790.7, 06/06/2009, signed | 4.70/3.00e | 2U, 8U | IBM LTO5 FH FC | 6.2.1.5, 01/13/2011, signed | A6S0 |
| FlexStor II 4U |   | 5.2.3790.7, 06/06/2009, signed | 4.70/3.00e | 2U, 8U | IBM LTO5 FH SAS | 6.2.1.5, 01/13/2011, signed | A6S0 |
| FlexStor II 4U |   | 5.2.3790.7, 06/06/2009, signed | 4.70/3.00e | 1U, 2U, 8U | IBM LTO5 HH FC | 6.2.1.5, 01/13/2011, signed | A6S1 |
| FlexStor II 4U |   | 5.2.3790.7, 06/06/2009, signed | 4.70/3.00e | 1U, 2U, 8U | IBM LTO5 HH SAS | 6.2.1.5, 01/13/2011, signed | A6S1 |
| FlexStor II 4U | 2008 R2 | 5.2.3790.7, 06/06/2009, signed | 4.90/3.20e | 1U, 2U, 8U | HP LTO6 HH FC | 1.0.7.1, 02/11/2013, signed | 22EB |
| FlexStor II 4U | 2012 | 8.0.0.1, 07/05/2012, signed | 4.90/3.20e | 1U, 2U, 8U | HP LTO6 HH FC | 1.0.7.1, 02/11/2013, signed | 22 EB |
| FlexStor II 4U | 2008 R2 | 5.2.3790.7, 06/06/2009, signed | 4.90/3.20e | 1U, 2U, 8U | HP LTO6 HH SAS | 1.0.7.1, 02/11/2013, signed | 32CB |
| FlexStor II 4U | 2012 | 8.0.0.1, 07/05/2012, signed | 4.90/3.20e | 1U, 2U, 8U | HP LTO6 HH SAS | 1.0.7.1, 02/11/2013, signed | 32CB |
| FlexStor II 4U | 2008 R2 | 5.2.3790.7, 06/06/2009, signed | 4.90/3.20e | 1U, 2U, 8U | IBM LTO6 HH FC | 6.2.3.3, 10/29/2012, signed | CBW5 |
| FlexStor II 4U | 2012 | 8.0.0.1, 07/05/2012, signed | 4.90/3.20e | 1U, 2U, 8U | IBM LTO6 HH FC | 6.2.3.3, 10/29/2012, signed | CBW5 |
| FlexStor II 4U | 2008 R2 | 5.2.3790.7, 06/06/2009, signed | 4.90/3.20e | 1U, 2U, 8U | IBM LTO6 HH SAS | 6.2.3.3, 10/29/2012, signed | CBW5 |
| FlexStor II 4U | 2012 | 8.0.0.1, 07/05/2012, signed | 4.90/3.20e | 1U, 2U, 8U | IBM LTO6 HH SAS | 6.2.3.3, 10/29/2012, signed | CBW5 |
| FlexStor II 4U | 2012\2012R2 | 8.1.0.0, 01/07/2014, signed | 5.03/3.20e | 1U, 2U | IBM LTO7 HH FC | 6.2.5.5, 09/08/2015, signed | FA11 |
| FlexStor II 4U | 2012\2012R2 | 8.1.0.0, 01/07/2014, signed | 5.03/3.20e | 1U, 2U | IBM LTO7 HH SAS | 6.2.5.5, 09/08/2015, signed | FA11 |
| FlexStor II 4U | 2012/2012R2 | 8.1.0.0, 01/07/2014, signed | 5.40/3.20e | 1U, 2U | IBM LTO8 HH FC | 6.2.6.6, 10/24/2017, signed | HB81 |
| FlexStor II 4U | 2012/2012R2 | 8.1.0.0, 01/07/2014, signed | 5.40/3.20e | 1U, 2U | IBM LTO8 HH SAS | 6.2.6.6, 10/24/2017, signed | HB81 |
| FlexStor II 4U | 2016 | 8.3.0.2, 07/03/2017, signed | 5.40/3.20e | 1U, 2U | IBM LT08 HH FC | 6.2.6.6, 10/24/2017, signed | HB81 |
| FlexStor II 4U | 2016 | 8.3.0.2, 07/03/2017, signed | 5.40/3.20e | 1U, 2U | IBM LTO8 HH SAS | 6.2.6.6, 10/24/2017, signed | HB81 |
| MultiStor | 2012/2012R2 | 8.1.0.0, 01/07/2014, signed | 1.1.0-0012 |   | IBM LTO6 HH FC | 6.2.6.6, 10/24/2017, signed | H991 |
| MultiStor | 2012/2012R2 | 8.1.0.0, 01/07/2014, signed | 1.1.0-0012 |   | IBM LT06 HH SAS | 6.2.6.6, 10/24/2017, signed | H991 |
| MultiStor | 2012/2012R2 | 8.1.0.0, 01/07/2014, signed | 1.1.0-0012 |   | IBM LT07 HH FC | 6.2.6.6, 10/24/2017, signed | HB81 |
| MultiStor | 2012/2012R2 | 8.1.0.0, 01/07/2014, signed | 1.1.0-0012 |   | IBM LT07 HH SAS | 6.2.6.6, 10/24/2017, signed | HB81 |
| MultiStor | 2012/2012R2 | 8.1.0.0, 01/07/2014, signed | 1.1.0-0012 |   | IBM LT08 HH FC | 6.2.6.6, 10/24/2017, signed | HB81 |
| MultiStor | 2012/2012R2 | 8.1.0.0, 01/07/2014, signed | 1.1.0-0012 |   | IBM LT08 HH SAS | 6.2.6.6, 10/24/2017 signed | HB81 |
| MultiStor | 2016 | 8.3.0.2, 07/03/2017, signed | 1.1.0-0012 |   | IBM LT06 HH FC | 6.2.6.6, 10/24/2017, signed | H991 |
| MultiStor | 2016 | 8.3.0.2, 07/03/2017, signed | 1.1.0-0012 |   | IBM LT06 HH SAS | 6.2.6.6, 10/24/2017, signed | H991 |
| MultiStor | 2016 | 8.3.0.2, 07/03/2017, signed | 1.1.0-0012 |   | IBM LT07 HH FC | 6.2.6.6, 10/24/2017, signed | HB81 |
| MultiStor | 2016 | 8.3.0.2, 07/03/2017, signed | 1.1.0-0012 |   | IBM LT07 HH SAS | 6.2.6.6, 10/24/2017, signed | HB81 |
| MultiStor | 2016 | 8.3.0.2, 07/03/2017, signed | 1.1.0-0012 |   | IBM LT08 HH FC | 6.2.6.6, 10/24/2017, signed | HB81 |
| MultiStor | 2016 | 8.3.0.2, 07/03/2017, signed | 1.1.0-0012 |   | IBM LT08 HH SAS | 6.2.6.6, 10/24/2017, signed | HB81 |
| MULTISTAK | 2012 | 8.3.0.0, 05/07/2014, signed | 1.7 | - | HP LTO5 HH FC | 1.0.7.1, 02/11/2013, signed | Y64B |
| MULTISTAK | 2012 R2 | 8.1.0.0, 01/07/2014, signed | 1.7 | - | HP LTO5 HH FC | 1.0.7.1, 02/11/2013, signed | Y64B |
| MULTISTAK | 2012 | 8.3.0.0, 05/07/2014, signed | 1.7 | - | HP LTO5 HH SAS | 1.0.7.1, 02/11/2013, signed | Z64B |
| MULTISTAK | 2012 R2 | 8.1.0.0, 01/07/2014, signed | 1.7 | - | HP LTO5 HH SAS | 1.0.7.1, 02/11/2013, signed | Z64B |
| MULTISTAK | 2012 | 8.3.0.0, 05/07/2014, signed | 1.7 | - | HP LTO6 HH FC | 1.0.7.1, 02/11/2013, signed | 238B |
| MULTISTAK | 2012 R2 | 8.1.0.0, 01/07/2014, signed | 1.7 | - | HP LTO6 HH FC | 1.0.7.1, 02/11/2013, signed | 238B |
| MULTISTAK | 2012 | 8.3.0.0, 05/07/2014, signed | 1.7 | - | HP LTO6 HH SAS | 1.0.7.1, 02/11/2013, signed | 338B |
| MULTISTAK | 2012 R2 | 8.1.0.0, 01/07/2014, signed | 1.7 | - | HP LTO6 HH SAS | 1.0.7.1, 02/11/2013, signed | 338B |
| MULTISTAK | 2012 | 8.3.0.0, 05/07/2014, signed | 1.7 | - | IBM LTO5 HH FC | i6.2.3.3, 10/29/2012, signed | E4J6 |
| MULTISTAK | 2012 R2 | 8.1.0.0, 01/07/2014, signed | 1.7 | - | IBM LTO5 HH FC | 6.2.3.3, 10/29/2012, signed | E4J6 |
| MULTISTAK | 2012 | 8.3.0.0, 05/07/2014, signed | 1.7 | - | IBM LTO5 HH SAS | i6.2.3.3, 10/29/2012, signed | E4J6 |
| MULTISTAK | 2012 R2 | 8.1.0.0, 01/07/2014, signed | 1.7 | - | IBM LTO5 HH SAS | 6.2.3.3, 10/29/2012, signed | E4J6 |
| MULTISTAK | 2012 | 8.3.0.0, 05/07/2014, signed | 1.7 | - | IBM LTO6 HH FC | 6.2.3.3, 10/29/2012, signed | E4J6 |
| MULTISTAK | 2012 R2 | 8.1.0.0, 01/07/2014, signed | 1.7 | - | IBM LTO6 HH FC | 6.2.3.3, 10/29/2012, signed | E4J6 |
| MULTISTAK | 2012 | 8.3.0.0, 05/07/2014, signed | 1.7 | - | IBM LTO6 HH SAS | 6.2.3.3, 10/29/2012, signed | E4J6 |
| MULTISTAK | 2012 R2 | 8.1.0.0, 01/07/2014, signed | 1.7 | - | IBM LTO6 HH SAS | 6.2.3.3, 10/29/2012, signed | E4J6 |
| MULTISTAK | 2012 | 8.3.0.0, 05/07/2014, signed | 1.7 | - | HP LTO6 HH FC | 1.0.7.1, 02/11/2013, signed | 238B |
| MULTISTAK | 2012 R2 | 8.1.0.0, 01/07/2014, signed | 1.7 | - | HP LTO6 HH FC | 1.0.7.1, 02/11/2013, signed | 238B |
| MULTISTAK | 2012 | 8.3.0.0, 05/07/2014, signed | 1.7 | - | HP LTO6 HH SAS | 1.0.7.1, 02/11/2013, signed | 338B |
| MULTISTAK | 2012 R2 | 8.1.0.0, 01/07/2014, signed | 1.7 | - | HP LTO6 HH SAS | 1.0.7.1, 02/11/2013, signed | 338B |
| MULTISTAK | 2012\2012R2 | 8.3.0.0, 05/07/2014, signed | 2.05 |   | IBM LTO7 HH FC | 6.2.5.5, 09/08/2015, signed | FA11 |
| MULTISTAK | 2012\2012R2 | 8.3.0.0, 05/07/2014, signed | 2.05 |   | IBM LTO7 HH SAS | 6.2.5.5, 09/08/2015, signed | FA11 |
| MULTISTAK | 2012\2012R2 | 8.1.0.0, 01/07/2014, signed | 2.60 |   | IBM LTO8 HH FC | 6.2.6.6, 10/24/2017, signed | HB81 |
| MULTISTAK | 2012\2012R2 | 8.1.0.0, 01/07/2014, signed | 2.60 |   | IBM LTO8 HH SAS | 6.2.6.6, 10/24/2017, signed | HB81 |
| MULTISTAK | 2016 | 8.3.0.2, 07/03/2017, signed | 2.60 |   | IBM LTO8 HH FC | 6.2.6.6, 10/24/2017, signed | HB81 |
| MULTISTAK | 2016 | 8.3.0.2, 07/03/2017, signed | 2.60 |   | IBM LTO8 HH SAS | 6.2.6.6, 10/24/2017, signed | HB81 |

## Dell

| Library Model Name | Operating System | Changer Driver Version | Library Firmware Revision | Tape Drive Type | Tape Driver Version | Tape Drive Firmware Revision |
| --- | --- | --- | --- | --- | --- | --- |
| ML6000 |   | Version v2.6.2.1, A09 | 585G | LTO5 FH | 6.1.9.9 | B6W0 |
| ML6000 |   | Version v2.6.2.1, A09 | 670G | LTO6 FH | 6.3.9600.16384 | F9A0 |
| ML6000 |   | Version v2.6.2.1, A09 | 670G | LTO7 FH | 6.3.9600.16384 | FA10 |
| TL1000 |   | 6.2.1.8 | 34 | LTO5 | 6.2.1.8 | B6W1 |
| TL1000 |   | 6.2.3.3 | 58 | LTO6 | 6.2.3.3 | F9A1 |
| TL1000 |   | 6.2.5.6 | 58 | LTO7 | 6.2.5.6 | FA11 |
| TL1000 |   |  6.2.5.6 | 0106 | LTO8 | 6.2.5.6 | H9Ex |
| TL2000/4000 |   | 6.2.1.5 | A.50 | LTO5 HH | 6.2.1.5 | B171 |
| TL2000/4000 |   | 6.2.3.3 | B.60 | LTO6 HH | 6.2.3.3 | C9T5 |
| TL2000/4000 |   | 6.2.5.6 | D.10 | LTO7 HH | 6.2.5.6 | FA11 |
|  ML3 |   |  6.2.6.5 |  1.1.1.0 |  LTO6 |  6.2.6.5 |  H99x |
|  ML3 |   |  6.2.6.5 |  1.1.1.0 |  LTO7 |  6.2.6.5 |  H9Ex |
|  ML3 |   |  6.2.6.5 |  1.1.1.0 |  LTO8 |  6.2.6.5 |  H9Ex |

## Fujitsu

| Library Model Name | Operating System | Changer Driver Version | Library Firmware Revision | Other Libraries in Test | Tape Drive Type | Tape Driver Version | Tape Drive Firmware Revision |
| --- | --- | --- | --- | --- | --- | --- | --- |
| ETERNUS LT60 |   | 7.7600.16385.0, 01/02/2010, signed | 4.51/3.00e | LT40 | HP LTO5 FH FC | 1.0.6.3, 10/07/2010, signed | I24B |
| ETERNUS LT60 |   | 7.7600.16385.0, 01/02/2010, signed | 4.51/3.00e | LT40, LT20 | HP LTO5 HH FC | 1.0.6.3, 10/07/2010, signed | Y23B |
| ETERNUS LT60 |   | 7.7600.16385.0, 01/02/2010, signed | 4.51/3.00e | LT40 | HP LTO5 FH SAS | 1.0.6.3, 10/07/2010, signed | X22B |
| ETERNUS LT60 |   | 7.7600.16385.0, 01/02/2010, signed | 4.51/3.00e | LT40, LT20 | HP LTO5 HH SAS | 1.0.6.3, 10/07/2010, signed | Z21B |
| ETERNUS LT60 S2 | 2008 R2 | 7.7600.16385.1, 2/15/2011, signed | 4.81/3.20e | LT40 S2 | HP LTO4 FH FC | 1.0.7.1, 02/11/2013, signed | H65B |
| ETERNUS LT60 S2 | 2012 | 8.0.0.1, 08/02/2012, signed | 4.81/3.20e | LT40 S2 | HP LTO4 FH FC | 1.0.7.1, 02/11/2013, signed | H65B |
| ETERNUS LT60 S2 | 2008 R2 | 7.7600.16385.1, 2/15/2011, signed | 4.81/3.20e | LT40 S2 | HP LTO4 FH SAS | 1.0.7.1, 02/11/2013, signed | A62B |
| ETERNUS LT60 S2 | 2012 | 8.0.0.1, 08/02/2012, signed | 4.81/3.20e | LT40 S2 | HP LTO4 FH SAS | 1.0.7.1, 02/11/2013, signed | A62B |
| ETERNUS LT60 S2 | 2008 R2 | 7.7600.16385.1, 2/15/2011, signed | 4.81/3.20e | LT40 S2, LT20 S2 | HP LTO4 HH FC | 1.0.7.1, 02/11/2013, signed | V63B |
| ETERNUS LT60 S2 | 2012 | 8.0.0.1, 08/02/2012, signed | 4.81/3.20e | LT40 S2, LT20 S2 | HP LTO4 HH FC | 1.0.7.1, 02/11/2013, signed | V63B |
| ETERNUS LT60 S2 | 2008 R2 | 7.7600.16385.1, 2/15/2011, signed | 4.81/3.20e | LT40 S2, LT20 S2 | HP LTO4 HH SAS | 1.0.7.1, 02/11/2013, signed | U64B |
| ETERNUS LT60 S2 | 2012 | 8.0.0.1, 08/02/2012, signed | 4.81/3.20e | LT40 S2, LT20 S2 | HP LTO4 HH SAS | 1.0.7.1, 02/11/2013, signed | U64B |
| ETERNUS LT60 S2 |   | 7.7600.16385.1, 02/15/2011, signed | 4.60/3.10e | LT40 S2 | HP LTO5 FH FC | 1.0.6.3, 10/07/2010, signed | I24B |
| ETERNUS LT60 S2 |   | 7.7600.16385.1, 02/15/2011, signed | 4.60/3.10e | LT40 S2, LT20 S2 | HP LTO5 HH FC | 1.0.6.3, 10/07/2010, signed | Y34B |
| ETERNUS LT60 S2 |   | 7.7600.16385.1, 02/15/2011, signed | 4.60/3.10e | LT40 S2 | HP LTO5 FH SAS | 1.0.6.3, 10/07/2010, signed | X22B |
| ETERNUS LT60 S2 |   | 7.7600.16385.1, 02/15/2011, signed | 4.60/3.10e | LT40 S2, LT20 S2 | HP LTO5 HH SAS | 1.0.6.3, 10/07/2010, signed | Z21B |
| ETERNUS LT60 S2 | 2008 R2 | 7.7600.16385.1, 2/15/2011, signed | 4.81/3.20e | LT40 S2, LT20 S2 | HP LTO6 HH FC | 1.0.7.1, 02/11/2013, signed | 22EB |
| ETERNUS LT60 S2 | 2012 | 8.0.0.1, 08/02/2012, signed | 4.81/3.20e | LT40 S2, LT20 S2 | HP LTO6 HH FC | 1.0.7.1, 02/11/2013, signed | 22EB |
| ETERNUS LT60 S2 | 2008 R2 | 7.7600.16385.1, 2/15/2011, signed | 4.81/3.20e | LT40 S2, LT20 S2 | HP LTO6 HH SAS | 1.0.7.1, 02/11/2013, signed | 32CB |
| ETERNUS LT60 S2 | 2012 | 8.0.0.1, 08/02/2012, signed | 4.81/3.20e | LT40 S2, LT20 S2 | HP LTO6 HH SAS | 1.0.7.1, 02/11/2013, signed | 32CB |
| ETERNUS LT60 S2 | 2012\2012R2 | 8.2.0.1, 05/22/2014, signed | 4.88/3.20e | ETERNUS LT20 S2 ETERNUS LT40 S2 | IBM LTO6 HH FC | 6.2.5.5, 09/08/2015, signed | F9A1 |
| ETERNUS LT60 S2 | 2012\2012R2 | 8.2.0.1, 05/22/2014, signed | 4.88/3.20e | ETERNUS LT20 S2 ETERNUS LT40 S2 | IBM LTO6 HH SAS | 6.2.5.5, 09/08/2015, signed | F9A1 |
| ETERNUS LT60 S2 | 2012\2012R2 | 8.2.0.1, 05/22/2014, signed | 4.88/3.20e | ETERNUS LT20 S2 ETERNUS LT40 S2 | IBM LTO7 HH FC | 6.2.5.5, 09/08/2015, signed | FA11 |
| ETERNUS LT60 S2 | 2012\2012R2 | 8.2.0.1, 05/22/2014, signed | 4.88/3.20e | ETERNUS LT20 S2 ETERNUS LT40 S2 | IBM LTO7 HH SAS | 6.2.5.5, 09/08/2015, signed | FA11 |
| ETERNUS LT60 S2 | 2012/2012R2 | 8.2.0.1, 05/22/2014, signed | 5.10/3.20e | ETERNUS LT20 S2 ETERNUS LT40 S2 | IBM LTO8 HH FC | 6.2.6.6, 10/24/2017, signed | HB81 |
| ETERNUS LT60 S2 | 2012\2012R2 | 8.2.0.1, 05/22/2014, signed | 5.10/3.20e | ETERNUS LT20 S2 ETERNUS LT40 S2 | IBM LTO8 HH SAS | 6.2.6.6, 10/24/2017, signed | HB81 |
| ETERNUS LT60 S2 | 2016 | 8.2.0.6, 07/03/2017, signed | 5.10/3.20e | ETERNUS LT20 S2 ETERNUS LT40 S2 | IBM LTO8 HH FC | 6.2.6.6, 10/24/2017, signed | HB81 |
| ETERNUS LT60 S2 | 2016 | 8.2.0.6, 07/03/2017, signed | 5.10/3.20e | ETERNUS LT20 S2 ETERNUS LT40 S2 | IBM LTO8 HH SAS | 6.2.6.6, 10/24/2017, signed | HB81 |
| ETERNUS LT140 | 2012R2 | 8.2.0.1, 05/22/2014, signed | 1.0.0-A00 |   | IBM LTO6 HH FC IBM LTO6 HH SAS | 6.2.6.6, 10/24/2017, signed | JAX1 |
| ETERNUS LT140 | 2012R2 | 8.2.0.1, 05/22/2014, signed | 1.0.0-A00 |   | IBM LTO7 HH FC IBM LTO7 HH SAS | 6.2.6.6, 10/24/2017, signed | JAY1 |
| ETERNUS LT140 | 2012R2 | 8.2.0.1, 05/22/2014, signed | 1.0.0-A00 |   | IBM LTO8 HH FC IBM LTO8 HH SAS | 6.2.6.6, 10/24/2017, signed | JAY1 |
| ETERNUS LT140 | 2016 | 8.2.0.6, 07/03/2017, signed | 1.0.0-A00 |   | IBM LTO6 HH FC IBM LTO6 HH SAS | 6.2.6.6, 10/24/2017, signed | JAX1 |
| ETERNUS LT140 | 2016 | 8.2.0.6, 07/03/2017, signed | 1.0.0-A00 |   | IBM LTO7 HH FC IBM LTO7 HH SAS | 6.2.6.6, 10/24/2017, signed | JAY1 |
| ETERNUS LT140 | 2016 | 8.2.0.6, 07/03/2017, signed | 1.0.0-A00 |   | IBM LTO8 HH FC IBM LTO HH SAS | 6.2.6.6, 10/24/2017, signed | JAY1 |
| ETERNUS LT260 | 2012 | 8.2.0.1, 05/22/2014, signed | 6.1 |   | HP LTO4 FH FC | 1.0.7.1, 02/11/2013, signed | H66B |
| ETERNUS LT260 | 2012 R2 | 8.2.0.1, 05/22/2014, signed | 6.1 |   | HP LTO4 FH FC | 1.0.7.1, 02/11/2013, signed | H66B |
| ETERNUS LT260 |   | 8.2.0.1, 05/22/2014, signed | 6.1 |   | HP LTO4 FH FC | 1.0.7.1, 02/11/2013, signed | V64B |
| ETERNUS LT260 | 2012 | 8.2.0.1, 05/22/2014, signed | 6.1 |   | HP LTO5FH FC | 1.0.7.1, 02/11/2013, signed | I66B |
| ETERNUS LT260 | 2012 R2 | 8.2.0.1, 05/22/2014, signed | 6.1 |   | HP LTO5 FH FC | 1.0.7.1, 02/11/2013, signed | I66B |
| ETERNUS LT260 | 2012 | 8.2.0.1, 05/22/2014, signed | 6.1 |   | HP LTO5 HH FC | 1.0.7.1, 02/11/2013, signed | Y67B |
| ETERNUS LT260 | 2012 R2 | 8.2.0.1, 05/22/2014, signed | 6.1 |   | HP LTO5 HH FC | 1.0.7.1, 02/11/2013, signed | Y67B |
| ETERNUS LT260 | 2012 | 8.2.0.1, 05/22/2014, signed | 6.1 |   | HP LTO5 HH SAS | 1.0.7.1, 02/11/2013, signed | Z67B |
| ETERNUS LT260 | 2012 R2 | 8.2.0.1, 05/22/2014, signed | 6.1 |   | HP LTO5 HH SAS | 1.0.7.1, 02/11/2013, signed | Z67B |
| ETERNUS LT260 | 2012 | 8.2.0.1, 05/22/2014, signed | 6.1 |   | HP LTO6 HH FC | 1.0.7.1, 02/11/2013, signed | 238B |
| ETERNUS LT260 | 2012 R2 | 8.2.0.1, 05/22/2014, signed | 6.1 |   | HP LTO6 HH FC | 1.0.7.1, 02/11/2013, signed | 238B |
| ETERNUS LT260 | 2012 | 8.2.0.1, 05/22/2014, signed | 6.1 |   | HP LTO6 HH SAS | 1.0.7.1, 02/11/2013, signed | 338B |
| ETERNUS LT260 | 2012R2 | 8.2.0.1, 05/22/2014, signed | 6.1 |   | HP LTO6 HH SAS | 1.0.7.1, 02/11/2013, signed | 338B |
| ETERNUS LT260 | 2012\2012R2 | 8.2.0.1, 05/22/2014, signed | 6.71 |   | IBMLTO6 HH FC | 6.2.5.5, 09/08/2015, signed | FA91 |
| ETERNUS LT260 | 2012\2012R2 | 8.2.0.1, 05/22/2014, signed | 6.71 |   | IBMLTO6 HH SAS | 6.2.5.5, 09/08/2015, signed | FA91 |
| ETERNUS LT260 | 2012\2012R2 | 8.2.0.1, 05/22/2014, signed | 6.71 |   | IBMLTO7 HH FC | 6.2.5.5, 09/08/2015, signed | FA11 |
| ETERNUS LT260 | 2012\2012R2 | 8.2.0.1, 05/22/2014, signed | 6.71 |   | IBM LTO7 HH SAS | 6.2.5.5, 09/08/2015, signed | FA11 |
| ETERNUS LT260 | 2012\2012R2 | 8.2.0.1, 05/22/2014, signed | 7.50 |   | IBM LTO8 HH FC | 6.2.6.6, 10/24/2017, signed | HB81 |
| ETERNUS LT260 | 2012\2012R2 | 8.2.0.1, 05/22/2014, signed | 7.50 |   | IBM LTO8 HH SAS | 6.2.6.6, 10/24/2017, signed | HB81 |
| ETERNUS LT260 | 2016 | 8.2.0.6, 07/03/2017, signed | 7.50 |   | IBM LTO8 HH FC | 6.2.6.6, 10/24/2017, signed | HB81 |
| ETERNUS LT260 | 2016 | 8.2.0.6, 07/03/2017, signed | 7.50 |   | IBM LTO8 HH SAS | 6.2.6.6, 10/24/2017, signed | HB81 |


## Hewlett Packard Enterprise

::: moniker range="<=sc-dpm-2019"

| Library Model Name | Operating System | Changer Driver Version | Library Firmware Revision | Tape Drive Type | Tape Driver Version | Tape Drive Firmware Revision |
| --- | --- | --- | --- | --- | --- | --- |
| Standalone Drive |   | N/A | N/A | HPE LTO7 HPE LTO8 | 1.0.9.1 or later 1.0.9.3 or later | G9Q1 or later <br><br>J4DB or later |
| StoreOnce VTL |   | HP StoreEver Tape Drivers for Windows v4.0.0.0 or later | 3.11.x or later | HP LTO Drives | HP StoreEver Tape Drivers for Windows v4.0.0.0 or later | N/A |
| ESL G3 |   | HP StoreEver Tape Drivers for Windows v4.0.0.0 or later | 680H.GS50501 MCB2 or later <br>656H.GS10801 MCB1 or later | HPE LTO7 FH FC <br><br>HP LTO6 FH FC <br><br>HP LTO5 FH FC <br><br>HP LTO4 FH FC | HP StoreEver Tape Drivers for Windows v4.0.0.0 or later | FA18 or later <br><br>J3PW or later <br><br>I6GW or later <br><br>H6HW or later |
| MSL 6480 |   | HP StoreEver Tape Drivers for Windows v4.4.0.0 or later | 4.60 or later | HPE LTO8 HH FC <br><br>HPE LTO8 HH SAS <br><br>HPE LTO7 HH FC <br><br>HPE LTO7 HH SAS <br><br>HP LTO6 HH FCHP LTO6 HH SAS <br><br>HP LTO5 FH FC <br><br>HP LTO5 HH FC <br><br>HP LTO5 HH SAS <br><br>HP LTO4 FH FC <br><br>HP LTO4 HH SAS | HPE StoreEver Tape Drivers for Windows v4.4.0.0 or later | J4DB or later <br><br>J4DB or later <br><br>FA17 or later <br><br>FA17 or later <br><br>252W or later <br><br>352W or later <br><br>I6GW or later <br><br>Y6DW or later <br><br>Z6DW or later <br><br>H6FW or later <br><br>U62W or later |
| MSL 3040 |   | HP StoreEver Tape Drivers for Windows v4.4.0.0 or later | 3210 or later | HPE LTO8 HH FC <br><br>HPE LTO8 HH SAS | HP StoreEver Tape Drivers for Windows v4.4.0.0 or later | J4DB or later <br><br>J4DB or later |
| MSL G3 Family |   | HP StoreEver Tape Drivers for Windows v4.4.0.0 or later | MSL8096-1130 or later <br><br>MSL4048-8.70 or later <br><br>MSL2024-6.20 or later | HPE LTO8 HH FC <br><br>HPE LTO8 HH SAS <br><br>HPE LTO7 HH FC <br><br>HPE LTO7 HH SAS <br><br>HP LTO6 HH FC <br><br>HP LTO6 HH SAS <br><br>HP LTO5 FH FC <br><br>HP LTO5 HH FC <br><br>HP LTO5 HH SAS <br><br>HP LTO4 FH FC <br><br>HP LTO4 HH SAS | HPE StoreEver Tape Drivers for Windows v4.4.0.0 or later | J4DB or later <br><br>J4DB or later <br><br>FA17 or later <br><br>FA17 or later <br><br>252W or later <br><br>352W or later <br><br>I6GW or later <br><br>Y6DW or later <br><br>Z6DW or later <br><br>H6FW or later <br><br>U62W or later |
| 1/8 G2 Autoloader |   | HP StoreEver Tape Drivers for Windows v4.4.0.0 or later | 4.30 or later | HPE LTO8 HH FC <br><br>HPE LTO8 HH SAS <br><br>HPE LTO7 HH FC <br><br>HPE LTO7 HH SAS <br><br>HP LTO6 HH FC <br><br>HP LTO6 HH SAS <br><br>HP LTO5 HH FC <br><br>HP LTO5 HH SAS <br><br>HP LTO4 HH SAS | HPE StoreEver Tape Drivers for Windows v4.4.0.0 or later | J4DB or later <br><br>J4DB or later <br><br>FA17 or later <br><br>FA17 or later <br><br>252W or later <br><br>352W or later <br><br>Y6DW or later <br><br>Z6DW or later <br><br>U62W or later |

::: moniker-end

::: moniker range="sc-dpm-2022"

| Library Model Name | Operating System | Changer Driver Version | Library Firmware Revision | Tape Drive Type | Tape Driver Version | Tape Drive Firmware Revision |
| --- | --- | --- | --- | --- | --- | --- |
| Standalone Drive | - <br><br>Win Server 2016  | N/A <br><br>N/A | N/A <br><br>N/A | HPE LTO7 HPE LTO8<br><br>HPE LTO9 HH SAS | 1.0.9.1 or later 1.0.9.3 or later <br><br>1.09.4 or later | G9Q1 or later <br><br>J4DB or later <br><br>P371 or later |
| StoreOnce VTL |   | HP StoreEver Tape Drivers for Windows v4.0.0.0 or later | 3.11.x or later | HP LTO Drives | HP StoreEver Tape Drivers for Windows v4.0.0.0 or later | N/A |
| ESL G3 |   | HP StoreEver Tape Drivers for Windows v4.0.0.0 or later | 680H.GS50501 MCB2 or later <br>656H.GS10801 MCB1 or later | HPE LTO7 FH FC <br><br>HP LTO6 FH FC <br><br>HP LTO5 FH FC <br><br>HP LTO4 FH FC | HP StoreEver Tape Drivers for Windows v4.0.0.0 or later | FA18 or later <br><br>J3PW or later <br><br>I6GW or later <br><br>H6HW or later |
| MSL 6480 |  - <br><br>Win Server 2016 | HP StoreEver Tape Drivers for Windows v4.4.0.0 or later <br><br>HPE StoreEver Tape Drivers for Windows 4.6.0.0 or later | 4.60 or later <br><br>6.40 or later | HPE LTO8 HH FC <br><br>HPE LTO8 HH SAS <br><br>HPE LTO7 HH FC <br><br>HPE LTO7 HH SAS <br><br>HP LTO6 HH FCHP LTO6 HH SAS <br><br>HP LTO5 FH FC <br><br>HP LTO5 HH FC <br><br>HP LTO5 HH SAS <br><br>HP LTO4 FH FC <br><br>HP LTO4 HH SAS <br><br>HPE LTO9 HH FC <br><br>HPE LTO9 HH SAS | HPE StoreEver Tape Drivers for Windows v4.4.0.0 or later <br><br>HPE StoreEver Tape Drivers for Windows 4.6.0.0 or later | J4DB or later <br><br>J4DB or later <br><br>FA17 or later <br><br>FA17 or later <br><br>252W or later <br><br>352W or later <br><br>I6GW or later <br><br>Y6DW or later <br><br>Z6DW or later <br><br>H6FW or later <br><br>U62W or later <br><br>P371 or later |
| MSL 3040 | - <br><br>Win Server 2016  | HP StoreEver Tape Drivers for Windows v4.4.0.0 or later <br><br>HPE StoreEver Tape Drivers for Windows 4.6.0.0 or later | 3210 or later <br><br>3290 or later | HPE LTO8 HH FC <br><br>HPE LTO8 HH SAS <br><br>HPE LTO9 HH FC <br><br>HPE LTO9 HH SAS | HP StoreEver Tape Drivers for Windows v4.4.0.0 or later <br><br>HPE StoreEver Tape Drivers for Windows 4.6.0.0 or later | J4DB or later <br><br>J4DB or later <br><br>P371 or later |
| MSL G3 Family |   | HP StoreEver Tape Drivers for Windows v4.4.0.0 or later | MSL8096-1130 or later <br><br>MSL4048-8.70 or later <br><br>MSL2024-6.20 or later | HPE LTO8 HH FC <br><br>HPE LTO8 HH SAS <br><br>HPE LTO7 HH FC <br><br>HPE LTO7 HH SAS <br><br>HP LTO6 HH FC <br><br>HP LTO6 HH SAS <br><br>HP LTO5 FH FC <br><br>HP LTO5 HH FC <br><br>HP LTO5 HH SAS <br><br>HP LTO4 FH FC <br><br>HP LTO4 HH SAS | HPE StoreEver Tape Drivers for Windows v4.4.0.0 or later | J4DB or later <br><br>J4DB or later <br><br>FA17 or later <br><br>FA17 or later <br><br>252W or later <br><br>352W or later <br><br>I6GW or later <br><br>Y6DW or later <br><br>Z6DW or later <br><br>H6FW or later <br><br>U62W or later |
| 1/8 G2 Autoloader |   | HP StoreEver Tape Drivers for Windows v4.4.0.0 or later | 4.30 or later | HPE LT09 HH FC <br><br>HPE LT09 HH SAS <br><br>HPE LTO8 HH FC <br><br>HPE LTO8 HH SAS <br><br>HPE LTO7 HH FC <br><br>HPE LTO7 HH SAS <br><br>HP LTO6 HH FC <br><br>HP LTO6 HH SAS <br><br>HP LTO5 HH FC <br><br>HP LTO5 HH SAS <br><br>HP LTO4 HH SAS | HPE StoreEver Tape Drivers for Windows v4.4.0.0 or later | J4DB or later <br><br>J4DB or later <br><br>FA17 or later <br><br>FA17 or later <br><br>252W or later <br><br>352W or later <br><br>Y6DW or later <br><br>Z6DW or later <br><br>U62W or later |
|1/8 G3 Tape Autoloader|Win Server 2025, 2019 and 2016|3.0.0.10|1000|HPE LTO-9<br><br>HPE LTO-8<br><br>HPE LTO-7<br><br>HPE LTO-6|1.0.9.4<br><br>1.0.9.4<br><br>1.0.9.4<br><br>1.0.9.4|R3G3<br><br>Q387<br><br>Q387<br><br>35PW|
|MSL2024 G4 Tape Library|Win Server 2025, 2019 and 2016|3.0.0.10|1000|HPE LTO-9<br><br>HPE LTO-8<br><br>HPE LTO-7<br><br>HPE LTO-6|1.0.9.4<br><br>1.0.9.4<br><br>1.0.9.4<br><br>1.0.9.4|R3G3<br><br>Q387<br><br>Q387<br><br>35PW|

::: moniker-end

::: moniker range="sc-dpm-2025"

| Library Model Name | Operating System | Changer Driver Version | Library Firmware Revision | Tape Drive Type | Tape Driver Version | Tape Drive Firmware Revision |
| --- | --- | --- | --- | --- | --- | --- |
| Standalone Drive | - <br><br>Win Server 2016  | N/A <br><br>N/A | N/A <br><br>N/A | HPE LTO7 HPE LTO8<br><br>HPE LTO9 HH SAS | 1.0.9.1 or later 1.0.9.3 or later <br><br>1.09.4 or later | G9Q1 or later <br><br>J4DB or later <br><br>P371 or later |
| StoreOnce VTL |   | HP StoreEver Tape Drivers for Windows v4.0.0.0 or later | 3.11.x or later | HP LTO Drives | HP StoreEver Tape Drivers for Windows v4.0.0.0 or later | N/A |
| ESL G3 |   | HP StoreEver Tape Drivers for Windows v4.0.0.0 or later | 680H.GS50501 MCB2 or later <br>656H.GS10801 MCB1 or later | HPE LTO7 FH FC <br><br>HP LTO6 FH FC <br><br>HP LTO5 FH FC <br><br>HP LTO4 FH FC | HP StoreEver Tape Drivers for Windows v4.0.0.0 or later | FA18 or later <br><br>J3PW or later <br><br>I6GW or later <br><br>H6HW or later |
| MSL 6480 |  - <br><br>Win Server 2016 | HP StoreEver Tape Drivers for Windows v4.4.0.0 or later <br><br>HPE StoreEver Tape Drivers for Windows 4.6.0.0 or later | 4.60 or later <br><br>6.40 or later | HPE LTO8 HH FC <br><br>HPE LTO8 HH SAS <br><br>HPE LTO7 HH FC <br><br>HPE LTO7 HH SAS <br><br>HP LTO6 HH FCHP LTO6 HH SAS <br><br>HP LTO5 FH FC <br><br>HP LTO5 HH FC <br><br>HP LTO5 HH SAS <br><br>HP LTO4 FH FC <br><br>HP LTO4 HH SAS <br><br>HPE LTO9 HH FC <br><br>HPE LTO9 HH SAS | HPE StoreEver Tape Drivers for Windows v4.4.0.0 or later <br><br>HPE StoreEver Tape Drivers for Windows 4.6.0.0 or later | J4DB or later <br><br>J4DB or later <br><br>FA17 or later <br><br>FA17 or later <br><br>252W or later <br><br>352W or later <br><br>I6GW or later <br><br>Y6DW or later <br><br>Z6DW or later <br><br>H6FW or later <br><br>U62W or later <br><br>P371 or later |
| MSL 3040 | - <br><br>Win Server 2016  | HP StoreEver Tape Drivers for Windows v4.4.0.0 or later <br><br>HPE StoreEver Tape Drivers for Windows 4.6.0.0 or later | 3210 or later <br><br>3290 or later | HPE LTO8 HH FC <br><br>HPE LTO8 HH SAS <br><br>HPE LTO9 HH FC <br><br>HPE LTO9 HH SAS | HP StoreEver Tape Drivers for Windows v4.4.0.0 or later <br><br>HPE StoreEver Tape Drivers for Windows 4.6.0.0 or later | J4DB or later <br><br>J4DB or later <br><br>P371 or later |
| MSL G3 Family |   | HP StoreEver Tape Drivers for Windows v4.4.0.0 or later | MSL8096-1130 or later <br><br>MSL4048-8.70 or later <br><br>MSL2024-6.20 or later | HPE LTO8 HH FC <br><br>HPE LTO8 HH SAS <br><br>HPE LTO7 HH FC <br><br>HPE LTO7 HH SAS <br><br>HP LTO6 HH FC <br><br>HP LTO6 HH SAS <br><br>HP LTO5 FH FC <br><br>HP LTO5 HH FC <br><br>HP LTO5 HH SAS <br><br>HP LTO4 FH FC <br><br>HP LTO4 HH SAS | HPE StoreEver Tape Drivers for Windows v4.4.0.0 or later | J4DB or later <br><br>J4DB or later <br><br>FA17 or later <br><br>FA17 or later <br><br>252W or later <br><br>352W or later <br><br>I6GW or later <br><br>Y6DW or later <br><br>Z6DW or later <br><br>H6FW or later <br><br>U62W or later |
| 1/8 G2 Autoloader |   | HP StoreEver Tape Drivers for Windows v4.4.0.0 or later | 4.30 or later | HPE LT09 HH FC <br><br>HPE LT09 HH SAS <br><br>HPE LTO8 HH FC <br><br>HPE LTO8 HH SAS <br><br>HPE LTO7 HH FC <br><br>HPE LTO7 HH SAS <br><br>HP LTO6 HH FC <br><br>HP LTO6 HH SAS <br><br>HP LTO5 HH FC <br><br>HP LTO5 HH SAS <br><br>HP LTO4 HH SAS | HPE StoreEver Tape Drivers for Windows v4.4.0.0 or later | J4DB or later <br><br>J4DB or later <br><br>FA17 or later <br><br>FA17 or later <br><br>252W or later <br><br>352W or later <br><br>Y6DW or later <br><br>Z6DW or later <br><br>U62W or later |

::: moniker-end

## IBM

| Library Model Name | Operating System | Changer Driver Version | Library Firmware Revision | Tape Drive Type | Tape Driver Version | Tape Drive Firmware Revision |
| --- | --- | --- | --- | --- | --- | --- |
| Standalone Drive |   | N/A | N/A | IBM LTO5 FH Standalone | Inbox ltotape.sys |   |
| Total Storage 3572 (TS2900) |   | ibmcg2k12, 6.2.3.3 | B.50 | LTO6 HH SAS | ibmcg2k12, 6.2.3.3 | CB21 |
| Total Storage 3572 (TS2900) |   | ibmcg2k8, 6.2.1.8, x64 | 17 | LTO5 HH SAS | ibmtp2k8, 6.2.1.8, x64 | B6W1 |
| Total Storage 3573 |   | ibmcg2k8, 6.2.1.8, x64 | A.40 | IBM LTO5 3580 | ibmtp2k8, 6.2.1.8, x64 | B6W0 |
| Total Storage 3573 (TS3100/TS3200) |   | ibmcg2k12, 6.2.3.3 | B.50 | LTO6 FH FC | ibmcg2k12, 6.2.3.3 | C9T4 |
| Total Storage 3573 (TS3100/TS3200) |   | ibmcg2k8, 6.2.1.8, x64 | A.40 | LTO4 FH FC | ibmcg2k8, 6.2.1.8, x64 | A230 |
| Total Storage 3573 (TS3100/TS3200) |   | ibmcg2k12, 6.2.3.3 | B.50 | LTO6 HH SAS | ibmcg2k12, 6.2.3.3 | C9T5 |
| Total Storage 3576 (TS3310) |   | ibmcg2k12, 6.2.3.3 | 630G | LTO6 FH FC | ibmcg2k12, 6.2.3.3 | CB20 |
| Total Storage 3584 (TS3500/TS4500) | 2012/2012R2 | 6.2.5.6 | F030 | LTO6 FH FC | 6.2.5.6 | F9A0 |
| Total Storage 3572 (TS2900) | 2012/2012R2 | 6.2.5.6 | 58 | LTO7 HH SAS | 6.2.5.6 | FA11 |
| Total Storage 3573 (TS3100) | 2012/2012R2 | 6.2.5.6 | D.00 | LTO7 FH FC | 6.2.5.6 | FA10 |
| Total Storage 3573 (TS3100) | 2012/2012R2 | 6.2.5.6 | D.00 | LTO7 HH FC/SAS | 6.2.5.6 | FA11 |
| Total Storage 3573 (TS3200) | 2012/2012R2 | 6.2.5.6 | D.00 | LTO7 FH FC | 6.2.5.6 | FA10 |
| Total Storage 3573 (TS3200) | 2012/2012R2 | 6.2.5.6 | D.00 | LTO7 HH FC/SAS | 6.2.5.6 | FA11 |
| Total Storage 3576 (TS3310) | 2012/2012R2 | 6.2.5.6 | 670G | LTO7 FH FC | 6.2.5.6 | FA10 |
| Total Storage 3584 (TS3500/TS4500) | 2012/2012R2 | 6.2.5.6 | F030/1201 | LTO7 FH FC | 6.2.5.6 | F980 |
| Total Storage 3584 (TS4500/TS3500) |   | 6.2.6.6 | 1413/G060 | LTO8 | 6.2.6.6 | J4D0 |
| Total Storage 3573 (TS4300/TS3200/TS3100) |   | 6.2.6.6 | 1112/F00 | LTO8 | 6.2.6.6 | J4D0/J4D1 |
| Total Storage 3572 (TS2900) |   | 6.2.6.6 | 0080 | LTO8 | 6.2.6.6 | HB83 |

> [!Tip]
> The following registry key needs to be added to enable support for TS 2900: DWORD **RSMCompatMode** under `HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Microsoft Data Protection Manager\Agent` and set it to 29 (decimal).

## Quantum

| Library Model Name | Operating System | Changer Driver Version | Library Firmware Revision | Other Libraries in Test | Tape Drive Type | Tape Driver Version | Tape Drive Firmware Revision |
| --- | --- | --- | --- | --- | --- | --- | --- |
| DXi6701 Scalar (emulating i2000) |   | Qi2Kx64.sys, 7.5.0.0 | V 2.1.1 | DXi6702 | HP LTO5 | hplto.sys, 1.6.0.3 | I30Z |
| DXi6701 Scalar (emulating i2000) |   | Qi2Kx64.sys, 7.5.0.0 | V 2.1.1 | DXi6702 | IBM LTO5 | ibmtp2k8.sys, 6.2.1.8 | A5MO |
| DXi8500 2TB Scalar (emulating i2000) |   | Qi2Kx64.sys, 7.5.0.0 | V1.5.0\_85 |   | HP LTO4 | hplto.sys, 1.6.0.3 | H44Z |
| DXi8500 2TB Scalar (emulating i2000) |   | Qi2Kx64.sys, 7.5.0.0 | V1.5.0\_85 |   | IBM LTO4 | ibmtp2k8.sys, 6.2.1.8 | A2FB |
| DXi8502 (VTL) |   | Qi500X64.sys, 7.5.0.0 | 2.0.2\_85 |   | HP LTO5 | hplto.sys, 1.6.0.3 | I30Z |
| DXi6902 (VTL) |   | Qi2kx64.sys, 7.6.1.0 | 3.0 |   | HP LTO5IBM LTO5 | hplto.xyx, 1.0.7.16.2.9200.16348 | I6PZF990 |
| DXi6902 (VTL) emulating Scalar i6000 | Windows 2016 | QntmLib.sys 1.0.0.1 |  3.2.5 |   | IBM LTO5 | ibmtp2k16 6.2.6.1 | A5M0 |
| DXi4701 (VTL) |   | Qi2kx64.sys, 7.6.1.0 | 3.0 |   | HP LTO5IBM LTO5 | hplto.xyx, 1.0.7.16.2.9200.16348 | I6PZF990 |
| DXi4701 (VTL) emulating Scalar i6000 | Windows 2016 | QntmLib.sys 1.0.0.1 | 3.2.5 |   | IBM LTO5 | ibmtp2k16 6.2.6.1 | A5M0 |
| Scalar i40 |   | Qi40X64.sys, 7.5.2.0 | 130G |   | HP LTO5 | hplto.sys, 1.6.0.2 | Y35Z |
| Scalar i40 |   | Qi40X64.sys, 7.6.0.0 | 175G |   | IBM LTO6 | 6.3.9600.16384 | F3JD |
| Scalar i40 |   | Qi40X64.sys, 7.6.0.0 | 180B |   | IBM LTO7 | 6.3.9600.16384 | FA17 |
| Scalar i80 |   | Qi40X64.sys, 7.5.2.0 | 130G |   | HP LTO5 | hplto.sys, 1.6.0.2 | Y35Z |
| Scalar i80 |   | Qi40X64.sys, 7.6.0.0 | 175G |   | IBM LTO6 | 6.3.9600.16384 | F3JD |
| Scalar i80 |   | Qi40X64.sys, 7.6.0.0 | 180G |   | IBM LTO7 | 6.3.9600.16384 | FA17 |
| Scalar i500 |   | ad500x64.sys, 7.4.0.0 | 500G |   | IBM LTO4 | ibmtp2k3.sys, 6.1.8.9 | 82FB |
| Scalar i500 |   | Qi500X64.sys, 7.5.0.0 | 607G |   | HP LTO5 | hplto.sys, 1.6.0.2 | I3EZ |
| Scalar i500 |   | Qi500X64.sys, 7.5.0.0 | 607G |   | IBM LTO5 | ibmtp2k8.sys, 6.1.9.9 | B170 |
| Scalar i500 |   | Qi500X64.sys, 7.5.0.0 | 607G |   | HP LTO4 | hplto.sys, 1.6.0.2 | H58Z |
| Scalar i500 |   | Qi500x64.sys, 7.6.0.0 | 670G |   | IBM LTO6 | 6.3.9600.16384 | F9A0 |
| Scalar i500 |   | Qi500x64.sys, 7.6.0.0 | 670G |   | IBM LTO7 | 6.3.9600.16384 | FA10 |
| Scalar i500 |  Windows 2016 | QtmLib 1.0.0.1 | 700G |   | IBM LTO8 | ltotape 10.0.14393.206 | H7TF |
| Scalar i6000 |   | Qi6Kx64.sys, 7.5.5.0 | 606A.GS00301 | Scalar i2000 | HP LTO4 FC | hplto.sys, 1.6.0.1 | H58Z |
| Scalar i6000 |   | Qi6Kx64.sys, 7.5.5.0 | 606A.GS00301 | Scalar i2000 | HP LTO5 FC | hplto.sys, 1.6.0.1 | I3AZ |
| Scalar i6000 |   | Qi6Kx64.sys, 7.5.5.0 | 606A.GS00301 | Scalar i2000 | IBM LTO5 FC | lto.sys, 6.1.7600.16385 | A6SA |
| Scalar i6000 |   | Qi6Kx64.sys, 7.5.5.0 | 606A.GS00301 | Scalar i2000 | IBM LTO5 FC | lto.sys, 6.1.7600.16385 | B170 |
| Scalar i6000 |   | Qi6Kx64.sys, 7.5.5.0 | 606A.GS00301 | Scalar i2000 | IBM LTO4 FC | lto.sys, 6.1.7600.16385 | A23D |
| Scalar i6000 |   | Qi6kx64.sys, 7.6.1.0 | 720Q |   | IBM LTO6 | 6.3.9600.16384 | F9A0 |
| Scalar i6000 |   | Qi6kx64.sys, 7.6.1.0 | 720Q |   | IBM LTO7 | 6.3.9600.16384 | FA10 |
| Scalar i6000 | Windows 2016 | QntmLib 1.0.0.1 | 760Q |   | IBM LTO8 | ltotape 10.0.14393.206 | H980 |
| Superloader |   | QsmcX64.sys, 2.5.1.0 | V61 |   | Quantum LTO4 | QLTOx64.sys, 3.4.0 | 2103 |
| Superloader |   | QsmcX64.sys, 2.6.2.0 | 75 |   | Quantum LTO5 | QLTOx64.sys, 3.4.0.0 | 3060 |
| Superloader |   | QsmcX64.sys, 2.6.3.0 | V91 |   | IBM LTO5 | 6.3.9600.16384 | F3HB |
| Superloader |   | QsmcX64.sys, 2.6.3.0 | V91 |   | IBM LTO6 | 6.3.9600.16384 | F3JD |
| Superloader |   | QsmcX64.sys, 2.6.3.0 | V92 |   | IBM LTO7 | 6.3.9600.16384 | FA17 |
| Superloader | Windows 2016 | QntmLib, 1.0.0.1 | V94 |   | IBM LTO8 | ltotape 10.0.14393.206 | H7TF |
|  Scalar i3 |   | 6.3.9600.16384 | 110G |   | IBM LTO6 HH | 6.3.9600.16384 | G9P1 |
|  Scalar i3 |   | 6.3.9600.16384 | 110G |   | IBM LTO7 HH | 6.3.9600.16384 | G9Q1 |
|  Scalar i3 |  Windows 2016 | QntmLib 1.0.0.1 | 150G |   | IBM LTO8 HH | ltotape 10.0.14393.206 | H7TF |
|  Scalar i6 |   | 6.3.9600.16384 | 110G |   | IBM LTO6 | 6.3.9600.16384 | G9P0 |
|  Scalar i6 |   | 6.3.9600.16384 | 110G |   | IBM LTO7 | 6.3.9600.16384 | G9Q0 |
|  Scalar i6 | Windows 2016 | QntmLib 1.0.0.1 | 150G |   | IBM LTO8 | ltotape 10.0.14393.206 | H7TF |

## Tandberg Data

| Library Model Name | Operating System | Changer Driver Version | Library Firmware Revision | Other Libraries in Test | Tape Drive Type | Tape Driver Version | Tape Drive Firmware Revision |
| --- | --- | --- | --- | --- | --- | --- | --- |
| StorageLoader LTO |   | 1.8.0.11 | 3.47 |   | HP 3000 LTO 5 HH SAS | 1.0.6.1 | Z21U |
| StorageLoader LTO |   | 1.8.0.11 | 3.47 |   | HP 3000 LTO 5 HH SAS | 1.0.6.1 | Z33U |
|   |   | exbchgx64.sys, 2.1.9.0, 11/21/2008, signed, 64 bit | V1C270 |   | LTO4 | hplto.sys, 1.0.5.2, 12/10/2007, signed, 64 bit | D217 |
|   |   | exachgx64.sys, 2.1.9.0, 11/21/2008, unsigned, 64 bit | V1C270 |   | LTO4 | ibmtp2k8.sys, 6.1.8.9, 3/19/2008, signed, 64 bit | 85V3 |
|   |   | exbchgx64.sys, 2.1.9.0, 11/21/2008, signed, 64 bit | V1D170 |   | LTO4 | ibmtp2k8.sys, 6.1.9.5, 6/11/2008, signed, 64 bit | 85V3 |
|   |   | exachgx64.sys, 2.1.9.0, 11/21/2008, unsigned, 64 bit | V1D170 |   | LTO4 | ibmtp2k3.sys, 6.1.8.9, 3/19/2008, signed, 64 bit | 85V3 |
|   |   | 3.01.0009.0 | V1C290 | Magnum 224, StorageLoader 2U LTO | HP 3000 LTO 5 HH SAS | 1.0.6.1 | Z21U |
|   |   | 3.01.0009.0 | V1C290 | Magnum 224, StorageLoader 2U LTO | HP 3000 LTO 5 HH SAS | 1.0.6.1 | Z33U |
|   |   | 3.01.0009.0 | V1C290 | Magnum 224, StorageLoader 2U LTO | HP 3000 LTO 5 HH FC | 1.0.6.1 | Y21U |
|   |   | 3.01.0009.0 | V1C290 | Magnum 224, StorageLoader 2U LTO | HP 3000 LTO 5 HH FC | 1.0.6.1 | Y31U |
|   |   | 3.01.0009.0 | V1C290 | Magnum 224, StorageLoader 2U LTO | HP 3000 LTO 5 HH FC | 1.0.6.1 | Y32U |
|   |   | 3.01.0009.0 | V1C290 | Magnum 224, StorageLoader 2U LTO | HP 1760 LTO 4 HH FC | 1.0.6.1 | V51U |
|   |   | 3.01.0009.0 | V1C290 | Magnum 224, StorageLoader 2U LTO | HP 1760 LTO 4 HH SAS | 1.0.6.1 | U51U |
|   |   | 3.01.0009.0 | V1C290 | Magnum 224, StorageLoader 2U LTO | HP 1760 LTO 4 HH SCSI | 1.0.6.1 | W51U |
|   |   | tdsafe.sys, 1.7.0.0, 1/4/2008, signed, 64 bit | 3.42 |   | LTO4 | hplto.sys, 1.0.5.2, 12/10/2007, signed, 64 bit | W22U |
|   |   | tdsafe.sys, 1.7.0.0, 1/4/2008, signed, 64 bit | 3.8 |   | LTO4 | ltotape.sys, 6.0.6001.18000, 6/21/2006, signed, 64 bit | 85V3 |
|   |   | tdsafe.sys, 1.7.0.0, 1/4/2008, signed, 64 bit | 3.63 |   | LTO4 | ibmtp2k8.sys, 6.1.8.9, 3/19/2008, signed, 64 bit | 85V3 |
|   |   | 1.8.0.11 | 3.47 |   | HP 3000 LTO 5 HH FC | 1.0.6.1 | Y21U |
|   |   | 1.8.0.11 | 3.47 |   | HP 3000 LTO 5 HH FC | 1.0.6.1 | Y31U |
|   |   | 1.8.0.11 | 3.47 |   | HP 3000 LTO 5 HH FC | 1.0.6.1 | Y32U |
|   |   | 1.8.0.11 | 3.47 |   | HP 1760 LTO 4 HH SAS | 1.0.6.1 | U51U |

## Oracle StorageTek

| Library Model Name | Operating System | Changer Driver Version | Library Firmware Revision | Tape Drive Type | Tape Driver Version | Tape Drive Firmware Revision |
| --- | --- | --- | --- | --- | --- | --- |
| SL150 |   |   | 2.50 | HP LTO5 HH FC |   | Y6IS |
| SL150 |   |   | 2.50 | HP LTO5 HH SAS |   | Z6FS |
| SL150 |   |   | 2.50 | HP LTO6 HH FC |   | 25FS |
| SL150 |   |   | 2.50 | HP LTO6 HH SAS |   | 35FS |
| SL150 |   |   | 2.50 | IBM LTO7 HH FC |   | G341 |
| SL150-Tested |   |   | 2.50 | IBM LTO7 HH SAS |   | G341 |
