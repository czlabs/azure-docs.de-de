---
title: Azure Container Registry-SKUs
description: Vergleich der verschiedenen in Azure Container Registry verfügbaren Dienstebenen.
services: container-registry
author: mmacy
manager: jeconnoc
ms.service: container-registry
ms.topic: article
ms.date: 03/15/2018
ms.author: marsma
ms.openlocfilehash: a8dcc6fc60b80a19c4edebd57fdad5bb10cfdd0b
ms.sourcegitcommit: e2adef58c03b0a780173df2d988907b5cb809c82
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/28/2018
---
# <a name="azure-container-registry-skus"></a>Azure Container Registry-SKUs

Azure Container Registry (ACR) steht in verschiedenen Dienstebenen, sogenannten SKUs, zur Verfügung. Durch diese SKUs können Preise im Voraus eingeschätzt werden. Darüber hinaus bieten sie verschiedene Optionen zur Anpassung an die Kapazität und das Nutzungsverhalten Ihrer privaten Docker-Registrierung in Azure.

| SKU | Verwaltet | BESCHREIBUNG |
| --- | :-------: | ----------- |
| **Basic** | Ja | Ein kostenoptimierter Einstiegspunkt für Entwickler, die sich mit Azure Container Registry vertraut machen. Basic-Registrierungen verfügen über die gleichen Programmfunktionen wie Standard- und Premium-Registrierungen (Azure Active Directory-Authentifizierungsintegration, Löschen von Images sowie Webhooks). Allerdings bestehen Einschränkungen bei Größe und Nutzung. |
| **Standard** | Ja | Standard-Registrierungen bieten die gleichen Funktionen wie Basic. In Standard gibt es jedoch erweiterte Speicherlimits und einen erhöhten Imagedurchsatz. Standard-Registrierungen erfüllen üblicherweise die Bedürfnisse der meisten Produktionsszenarios. |
| **Premium** | Ja | Premium-Registrierungen sind die Grenzwerte für den Speicher und gleichzeitige Vorgänge noch höher, sodass Szenarios mit großen Volumen möglich sind. Zusätzlich zu Funktionen für einen erhöhten Imagedurchsatz enthält Premium Funktionen wie die [Georeplikation][container-registry-geo-replication] zum regionsübergreifenden Verwalten einer Registrierung, sodass die Registrierung jeder Bereitstellung netzwerknah ist. |
| Klassisch | Nein  | Durch die klassische Registrierungs-SKU war das erstmalige Release des Azure Container Registry-Diensts in Azure möglich. Klassische Registrierungen werden von einem Speicherkonto unterstützt, das von Azure in Ihrem Abonnement erstellt wird, das dazu führt, dass ACR nur eingeschränkt allgemeine Funktionen wie einen erhöhten Durchsatz oder die Georeplikation bieten kann. Durch diese eingeschränkten Funktionen wird die Unterstützung für die klassische SKU in naher Zukunft eingestellt. |

Die Wahl einer übergeordneten SKU bringt eine höhere Leistung und Skalierbarkeit, jedoch bieten alle verwalteten SKUs die gleichen programmgesteuerten Möglichkeiten. Wenn mehrere Dienstebenen vorhanden sind, können Sie mit Basic beginnen und dann bei zunehmender Registrierungsnutzung in Standard und Premium konvertieren.

> [!NOTE]
> Wegen der geplanten Einstellung der Unterstützung für die klassische Registrierungs-SKU wird empfohlen, Basic, Standard oder Premium für alle neuen Registrierungen zu verwenden. Informationen zum Konvertieren Ihrer vorhandenen klassischen Registrierung finden Sie unter [Aktualisieren einer klassischen Registrierung][container-registry-upgrade].
>

## <a name="managed-vs-unmanaged"></a>Verwaltete im Vergleich zu nicht verwalteten Registrierungen

Die Basic-, Standard- und Premium-SKUs werden zusammenfassend als *verwaltete* Registrierungen und klassische als *nicht verwaltete* Registrierungen bezeichnet. Der Hauptunterschied zwischen den beiden liegt darin, wie die Containerimages gespeichert werden.

### <a name="managed-basic-standard-premium"></a>Verwaltet (Basic, Standard, Premium)

Imagespeicher, die vollständig von Azure verwaltet werden, sind insbesondere für verwaltete Registrierungen von Vorteil. Ein Speicherkonto, in dem die Images gespeichert werden, wird also nicht in Ihrem Azure-Abonnement angezeigt. Es gibt mehrere Vorteile, die sich aus der Verwendung einer der verwalteten Registrierungs-SKUs ergeben, die ausführlich unter [Speichern von Containerimages in Azure Container Registry][container-registry-storage] beschrieben werden. Der Schwerpunkt dieses Artikels liegt auf den verwalteten Registrierungs-SKUs und den Möglichkeiten, die sie bieten.

### <a name="unmanaged-classic"></a>Nicht verwaltet (klassisch)

Klassische Registrierungen werden als „nicht verwaltet“ bezeichnet, da sich das Speicherkonto, das eine klassische Registrierung unterstützt, in *Ihrem* Azure-Abonnement befindet. Daher sind Sie selbst für die Verwaltung des Speicherkontos verantwortlich, in dem Ihre Containerimages gespeichert sind. Bei nicht verwalteten Registrierungen ist ein bedarfsgerechter Wechsel zwischen SKUs nicht möglich (außer bei einem [Upgrade][container-registry-upgrade] auf eine verwaltete Registrierung), und einige Features der verwalteten Registrierungen sind nicht verfügbar (z.B. Containerimagelöschung, [Georeplikation][container-registry-geo-replication] und [Webhooks][container-registry-webhook]).

Weitere Informationen zum Durchführen eines Upgrades von einer klassischen Registrierung auf eine der verwalteten SKUs finden Sie unter [Aktualisieren einer klassischen Registrierung][container-registry-upgrade].

## <a name="sku-feature-matrix"></a>SKU-Featurematrix

In der folgenden Tabelle werden die Features und Grenzwerte der Dienstebenen Basic, Standard und Premium dargestellt.

[!INCLUDE [container-instances-limits](../../includes/container-registry-limits.md)]

## <a name="changing-skus"></a>Wechseln von SKUs

Sie können die SKU einer Registrierung mit der Azure CLI oder im Azure-Portal wechseln. Zwischen den verwalteten SKUs können Sie sich frei bewegen, solange die SKU, zu der Sie wechseln, über die erforderliche maximale Speicherkapazität verfügt. Wenn Sie von der klassischen Registrierung zu einer der verwalteten SKUs wechseln, kann dieser Vorgang nicht mehr rückgängig gemacht werden.

### <a name="azure-cli"></a>Azure-Befehlszeilenschnittstelle

Verwenden Sie zum Wechseln zwischen SKUs in der Azure CLI den Befehl [az acr update][az-acr-update]. Gehen Sie beispielsweise wie folgt vor, um zu Premium zu wechseln:

```azurecli
az acr update --name myregistry --sku Premium
```

### <a name="azure-portal"></a>Azure-Portal

Klicken Sie im Azure-Portal in der Containerregistrierung **Übersicht** auf **Update**, und wählen Sie anschließend im Dropdownmenü die neue **SKU** aus.

![Aktualisieren der Containerregistrierung-SKU im Azure-Portal][update-registry-sku]

Wenn eine klassische Registrierung vorliegt, ist die Auswahl einer verwalteten SKU im Azure-Portal nicht möglich. Stattdessen müssen Sie zuerst ein [Upgrade][container-registry-upgrade] auf eine verwaltete Registrierung durchführen (siehe [Wechseln von der klassischen Registrierung](#changing-from-classic)).

## <a name="changing-from-classic"></a>Wechseln von der klassischen Registrierung

Bei der Migration einer nicht verwalteten klassischen Registrierung zu einer der verwalteten Basic-, Standard- oder Premium-SKUs sind zusätzliche Aspekte zu berücksichtigen. Wenn Ihre klassische Registrierung eine große Anzahl von Images enthält und viele Gigabytes groß ist, kann die Migration einige Zeit in Anspruch nehmen. Darüber hinaus sind `docker push`-Vorgänge deaktiviert, bis die Migration abgeschlossen ist.

Weitere Informationen zum Durchführen eines Upgrades von Ihrer klassischen Registrierung auf eine der verwalteten SKUs finden Sie unter [Aktualisieren einer klassischen Containerregistrierung][container-registry-upgrade].

## <a name="pricing"></a>Preise

Informationen zu Preisen für jede SKU von Azure Container Registry finden Sie unter [Preise von Azure Container Registry][container-registry-pricing].

## <a name="next-steps"></a>Nächste Schritte

**Azure Container Registry – Roadmap**

Besuchen Sie [ACR Roadmap][acr-roadmap] auf GitHub, wo Sie Informationen zu zukünftigen Features des Diensts finden.

**Azure Container Registry – UserVoice**

Unter [ACR UserVoice][container-registry-uservoice] können Sie neue Featurevorschläge einsenden oder für diese abstimmen.

<!-- IMAGES -->
[update-registry-sku]: ./media/container-registry-skus/update-registry-sku.png

<!-- LINKS - External -->
[acr-roadmap]: https://aka.ms/acr/roadmap
[container-registry-pricing]: https://azure.microsoft.com/pricing/details/container-registry/
[container-registry-uservoice]: https://feedback.azure.com/forums/903958-azure-container-registry

<!-- LINKS - Internal -->
[az-acr-update]: /cli/azure/acr#az_acr_update
[container-registry-geo-replication]: container-registry-geo-replication.md
[container-registry-upgrade]: container-registry-upgrade.md
[container-registry-storage]: container-registry-storage.md
[container-registry-webhook]: container-registry-webhook.md
