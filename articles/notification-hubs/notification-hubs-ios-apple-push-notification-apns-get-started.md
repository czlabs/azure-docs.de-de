---
title: Senden von Pushbenachrichtigungen an iOS-Apps mit Azure Notification Hubs | Microsoft-Dokumentation
description: In diesem Tutorial erfahren Sie, wie Sie mithilfe von Azure Notification Hubs Pushbenachrichtigungen an iOS-Anwendungen senden.
services: notification-hubs
documentationcenter: ios
keywords: Pushbenachrichtigung,Pushbenachrichtigungen,iOS-Pushbenachrichtigungen
author: dimazaid
manager: kpiteira
editor: spelluru
ms.assetid: b7fcd916-8db8-41a6-ae88-fc02d57cb914
ms.service: notification-hubs
ms.workload: mobile
ms.tgt_pltfrm: mobile-ios
ms.devlang: objective-c
ms.topic: tutorial
ms.custom: mvc
ms.date: 04/14/2018
ms.author: dimazaid
ms.openlocfilehash: 083b0c956055ab5b54a4af2eec57f096613cbe65
ms.sourcegitcommit: e221d1a2e0fb245610a6dd886e7e74c362f06467
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 05/07/2018
---
# <a name="tutorial-push-notifications-to-ios-apps-using-azure-notification-hubs"></a>Tutorial: Senden von Pushbenachrichtigungen an iOS-Apps mit Azure Notification Hubs
[!INCLUDE [notification-hubs-selector-get-started](../../includes/notification-hubs-selector-get-started.md)]

In diesem Tutorial verwenden Sie Azure Notification Hubs, um Pushbenachrichtigungen an eine iOS-Anwendung zu senden. Sie erstellen eine leere iOS-App, die Pushbenachrichtigungen mithilfe des Apple-Pushbenachrichtigungsdiensts ([Apple Push Notification Service, APNs](https://developer.apple.com/library/content/documentation/NetworkingInternet/Conceptual/RemoteNotificationsPG/APNSOverview.html#//apple_ref/doc/uid/TP40008194-CH8-SW1)) empfängt. 

In diesem Tutorial führen Sie die folgenden Schritte aus:

> [!div class="checklist"]
> * Generieren der Datei für die Anforderung der Zertifikatsignierung
> * Anfordern von Pushbenachrichtigungen für Ihre App
> * Erstellen eines Bereitstellungsprofils für die App
> * Konfigurieren Ihres Notification Hub für iOS-Pushbenachrichtigungen
> * Verbinden der iOS-App mit Notification Hubs
> * Senden von Test-Pushbenachrichtigungen
> * Überprüfen, ob die App Benachrichtigungen empfängt

Den vollständigen Code für dieses Tutorial finden Sie [auf GitHub](https://github.com/Azure/azure-notificationhubs-samples/tree/master/iOS/GetStartedNH/GetStarted). 

## <a name="prerequisites"></a>Voraussetzungen

- Ein aktives Azure-Konto. Wenn Sie noch kein Konto besitzen, können Sie innerhalb weniger Minuten ein [kostenloses Testkonto](https://azure.microsoft.com/free) erstellen. 
- [Microsoft Azure-Messaging-Framework]
- Neueste Version von [Xcode]
- Für iOS 10 (oder eine neuere Version) geeignetes Gerät
- [Apple-Entwicklerprogramm-Mitgliedschaft](https://developer.apple.com/programs/)
  
  > [!NOTE]
  > Pushbenachrichtigungen müssen aufgrund von Konfigurationsanforderungen auf einem physischen iOS-Gerät (iPhone oder iPad) anstatt im iOS-Simulator bereitgestellt und getestet werden.
  
Das Abschließen dieses Lernprogramms ist eine Voraussetzung für alle anderen Notification Hubs-Lernprogramme für iOS-Apps.

[!INCLUDE [Notification Hubs Enable Apple Push Notifications](../../includes/notification-hubs-enable-apple-push-notifications.md)]

## <a name="configure-your-notification-hub-for-ios-push-notifications"></a>Konfigurieren Ihres Notification Hub für iOS-Pushbenachrichtigungen
In diesem Abschnitt erstellen Sie einen neuen Notification Hub und konfigurieren die Authentifizierung mit APNs unter Verwendung des zuvor erstellten Pushzertifikats vom Typ **.p12**. Wenn Sie einen bereits erstellten Notification Hub verwenden möchten, können Sie zu Schritt 5 springen.

[!INCLUDE [notification-hubs-portal-create-new-hub](../../includes/notification-hubs-portal-create-new-hub.md)]

### <a name="configure-your-notification-hub-with-apns-information"></a>Konfigurieren Ihres Notification Hubs mit APNs-Informationen

1. Wählen Sie unter **Notification Services** die Option **Apple (APNS)** aus. 
2. Wählen Sie **Certificate**aus.
3. Wählen Sie das **Dateisymbol** aus.
4. Wählen Sie die **.p12**-Datei, die Sie zuvor exportiert haben.
5. Geben Sie das richtige **Kennwort** an.
6. Wählen Sie den Modus **Sandbox**. Wählen Sie den Modus **Produktion** nur dann, wenn Sie Pushbenachrichtigungen an Benutzer senden möchten, die Ihre App im Store erworben haben.

    ![Konfigurieren der APNS-Zertifizierung im Azure-Portal][7]

Sie haben nun Ihren Notification Hub mit APNS konfiguriert und verfügen über die Verbindungszeichenfolge zum Registrieren Ihrer App sowie zum Versenden von Pushbenachrichtigungen.

## <a name="connect-your-ios-app-to-notification-hubs"></a>Verbinden der iOS-App mit Notification Hubs
1. Erstellen Sie in Xcode ein neues iOS-Projekt, und wählen Sie die Vorlage **Single View Application** aus.
   
    ![Xcode – Single View Application][8]
    
2. Achten Sie beim Festlegen der Optionen für das neue Projekt darauf, dass Sie den gleichen **Produktnamen** und die gleiche **Organisations-ID** verwenden wie beim Festlegen der Paket-ID im Apple-Entwicklerportal.
   
    ![Xcode – Projektoptionen][11]
    
3. Klicken Sie in der Projektnavigation auf Ihren Projektnamen, klicken Sie auf die Registerkarte **Allgemein**, und suchen Sie nach **Signierung**. Wählen Sie das passende Team für Ihr Apple-Entwicklerkonto aus. Xcode sollte auf der Grundlage Ihrer Paket-ID automatisch das Bereitstellungsprofil abrufen, das Sie zuvor erstellt haben.
   
    Wenn das neue in Xcode erstellte Bereitstellungsprofil nicht angezeigt wird, versuchen Sie, die Profile für Ihre Signaturidentität zu aktualisieren. Klicken Sie in der Menüleiste auf **Xcode**, dann auf **Voreinstellungen**, auf die Registerkarte **Konto**, auf die Schaltfläche **Details anzeigen**, auf die Signaturidentität und anschließend rechts unten auf die Schaltfläche „Aktualisieren“.

    ![Xcode – Bereitstellungsprofil][9]

4. Vergewissern Sie sich auf der Registerkarte **Funktionen**, dass Pushbenachrichtigungen aktiviert sind.

    ![Xcode – Pushfunktionen][12]
   
5. Laden Sie das [Microsoft Azure-Messaging-Framework] herunter, und entzippen Sie die Datei. Klicken Sie in Xcode mit der rechten Maustaste auf Ihr Projekt, und klicken Sie dann auf die Option **Add Files to** zum Hinzufügen des Ordners **WindowsAzureMessaging.framework** zum Xcode-Projekt. Klicken Sie auf **Optionen**, vergewissern Sie sich, dass die Option **Copy items if needed** (Elemente kopieren, wenn nötig) aktiviert ist, und klicken Sie dann auf **Hinzufügen**.

    ![Azure SDK entzippen][10]

6. Fügen Sie Ihrem Projekt eine neue Headerdatei namens **HubInfo.h** hinzu. Diese Datei enthält die Konstanten für Ihren Notification Hub. Fügen Sie die folgenden Definitionen hinzu, und ersetzen Sie die Platzhalter für Zeichenfolgenliterale durch Ihren *Hubnamen* und den zuvor notierten Wert für *DefaultListenSharedAccessSignature*.

    ```obj-c
        #ifndef HubInfo_h
        #define HubInfo_h
   
            #define HUBNAME @"<Enter the name of your hub>"
            #define HUBLISTENACCESS @"<Enter your DefaultListenSharedAccess connection string"
   
        #endif /* HubInfo_h */
    ```
    
7. Öffnen Sie die Datei **AppDelegate.h**, und fügen Sie die folgenden Importdirektiven hinzu:

    ```obj-c
        #import <WindowsAzureMessaging/WindowsAzureMessaging.h>
        #import <UserNotifications/UserNotifications.h> 
        #import "HubInfo.h"
    ```
8. Fügen Sie in der Datei **AppDelegate.m** der Methode **didFinishLaunchingWithOptions** die folgenden Codezeilen hinzu (abhängig von Ihrer iOS-Version). Dieser Code registriert Ihr Gerätehandle bei APNS:

    ```obj-c
        UIUserNotificationSettings *settings = [UIUserNotificationSettings settingsForTypes:UIUserNotificationTypeSound |
            UIUserNotificationTypeAlert | UIUserNotificationTypeBadge categories:nil];
   
        [[UIApplication sharedApplication] registerUserNotificationSettings:settings];
        [[UIApplication sharedApplication] registerForRemoteNotifications];
    ```
   
9. Fügen Sie in der gleichen Datei die folgenden Methoden hinzu:

    ```obj-c
         - (void) application:(UIApplication *) application didRegisterForRemoteNotificationsWithDeviceToken:(NSData *) deviceToken {
           SBNotificationHub* hub = [[SBNotificationHub alloc] initWithConnectionString:HUBLISTENACCESS
                                        notificationHubPath:HUBNAME];
   
            [hub registerNativeWithDeviceToken:deviceToken tags:nil completion:^(NSError* error) {
               if (error != nil) {
                   NSLog(@"Error registering for notifications: %@", error);
                }
                else {
                   [self MessageBox:@"Registration Status" message:@"Registered"];
              }
          }];
         }
   
        -(void)MessageBox:(NSString *) title message:(NSString *)messageText
        {
         UIAlertView *alert = [[UIAlertView alloc] initWithTitle:title message:messageText delegate:self
                cancelButtonTitle:@"OK" otherButtonTitles: nil];
            [alert show];
        }
    ```

    Mit diesem Code wird eine Verbindung mit dem Notification Hub mithilfe der in „HubInfo.h“ angegebenen Verbindungsinformationen hergestellt. Dieser Code übergibt das Gerätetoken an den Notification Hub, sodass dieser Benachrichtigungen senden kann.

10. Fügen Sie in derselben Datei folgende Methode hinzu, um einen **UIAlert** anzuzeigen, wenn die Benachrichtigung empfangen wird, während die App aktiv ist:

    ```obj-c
            - (void)application:(UIApplication *)application didReceiveRemoteNotification: (NSDictionary *)userInfo {
               NSLog(@"%@", userInfo);
               [self MessageBox:@"Notification" message:[[userInfo objectForKey:@"aps"] valueForKey:@"alert"]];
           }
    ```

11. Erstellen Sie die App auf Ihrem Gerät, und führen Sie sie dort aus, um Fehler auszuschließen.

## <a name="send-test-push-notifications"></a>Senden von Test-Pushbenachrichtigungen
Mit der Option *Testsendevorgang* im [Azure-Portal] können Sie den Empfang von Benachrichtigungen in Ihrer App testen. Diese Option sendet zu Testzwecken eine Pushbenachrichtigung an Ihr Gerät.

![Azure-Portal – Testsendung][30]

[!INCLUDE [notification-hubs-sending-notifications-from-the-portal](../../includes/notification-hubs-sending-notifications-from-the-portal.md)]


## <a name="verify-that-your-app-receives-push-notifications"></a>Überprüfen, ob die App Pushbenachrichtigungen empfängt
Zum Testen von Pushbenachrichtigungen unter iOS müssen Sie die App auf einem physischen iOS-Gerät bereitstellen. Sie können keine Apple-Pushbenachrichtigungen mit dem iOS-Simulator senden.

1. Führen Sie die App aus, und überprüfen Sie, ob die Registrierung erfolgreich ist. Drücken Sie dann **OK**.
   
    ![Registrierungstest für iOS-App-Pushbenachrichtigungen][33]
2. Als Nächstes senden Sie zu Testzwecken eine Pushbenachrichtigung über das [Azure-Portal], wie im vorherigen Abschnitt beschrieben. 

3. Die Pushbenachrichtigung wird an alle Geräte gesendet, die dafür registriert sind, die Benachrichtigungen vom jeweiligen Notification Hub zu erhalten.
   
    ![iOS-App-Pushbenachrichtigung – Testempfang][35]

## <a name="next-steps"></a>Nächste Schritte
In diesem einfachen Beispiel haben Sie Pushbenachrichtigungen an alle Ihre registrierten iOS-Geräte übertragen. Um zu erfahren, wie Sie Pushbenachrichtigungen an bestimmte iOS-Geräte senden, fahren Sie mit dem folgenden Tutorial fort: 

> [!div class="nextstepaction"]
>[Senden von Pushbenachrichtigungen an bestimmte Geräte](notification-hubs-ios-xplat-segmented-apns-push-notification.md)


<!-- Images. -->

[6]: ./media/notification-hubs-ios-get-started/notification-hubs-apple-config.png
[7]: ./media/notification-hubs-ios-get-started/notification-hubs-apple-config-cert.png
[8]: ./media/notification-hubs-ios-get-started/notification-hubs-create-ios-app.png
[9]: ./media/notification-hubs-ios-get-started/notification-hubs-create-ios-app2.png
[10]: ./media/notification-hubs-ios-get-started/notification-hubs-create-ios-app3.png
[11]: ./media/notification-hubs-ios-get-started/notification-hubs-xcode-product-name.png
[12]: ./media/notification-hubs-ios-get-started/notification-hubs-enable-push.png

[30]: ./media/notification-hubs-ios-get-started/notification-hubs-test-send.png

[31]: ./media/notification-hubs-ios-get-started/notification-hubs-ios-ui.png
[32]: ./media/notification-hubs-ios-get-started/notification-hubs-storyboard-view.png
[33]: ./media/notification-hubs-ios-get-started/notification-hubs-test1.png
[35]: ./media/notification-hubs-ios-get-started/notification-hubs-test3.png



<!-- URLs. -->
[Microsoft Azure-Messaging-Framework]: http://go.microsoft.com/fwlink/?LinkID=799698&clcid=0x409
[Mobile Services iOS SDK]: http://go.microsoft.com/fwLink/?LinkID=266533
[Submit an app page]: http://go.microsoft.com/fwlink/p/?LinkID=266582
[My Applications]: http://go.microsoft.com/fwlink/p/?LinkId=262039
[Live SDK for Windows]: http://go.microsoft.com/fwlink/p/?LinkId=262253

[Get started with Mobile Services]: /develop/mobile/tutorials/get-started-ios
[Notification Hubs Guidance]: http://msdn.microsoft.com/library/jj927170.aspx
[Xcode]: https://go.microsoft.com/fwLink/p/?LinkID=266532
[iOS Provisioning Portal]: http://go.microsoft.com/fwlink/p/?LinkId=272456

[Get started with push notifications in Mobile Services]: ../mobile-services-javascript-backend-ios-get-started-push.md
[Azure Notification Hubs Notify Users for iOS with .NET backend]: notification-hubs-aspnet-backend-ios-apple-apns-notification.md
[Use Notification Hubs to send breaking news]: notification-hubs-ios-xplat-segmented-apns-push-notification.md

[Local and Push Notification Programming Guide]: http://developer.apple.com/library/mac/#documentation/NetworkingInternet/Conceptual/RemoteNotificationsPG/Chapters/ApplePushService.html#//apple_ref/doc/uid/TP40008194-CH100-SW1
[Azure-Portal]: https://portal.azure.com
