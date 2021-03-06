---
title: Wie werden Abfragen von Diagrammdaten in Azure Cosmos DB durchgeführt? | Microsoft-Dokumentation
description: Erfahren Sie, wie Sie Abfragen von Diagrammdaten in Azure Cosmos DB durchführen.
services: cosmos-db
documentationcenter: ''
author: luisbosquez
manager: kfile
editor: ''
tags: ''
ms.assetid: 8bde5c80-581c-4f70-acb4-9578873c92fa
ms.service: cosmos-db
ms.devlang: na
ms.topic: tutorial
ms.tgt_pltfrm: na
ms.workload: ''
ms.date: 01/02/2018
ms.author: lbosq
ms.custom: mvc
ms.openlocfilehash: 449821d6121f8fec40b151ae06f687586133c3d1
ms.sourcegitcommit: fc64acba9d9b9784e3662327414e5fe7bd3e972e
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 05/12/2018
---
# <a name="tutorial-query-azure-cosmos-db-graph-api-by-using-gremlin"></a>Tutorial: Abfragen der Graph-API von Azure Cosmos BD mithilfe von Gremlin

Die [Graph-API](graph-introduction.md) von Azure Cosmos DB unterstützt [Gremlin](https://github.com/tinkerpop/gremlin/wiki)-Abfragen. Dieser Artikel enthält Beispieldokumente und Abfragen, um Ihnen den Einstieg zu erleichtern. Eine detaillierte Gremlin-Referenz finden Sie im Artikel [Azure Cosmos DB Gremlin graph support](gremlin-support.md) (Azure Cosmos DB: Gremlin-Graphunterstützung).

In diesem Artikel werden die folgenden Aufgaben behandelt: 

> [!div class="checklist"]
> * Abfragen von Daten mit Gremlin

## <a name="prerequisites"></a>Voraussetzungen

Diese Abfragen können nur funktionieren, wenn Sie über ein Azure Cosmos DB-Konto verfügen und Diagrammdaten im Container vorliegen. Sie haben beides nicht? Absolvieren Sie den [5-Minuten-Schnellstart](create-graph-dotnet.md) oder das [Entwicklertutorial](tutorial-query-graph.md) zum Erstellen eines Kontos und Füllen Ihrer Datenbank. Sie können die folgenden Abfragen mit der [Azure Cosmos DB .NET-Graphbibliothek](graph-sdk-dotnet.md), der [Gremlin-Konsole](https://tinkerpop.apache.org/docs/current/reference/#gremlin-console) oder Ihrem bevorzugten Gremlin-Treiber durchführen.

## <a name="count-vertices-in-the-graph"></a>Anzahl der Scheitelpunkte im Diagramm

Der folgende Codeausschnitt zeigt, wie Sie die Anzahl der Scheitelpunkte im Diagramm zählen:

```
g.V().count()
```

## <a name="filters"></a>Filter

Filter können Sie in den Gremlin-Schritten `has` und `hasLabel` anwenden und sie mithilfe von `and`, `or`, und `not` kombinieren, um komplexere Filter zu erstellen. Azure Cosmos DB bietet schemaunabhängige Indizierung aller Eigenschaften in den Scheitelpunkten und Graden für schnelle Abfragen:

```
g.V().hasLabel('person').has('age', gt(40))
```

## <a name="projection"></a>Projektion

Sie können bestimmte Eigenschaften in den Abfrageergebnissen mit dem `values`-Schritt projizieren:

```
g.V().hasLabel('person').values('firstName')
```

## <a name="find-related-edges-and-vertices"></a>Suchen verwandter Kanten und Scheitelpunkte

Bisher haben wir nur Abfrageoperatoren gesehen, die in jeder Datenbank funktionieren. Diagramme sind schnell und effizient bei Traversierungen, wenn Sie zu verwandten Kanten und Scheitelpunkten navigieren müssen. Wir suchen nun alle Freunde von Thomas. Hierzu suchen wir mit Schritt `outE` von Gremlin alle Out-Edges von Thomas und traversieren dann mit dem Gremlin-Schritt `inV` zu den In-Vertices dieser Kanten:

```cs
g.V('thomas').outE('knows').inV().hasLabel('person')
```

Die nächste Abfrage führt durch zweimaligen Aufruf von `outE` und `inV` zwei Hops aus, um alle „Freunde von Freunden“ von Thomas zu finden. 

```cs
g.V('thomas').outE('knows').inV().hasLabel('person').outE('knows').inV().hasLabel('person')
```

Mit Gremlin können Sie komplexere Abfragen erstellen und leistungsstarke Logik zur Graphdurchsuchung implementieren, einschließlich Mischen von Filterausdrücken, Ausführen von Schleifen mithilfe des `loop`-Schritts und Implementieren bedingter Navigation mithilfe des `choose`-Schritts. Erfahren Sie mehr darüber, was Sie mit [Gremlin-Unterstützung](gremlin-support.md) tun können!

## <a name="next-steps"></a>Nächste Schritte

In diesem Tutorial haben Sie die folgenden Aufgaben ausgeführt:

> [!div class="checklist"]
> * Sie haben gelernt, wie Sie Abfragen mithilfe von Graph durchführen. 

Sie können jetzt mit dem nächsten Tutorial fortfahren, um zu erfahren, wie Sie Ihre Daten global verteilen.

> [!div class="nextstepaction"]
> [Globales Verteilen Ihrer Daten](tutorial-global-distribution-graph.md)
