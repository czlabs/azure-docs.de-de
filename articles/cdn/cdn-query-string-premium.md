---
title: Steuern des Azure CDN-Zwischenspeicherverhaltens mit Abfragezeichenfolgen – Premium-Tarif | Microsoft-Dokumentation
description: Das Zwischenspeichern von Azure CDN-Abfragezeichenfolgen steuert, wie Dateien zwischengespeichert werden, wenn eine Webanforderung eine Abfragezeichenfolge enthält. In diesem Artikel wird das Zwischenspeichern von Abfragezeichenfolgen im Produkt Azure CDN Premium von Verizon beschrieben.
services: cdn
documentationcenter: ''
author: dksimpson
manager: akucer
editor: ''
ms.assetid: 99db4a85-4f5f-431f-ac3a-69e05518c997
ms.service: cdn
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/30/2018
ms.author: mazha
ms.openlocfilehash: a1ef5f3e502b5383343dbec2c427d36054a3edc4
ms.sourcegitcommit: e221d1a2e0fb245610a6dd886e7e74c362f06467
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 05/07/2018
---
# <a name="control-azure-cdn-caching-behavior-with-query-strings---premium-tier"></a>Steuern des Azure CDN-Zwischenspeicherverhaltens mit Abfragezeichenfolgen – Premium-Tarif
> [!div class="op_single_selector"]
> * [Standard-Tarif](cdn-query-string.md)
> * [Premium-Tarif](cdn-query-string-premium.md)
> 
> 

## <a name="overview"></a>Übersicht
Mit Azure Content Delivery Network (CDN) können Sie steuern, wie Dateien für eine Webanforderung, die eine Abfragezeichenfolge enthält, zwischengespeichert werden. In einer Webanforderung mit einer Abfragezeichenfolge ist die Abfragezeichenfolge der Teil der Anforderung, der auf das Fragezeichen („?“) folgt. Eine Abfragezeichenfolge kann ein oder mehrere Schlüssel-Wert-Paare enthalten, wobei der Feldname und sein Wert durch ein Gleichheitszeichen („=“) getrennt sind. Die einzelnen Schlüssel-Wert-Paare sind durch ein kaufmännisches Und-Zeichen („&“) voneinander getrennt. Bespiel: http:\//www.contoso.com/content.mov?field1=value1&field2=value2. Falls mehrere Schlüssel-Wert-Paare in einer Abfragezeichenfolge derselben Anforderung vorhanden sind, spielt die Reihenfolge keine Rolle. 

> [!IMPORTANT]
> Die CDN-Produkte „Standard“ und „Premium“ bieten die gleiche Funktionalität zum Zwischenspeichern von Abfragezeichenfolgen, aber mit einer anderen Benutzeroberfläche. In diesem Artikel wird die Benutzeroberfläche für **Azure CDN Premium von Verizon** beschrieben. Informationen zum Zwischenspeichern von Abfragezeichenfolgen mit Azure CDN Standard-Produkten finden Sie unter [Steuern des Azure CDN-Zwischenspeicherverhaltens mit Abfragezeichenfolgen – Standard](cdn-query-string.md).
>


Es sind drei Abfragezeichenfolgenmodi verfügbar:

- **standard-cache**: Standardmodus. In diesem Modus übergibt der CDN-POP-Knoten (Point of Presence) die Abfragezeichenfolgen bei der ersten Anforderung vom Anforderer an den Ursprungsserver und speichert das Objekt im Cache zwischen. Für alle nachfolgenden Anforderungen des Objekts, die vom POP-Server verarbeitet werden, werden die Abfragezeichenfolgen bis zum Ablauf des zwischengespeicherten Objekts ignoriert.

    >[!IMPORTANT] 
    > Wenn die Tokenberechtigung für einen beliebigen Pfad für dieses Konto aktiviert ist, ist der Standardcachemodus der einzige Modus, der verwendet werden kann. 

- **no-cache**: In diesem Modus werden Anforderungen mit Abfragezeichenfolgen nicht auf dem CDN-POP-Knoten zwischengespeichert. Der POP-Knoten ruft das Objekt direkt vom Ursprungsserver ab und übergibt es bei jeder Anforderung an den Anforderer.

- **unique-cache**: In diesem Modus wird jede Anforderung mit einer eindeutigen URL, einschließlich der Abfragezeichenfolge, als eindeutiges Objekt mit eigenem Cache behandelt. So wird beispielsweise die Antwort vom Ursprungsserver für eine Anforderung von „example.ashx?q=test1“ auf dem POP-Knoten zwischengespeichert und für nachfolgende Caches mit der gleichen Abfragezeichenfolge zurückgegeben. Eine Anforderung von „example.ashx?q=test2“ wird als separates Objekt mit eigener Einstellung für die Gültigkeitsdauer zwischengespeichert.
   
    >[!IMPORTANT] 
    > Verwenden Sie diesen Modus nicht, wenn die Abfragezeichenfolge Parameter enthält, die sich bei jeder Anforderung ändern, z.B. eine Sitzungs-ID oder einen Benutzernamen, da dies zu einer niedrigen Cachetrefferquote führt.

## <a name="changing-query-string-caching-settings-for-premium-cdn-profiles"></a>Ändern der Einstellungen für das Zwischenspeichern von Abfragezeichenfolgen für CDN-Premiumprofile
1. Öffnen Sie ein CDN-Profil, und klicken Sie anschließend auf **Verwalten**.
   
    ![Schaltfläche „Verwalten“ für CDN-Profile](./media/cdn-query-string-premium/cdn-manage-btn.png)
   
    Das CDN-Verwaltungsportal wird geöffnet.
2. Zeigen Sie auf die Registerkarte **HTTP Groß** und dann auf das Flyout-Menü **Cacheeinstellungen**. Klicken Sie auf **Query-String Caching**.
   
    Die Zwischenspeicherungsoptionen für Abfragezeichenfolgen werden angezeigt.
   
    ![Zwischenspeicherungsoptionen für CDN-Abfragezeichenfolgen](./media/cdn-query-string-premium/cdn-query-string.png)
3. Wählen Sie einen Abfragezeichenfolgenmodus aus, und klicken Sie auf **Aktualisieren**.

> [!IMPORTANT]
> Da die Verteilung der Registrierung über das CDN eine Weile dauern kann, sind die Änderungen der Cachezeichenfolgen-Einstellungen unter Umständen nicht sofort sichtbar. Bei **Azure CDN Premium von Verizon**-Profilen ist die Weitergabe in der Regel in 90 Minuten abgeschlossen.
 

