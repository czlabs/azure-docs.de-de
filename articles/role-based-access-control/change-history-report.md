---
title: Anzeigen von Aktivitätsprotokollen für Änderungen an der rollenbasierten Zugriffssteuerung in Azure | Microsoft-Dokumentation
description: Zeigen Sie Aktivitätsprotokolle für Änderungen an der rollenbasierten Zugriffssteuerung für die letzten 90 Tage an.
services: active-directory
documentationcenter: ''
author: rolyon
manager: mtillman
ms.assetid: 2bc68595-145e-4de3-8b71-3a21890d13d9
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 04/23/2017
ms.author: rolyon
ms.reviewer: rqureshi
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 5e09ccdc4942a39e54b760cb5ad78c035dbc05f8
ms.sourcegitcommit: 6e43006c88d5e1b9461e65a73b8888340077e8a2
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 05/01/2018
ms.locfileid: "32312422"
---
# <a name="view-activity-logs-for-role-based-access-control-changes"></a>Anzeigen von Aktivitätsprotokoll für Änderungen an der rollenbasierten Zugriffssteuerung

Jedes Mal, wenn ein Benutzer Änderungen an den Rollendefinitionen oder Rollenzuweisungen vornimmt, werden die Änderungen im [Azure-Aktivitätsprotokoll](../monitoring-and-diagnostics/monitoring-overview-activity-logs.md) in der Kategorie „Administration“ aufgezeichnet. Sie können die Aktivitätsprotokolle öffnen, um alle Änderungen an der rollenbasierten Zugriffssteuerung für die letzten 90 Tage anzuzeigen.

## <a name="operations-that-are-logged"></a>Protokollierte Vorgänge

Folgende Vorgänge im Bezug auf die rollenbasierte Zugriffssteuerung werden im Aktivitätsprotokoll erfasst:

- Erstellen oder Aktualisieren von benutzerdefinierten Rollendefinition
- Löschen von benutzerdefinierten Rollendefinition
- Erstellen von Rollenzuweisungen
- Löschen von Rollenzuweisungen

## <a name="azure-portal"></a>Azure-Portal

Der einfachste Einstieg besteht im Anzeigen der Aktivitätsprotokolle im Azure-Portal. Auf folgendem Screenshot sehen Sie ein Beispiel für ein Aktivitätsprotokoll, das gefiltert wurde, um die Kategorie **Administration** und die Vorgänge „Rollendefinition“ und „Rollenzuweisung“ anzuzeigen. Es enthält ebenfalls einen Link, um die Protokolle als CSV-Datei herunterzuladen.

![Screenshot: Aktivitätsprotokolle im Portal](./media/change-history-report/activity-log-portal.png)

Weitere Informationen finden Sie in der [Anzeigen von Ereignissen im Aktivitätsprotokoll](/azure/azure-resource-manager/resource-group-audit?toc=%2fazure%2fmonitoring-and-diagnostics%2ftoc.json).

## <a name="azure-powershell"></a>Azure PowerShell

Verwenden Sie den Befehl [Get-AzureRmLog](/powershell/module/azurerm.insights/get-azurermlog), um Aktivitätsprotokolle mit Azure PowerShell anzuzeigen.

Dieser Befehl führt alle Änderungen an der Rollenzuweisung in einem Abonnement für die letzten sieben Tage auf:

```azurepowershell
Get-AzureRmLog -StartTime (Get-Date).AddDays(-7) | Where-Object {$_.Authorization.Action -like 'Microsoft.Authorization/roleAssignments/*'}
```

Dieser Befehl führt alle Änderungen an der Rollendefinition in einer Ressourcengruppe für die letzten sieben Tage auf:

```azurepowershell
Get-AzureRmLog -ResourceGroupName pharma-sales-projectforecast -StartTime (Get-Date).AddDays(-7) | Where-Object {$_.Authorization.Action -like 'Microsoft.Authorization/roleDefinitions/*'}
```

Dieser Befehl führt alle Änderungen an der Rollenzuweisung und der Rollendefinition in einem Abonnement für die letzten sieben Tage auf und stellt die Ergebnisse in einer Liste dar:

```azurepowershell
Get-AzureRmLog -StartTime (Get-Date).AddDays(-7) | Where-Object {$_.Authorization.Action -like 'Microsoft.Authorization/role*'} | Format-List Caller,EventTimestamp,{$_.Authorization.Action},Properties
```

```Example
Caller                  : alain@example.com
EventTimestamp          : 4/20/2018 9:18:07 PM
$_.Authorization.Action : Microsoft.Authorization/roleAssignments/write
Properties              :
                          statusCode     : Created
                          serviceRequestId: 11111111-1111-1111-1111-111111111111

Caller                  : alain@example.com
EventTimestamp          : 4/20/2018 9:18:05 PM
$_.Authorization.Action : Microsoft.Authorization/roleAssignments/write
Properties              :
                          requestbody    : {"Id":"22222222-2222-2222-2222-222222222222","Properties":{"PrincipalId":"33333333-3333-3333-3333-333333333333","RoleDefinitionId":"/subscriptions/00000000-0000-0000-0000-000000000000/providers
                          /Microsoft.Authorization/roleDefinitions/b24988ac-6180-42a0-ab88-20f7382dd24c","Scope":"/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/pharma-sales-projectforecast"}}

```

## <a name="azure-cli"></a>Azure-Befehlszeilenschnittstelle

Verwenden Sie den Befehl [az monitor activity-log list](/cli/azure/monitor/activity-log#az-monitor-activity-log-list), um Aktivitätsprotokolle mit der Azure CLI anzuzeigen.

Dieser Befehl führt die Aktivitätsprotokolle in einer Ressourcengruppe seit dem Start auf:

```azurecli
az monitor activity-log list --resource-group pharma-sales-projectforecast --start-time 2018-04-20T00:00:00Z
```

Dieser Befehl führt die Aktivitätsprotokolle für den Ressourcenanbieter der Autorisierung seit dem Start auf:

```azurecli
az monitor activity-log list --resource-provider "Microsoft.Authorization" --start-time 2018-04-20T00:00:00Z
```

## <a name="azure-log-analytics"></a>Azure Log Analytics

[Azure Log Analytics](../log-analytics/log-analytics-overview.md) ist ein weiteres Tool, das Sie verwenden können, um Änderungen an der rollenbasierten Zugriffssteuerung für alle Azure-Ressourcen zu erfassen und zu analysieren. Log Analytics hat folgende Vorteile:

- Schreiben komplexer Abfragen und Logiken
- Integration in Warnungen, Power BI und andere Tools
- Aufbewahren von Daten für längere Zeiträume
- Querverweise mit anderen Protokollen wie Sicherheitsprotokollen, Protokollen virtueller Computer und benutzerdefinierten Protokollen

Folgende Schritte sind für den Einstieg grundlegend:

1. [Erstellen eines Log Analytics-Arbeitsbereichs](../log-analytics/log-analytics-quick-create-workspace.md)

1. [Konfigurieren der Lösung für die Aktivitätsprotokollanalyse](../log-analytics/log-analytics-activity.md#configuration) für Ihren Arbeitsbereich.

1. [Anzeigen der Aktivitätsprotokolle](../log-analytics/log-analytics-activity.md#using-the-solution) Sie können schnell zur Übersichtsseite für die Aktivitätsprotokollanalyse navigieren, indem Sie auf die Option **Log Analytics** klicken.

   ![Option „Log Analytics“ im Portal](./media/change-history-report/azure-log-analytics-option.png)

1. Verwenden Sie optional die Seite [Protokollsuche](../log-analytics/log-analytics-log-search.md) oder das [Advanced Analytics-Portal](https://docs.loganalytics.io/docs/Learn), um die Protokolle abzufragen und anzuzeigen. Weitere Informationen zu diesen beiden Optionen finden Sie unter [Log Search page or the Advanced Analytics portal (Seite „Protokollsuche“ bzw. das Advanced Analytics-Portal)](../log-analytics/log-analytics-log-search-portals.md).

Im Folgenden finden Sie eine Abfrage, die neue Rollenzuweisungen zurückgibt, die vom Anbieter der Zielressource geordnet wurden:

```
AzureActivity
| where TimeGenerated > ago(60d) and OperationName startswith "Microsoft.Authorization/roleAssignments/write" and ActivityStatus == "Succeeded"
| parse ResourceId with * "/providers/" TargetResourceAuthProvider "/" *
| summarize count(), makeset(Caller) by TargetResourceAuthProvider
```

Im Folgenden finden Sie eine Abfrage, die Änderungen an der Rollenzuweisung zurückgibt, die in einem Diagramm angezeigt werden:

```
AzureActivity
| where TimeGenerated > ago(60d) and OperationName startswith "Microsoft.Authorization/roleAssignments"
| summarize count() by bin(TimeGenerated, 1d), OperationName
| render timechart
```

![Screenshot: Aktivitätsprotokolle im Advanced Analytics-Portal](./media/change-history-report/azure-log-analytics.png)

## <a name="next-steps"></a>Nächste Schritte
* [Anzeigen von Ereignissen im Aktivitätsprotokoll](/azure/azure-resource-manager/resource-group-audit?toc=%2fazure%2fmonitoring-and-diagnostics%2ftoc.json)
* [Monitor Subscription Activity with the Azure Activity Log (Überwachen der Abonnementaktivität per Azure-Aktivitätsprotokoll)](/azure/monitoring-and-diagnostics/monitoring-overview-activity-logs)
