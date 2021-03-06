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
ms.openlocfilehash: 865f4a963dfbaa7b8392865f8b0c468734673ba0
ms.sourcegitcommit: 48ab1b6526ce290316b9da4d18de00c77526a541
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 03/23/2018
---
### <a name="to-modify-the-local-network-gateway-gatewayipaddress"></a>So ändern Sie die Angabe für „gatewayIpAddress“ für ein Gateway des lokalen Netzwerks

Wenn für das VPN-Gerät, mit dem Sie eine Verbindung herstellen möchten, die öffentliche IP-Adresse geändert wurde, müssen Sie das Gateway des lokalen Netzwerks entsprechend anpassen. Die Gateway-IP-Adresse kann geändert werden, ohne dass eine vorhandene VPN-Gatewayverbindung (sofern vorhanden) entfernt werden muss. Ersetzen Sie zum Ändern der Gateway-IP-Adresse die Werte „Site2“ und „TestRG1“ durch eigene Werte. Verwenden Sie dazu den Befehl [az network local-gateway update](https://docs.microsoft.com/cli/azure/network/local-gateway#az_network_local_gateway_update).

```azurecli
az network local-gateway update --gateway-ip-address 23.99.222.170 --name Site2 --resource-group TestRG1
```

Überprüfen Sie, ob die IP-Adresse in der Ausgabe korrekt ist:

```
"gatewayIpAddress": "23.99.222.170",
```