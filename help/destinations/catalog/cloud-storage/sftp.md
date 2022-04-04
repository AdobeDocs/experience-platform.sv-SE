---
keywords: SFTP;sftp
title: SFTP-anslutning
description: Skapa en utgående liveanslutning till SFTP-servern för att regelbundet exportera avgränsade datafiler från Adobe Experience Platform.
exl-id: 27abfc38-ec19-4321-b743-169370d585a0
source-git-commit: dbefe3e9b193ccef06b6a81919233501b6e938be
workflow-type: tm+mt
source-wordcount: '533'
ht-degree: 0%

---

# SFTP-anslutning

## Översikt {#overview}

Skapa en utgående liveanslutning till SFTP-servern för att regelbundet exportera avgränsade datafiler från Adobe Experience Platform.

>[!IMPORTANT]
>
> Adobe stöder dataexport till SFTP-servrar, men de rekommenderade molnlagringsplatserna för dataexport är [!DNL Amazon S3] och [!DNL Azure Blob].

## Exportera typ och frekvens {#export-type-frequency}

Se tabellen nedan för information om exporttyp och frekvens för destinationen.

| Objekt | Typ | Anteckningar |
---------|----------|---------|
| Exporttyp | **[!UICONTROL Profile-based]** | Du exporterar alla medlemmar i ett segment tillsammans med önskade schemafält (till exempel: e-postadress, telefonnummer, efternamn), som du har valt på skärmen Välj profilattribut i [arbetsflöde för målaktivering](../../ui/activate-batch-profile-destinations.md#select-attributes). |
| Exportfrekvens | **[!UICONTROL Batch]** | Batchdestinationer exporterar filer till efterföljande plattformar i steg om tre, sex, åtta, tolv eller tjugofyra timmar. Läs mer om [gruppfilsbaserade mål](/help/destinations/destination-types.md#file-based). |

{style=&quot;table-layout:auto&quot;}

![Profilbaserad SFTP-exporttyp](../../assets/catalog/cloud-storage/sftp/catalog.png)

## Anslut till målet {#connect}

Om du vill ansluta till det här målet följer du stegen som beskrivs i [självstudiekurs om destinationskonfiguration](../../ui/connect-destination.md).

### Anslutningsparametrar {#parameters}

>[!CONTEXTUALHELP]
>id="platform_destinations_connect_sftp_rsa"
>title="RSA offentlig nyckel"
>abstract="Du kan också bifoga den RSA-formaterade offentliga nyckeln för att lägga till kryptering till de exporterade filerna. Den offentliga nyckeln måste skrivas som en Base64-kodad sträng."

>[!CONTEXTUALHELP]
>id="platform_destinations_connect_sftp_ssh"
>title="SSH-nyckel"
>abstract="SSH-nyckeln kräver en Base64-sträng."

När [koppla](../../ui/connect-destination.md) till detta mål måste du ange följande information:

#### Autentiseringsinformation {#authentication-information}

Om du väljer **[!UICONTROL Basic authentication]** skriv för att ansluta till din SFTP-plats:

![Grundläggande autentisering för SFTP-mål](../..//assets/catalog/cloud-storage/sftp/stfp-basic-authentication.png)

* **[!UICONTROL Host]**: Adress till din SFTP-lagringsplats.
* **[!UICONTROL Username]**: Användarnamn för att logga in på din SFTP-lagringsplats.
* **[!UICONTROL Password]**: Lösenordet för att logga in på din SFTP-lagringsplats.
* **[!UICONTROL Encryption key]**: Du kan också bifoga den RSA-formaterade offentliga nyckeln för att lägga till kryptering till de exporterade filerna. Din offentliga nyckel måste skrivas som en [!DNL Base64] kodad sträng.
   * Exempel: `----BEGIN PGP PUBLIC KEY BLOCK---- {Base64-encoded string} ----END PGP PUBLIC KEY BLOCK----`. Nedan visas ett exempel på en korrekt formaterad PGP-nyckel, med den mellersta delen förkortad.

      ![PGP-nyckel](../..//assets/catalog/cloud-storage/sftp/pgp-key.png)


Om du väljer **[!UICONTROL SFTP with SSH key]** autentiseringstyp för att ansluta till din SFTP-plats:

![SSH-nyckelautentisering för SFTP-mål](../../assets/catalog/cloud-storage/sftp/sftp-ssh-key-authentication.png)

* **[!UICONTROL Domain]**: Fyll i IP-adressen eller domännamnet för ditt SFTP-konto
* **[!UICONTROL Port]**: Den port som används av SFTP-lagringsplatsen;
* **[!UICONTROL Username]**: Användarnamn för att logga in på din SFTP-lagringsplats.
* **[!UICONTROL SSH Key]**: SSH-nyckeln för att logga in på din SFTP-lagringsplats.
* **[!UICONTROL Encryption key]**: Du kan också bifoga den RSA-formaterade offentliga nyckeln för att lägga till kryptering till de exporterade filerna. Din offentliga nyckel måste skrivas som en [!DNL Base64] kodad sträng.
   * Exempel: `----BEGIN PGP PUBLIC KEY BLOCK---- {Base64-encoded string} ----END PGP PUBLIC KEY BLOCK----`. Nedan visas ett exempel på en korrekt formaterad PGP-nyckel, med den mellersta delen förkortad.

      ![PGP-nyckel](../..//assets/catalog/cloud-storage/sftp/pgp-key.png)

#### Destinationsinformation {#destination-details}

När du har upprättat autentiseringsanslutningen till SFTP-platsen anger du följande information för målet:

![Tillgänglig målinformation för SFTP-mål](../../assets/catalog/cloud-storage/sftp/sftp-destination-details.png)

* **[!UICONTROL Name]**: Ange ett namn som hjälper dig att identifiera destinationen i användargränssnittet i Experience Platform.
* **[!UICONTROL Description]**: Ange en beskrivning av destinationen.
* **[!UICONTROL Folder path]**: Ange sökvägen till mappen på SFTP-platsen dit filerna ska exporteras.

## Exporterade data {#exported-data}

För [!DNL SFTP] mål, Platform skapar en `.csv` filen på lagringsplatsen som du angav. Mer information om filerna finns i [Aktivera målgruppsdata för att batchprofilera exportmål](../../ui/activate-batch-profile-destinations.md) i segmentaktiveringssjälvstudiekursen.

## IP-adress tillåtelselista

Se [IP-adress tillåtelselista för molnlagringsmål](ip-address-allow-list.md) om du behöver lägga till IP-adresser för Adobe i ett tillåtelselista.
