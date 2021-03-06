---
title: 'Tutorial: Azure Active Directory-Integration mit PerformanceCentre | Microsoft Docs'
description: Erfahren Sie, wie Sie das einmalige Anmelden zwischen Azure Active Directory und PerformanceCentre konfigurieren.
services: active-directory
documentationCenter: na
author: jeevansd
manager: mtillman
ms.assetid: 65288c32-f7e6-4eb3-a6dc-523c3d748d1c
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/28/2017
ms.author: jeedes
ms.openlocfilehash: afee73a18502c48a6ff933f269f2572333d14196
ms.sourcegitcommit: b6319f1a87d9316122f96769aab0d92b46a6879a
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 05/20/2018
---
# <a name="tutorial-azure-active-directory-integration-with-performancecentre"></a>Tutorial: Azure Active Directory-Integration mit PerformanceCentre

In diesem Tutorial erfahren Sie, wie Sie PerformanceCentre in Azure Active Directory (Azure AD) integrieren.

Die Integration von PerformanceCentre in Azure AD bietet die folgenden Vorteile:

- Sie können in Azure AD steuern, wer Zugriff auf PerformanceCentre hat.
- Sie können es Benutzern ermöglichen, sich mit ihren Azure AD-Konten automatisch bei PerformanceCentre anzumelden (einmaliges Anmelden).
- Sie können Ihre Konten an einem zentralen Ort verwalten – im Azure-Portal.

Weitere Informationen zur Integration von SaaS-Apps in Azure AD finden Sie unter [Was bedeuten Anwendungszugriff und einmaliges Anmelden mit Azure Active Directory?](manage-apps/what-is-single-sign-on.md).

## <a name="prerequisites"></a>Voraussetzungen

Um die Azure AD-Integration mit PerformanceCentre konfigurieren zu können, benötigen Sie Folgendes:

- Ein Azure AD-Abonnement
- Ein PerformanceCentre-Abonnement, für das die einmalige Anmeldung aktiviert ist

> [!NOTE]
> Um die Schritte in diesem Tutorial zu testen, wird empfohlen, keine Produktionsumgebung zu verwenden.

Um die Schritte in diesem Tutorial zu testen, sollten Sie folgende Empfehlungen beachten:

- Verwenden Sie die Produktionsumgebung nur, wenn dies unbedingt erforderlich ist.
- Wenn Sie keine Azure AD-Testumgebung haben, können Sie [hier](https://azure.microsoft.com/pricing/free-trial/)eine einmonatige Testversion anfordern.

## <a name="scenario-description"></a>Beschreibung des Szenarios
In diesem Tutorial testen Sie das einmalige Anmelden für Azure AD in einer Testumgebung. Das in diesem Tutorial beschriebene Szenario besteht aus zwei Hauptbestandteilen:

1. Hinzufügen von PerformanceCentre aus dem Katalog
2. Konfigurieren und Testen der einmaligen Anmeldung von Azure AD

## <a name="adding-performancecentre-from-the-gallery"></a>Hinzufügen von PerformanceCentre aus dem Katalog
Zum Konfigurieren der Integration von PerformanceCentre in Azure AD müssen Sie PerformanceCentre aus dem Katalog zur Liste der verwalteten SaaS-Apps hinzufügen.

**Um PerformanceCentre aus dem Katalog hinzuzufügen, führen Sie die folgenden Schritte aus:**

1. Klicken Sie im linken Navigationsbereich des **[Azure-Portals](https://portal.azure.com)** auf das Symbol für **Azure Active Directory**. 

    ![Active Directory][1]

2. Navigieren Sie zu **Unternehmensanwendungen**. Wechseln Sie dann zu **Alle Anwendungen**.

    ![ANWENDUNGEN][2]
    
3. Klicken Sie oben im Dialogfeld auf die Schaltfläche **Neue Anwendung**, um eine neue Anwendung hinzuzufügen.

    ![ANWENDUNGEN][3]

4. Geben Sie in das Suchfeld als Suchbegriff **PerformanceCentre**ein.

    ![Erstellen eines Azure AD-Testbenutzers](./media/active-directory-saas-performancecentre-tutorial/tutorial_performancecentre_search.png)

5. Wählen Sie im Ergebnisbereich die Option **PerformanceCentre** aus, und klicken Sie dann auf die Schaltfläche **Hinzufügen**, um die Anwendung hinzuzufügen.

    ![Erstellen eines Azure AD-Testbenutzers](./media/active-directory-saas-performancecentre-tutorial/tutorial_performancecentre_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a>Konfigurieren und Testen der einmaligen Anmeldung von Azure AD
In diesem Abschnitt konfigurieren und testen Sie das einmalige Anmelden mit Azure AD bei PerformanceCentre mithilfe einer Testbenutzerin namens „Britta Simon“.

Damit einmaliges Anmelden funktioniert, muss Azure AD wissen, welcher Benutzer in PerformanceCentre als Gegenbenutzer zu einem Benutzer in Azure AD fungiert. Anders ausgedrückt: Zwischen einem Azure AD-Benutzer und dem entsprechenden Benutzer in PerformanceCentre muss eine Linkbeziehung eingerichtet werden.

Weisen Sie in PerformanceCentre den Wert für **Benutzername** in Azure AD als Wert für **Benutzername** zu, um eine Linkbeziehung herzustellen.

Zum Konfigurieren und Testen des einmaligen Anmeldens in Azure AD bei PerformanceCentre müssen Sie die folgenden Bausteine ausführen:

1. **[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**, um Ihren Benutzern das Verwenden dieser Funktion zu ermöglichen.
2. **[Erstellen eines Azure AD-Testbenutzers](#creating-an-azure-ad-test-user)** , um das einmalige Anmelden von Azure AD mit der Testbenutzerin Britta Simon zu testen.
3. **[Erstellen eines PerformanceCentre-Testbenutzers](#creating-a-performancecentre-test-user)** , um eine Entsprechung von Britta Simon in PerformanceCentre zu erhalten, die mit der Darstellung dieses Benutzers in Azure AD verknüpft ist.
4. **[Zuweisen des Azure AD-Testbenutzers](#assigning-the-azure-ad-test-user)**, um Britta Simon für das einmalige Anmelden von Azure AD zu aktivieren.
5. **[Testing Single Sign-On](#testing-single-sign-on)** , um zu überprüfen, ob die Konfiguration funktioniert.

### <a name="configuring-azure-ad-single-sign-on"></a>Konfigurieren des einmaligen Anmeldens von Azure AD

In diesem Abschnitt aktivieren Sie das einmalige Anmelden von Azure AD im Azure-Portal und konfigurieren das einmalige Anmelden in Ihrer PerformanceCentre-Anwendung.

**Führen Sie zum Konfigurieren des einmaligen Anmeldens in Azure AD mit PerformanceCentre die folgenden Schritte aus:**

1. Klicken Sie im Azure-Portal auf der Anwendungsintegrationsseite für **PerformanceCentre** auf **Einmaliges Anmelden**.

    ![Configure Single Sign-On][4]

2. Wählen Sie im Dialogfeld **Einmaliges Anmelden** als **Modus** die Option **SAML-basierte Anmeldung** aus, um einmaliges Anmelden zu aktivieren.
 
    ![Configure Single Sign-On](./media/active-directory-saas-performancecentre-tutorial/tutorial_performancecentre_samlbase.png)

3. Führen Sie im Abschnitt **Domäne und URLs für PerformanceCentre** die folgenden Schritte aus:

    ![Configure Single Sign-On](./media/active-directory-saas-performancecentre-tutorial/tutorial_performancecentre_url.png)

    a. Geben Sie im Textfeld **Anmelde-URL** eine URL im folgenden Format ein: `http://companyname.performancecentre.com/saml/SSO`.

    b. Geben Sie im Textfeld **Bezeichner** eine URL nach folgendem Muster ein: `http://companyname.performancecentre.com`

    > [!NOTE] 
    > Hierbei handelt es sich um Beispielwerte. Ersetzen Sie diese Werte durch die tatsächliche Anmelde-URL und den tatsächlichen Bezeichner. Wenden Sie sich an das [Clientsupportteam von PerformanceCentre](https://www.performancecentre.com/contact-us/), um diese Werte zu erhalten. 

4. Klicken Sie im Abschnitt **SAML-Signaturzertifikat** auf **Metadaten-XML**, und speichern Sie die Metadatendatei dann auf Ihrem Computer.

    ![Configure Single Sign-On](./media/active-directory-saas-performancecentre-tutorial/tutorial_performancecentre_certificate.png) 

5. Klicken Sie auf die Schaltfläche **Save** .

    ![Configure Single Sign-On](./media/active-directory-saas-performancecentre-tutorial/tutorial_general_400.png)

6. Klicken Sie im Abschnitt **PerformanceCentre-Konfiguration** auf **PerformanceCentre konfigurieren**, um das Fenster **Anmeldung konfigurieren** zu öffnen. Kopieren Sie die **SAML-Entitäts-ID und die URL für den SAML-SSO-Dienst** aus dem Abschnitt **Kurzübersicht**.

    ![Configure Single Sign-On](./media/active-directory-saas-performancecentre-tutorial/tutorial_performancecentre_configure.png) 

7. Melden Sie sich bei Ihrer **PerformanceCentre** -Unternehmenswebsite als Administrator an.

8. Klicken Sie auf der Registerkarte links auf **Configure**.
   
    ![Azure AD – einmaliges Anmelden][10]

9. Klicken Sie auf der Registerkarte links auf **Verschiedenes** und anschließend auf **Einmaliges Anmelden**.
   
    ![Azure AD – einmaliges Anmelden][11]

10. Wählen Sie unter **Protokoll** die Option **SAML** aus.
   
    ![Azure AD – einmaliges Anmelden][12]

11. Öffnen Sie die heruntergeladene Metadatendatei, kopieren Sie den Inhalt, und fügen Sie ihn in das Textfeld **Identity Provider Metadata** (Metadaten des Identitätsanbieters) ein. Klicken Sie anschließend auf **Speichern**.
   
    ![Azure AD – einmaliges Anmelden][13]

12. Vergewissern Sie sich, dass die Werte für **Entity Base URL** (Entitätsbasis-URL) und **Entity ID URL** (Entitäts-ID-URL) korrekt sind.
    
     ![Azure AD – einmaliges Anmelden][14]

> [!TIP]
> Während der Einrichtung der App können Sie im [Azure-Portal](https://portal.azure.com) nun eine Kurzfassung dieser Anweisungen lesen.  Nachdem Sie diese App aus dem Abschnitt **Active Directory > Unternehmensanwendungen** heruntergeladen haben, klicken Sie einfach auf die Registerkarte **Einmaliges Anmelden**, und rufen Sie die eingebettete Dokumentation über den Abschnitt **Konfiguration** um unteren Rand der Registerkarte auf. Weitere Informationen zur eingebetteten Dokumentation finden Sie hier: [Eingebettete Azure AD-Dokumentation]( https://go.microsoft.com/fwlink/?linkid=845985).
> 

### <a name="creating-an-azure-ad-test-user"></a>Erstellen eines Azure AD-Testbenutzers
Das Ziel dieses Abschnitts ist das Erstellen eines Testbenutzers namens Britta Simon im Azure-Portal.

![Azure AD-Benutzer erstellen][100]

**Um einen Testbenutzer in Azure AD zu erstellen, führen Sie die folgenden Schritte aus:**

1. Klicken Sie im linken Navigationsbereich des **Azure-Portals** auf das Symbol für **Azure Active Directory**.

    ![Erstellen eines Azure AD-Testbenutzers](./media/active-directory-saas-performancecentre-tutorial/create_aaduser_01.png) 

2. Wechseln Sie zu **Benutzer und Gruppen**, und klicken Sie auf **Alle Benutzer**, um die Liste der Benutzer anzuzeigen.
    
    ![Erstellen eines Azure AD-Testbenutzers](./media/active-directory-saas-performancecentre-tutorial/create_aaduser_02.png) 

3. Klicken Sie oben im Dialogfeld auf **Hinzufügen**, um das Dialogfeld **Benutzer** zu öffnen.
 
    ![Erstellen eines Azure AD-Testbenutzers](./media/active-directory-saas-performancecentre-tutorial/create_aaduser_03.png) 

4. Führen Sie auf der Dialogfeldseite **Benutzer** die folgenden Schritte aus:
 
    ![Erstellen eines Azure AD-Testbenutzers](./media/active-directory-saas-performancecentre-tutorial/create_aaduser_04.png) 

    a. Geben Sie in das Textfeld **Name** den Namen **BrittaSimon** ein.

    b. Geben Sie in das Textfeld **Benutzername** die **E-Mail-Adresse** von Britta Simon ein.

    c. Wählen Sie **Kennwort anzeigen** aus, und notieren Sie sich den Wert des **Kennworts**.

    d. Klicken Sie auf **Create**.
 
### <a name="creating-a-performancecentre-test-user"></a>Erstellen eines PerformanceCentre-Testbenutzers

Das Ziel dieses Abschnitts ist das Erstellen eines Benutzers namens Britta Simon in PerformanceCentre.

**Um einen Benutzer namens Britta Simon in PerformanceCentre zu erstellen, führen Sie die folgenden Schritte aus:**

1. Melden Sie sich bei Ihrer PerformanceCentre-Unternehmenswebsite als Administrator an.

2. Klicken Sie im Menü auf der linken Seite auf **Interrelate** (Verknüpfen) und anschließend auf **Create Participant** (Teilnehmer erstellen).
   
    ![Benutzer erstellen][400]

3. Führen Sie auf der Dialogfeldseite **Interrelate - Create Participant** die folgenden Schritte aus:
   
    ![Benutzer erstellen][401]
    
    a. Geben Sie die erforderlichen Attribute für Britta Simon in die entsprechenden Textfelder ein.
    
    >[!IMPORTANT]
    >Das Attribut für den Benutzernamen von Britta in PerformanceCentre muss mit dem Benutzernamen in Azure AD identisch sein.
    
    b. Wählen Sie unter **Rolle auswählen** die Option **Clientadministrator** aus.
    
    c. Klicken Sie auf **Speichern**. 

### <a name="assigning-the-azure-ad-test-user"></a>Zuweisen des Azure AD-Testbenutzers

In diesem Abschnitt ermöglichen Sie Britta Simon die Verwendung des einmaligen Anmeldens von Azure, indem Sie ihr Zugriff auf PerformanceCentre gewähren.

![Benutzer zuweisen][200] 

**Um Britta Simon PerformanceCentre zuzuweisen, führen Sie die folgenden Schritte aus:**

1. Öffnen Sie im Azure-Portal die Anwendungsansicht, navigieren Sie zur Verzeichnisansicht, wechseln Sie dann zu **Unternehmensanwendungen**, und klicken Sie auf **Alle Anwendungen**.

    ![Benutzer zuweisen][201] 

2. Wählen Sie in der Anwendungsliste **PerformanceCentre**aus.

    ![Configure Single Sign-On](./media/active-directory-saas-performancecentre-tutorial/tutorial_performancecentre_app.png) 

3. Klicken Sie im Menü auf der linken Seite auf **Benutzer und Gruppen**.

    ![Benutzer zuweisen][202] 

4. Klicken Sie auf die Schaltfläche **Hinzufügen**. Wählen Sie dann im Dialogfeld **Zuweisung hinzufügen** die Option **Benutzer und Gruppen** aus.

    ![Benutzer zuweisen][203]

5. Wählen Sie im Dialogfeld **Benutzer und Gruppen** in der Benutzerliste **Britta Simon** aus.

6. Klicken Sie im Dialogfeld **Benutzer und Gruppen** auf die Schaltfläche **Auswählen**.

7. Klicken Sie im Dialogfeld **Zuweisung hinzufügen** auf **Zuweisen**.
    
### <a name="testing-single-sign-on"></a>Testen der einmaligen Anmeldung

Das Ziel dieses Abschnitts ist das Testen Ihrer Azure AD-Konfiguration für einmaliges Anmelden (SSO) über den Zugriffsbereich.  

Wenn Sie im Zugriffsbereich auf die Kachel „PerformanceCentre“ klicken, sollten Sie automatisch bei Ihrer PerformanceCentre-Anwendung angemeldet werden.

## <a name="additional-resources"></a>Zusätzliche Ressourcen

* [Liste der Tutorials zur Integration von SaaS-Apps in Azure Active Directory](active-directory-saas-tutorial-list.md)
* [Was bedeuten Anwendungszugriff und einmaliges Anmelden mit Azure Active Directory?](manage-apps/what-is-single-sign-on.md)

<!--Image references-->

[1]: ./media/active-directory-saas-performancecentre-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-performancecentre-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-performancecentre-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-performancecentre-tutorial/tutorial_general_04.png
[10]: ./media/active-directory-saas-performancecentre-tutorial/tutorial_performancecentre_06.png
[11]: ./media/active-directory-saas-performancecentre-tutorial/tutorial_performancecentre_07.png
[12]: ./media/active-directory-saas-performancecentre-tutorial/tutorial_performancecentre_08.png
[13]: ./media/active-directory-saas-performancecentre-tutorial/tutorial_performancecentre_09.png
[14]: ./media/active-directory-saas-performancecentre-tutorial/tutorial_performancecentre_10.png

[100]: ./media/active-directory-saas-performancecentre-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-performancecentre-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-performancecentre-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-performancecentre-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-performancecentre-tutorial/tutorial_general_203.png
[400]: ./media/active-directory-saas-performancecentre-tutorial/tutorial_performancecentre_11.png
[401]: ./media/active-directory-saas-performancecentre-tutorial/tutorial_performancecentre_12.png

