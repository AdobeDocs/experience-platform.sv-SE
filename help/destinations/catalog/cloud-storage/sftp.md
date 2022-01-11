---
keywords: SFTP;sftp
title: SFTP-anslutning
description: Skapa en utgående liveanslutning till SFTP-servern för att regelbundet exportera avgränsade datafiler från Adobe Experience Platform.
exl-id: 27abfc38-ec19-4321-b743-169370d585a0
source-git-commit: bf46f4e6549fcbd975a9f0a6034040ed2e9b34e6
workflow-type: tm+mt
source-wordcount: '306'
ht-degree: 0%

---

# SFTP-anslutning

## Översikt {#overview}

Skapa en utgående liveanslutning till SFTP-servern för att regelbundet exportera avgränsade datafiler från Adobe Experience Platform.

>[!IMPORTANT]
>
> Adobe stöder dataexport till SFTP-servrar, men de rekommenderade molnlagringsplatserna för dataexport är [!DNL Amazon S3] och [!DNL Azure Blob].

## Exporttyp {#export-type}

**Profilbaserad** - du exporterar alla medlemmar i ett segment tillsammans med de önskade schemafälten (till exempel: e-postadress, telefonnummer, efternamn), som du väljer på skärmen Välj attribut på [arbetsflöde för målaktivering](../../ui/activate-batch-profile-destinations.md).

![Profilbaserad SFTP-exporttyp](../../assets/catalog/cloud-storage/sftp/catalog.png)

## Anslut till målet {#connect}

Om du vill ansluta till det här målet följer du stegen som beskrivs i [självstudiekurs om destinationskonfiguration](../../ui/connect-destination.md).

### Anslutningsparametrar {#parameters}

>[!CONTEXTUALHELP]
>id="platform_destinations_connect_sftp_rsa"
>title="RSA offentlig nyckel"
>abstract="Du kan också bifoga den RSA-formaterade offentliga nyckeln för att lägga till kryptering till de exporterade filerna. Den offentliga nyckeln måste skrivas som en Base64-kodad sträng."
>text="Learn more in documentation"

while [konfigurera](../../ui/connect-destination.md) Om du vill ange destinationen måste du ange följande information:

* **Värd**: Adress till din SFTP-lagringsplats
* **Användarnamn**: Användarnamnet som loggas in på din SFTP-lagringsplats
* **Lösenord**: Lösenordet för att logga in på din SFTP-lagringsplats
* **[!UICONTROL Name]**: Ange ett namn som hjälper dig att identifiera det här målet.
* **[!UICONTROL Description]**: Ange en beskrivning av destinationen.
* **[!UICONTROL Folder path]**: Ange sökvägen till målmappen som ska vara värd för de exporterade filerna.

Du kan också bifoga den RSA-formaterade offentliga nyckeln för att lägga till kryptering till de exporterade filerna. Din offentliga nyckel måste skrivas som en [!DNL Base64] kodad sträng.

## Exporterade data {#exported-data}

För [!DNL SFTP] mål, Platform skapar en `.csv` filen på lagringsplatsen som du angav. Mer information om filerna finns i [Aktivera målgruppsdata för att batchprofilera exportmål](../../ui/activate-batch-profile-destinations.md) i segmentaktiveringssjälvstudiekursen.

## IP-adress tillåtelselista

Se [IP-adress tillåtelselista för molnlagringsmål](ip-address-allow-list.md) om du behöver lägga till IP-adresser för Adobe i ett tillåtelselista.
