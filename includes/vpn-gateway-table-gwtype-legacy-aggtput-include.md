---
title: Includedatei
description: Includedatei
services: vpn-gateway
author: cherylmc
ms.service: vpn-gateway
ms.topic: include
ms.date: 03/21/2018
ms.author: cherylmc
ms.custom: include file
ms.openlocfilehash: 6efec75884857d93f2e128104136bf59a1114594
ms.sourcegitcommit: 48ab1b6526ce290316b9da4d18de00c77526a541
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 03/23/2018
---
In der folgenden Tabelle sind die Gatewaytypen und der geschätzte zusammengefasste Durchsatz nach Gateway-SKU angegeben. Diese Tabelle betrifft sowohl das Resource Manager-Bereitstellungsmodell als auch das klassische Bereitstellungsmodell. 

Für die einzelnen Gateway-SKUs gelten unterschiedliche Preise. Weitere Informationen finden Sie unter [VPN-Gateway: Preise](https://azure.microsoft.com/pricing/details/vpn-gateway).

Beachten Sie, dass die UltraPerformance-Gateway-SKU nicht in dieser Tabelle enthalten ist. Informationen zur UltraPerformance-SKU finden Sie in der Dokumentation zu [ExpressRoute](../articles/expressroute/expressroute-about-virtual-network-gateways.md).

|  | **VPN Gateway-Durchsatz (1)** | **Max. IPsec-Tunnel für VPN Gateway (2)** | **ExpressRoute-Gateway-Durchsatz** | **Gemeinsame Verwendung von VPN-Gateway und ExpressRoute** |
| --- | --- | --- | --- | --- |
| **Basic-SKU (3)(5)(6)** |100 MBit/s |10 |500 MBit/s (6) |Nein  |
| **Standard-SKU (4)(5)** |100 MBit/s |10 |1.000 MBit/s |Ja |
| **High-Performance-SKU (4)** |200 MBit/s |30 |2.000 MBit/s |Ja |


(1) Der VPN-Durchsatz ist eine grobe Schätzung, die auf Messungen zwischen den VNets einer Azure-Region basiert. Es ist kein garantierter Durchsatz für standortübergreifende Verbindungen über das Internet. Hierbei wird der maximal mögliche Durchsatz gemessen.

(2) Die Tunnelanzahl bezieht sich auf routenbasierte VPNs. Ein richtlinienbasiertes VPN kann nur einen Site-to-Site-VPN-Tunnel unterstützen.

(3) BGP wird für die Basic-SKU nicht unterstützt.

(4) Richtlinienbasierte VPNs werden für diese SKU nicht unterstützt. Sie werden nur für die Basic-SKU unterstützt.

(5) Aktiv-Aktiv-S2S-VPN-Gatewayverbindungen werden für diese SKU nicht unterstützt. Aktiv-Aktiv wird nur in der HighPerformance-SKU unterstützt.

(6) Die Basic-SKU ist für die Verwendung mit ExpressRoute veraltet.
