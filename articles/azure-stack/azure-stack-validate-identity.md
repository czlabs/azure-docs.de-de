---
title: Überprüfen einer Azure-Identität für Azure Stack | Microsoft-Dokumentation
description: Verwenden Sie Azure Stack Readiness Checker, um eine Azure-Identität zu überprüfen.
services: azure-stack
documentationcenter: ''
author: brenduns
manager: femila
editor: ''
ms.assetid: ''
ms.service: azure-stack
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 05/08/2018
ms.author: brenduns
ms.reviewer: ''
ms.openlocfilehash: fe5e7281cbe01ad11f667729df344f91ef1327d2
ms.sourcegitcommit: d98d99567d0383bb8d7cbe2d767ec15ebf2daeb2
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 05/10/2018
---
# <a name="validate-azure-identity"></a>Überprüfen der Azure-Identität 
Verwenden Sie das Tool Azure Stack Readiness Checker (AzsReadinessChecker), um zu überprüfen, ob Ihre Azure Active Directory-Instanz (Azure AD) mit Azure Stack verwendet werden kann. Überprüfen Sie Ihre Azure-Identitätslösung, bevor Sie mit einer Azure Stack-Bereitstellung beginnen.  

Bei der Überprüfung der Bereitschaft wird Folgendes geprüft:
 - Azure Active Directory (Azure AD) funktioniert als Identitätsanbieter für Azure Stack.
 - Das Azure AD-Konto, das Sie verwenden möchten, kann sich als globaler Administrator Ihrer Azure Active Directory-Instanz anmelden. 

Durch eine Überprüfung wird sichergestellt, dass Ihre Umgebung für Azure Stack verwendet werden kann und Informationen zu Benutzern, Anwendungen, Gruppen und Dienstprinzipalen aus Azure Stack in Ihrer Azure AD-Instanz speichern kann.

## <a name="get-the-readiness-checker-tool"></a>Beziehen des Tools zur Bereitschaftsüberprüfung
Laden Sie die neueste Version des Tools Azure Stack Readiness Checker (AzsReadinessChecker) über [PSGallery](https://aka.ms/AzsReadinessChecker) herunter.  

## <a name="prerequisites"></a>Voraussetzungen
Die folgenden Voraussetzungen müssen erfüllt werden:

**Auf dem Computer, auf dem das Tool ausgeführt wird, muss Folgendes installiert sein**:
 - Windows 10 oder Windows Server 2016 mit Internetkonnektivität
 - PowerShell 5.1 oder höher Um Ihre Version zu überprüfen, führen Sie den folgenden PowerShell-CMD-Befehl aus, und überprüfen Sie dann die *Hauptversion* und die *Nebenversionen*:  

   > `$PSVersionTable.PSVersion`
 - Konfigurieren Sie [PowerShell für Azure Stack](azure-stack-powershell-install.md). 
 - Laden Sie die neueste Version des Tools [Microsoft Azure Stack Readiness Checker](https://aka.ms/AzsReadinessChecker) herunter.

**Azure Active Directory-Umgebung**:
 - Bestimmen Sie das Azure AD-Konto, das Sie für Azure Stack verwenden möchten, und stellen Sie sicher, dass es einem globalem Azure Active Directory-Administrator gehört.
 - Ermitteln Sie den Namen Ihres Azure AD-Mandanten. Der Mandantenname muss der *primäre* Domänenname für Ihre Azure Active Directory-Instanz sein. Beispiel: *contoso.onmicrosoft.com*. 
 - Bestimmen Sie den AzureEnvironment-Wert, den Sie verwenden: *AzureCloud*, *AzureGermanCloud* oder *AzureChinaCloud*.

## <a name="validate-azure-identity"></a>Überprüfen der Azure-Identität 
1. Öffnen Sie auf einem Computer, der die Voraussetzungen erfüllt, eine administrative PowerShell-Eingabeaufforderung, und führen Sie den folgenden Befehl zum Installieren von AzsReadinessChecker aus:  

   > `Install-Module Microsoft.AzureStack.ReadinessChecker -Force`

2. Führen Sie in der PowerShell-Eingabeaufforderung Folgendes aus, um *$serviceAdminCredential* als Dienstadministrator für Ihren Azure AD-Mandanten festzulegen.  Ersetzen Sie *serviceadmin@contoso.onmicrosoft.com* durch Ihr Konto und Ihren Mandanten. 
   > `$serviceAdminCredential = Get-Credential serviceadmin@contoso.onmicrosoft.com -Message "Enter Credentials for Service Administrator of Azure Active Directory Tenant"` 

3. Führen Sie in der PowerShell-Eingabeaufforderung Folgendes aus, um die Überprüfung Ihrer Azure AD-Instanz zu starten: 
   - Legen Sie als Wert für AzureEnvironment *AzureCloud*, *AzureGermanCloud* oder *AzureChinaCloud* fest.  
   - Geben Sie als Ersatz für *contoso.onmicrosoft.com* den Namen Ihres Azure Active Directory-Mandanten ein. 

   > `Start-AzsReadinessChecker -AADServiceAdministrator $serviceAdminCredential -AzureEnvironment AzureCloud -AADDirectoryTenantName contoso.onmicrosoft.com`
4. Wenn das Tool ausgeführt wird, überprüfen Sie die Ausgabe. Vergewissern Sie sich, dass der Status für die Anmelde- und Registrierungsanforderungen **OK** lautet. Eine erfolgreiche Überprüfung wie etwa in der folgenden Abbildung wird angezeigt: 
 
![Ausführen der Überprüfung](./media/azure-stack-validate-identity/validation.png)


## <a name="report-and-log-file"></a>Berichts- und Protokolldatei
Bei jeder Ausführung einer Überprüfung werden Ergebnisse in den Dateien **AzsReadinessChecker.log** und **AzsReadinessCheckerReport.json** protokolliert. Der Speicherort dieser Dateien wird mit den Überprüfungsergebnissen in PowerShell angezeigt.

Anhand dieser Dateien können Sie den Überprüfungsstatus freigeben, bevor Sie Azure Stack bereitstellen oder Probleme mit der Überprüfung untersuchen.  Die Ergebnisse aller nachfolgenden Überprüfungen werden in beiden Dateien gespeichert. Der Bericht enthält die Bestätigung Ihres Bereitstellungsteams über die Identitätskonfiguration. Mithilfe der Protokolldatei kann Ihr Bereitstellungs- oder Supportteam Probleme bei der Überprüfung untersuchen. 

Standardmäßig werden beide Dateien in das Verzeichnis *C:\Users\<Benutzername>\AppData\Local\Temp\AzsReadinessChecker\AzsReadinessCheckerReport.json* geschrieben.  
 - Verwenden Sie den Parameter **-OutputPath** ***&lt;Pfad&gt;*** am Ende der Befehlszeilenausführung, um einen anderen Berichtsspeicherort anzugeben.   
 - Verwenden Sie den Parameter **-CleanReport** am Ende der Befehlszeilenausführung, um Informationen von früheren Ausführungen des Tools aus *AzsReadinessCheckerReport.json*  zu löschen. 

Weitere Informationen hierzu finden Sie unter [Azure Stack-Überprüfungsbericht](azure-stack-validation-report.md).

## <a name="validation-failures"></a>Fehler bei der Überprüfung
Wenn bei der Überprüfung Fehler auftreten, werden Details zum Fehler im PowerShell-Fenster angezeigt. Das Tool protokolliert Informationen außerdem in der Datei „AzsReadinessChecker.log“.

Die folgenden Beispiele veranschaulichen, wie häufige Fehler bei der Überprüfung behoben werden.

### <a name="expired-or-temporary-password"></a>Abgelaufenes oder temporäres Kennwort 
 
![Abgelaufenes Kennwort](./media/azure-stack-validate-identity/expired-password.png)
**Ursache**: Das Konto kann sich nicht anmelden, da das Kennwort entweder abgelaufen oder temporär ist.     

**Lösung**: Führen Sie in PowerShell Folgendes aus, und befolgen Sie die Eingabeaufforderungen zum Zurücksetzen des Kennworts.  
> `Login-AzureRMAccount`

Melden Sie sich alternativ unter https://portal.azure.com mit dem Konto an. Der Benutzer wird dann zur Änderung des Kennworts aufgefordert.
### <a name="unknown-user-type"></a>Unbekannter Benutzertyp 
 
![Unbekannter Benutzer](./media/azure-stack-validate-identity/unknown-user.png)
**Ursache**: Das Konto kann sich nicht bei der angegebenen Azure Active Directory-Umgebung (AADDirectoryTenantName) anmelden. In diesem Beispiel ist *AzureChinaCloud* für *AzureEnvironment* angegeben.

**Lösung**: Vergewissern Sie sich, dass das Konto für die angegebene Azure-Umgebung gültig ist. Führen Sie in PowerShell Folgendes aus, um zu überprüfen, ob das Konto für eine bestimmte Umgebung gültig ist: Login-AzureRmAccount – EnvironmentName AzureChinaCloud. 
### <a name="account-is-not-an-administrator"></a>Konto ohne Administratorrolle 
 
![Konto ohne Administratorrolle](./media/azure-stack-validate-identity/not-admin.png)

**Ursache**: Auch wenn sich das Konto erfolgreich anmelden kann, gehört das Konto nicht einem Administrator von Azure Active Directory (AADDirectoryTenantName).  

**Lösung**: Melden Sie sich unter https://portal.azure.com mit dem Konto an, und navigieren Sie zu **Azure Active Directory** > **Benutzer** > *. Wählen Sie dann den Benutzer aus, klicken Sie auf*  > **Verzeichnisrolle**, und vergewissern Sie sich, dass dem Benutzer die Rolle **Globaler Administrator** zugewiesen ist.  Wenn das Konto der jeweilige Benutzer ist, navigieren Sie zu **Azure Active Directory** > **Benutzerdefinierte Domänennamen**, und vergewissern Sie sich, dass der für *AADDirectoryTenantName* angegebene Name als primärer Domänenname für dieses Verzeichnis gekennzeichnet ist.  In diesem Beispiel ist dies *contoso.onmicrosoft.com*. 

Bei Azure Stack muss der Domänenname der primäre Domänenname sein.

## <a name="next-steps"></a>Nächste Schritte
[Überprüfen der Azure-Registrierung](azure-stack-validate-registration.md)  
[Anzeigen des Bereitschaftsberichts](azure-stack-validation-report.md)  
[Allgemeine Überlegungen zur Azure Stack-Integration](azure-stack-datacenter-integration.md)  

