---
title: Verwalten von Programmen und Steuerelementen für Azure AD-Zugriffsüberprüfungen | Microsoft Docs
description: Sie können zusätzliche Programme für jede Governance-, Risikomanagement- und Konformitätsinitiative in Ihrer Organisation erstellen, um Azure Active Directory-Zugriffsüberprüfungen als Steuerelemente zu erfassen und zu organisieren.
services: active-directory
documentationcenter: ''
author: markwahl-msft
manager: mtillman
editor: ''
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/14/2018
ms.author: billmath
ms.openlocfilehash: a3fb812623b490e27907f63c1f7c6610ae754fb8
ms.sourcegitcommit: eb75f177fc59d90b1b667afcfe64ac51936e2638
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 05/16/2018
ms.locfileid: "34192879"
---
# <a name="manage-programs-and-their-controls"></a>Verwalten von Programmen und ihren Steuerelementen 

Azure Active Directory (Azure AD) enthält Zugriffsüberprüfungen von Gruppenmitgliedern und Anwendungszugriff. Diese Beispiele für Steuerelemente sichern den Überblick, wer auf Gruppenmitgliedschaften und Anwendungen Ihrer Organisation zugreifen kann. Diese Steuerelemente ermöglichen Organisationen das effiziente Verwalten ihrer Governance-, Risikomanagement- und Konformitätsanforderungen.

## <a name="create-and-manage-programs-and-their-controls"></a>Erstellen und Verwalten von Programmen und ihren Steuerelementen
Sie können die Nachverfolgung und das Erfassen von Zugriffsüberprüfungen für verschiedene Zwecke vereinfachen, indem Sie diese Aufgaben in Programmen organisieren. Jede Zugriffsüberprüfung kann mit einem Programm verknüpft werden. Wenn Sie dann Berichte für einen Auditor vorbereiten, können Sie sich auf die Zugriffsüberprüfungen im Bereich einer bestimmten Initiative konzentrieren.  Programme und Zugriffsergebnisse werden Benutzern mit den Rollen „Globaler Administrator“, „Sicherheitsadministrator“ oder „Benutzer mit Leseberechtigung für Sicherheitsfunktionen“ angezeigt.

Um eine Liste der Programme anzuzeigen, navigieren Sie zur Seite [Zugriffsüberprüfungen](https://portal.azure.com/#blade/Microsoft_AAD_ERM/DashboardBlade/), und wählen Sie **Programme**.

**Standardprogramm** ist immer vorhanden. Wenn Sie die Rolle eines globalen Administrators ausüben, können Sie weitere Programme erstellen. Sie können z.B. ein Programm für jede Konformitätsinitiative oder für jedes Geschäftsziel verwenden.

Wenn ein Programm nicht mehr benötigt wird und keine Steuerelemente mit ihm verknüpft sind, können Sie es löschen.

## <a name="next-steps"></a>Nächste Schritte

- [Erstellen einer Zugriffsüberprüfung für Mitglieder einer Gruppe oder den Zugriff auf eine Anwendung](active-directory-azure-ad-controls-create-access-review.md)
- [Abrufen der Ergebnisse einer Zugriffsüberprüfung](active-directory-azure-ad-controls-retrieve-access-review.md)
