---
title: Kennenlernen der Benutzeroberfläche von Azure IoT Central | Microsoft-Dokumentation
description: Machen Sie sich als Ersteller mit den wichtigsten Bereichen der Benutzeroberfläche von Azure IoT Central vertraut, die Sie zur Erstellung von IoT-Lösungen verwenden.
services: iot-central
author: tanmaybhagwat
ms.author: tanmayb
ms.date: 4/13/2018
ms.topic: overview
ms.prod: microsoft-iot-central
manager: timlt
ms.openlocfilehash: aa0d496b073600bb976a639ea0039d2a5bbdbbcf
ms.sourcegitcommit: eb75f177fc59d90b1b667afcfe64ac51936e2638
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 05/16/2018
ms.locfileid: "34201474"
---
# <a name="take-a-tour-of-the-azure-iot-central-ui"></a>Kennenlernen der Benutzeroberfläche von Azure IoT Central

In diesem Artikel wird die Benutzeroberfläche von Microsoft Azure IoT Central vorgestellt. Über die Benutzeroberfläche können Sie Azure IoT Central-Lösungen und die damit verbundenen Geräte erstellen, verwalten und verwenden.

_Ersteller_ verwenden die Benutzeroberfläche von Azure IoT Central, um ihre Azure IoT Central-Lösung zu definieren. Die Benutzeroberfläche bietet folgende Möglichkeiten:

- Definieren der Art von Gerät, das eine Verbindung mit Ihrer Lösung herstellt
- Konfigurieren der Regeln und Aktionen für Ihre Geräte
- Anpassen der Benutzeroberfläche für einen _Bediener_, der Ihre Lösung verwendet

_Bediener_ verwenden die Benutzeroberfläche von Azure IoT Central, um ihre Azure IoT Central-Lösung zu verwalten. Die Benutzeroberfläche bietet folgende Möglichkeiten:

- Überwachen Ihrer Geräte
- Konfigurieren Ihrer Geräte
- Behandeln und Beheben von Problemen mit Ihren Geräten
- Bereitstellen von neuen Geräten

## <a name="use-the-left-navigation-menu"></a>Verwenden des linken Navigationsmenüs

Über das linke Navigationsmenü können Sie auf die verschiedenen Bereiche der Anwendung zugreifen:

| Menü | Beschreibung |
| ---- | ----------- |
| ![Linkes Navigationsmenü](media/overview-iot-central-tour/navigationbar.png) | <ul><li>Über die Schaltfläche **Startseite** gelangen Sie zur Startseite der Anwendung. Als Ersteller können Sie diese Startseite für die Bediener anpassen.</li><li>Die Schaltfläche **Device Explorer** dient zum Auflisten der in Ihrer Anwendung definierten Gerätevorlagen sowie der simulierten und echten Geräte, die den einzelnen Gerätevorlagen zugeordnet sind. Bediener verwenden den **Device Explorer**, um ihre verbundenen Geräte zu verwalten.</li><li>Die Schaltfläche **Device Sets** (Gerätegruppen) dient zum Anzeigen und Erstellen von Gerätegruppen. Bediener können Gerätegruppen als logische, durch eine Abfrage angegebene Sammlung von Geräten erstellen.</li><li>Die Schaltfläche **Analytics** dient zum Anzeigen von Analysen, die auf Gerätetelemetriedaten für Geräte und Gerätegruppen basieren. Bediener können benutzerdefinierte Ansichten auf der Grundlage von Gerätedaten erstellen, um basierend auf ihrer Anwendung Erkenntnisse zu gewinnen.</li><li>Die Schaltfläche **Application Builder** (Anwendungs-Generator) dient zum Anzeigen der von einem Ersteller verwendeten Tools (etwa des **Tools zum Erstellen von Gerätevorlagen**).</li><li>Die Schaltfläche **Verwaltung** dient zum Anzeigen der Seiten für die Anwendungsverwaltung, auf denen ein Administrator Anwendungseinstellungen, Benutzer und Rollen verwalten kann.</li></ul> |

## <a name="search-help-and-support"></a>Suche, Hilfe und Support

Das obere Menü wird auf jeder Seite angezeigt:

![Symbolleiste](media/overview-iot-central-tour/toolbar.png)

- Wenn Sie nach Gerätevorlagen und Geräten suchen möchten, klicken Sie auf das Symbol **Suche**.
- Wenn Sie Hilfe oder Unterstützung benötigen, klicken Sie auf das Dropdownmenü **Hilfe**, um eine Liste mit Ressourcen anzuzeigen.
- Über das Symbol **Konto** können Sie die Tutorials steuern, das Design der Benutzeroberfläche ändern oder sich von der Anwendung abmelden.

Sie können zwischen einem hellen und einem dunklen Benutzeroberflächendesign wählen:

![Auswählen eines Designs für die Benutzeroberfläche](media/overview-iot-central-tour/themes.png)

## <a name="home-page"></a>Startseite

![Startseite](media/overview-iot-central-tour/homepage.png)

Nach der Anmeldung bei Ihrer Azure IoT Central-Anwendung wird als Erstes die Startseite angezeigt. Als Ersteller können Sie der Startseite Kacheln hinzufügen und sie so für andere Benutzer der Anwendung anpassen. Weitere Informationen finden Sie im Tutorial [Customize the Azure IoT Central operator's view](tutorial-customize-operator.md) (Anpassen der Azure IoT Central-Ansicht für Bediener).

## <a name="device-explorer"></a>Device Explorer

![Explorer-Seite](media/overview-iot-central-tour/explorer.png)

Auf der Explorer-Seite werden die _Gerätevorlagen_ und _Geräte_ in Ihrer Azure IoT Central-Anwendung angezeigt.

* Eine Gerätevorlage definiert einen Gerätetyp, der eine Verbindung mit Ihrer Anwendung herstellen kann. Weitere Informationen finden Sie unter [Define a new device type in your Azure IoT Central application](tutorial-define-device-type.md) (Definieren eines neuen Gerätetyps in Ihrer Azure IoT Central-Anwendung).
* Bei einem Gerät handelt es sich um ein echtes oder simuliertes Gerät in Ihrer Anwendung. Weitere Informationen finden Sie unter [Add a real device to your Azure IoT Central application](tutorial-add-device.md) (Hinzufügen eines echten Geräts zu Ihrer Azure IoT Central-Anwendung).

## <a name="device-sets"></a>Gerätegruppen

![Seite „Device Sets“ (Gerätegruppen)](media/overview-iot-central-tour/devicesets.png)

Auf der Seite _Device Sets_ (Gerätegruppen) werden Gerätegruppen angezeigt, die der Ersteller erstellt hat. Bei einer Gerätegruppe handelt es sich um eine Sammlung verwandter Geräte. Ein Ersteller definiert eine Abfrage, um die in einer Gerätegruppe enthaltenen Geräte zu identifizieren. Gerätegruppen werden verwendet, wenn Sie die Analyse in Ihrer Anwendung anpassen. Weitere Informationen finden Sie im Artikel [Use device sets in your Azure IoT Central application](howto-use-device-sets.md) (Definieren von Gerätegruppen in Ihrer Azure IoT Central-Anwendung).

## <a name="analytics"></a>Analytics

![Seite „Analytics“](media/overview-iot-central-tour/analytics.png)

Anhand der Diagramme auf der Analyseseite können Sie das Verhalten der mit Ihrer Anwendung verbundenen Geräte nachvollziehen. Bediener verwenden diese Seite zur Überwachung und Untersuchung von Problemen mit verbundenen Geräten. Der Ersteller kann definieren, welche Diagramme auf dieser Seite angezeigt werden. Weitere Informationen finden Sie im Artikel [How to use analytics to analyze your device data](howto-create-analytics.md) (Analysieren Ihrer Anwendungsdaten mithilfe von Analysen).

## <a name="application-builder"></a>Anwendungs-Generator

![Seite „Application Builder“ (Anwendungs-Generator)](media/overview-iot-central-tour/applicationbuilder.png)

Die Seite mit dem Anwendungs-Generator enthält Links zu den Tools, die ein Ersteller verwendet, um eine Azure IoT Central-Anwendung zu erstellen. Hierzu zählen beispielsweise Tools zum Erstellen von Gerätevorlagen und zum Konfigurieren der Startseite. Weitere Informationen finden Sie im Tutorial [Define a new device type in your Azure IoT Central application](tutorial-define-device-type.md) (Definieren eines neuen Gerätetyps in Ihrer Azure IoT Central-Anwendung).

## <a name="administration"></a>Verwaltung

![Verwaltungsseite](media/overview-iot-central-tour/administration.png)

Die Verwaltungsseite enthält Links zu den Tools, die ein Administrator verwendet, um beispielsweise Benutzer und Rollen in der Anwendung zu definieren. Weitere Informationen finden Sie im Artikel [How to administer your application](howto-administer.md) (Verwalten Ihrer Anwendung).

## <a name="next-steps"></a>Nächste Schritte

Nachdem Sie sich nun einen Überblick über Azure IoT Central verschafft und sich mit dem Layout der Benutzeroberfläche vertraut gemacht haben, empfehlen wir, mit der Schnellstartanleitung zum [Erstellen einer Azure IoT Central-Anwendung](quick-deploy-iot-central.md) fortzufahren.