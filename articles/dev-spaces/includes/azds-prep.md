---
title: Includedatei
description: Includedatei
ms.custom: include file
services: azure-dev-spaces
ms.service: azure-dev-spaces
ms.component: azds-kubernetes
author: ghogen
ms.author: ghogen
ms.date: 05/11/2018
ms.topic: include
manager: douge
ms.openlocfilehash: e9f97f804985f948e5442c64a31d95e7931b03cd
ms.sourcegitcommit: eb75f177fc59d90b1b667afcfe64ac51936e2638
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 05/16/2018
ms.locfileid: "34198825"
---
## <a name="preparing-code-for-docker-and-kubernetes-development"></a>Vorbereiten von Code für die Entwicklung mit Docker und Kubernetes
Bisher verfügen Sie über eine einfache Web-App, die lokal ausgeführt werden kann. Jetzt werden Sie die App containerisieren, indem Sie Ressourcen erstellen, die den Container und die Bereitstellung der App für Kubernetes definieren. Mit Azure Dev Spaces können Sie diese Aufgabe problemlos ausführen: 

1. Starten Sie Visual Studio Code (VS Code), und öffnen Sie den Ordner `webfrontend`. (Sie können alle Standardaufforderungen zum Hinzufügen von Debugressourcen oder zum Wiederherstellen des Projekts ignorieren.)
1. Öffnen Sie in VS Code das integrierte Terminal (über das Menü **Ansicht > Integriertes Terminal**).
1. Führen Sie den folgenden Befehl aus (stellen Sie dabei sicher, dass **webfrontend** der aktuelle Ordner ist):

    ```cmd
    azds prep --public
    ```

Mit dem Azure CLI-Befehl `azds prep` werden Docker- und Kubernetes-Ressourcen mit Standardeinstellungen generiert:
* `./Dockerfile` beschreibt das Containerimage der App und wie der Quellcode erstellt und im Container ausgeführt wird.
* In einem [Helm-Diagramm](https://docs.helm.sh) unter `./charts/webfrontend` wird veranschaulicht, wie der Container für Kubernetes bereitgestellt wird.

Vorerst ist es nicht notwendig, den gesamten Inhalt dieser Dateien zu verstehen. Es ist jedoch erwähnenswert, dass **dieselben Konfiguration-als-Code-Ressourcen von Kubernetes und Docker von der Entwicklung bis zur Produktion verwendet werden können, wodurch eine bessere Konsistenz in verschiedenen Umgebungen erreicht wird.**
 
Außerdem wird mit dem `prep`-Befehl eine Datei namens `./azds.yaml` generiert. Das ist die Konfigurationsdatei für Azure Dev Spaces. Sie ergänzt die Docker- und Kubernetes-Artefakte durch eine zusätzliche Konfiguration, die eine iterative Entwicklungserfahrung in Azure ermöglicht. Das Helm-Standarddiagramm macht beispielsweise keine öffentlichen Endpunkte verfügbar. Manchmal ist es jedoch sinnvoll, einen öffentlichen Endpunkt während der Entwicklung vorübergehend zu öffnen, damit Sie den Code beispielsweise von einem mobilen Gerät oder einer Webhook-URL aus testen können. Die mit `azds prep --public` erstellte Datei „azds.yaml“ setzt die Helm-Standardparameter außer Kraft, um einen öffentlichen Endpunkt nur für die Entwicklungszeit verfügbar zu machen.
