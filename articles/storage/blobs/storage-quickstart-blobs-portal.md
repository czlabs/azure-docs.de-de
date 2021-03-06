---
title: 'Azure-Schnellstart: Erstellen eines Blobs im Objektspeicher mithilfe des Azure-Portals | Microsoft-Dokumentation'
description: In dieser Schnellstartanleitung verwenden Sie das Azure-Portal im Objektspeicher (Blob). Anschließend verwenden Sie das Azure-Portal, um ein Blob in Azure Storage hochzuladen, ein Blob herunterzuladen und die Blobs in einem Container aufzulisten.
services: storage
author: tamram
manager: jeconnoc
ms.custom: mvc
ms.service: storage
ms.topic: quickstart
ms.date: 04/09/2018
ms.author: tamram
ms.openlocfilehash: 1468aa0f12a05b71e3b997e1850d345a492308f2
ms.sourcegitcommit: 9cdd83256b82e664bd36991d78f87ea1e56827cd
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/16/2018
---
# <a name="quickstart-upload-download-and-list-blobs-using-the-azure-portal"></a>Schnellstart: Hochladen, Herunterladen und Auflisten von Blobs über das Azure-Portal

In dieser Schnellstartanleitung erfahren Sie, wie Sie über das [Azure-Portal](https://portal.azure.com/) einen Container in Azure Storage erstellen und Blockblobs in diesen Container hochladen bzw. daraus herunterladen.

## <a name="prerequisites"></a>Voraussetzungen

Wenn Sie kein Azure-Abonnement besitzen, können Sie ein [kostenloses Konto](https://azure.microsoft.com/free/?WT.mc_id=A261C142F) erstellen, bevor Sie beginnen.

[!INCLUDE [storage-quickstart-tutorial-create-account-portal](../../../includes/storage-quickstart-tutorial-create-account-portal.md)]

## <a name="create-a-container"></a>Erstellen eines Containers

Führen Sie die folgenden Schritte aus, um einen Container über das Azure-Portal zu erstellen:

1. Navigieren Sie im Azure-Portal zu Ihrem neuen Speicherkonto.
2. Scrollen Sie im linken Menü für das Speicherkonto zum Abschnitt **Blob-Dienst**, und klicken Sie auf **Blobs durchsuchen**.
3. Klicken Sie auf die Schaltfläche **Container hinzufügen**.
4. Geben Sie einen Namen für den neuen Container ein. Der Containername muss klein geschrieben werden, mit einem Buchstaben oder einer Zahl beginnen und darf nur Buchstaben, Zahlen und Bindestriche (-) enthalten. Weitere Informationen zu Container- und Blobnamen finden Sie unter [Benennen von Containern, Blobs und Metadaten und Verweisen auf diese](https://docs.microsoft.com/rest/api/storageservices/naming-and-referencing-containers--blobs--and-metadata).
5. Legen Sie die öffentliche Zugriffsebene für den Container fest. Die Standardebene ist **Private (no anonymous access)** (Privat (kein anonymer Zugriff)).
6. Klicken Sie auf **OK** aus, um den Container zu erstellen.

    ![Screenshot: Erstellen eines Containers über das Azure-Portal](media/storage-quickstart-blobs-portal/create-container.png)

## <a name="upload-a-block-blob"></a>Hochladen eines Blockblobs

Blockblobs bestehen aus Datenblöcken, die zusammen ein Blob bilden. In den meisten Blob Storage-Szenarien werden Blockblobs verwendet. Blockblobs eignen sich perfekt zum Speichern von Text und Binärdaten in der Cloud. Hierzu zählen beispielsweise Dateien, Bilder und Videos. In dieser Schnellstartanleitung erfahren Sie, wie Sie Blockblobs verwenden. 

Gehen Sie wie folgt vor, um über das Azure-Portal ein Blockblob in Ihren neuen Container hochzuladen:

1. Navigieren Sie im Azure-Portal zu dem Container, den Sie im vorherigen Abschnitt erstellt haben.
2. Wählen Sie den Container aus, um eine Liste mit den darin enthaltenen Blobs anzuzeigen. Da es sich in diesem Fall um einen neu erstellten Container handelt, sind darin keine Blobs enthalten.
3. Klicken Sie auf die Schaltfläche **Hochladen**, um ein Blob in den Container hochzuladen.
4. Navigieren Sie in Ihrem lokalen Dateisystem zu einer Datei, die Sie als Blockblob hochladen möchten, und klicken Sie auf **Hochladen**.
     
    ![Screenshot: Hochladen eines Blobs von Ihrem lokalen Laufwerk](media/storage-quickstart-blobs-portal/upload-blob.png)

5. Laden Sie auf diese Weise beliebig viele Blobs hoch. Wie Sie sehen, werden die neuen Blobs nun innerhalb des Containers aufgeführt.

    ![Screenshot: Liste mit den Blobs im Container](media/storage-quickstart-blobs-portal/list-blobs.png)

## <a name="download-a-block-blob"></a>Herunterladen eines Blockblobs

Sie können ein Blockblob herunterladen, um es im Browser anzuzeigen oder in Ihrem lokalen Dateisystem zu speichern. Gehen Sie zum Herunterladen eines Blockblobs wie folgt vor:

1. Navigieren Sie zu der Liste mit den Blobs, die Sie im vorherigen Abschnitt hochgeladen haben. 
2. Wählen Sie das Blob aus, das Sie herunterladen möchten.
3. Klicken Sie mit der rechten Maustaste auf die Schaltfläche **Mehr** (**...**), und klicken Sie auf **Herunterladen**. 

![Screenshot: Herunterladen eines Blobs über das Azure-Portal](media/storage-quickstart-blobs-portal/download-blob.png)

## <a name="clean-up-resources"></a>Bereinigen von Ressourcen

Wenn Sie die Ressourcen entfernen möchten, die Sie im Rahmen dieser Schnellstartanleitung erstellt haben, löschen Sie einfach den Container. Die Blobs im Container werden ebenfalls gelöscht.

So löschen Sie den Container:

1. Navigieren Sie im Azure-Portal zu der Liste mit den Containern in Ihrem Speicherkonto.
2. Wählen Sie den zu löschenden Container aus.
3. Klicken Sie mit der rechten Maustaste auf die Schaltfläche **Mehr** (**...**), und klicken Sie auf **Löschen**.
4. Bestätigen Sie, dass Sie den Container löschen möchten.

    ![Screenshot: Löschen eines Containers über das Azure-Portal](media/storage-quickstart-blobs-portal/delete-container.png)   

## <a name="next-steps"></a>Nächste Schritte

In diesem Schnellstart haben Sie gelernt, wie Sie mit .NET Dateien zwischen einem lokalen Datenträger und Azure Blob Storage übertragen. Weitere Informationen zum Arbeiten mit Blob Storage finden Sie in der exemplarischen Vorgehensweise zu Blob Storage.

> [!div class="nextstepaction"]
> [Gewusst wie: Blob Storage-Vorgänge](storage-dotnet-how-to-use-blobs.md)

