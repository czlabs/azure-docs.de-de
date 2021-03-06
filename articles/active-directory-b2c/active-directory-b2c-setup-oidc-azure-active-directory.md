---
title: 'Azure Active Directory B2C: Hinzufügen eines Azure AD-Anbieters mithilfe integrierter Richtlinien | Microsoft-Dokumentation'
description: Informationen zum Hinzufügen eines Open ID-Identitätsanbieters (Azure AD)
services: active-directory-b2c
documentationcenter: ''
author: parakhj
manager: krassk
editor: parakhj
ms.assetid: 7dac9545-d5f1-4136-a04d-1c5740aea499
ms.service: active-directory-b2c
ms.workload: identity
ms.tgt_pltfrm: na
ms.topic: article
ms.devlang: na
ms.date: 04/27/2018
ms.author: parja
ms.openlocfilehash: 52a752df9cf199acf39596f49e7368bce27a8158
ms.sourcegitcommit: 6e43006c88d5e1b9461e65a73b8888340077e8a2
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/30/2018
ms.locfileid: "32309015"
---
# <a name="azure-active-directory-b2c-sign-in-using-azure-ad-accounts-through-a-built-in-policy"></a>Azure Active Directory B2C: Anmelden mithilfe von Azure AD-Konten über eine integrierte Richtlinie

>[!NOTE]
> Dieses Feature befindet sich in der Phase der öffentlichen Vorschau. Verwenden Sie dieses Feature nicht in Produktionsumgebungen.

In diesem Artikel erfahren Sie, wie Sie die Anmeldung für Benutzer einer bestimmten Azure Active Directory-Organisation (Azure AD) mittels integrierter Richtlinien aktivieren.

## <a name="create-an-azure-ad-app"></a>Erstellen einer Azure AD-App

Um die Anmeldung für Benutzer von einer bestimmten Azure AD-Organisation zu aktivieren, müssen Sie eine Anwendung im Azure AD-Mandanten der Organisation registrieren.

>[!NOTE]
> Wir verwenden „Contoso.com“ für den Azure AD-Mandanten der Organisation und „fabrikamb2c.onmicrosoft.com“ als den Azure AD B2C-Mandanten in den folgenden Anweisungen.

1. Melden Sie sich beim [Azure-Portal](https://portal.azure.com) an.
1. Wählen Sie in der oberen Leiste Ihr Konto aus. Wählen Sie in der **Verzeichnisliste** den Azure AD-Mandanten der Organisation aus, bei dem Sie Ihre Anwendung registrieren möchten (contoso.com).
1. Wählen Sie im linken Navigationsbereich **Alle Dienste** aus, und suchen Sie nach „App-Registrierungen“.
1. Wählen Sie **Registrierung einer neuen Anwendung** aus.
1. Geben Sie einen Namen für Ihre Anwendung ein (z.B. `Azure AD B2C App`).
1. Wählen Sie **Web-App/API** als Anwendungstyp aus.
1. Geben Sie für **Anmelde-URL** die folgende URL ein, in der `yourtenant` durch den Namen Ihres Azure AD B2C-Mandanten (`fabrikamb2c.onmicrosoft.com`) ersetzt wird:

    >[!NOTE]
    >Der Wert für „yourtenant“ muss in der **Anmelde-URL** in Kleinbuchstaben angegeben werden.

    ```Console
    https://login.microsoftonline.com/te/yourtenant.onmicrosoft.com/oauth2/authresp
    ```

1. Speichern Sie die Anwendungs-ID, die Sie im nächsten Abschnitt als Client-ID verwenden werden.
1. Wählen Sie auf dem Blatt **Einstellungen** die Option **Schlüssel** aus.
1. Geben Sie eine **Schlüsselbeschreibung** im Abschnitt **Kennwörter** ein, und legen Sie die **Dauer** auf „Läuft nie ab“ fest. 
1. Klicken Sie auf **Speichern**, und notieren Sie sich den daraus ergebenden **Wert** des Schlüssels, den Sie im nächsten Abschnitt als Clientgeheimnis verwenden werden.

## <a name="configure-azure-ad-as-an-identity-provider-in-your-tenant"></a>Konfigurieren von Azure AD als Identitätsanbieter in Ihrem Mandanten

1. Wählen Sie in der oberen Leiste Ihr Konto aus. Wählen Sie in der Liste **Verzeichnis** den Azure AD B2C-Mandanten (fabrikamb2c.onmicrosoft.com) aus.
1. [Wechseln Sie zum Azure AD B2C-Einstellungenmenü](active-directory-b2c-app-registration.md#navigate-to-b2c-settings) im Azure-Portal.
1. Klicken Sie im Azure AD B2C-Einstellungenmenü auf **Identitätsanbieter**.
1. Klicken Sie oben auf dem Blatt auf **+Hinzufügen** .
1. Geben Sie als **Name** einen aussagekräftigen Namen für die Konfiguration des Identitätsanbieters ein. Geben Sie beispielsweise „Contoso Azure AD“ ein.
1. Klicken Sie auf **Identitätsanbietertyp**, wählen Sie **Open ID Connect** aus, und klicken Sie auf **OK**.
1. Klicken Sie auf **Diesen Identitätsanbieter einrichten**.
1. Geben Sie für **Metadaten-URL** die folgende URL ein, in der `yourtenant` durch den Namen Ihres Azure AD-Mandanten (z.B. `contoso.com`) ersetzt wird:

    ```Console
    https://login.microsoftonline.com/yourtenant/.well-known/openid-configuration
    ```
1. Geben Sie für **Client-ID** und **Clientgeheimnis** Anwendungs-ID und Schlüssel aus dem vorherigen Abschnitt ein.
1. Behalten Sie den Standardwert für **Bereich** bei, der auf `openid` festgelegt sein sollte.
1. Behalten Sie den Standardwert für **Antworttyp** bei, der auf `code` festgelegt sein sollte.
1. Behalten Sie den Standardwert für **Antwortmodus** bei, der auf `form_post` festgelegt sein sollte.
1. Geben Sie optional einen Wert für **Domäne** ein (z.B. `ContosoAD`). Dieser Wert wird zum Verweis auf diesen Identitätsanbieter mit *domain_hint* in der Anforderung verwendet. 
1. Klicken Sie auf **OK**.
1. Klicken Sie auf **Ansprüche dieses Identitätsanbieters zuordnen**.
1. Geben Sie für **Benutzer-ID** `oid` ein.
1. Geben Sie für **Anzeigename** `name` ein.
1. Geben Sie für **Vorname** `given_name` ein.
1. Geben Sie für **Nachname** `family_name` ein.
1. Geben Sie für **E-Mail** `unique_name` ein.
1. Klicken Sie auf **OK** und dann auf **Erstellen**, um Ihre Konfiguration zu speichern.

## <a name="next-steps"></a>Nächste Schritte

Fügen Sie den neu erstellten Azure AD-Identitätsanbieter einer integrierten Richtlinie hinzu, und senden Sie Feedback an [AADB2CPreview@microsoft.com](mailto:AADB2CPreview@microsoft.com).
