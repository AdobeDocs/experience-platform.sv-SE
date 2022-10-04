---
keywords: SFTP;sftp
title: SFTP-anslutning
description: Skapa en utgående liveanslutning till SFTP-servern för att regelbundet exportera avgränsade datafiler från Adobe Experience Platform.
exl-id: 27abfc38-ec19-4321-b743-169370d585a0
source-git-commit: 1dd87ce19c3d9f4eb07c49968754ab979b4dee5c
workflow-type: tm+mt
source-wordcount: '656'
ht-degree: 0%

---

# SFTP-anslutning

## Översikt {#overview}

Skapa en utgående liveanslutning till SFTP-servern för att regelbundet exportera avgränsade datafiler från Adobe Experience Platform.

>[!IMPORTANT]
>
> Experience Platform stöder dataexport till SFTP-servrar, men de rekommenderade molnlagringsplatserna för dataexport är [!DNL Amazon S3] och [!DNL Azure Blob].

## Exportera typ och frekvens {#export-type-frequency}

Se tabellen nedan för information om exporttyp och frekvens för destinationen.

| Objekt | Typ | Anteckningar |
---------|----------|---------|
| Exporttyp | **[!UICONTROL Profile-based]** | Du exporterar alla medlemmar i ett segment tillsammans med önskade schemafält (till exempel: e-postadress, telefonnummer, efternamn), som du har valt på skärmen Välj profilattribut i [arbetsflöde för målaktivering](../../ui/activate-batch-profile-destinations.md#select-attributes). |
| Exportfrekvens | **[!UICONTROL Batch]** | Batchdestinationer exporterar filer till efterföljande plattformar i steg om tre, sex, åtta, tolv eller tjugofyra timmar. Läs mer om [gruppfilsbaserade mål](/help/destinations/destination-types.md#file-based). |

{style=&quot;table-layout:auto&quot;}

![Profilbaserad SFTP-exporttyp](../../assets/catalog/cloud-storage/sftp/catalog.png)

## Anslut till målet {#connect}

>[!IMPORTANT]
> 
>Om du vill ansluta till målet behöver du **[!UICONTROL Manage Destinations]** [åtkomstkontrollbehörighet](/help/access-control/home.md#permissions). Läs [åtkomstkontroll - översikt](/help/access-control/ui/overview.md) eller kontakta produktadministratören för att få de behörigheter som krävs.

Om du vill ansluta till det här målet följer du stegen som beskrivs i [självstudiekurs om destinationskonfiguration](../../ui/connect-destination.md). I arbetsflödet för att konfigurera mål fyller du i fälten som listas i de två avsnitten nedan.

### Autentiseringsinformation {#authentication-information}

>[!CONTEXTUALHELP]
>id="platform_destinations_connect_sftp_rsa"
>title="RSA offentlig nyckel"
>abstract="Du kan också bifoga den RSA-formaterade offentliga nyckeln för att lägga till kryptering till de exporterade filerna. Den offentliga nyckeln måste skrivas som en Base64-kodad sträng."

>[!CONTEXTUALHELP]
>id="platform_destinations_connect_sftp_ssh"
>title="Privat SSH-nyckel"
>abstract="Den privata SSH-nyckeln måste vara formaterad som en Base64-kodad sträng och får inte vara lösenordsskyddad."

Om du väljer **[!UICONTROL Basic authentication]** skriv för att ansluta till din SFTP-plats:

![Grundläggande autentisering för SFTP-mål](../../assets/catalog/cloud-storage/sftp/stfp-basic-authentication.png)

* **[!UICONTROL Host]**: Adress till din SFTP-lagringsplats.
* **[!UICONTROL Username]**: Användarnamn för att logga in på din SFTP-lagringsplats.
* **[!UICONTROL Password]**: Lösenordet för att logga in på din SFTP-lagringsplats.
* **[!UICONTROL Encryption key]**: Du kan också bifoga den RSA-formaterade offentliga nyckeln för att lägga till kryptering till de exporterade filerna. Din offentliga nyckel måste skrivas som en [!DNL Base64-encoded] sträng. Visa ett exempel på en korrekt formaterad, base64-kodad nyckel i dokumentationslänken nedan. Mittdelen förkortas av utrymmesskäl.

![Bild som visar ett exempel på en korrekt formaterad och base64-krypterad PGP-nyckel i användargränssnittet](../../assets/catalog/cloud-storage/sftp/pgp-key.png)


Om du väljer **[!UICONTROL SFTP with SSH key]** autentiseringstyp för att ansluta till din SFTP-plats:

![SSH-nyckelautentisering för SFTP-mål](../../assets/catalog/cloud-storage/sftp/sftp-ssh-key-authentication.png)

* **[!UICONTROL Domain]**: Fyll i IP-adressen eller domännamnet för ditt SFTP-konto
* **[!UICONTROL Port]**: Den port som används av SFTP-lagringsplatsen;
* **[!UICONTROL Username]**: Användarnamn för att logga in på din SFTP-lagringsplats.
* **[!UICONTROL SSH Key]**: Den privata SSH-nyckeln som används för att logga in på din SFTP-lagringsplats. Den privata nyckeln måste vara formaterad som en Base64-kodad sträng och får inte vara lösenordsskyddad.
* **[!UICONTROL Encryption key]**: Du kan också bifoga den RSA-formaterade offentliga nyckeln för att lägga till kryptering till de exporterade filerna. Din offentliga nyckel måste skrivas som en [!DNL Base64] kodad sträng.
   * Exempel: `----BEGIN PGP PUBLIC KEY BLOCK---- {Base64-encoded string} ----END PGP PUBLIC KEY BLOCK----`. Nedan visas ett exempel på en korrekt formaterad PGP-nyckel, med den mellersta delen förkortad.

      ![PGP-nyckel](../../assets/catalog/cloud-storage/sftp/pgp-key.png)

### Destinationsinformation {#destination-details}

När du har upprättat autentiseringsanslutningen till SFTP-platsen anger du följande information för målet:

![Tillgänglig målinformation för SFTP-mål](../../assets/catalog/cloud-storage/sftp/sftp-destination-details.png)

* **[!UICONTROL Name]**: Ange ett namn som hjälper dig att identifiera destinationen i användargränssnittet i Experience Platform.
* **[!UICONTROL Description]**: Ange en beskrivning av destinationen.
* **[!UICONTROL Folder path]**: Ange sökvägen till mappen på SFTP-platsen dit filerna ska exporteras.

## Aktivera segment till den här destinationen {#activate}

>[!IMPORTANT]
> 
>Om du vill aktivera data måste du ha **[!UICONTROL Manage Destinations]**, **[!UICONTROL Activate Destinations]**, **[!UICONTROL View Profiles]** och **[!UICONTROL View Segments]** [behörigheter för åtkomstkontroll](/help/access-control/home.md#permissions). Läs [åtkomstkontroll - översikt](/help/access-control/ui/overview.md) eller kontakta produktadministratören för att få de behörigheter som krävs.

Se [Aktivera målgruppsdata för att batchprofilera exportmål](../../ui/activate-batch-profile-destinations.md) om du vill ha instruktioner om hur du aktiverar målgruppssegment till det här målet.

## Exporterade data {#exported-data}

För [!DNL SFTP] mål, Platform skapar en `.csv` filen på lagringsplatsen som du angav. Mer information om filerna finns i [Aktivera målgruppsdata för att batchprofilera exportmål](../../ui/activate-batch-profile-destinations.md) i segmentaktiveringssjälvstudiekursen.

## IP-adress tillåtelselista

Se [IP-adress tillåtelselista för molnlagringsmål](ip-address-allow-list.md) om du behöver lägga till IP-adresser för Adobe i ett tillåtelselista.
