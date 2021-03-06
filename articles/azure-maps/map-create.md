---
title: Erstellen einer Karte mit Azure Maps | Microsoft-Dokumentation
description: Erstellen einer JavaScript-Karte
services: azure-maps
keywords: ''
author: jinzh-azureiot
ms.author: jinzh
ms.date: 05/07/2018
ms.topic: article
ms.service: azure-maps
documentationcenter: ''
manager: timlt
ms.devlang: na
ms.custom: codepen
ms.openlocfilehash: 9a7c611860a6d32f82d6714d945c62e6c562f91f
ms.sourcegitcommit: e221d1a2e0fb245610a6dd886e7e74c362f06467
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 05/07/2018
---
# <a name="create-a-map"></a>Erstellen einer Karte

In diesem Artikel wird gezeigt, wie Sie eine Karte erstellen.  

## <a name="understand-the-code"></a>Grundlegendes zum Code

Es gibt zwei Wege, um eine Karte zu erstellen. Sie können die Kamera der Karte einstellen, indem Sie den Mittelpunkt und den Zoomfaktor angeben, oder die Kameragrenzen der Karte festlegen, indem Sie den südwestlichen und nordöstlichen Begrenzungspunkt angeben.

<a id="setCameraOptions"></a>

### <a name="setting-the-camera"></a>Einstellen der Kamera

<iframe height='310' scrolling='no' title='Erstellen einer Karte über „CameraOptions“' src='//codepen.io/azuremaps/embed/qxKBMN/?height=265&theme-id=0&default-tab=js,result&embed-version=2&editable=true' frameborder='no' allowtransparency='true' allowfullscreen='true' style='width: 100%;'>Weitere Informationen finden Sie unter dem Pen <a href='https://codepen.io/azuremaps/pen/qxKBMN/'>Create a map via CameraOptions</a> (Erstellen einer Karte über „CameraOptions“) von Azure Maps (<a href='https://codepen.io/azuremaps'>@azuremaps</a>) auf <a href='https://codepen.io'>CodePen</a>.
</iframe>

Im oben gezeigten Code wird ein [Kartenobjekt](https://docs.microsoft.com/javascript/api/azure-maps-javascript/map?view=azure-iot-typescript-latest) über `new atlas.Map()` erstellt. Karteneigenschaften wie Mittelpunkt und Zoomfaktor sind Teil der [CameraOptions](https://docs.microsoft.com/javascript/api/azure-maps-javascript/cameraoptions?view=azure-iot-typescript-latest). „CameraOptions“ können Sie im Kartenkonstruktor oder über die Funktion [setCamera](https://docs.microsoft.com/javascript/api/azure-maps-javascript/map?view=azure-iot-typescript-latest#setcamera) der Map-Klasse definieren.

<a id="setCameraBoundsOptions"></a>

### <a name="setting-the-camera-bounds"></a>Festlegen der Kameragrenzen

<iframe height='310' scrolling='no' title='Erstellen einer Karte über „CameraBoundsOptions“' src='//codepen.io/azuremaps/embed/ZrRbPg/?height=265&theme-id=0&default-tab=js,result&embed-version=2&editable=true' frameborder='no' allowtransparency='true' allowfullscreen='true' style='width: 100%;'>Weitere Informationen finden Sie unter dem Pen <a href='https://codepen.io/azuremaps/pen/ZrRbPg/'>Create a map via CameraBoundsOptions</a> (Erstellen einer Karte über „CameraOptions“) von Azure Maps (<a href='https://codepen.io/azuremaps'>@azuremaps</a>) auf <a href='https://codepen.io'>CodePen</a>.
</iframe>

Im oben gezeigten Code wird ein [Kartenobjekt](https://docs.microsoft.com/javascript/api/azure-maps-javascript/map?view=azure-iot-typescript-latest) über `new atlas.Map()` erstellt. Karteneigenschaften wie ein Begrenzungsrahmen sind Teil der [CameraBoundsOptions](https://docs.microsoft.com/javascript/api/azure-maps-javascript/cameraboundsoptions?view=azure-iot-typescript-latest). „CameraBoundsOptions“ können Sie über die Funktion [setCameraBounds](https://docs.microsoft.com/javascript/api/azure-maps-javascript/map?view=azure-iot-typescript-latest#setcamerabounds) der Map-Klasse definieren.

## <a name="try-out-the-code"></a>Testen Sie den Code 

Sehen Sie sich den obigen Beispielcode an. Sie können den JavaScript-Code links auf der Registerkarte „JS“ bearbeiten und die Änderungen an der Kartenansicht rechts auf der Registerkarte „Ergebnis“ sehen. Außerdem können Sie auf die Schaltfläche „Auf CodePen bearbeiten“ klicken, und den Code auf CodePen bearbeiten. 

<a id="relatedReference"></a>

## <a name="next-steps"></a>Nächste Schritte

Erfahren Sie mehr zu den in diesem Artikel verwendeten Klassen und Methoden: 
* [Map](https://docs.microsoft.com/javascript/api/azure-maps-javascript/map?view=azure-iot-typescript-latest)
    * [setCamera](https://docs.microsoft.com/javascript/api/azure-maps-javascript/map?view=azure-iot-typescript-latest#setcamera)
    * [setCameraBounds](https://docs.microsoft.com/javascript/api/azure-maps-javascript/map?view=azure-iot-typescript-latest#setcamerabounds)

