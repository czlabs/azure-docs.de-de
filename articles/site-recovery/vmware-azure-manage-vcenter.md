---
title: " Verwalten von VMware vCenter Server in Azure Site Recovery | Microsoft-Dokumentation"
description: In diesem Artikel wird beschrieben, wie Sie VMware vCenter in Azure Site Recovery hinzufügen und verwalten.
services: site-recovery
author: AnoopVasudavan
manager: gauravd
ms.service: site-recovery
ms.devlang: na
ms.topic: article
ms.date: 03/05/2018
ms.author: anoopkv
ms.openlocfilehash: be415340da09043eccd361b0168bb304d8904bef
ms.sourcegitcommit: 8c3267c34fc46c681ea476fee87f5fb0bf858f9e
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 03/09/2018
---
# <a name="manage-vmware-vcenter-servers"></a>Verwalten von VMware vCenter Server 

Dieser Artikel beschreibt die verschiedenen Site Recovery-Vorgänge, die in einem VMware vCenter ausgeführt werden können. Überprüfen Sie die [Voraussetzungen](vmware-physical-azure-support-matrix.md#replicated-machines), bevor Sie beginnen.


## <a name="set-up-an-account-for-automatic-discovery"></a>Einrichten eines Kontos für die automatische Ermittlung

Für Site Recovery ist der Zugriff auf VMware erforderlich, damit der Prozessserver VMs automatisch ermitteln und das Failover und Failback von VMs durchgeführt werden kann. Erstellen Sie wie folgt ein Konto für den Zugriff:

1. Melden Sie sich auf dem Konfigurationsservercomputer an.
2. Starten Sie die Datei „cspsconfigtool.exe“ über die Desktopverknüpfung.
3. Klicken Sie auf der Registerkarte **Konten verwalten** auf **Konto hinzufügen**.

  ![add-account](./media/vmware-azure-manage-vcenter/addaccount.png)
1. Geben Sie die Kontodetails ein, und klicken Sie auf **OK**, um es hinzuzufügen.  Für das Konto sollten die Berechtigungen in der folgenden Tabelle zusammengefasst sein. 

Es dauert ungefähr 15 Minuten, bis die Kontoinformationen mit dem Site Recovery-Dienst synchronisiert sind.

### <a name="account-permissions"></a>Kontoberechtigungen

|**Task** | **Konto** | **Berechtigungen** | **Details**|
|--- | --- | --- | ---|
|**Automatische Ermittlung/Migration (ohne Failback)** | Sie benötigen mindestens einen Benutzer mit Lesezugriff. | Data Center object (Rechenzentrenobjekt) –> Propagate to Child Object (An untergeordnetes Objekt weitergeben), role=Read-only (Rolle=schreibgeschützt) | Der Benutzer wird auf Datencenterebene zugewiesen und hat Zugriff auf alle Objekte im Datencenter.<br/><br/> Um den Zugriff einzuschränken, weisen Sie den untergeordneten Objekten (vSphere-Hosts, Datenspeicher, VMs und Netzwerke) die Rolle **No access** (Kein Zugriff) mit **Propagate to child object** (Auf untergeordnetes Objekt übertragen) zu.|
|**Replikation/Failover** | Sie benötigen mindestens einen Benutzer mit Lesezugriff.| Data Center object (Rechenzentrenobjekt) –> Propagate to Child Object (An untergeordnetes Objekt weitergeben), role=Read-only (Rolle=schreibgeschützt) | Der Benutzer wird auf Datencenterebene zugewiesen und hat Zugriff auf alle Objekte im Datencenter.<br/><br/> Um den Zugriff einzuschränken, weisen Sie den untergeordneten Objekten (vSphere-Hosts, Datenspeicher, VMs und Netzwerke) die Rolle **No access** (Kein Zugriff) mit **Propagate to child object** (Auf untergeordnetes Objekt übertragen) zu.<br/><br/> Ist für Migrationszwecke geeignet, aber nicht für die vollständige Replikation, Failover oder Failback.|
|**Replikation/Failover/Failback** | Wir empfehlen, dass Sie eine Rolle (AzureSiteRecoveryRole) mit den erforderlichen Berechtigungen erstellen und sie dann einem VMware-Benutzer oder einer VMware-Gruppe zuweisen | Rechenzentrumsobjekt -> An untergeordnetes Objekt weitergeben, Rolle=AzureSiteRecoveryRole<br/><br/> Datenspeicher -> Speicherplatz zuordnen, Datenspeicher durchsuchen, Low-Level-Dateivorgänge, Datei entfernen, Dateien virtueller Computer aktualisieren<br/><br/> Netzwerk -> Netzwerk zuweisen<br/><br/> Ressource -> Zuweisen der VM zu einem Ressourcenpool, ausgeschaltete VM migrieren, eingeschaltete VM migrieren<br/><br/> Tasks (Aufgaben) -> Create task (Aufgabe erstellen), update task (Aufgabe aktualisieren)<br/><br/> Virtueller Computer -> Konfiguration<br/><br/> Virtueller Computer -> Interagieren -> Frage beantworten, Geräteverbindung, CD-Medien konfigurieren, Diskettenmedien konfigurieren, Ausschalten, Einschalten, VMware-Tools installieren<br/><br/> Virtueller Computer -> Inventar -> Erstellen, Registrieren, Registrierung aufheben<br/><br/> Virtueller Computer -> Bereitstellung -> Download virtueller Computer zulassen, Upload von Dateien virtueller Computer zulassen<br/><br/> Virtual machine -> Snapshots -> Remove snapshots | Der Benutzer wird auf Rechenzentrumsebene zugewiesen und hat Zugriff auf alle Objekte im Rechenzentrum.<br/><br/> Um den Zugriff einzuschränken, weisen Sie den untergeordneten Objekten (vSphere-Hosts, Datenspeicher, VMs und Netzwerke) die Rolle **No access** (Kein Zugriff) mit **Propagate to child object** (Auf untergeordnetes Objekt übertragen) zu.|


## <a name="add-vmware-server-to-the-vault"></a>Hinzufügen von VMware Server zum Tresor

1. Öffnen Sie im Azure-Portal Ihren Tresor, navigieren Sie zu **Site Recovery-Infrastruktur** > **Konfigurationsserver**, und öffnen Sie den Konfigurationsserver.
2. Klicken Sie auf der Seite **Details** auf **+vCenter**.

[!INCLUDE [site-recovery-add-vcenter](../../includes/site-recovery-add-vcenter.md)]

## <a name="modify-credentials"></a>Ändern von Anmeldeinformationen

Ändern Sie wie im Folgenden beschrieben die Anmeldeinformationen zum Herstellen der Verbindung mit vCenter Server oder dem ESXi-Host:

1. Melden Sie sich beim Konfigurationsserver an, und rufen Sie über den Desktop die Datei „cspsconfigtool.exe“ auf.
2. Klicken Sie auf der Registerkarte **Konten verwalten** auf **Konto hinzufügen**.

  ![add-account](./media/vmware-azure-manage-vcenter/addaccount.png)
3. Geben Sie die Details des neuen Kontos ein, und klicken Sie auf **OK**, um es hinzuzufügen. Das Konto sollte über die [oben](#account-permissions) aufgeführten Berechtigungen verfügen.
4. Öffnen Sie im Azure-Portal den Tresor, navigieren Sie zu **Site Recovery-Infrastruktur** > **Konfigurationsserver**, und öffnen Sie den Konfigurationsserver.
5. Klicken Sie auf der Seite **Details** auf **Server aktualisieren**.
6. Wählen Sie vCenter Server nach Abschluss des Auftrags „Server aktualisieren“ aus, um die vCenter-Seite **Zusammenfassung** zu öffnen.
7. Wählen Sie das neu hinzugefügte Konto im Feld **vCenter Server/vSphere-Hostkonto** aus, und klicken Sie auf **Speichern**.

    ![modify-account](./media/vmware-azure-manage-vcenter/modify-vcente-creds.png)

## <a name="delete-a-vcenter-server"></a>Löschen von vCenter Server

1. Öffnen Sie im Azure-Portal Ihren Tresor, navigieren Sie zu **Site Recovery-Infrastruktur** > **Konfigurationsserver**, und öffnen Sie den Konfigurationsserver.
2. Wählen Sie vCenter Server auf der Seite **Details**.
3. Klicken Sie auf die Schaltfläche **Löschen**.

  ![delete-account](./media/vmware-azure-manage-vcenter/delete-vcenter.png)

> [!NOTE]
Wenn Sie Änderungen an der IP-Adresse, den FQDN oder den Port von vCenter vornehmen müssen, dann müssen Sie vCenter Server löschen und wieder zum Portal hinzufügen.
