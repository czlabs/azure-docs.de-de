---
title: Windows-Softwarekosten für reservierte Azure-Instanzen – Azure-Abrechnung | Microsoft-Dokumentation
description: Erfahren Sie, welche Verbrauchseinheiten für Windows-Software nicht in den Kosten für reservierte Azure-VM-Instanzen enthalten sind.
services: billing
documentationcenter: ''
author: manish-shukla01
manager: manshuk
editor: ''
tags: billing
ms.service: billing
ms.devlang: na
ms.topic: conceptual
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 05/09/2018
ms.author: manshuk
ms.openlocfilehash: b526ca578a72d7d35fb4198affeb02db4d308b20
ms.sourcegitcommit: 688a394c4901590bbcf5351f9afdf9e8f0c89505
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 05/18/2018
ms.locfileid: "34303350"
---
# <a name="windows-software-costs-not-included-with-azure-reserved-instances"></a>Nicht in reservierten Azure-Instanzen enthaltene Windows-Softwarekosten

Wenn Sie für Ihre reservierten VM-Instanzen keinen Azure-Hybridvorteil besitzen, werden Ihnen die im folgenden Abschnitt aufgeführten Verbrauchseinheiten für Windows-Software berechnet.

## <a name="windows-software-meters-not-included-in-reserved-instance-cost"></a>Kosten für nicht in reservierten Instanzen enthaltene Verbrauchseinheiten für Windows-Software

| MeterId | MeterName in Verwendungsdatei | Von virtuellem Computer verwendet |
| ------- | ------------------------| --- |
| e7e152ac-f29c-4cce-ad6e-026192c01ef2 | Burstzeiträume für reservierte Windows Server-Instanzen (1 Kern) | B-Serie |
| cac255a2-9f0f-4c62-8bd6-f0fa449c5f76 | Burstzeiträume für reservierte Windows Server-Instanzen (2 Kerne) | B-Serie |
| 09756b58-3fb5-4390-976d-9ddd14f9ed18 | Burstzeiträume für reservierte Windows Server-Instanzen (4 Kerne) | B-Serie |
| e828cb37-5920-4dc7-b30f-664e4dbcb6c7 | Burstzeiträume für reservierte Windows Server-Instanzen (8 Kerne) | B-Serie |
| f65a06cf-c9c3-47a2-8104-f17a8542215a | Reservierte Windows Server-Instanzen (1 Kern) | Alle außer B-Serie |
| b99d40ae-41fe-4d1d-842b-56d72f3d15ee | Reservierte Windows Server-Instanzen (2 Kerne) | Alle außer B-Serie |
| 1cb88381-0905-4843-9ba2-7914066aabe5 | Reservierte Windows Server-Instanzen (4 Kerne) | Alle außer B-Serie |
| 07d9e10d-3e3e-4672-ac30-87f58ec4b00a | Reservierte Windows Server-Instanzen (6 Kerne) | Alle außer B-Serie |
| 603f58d1-1e96-460b-a933-ce3775ac7e2e | Reservierte Windows Server-Instanzen (8 Kerne) | Alle außer B-Serie |
| 36aaadda-da86-484a-b465-c8b5ab292d71 | Reservierte Windows Server-Instanzen (12 Kerne) | Alle außer B-Serie |
| 02968a6b-1654-4495-ada6-13f378ba7172 | Reservierte Windows Server-Instanzen (16 Kerne) | Alle außer B-Serie |
| 175434d8-75f9-474b-9906-5d151b6bed84 | Reservierte Windows Server-Instanzen (20 Kerne) | Alle außer B-Serie |
| 77eb6dd0-88f5-4a16-ab39-05d1742efb25 | Reservierte Windows Server-Instanzen (24 Kerne) | Alle außer B-Serie |
| 0d5bdf46-b719-4b1f-a780-b9bdfffd0591 | Reservierte Windows Server-Instanzen (32 Kerne) | Alle außer B-Serie |
| f1214b5c-cc16-445f-be6c-a3bb75f8395a | Reservierte Windows Server-Instanzen (40 Kerne) | Alle außer B-Serie |
| 637b7c77-65ad-4486-9cc7-dc7b3e9a8731 | Reservierte Windows Server-Instanzen (64 Kerne) | Alle außer B-Serie |
| da612742-e7cc-4ca3-9334-0fb7234059cd | Reservierte Windows Server-Instanzen (72 Kerne) | Alle außer B-Serie |
| a485cb8c-069b-4cf3-9a8e-ddd84b323da2 | Reservierte Windows Server-Instanzen (128 Kerne) | Alle außer B-Serie |
| 904c5c71-1eb7-43a6-961c-d305a9681624 | Reservierte Windows Server-Instanzen (256 Kerne) | Alle außer B-Serie |
| 6fdab81b-4284-4df9-8939-c237cc7462fe | Reservierte Windows Server-Instanzen (96 Kerne) | Alle außer B-Serie |

Sie können die Kosten jeder dieser Verbrauchseinheiten über die Azure RateCard-API abrufen. Informationen zum Abrufen der Tarife für eine Azure-Verbrauchseinheit finden Sie unter [Abrufen von Preis- und Metadateninformationen für in einem Azure-Abonnement verwendete Ressourcen](https://msdn.microsoft.com/library/azure/mt219004).

## <a name="next-steps"></a>Nächste Schritte
Weitere Informationen zu reservierten Azure-Instanzen finden Sie in den folgenden Artikeln:

- [Einsparung von Kosten für virtuelle Computer mit reservierten Azure-Instanzen](billing-save-compute-costs-reservations.md)
- [Vorauszahlen für virtuelle Computer mit reservierten VM-Instanzen](../virtual-machines/windows/prepay-reserved-vm-instances.md)
- [Verwalten von reservierten Instanzen](billing-manage-reserved-vm-instance.md)
- [Grundlegendes zur Anwendung des Rabatts für reservierte VM-Instanzen](billing-understand-vm-reservation-charges.md)
- [Grundlagen zur Verwendung reservierter Azure-Instanzen für Ihr Abonnement mit nutzungsbasierter Zahlung](billing-understand-reserved-instance-usage.md)
- [Grundlegendes zur Nutzung reservierter Instanzen für die Enterprise-Registrierung](billing-understand-reserved-instance-usage-ea.md)

## <a name="need-help-contact-support"></a>Sie brauchen Hilfe? Support kontaktieren

Bei weiteren Fragen [wenden Sie sich an den Support](https://portal.azure.com/?#blade/Microsoft_Azure_Support/HelpAndSupportBlade), um das Problem schnell zu lösen.



