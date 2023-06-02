---
title: SFTP-anslutning
description: Skapa en utgående liveanslutning till SFTP-servern för att regelbundet exportera avgränsade datafiler från Adobe Experience Platform.
exl-id: 27abfc38-ec19-4321-b743-169370d585a0
source-git-commit: d30cd0729aa13044d8e7009fde5cae846e7a2864
workflow-type: tm+mt
source-wordcount: '851'
ht-degree: 0%

---

# SFTP-anslutning

## Destinationsändringslogg {#changelog}

>[!IMPORTANT]
>
>Med betaversionen av exportdataset och de förbättrade funktionerna för filexport kan du nu se två [!DNL SFTP] i målkatalogen.
>* Om du redan exporterar filer till **[!UICONTROL SFTP]** mål: Skapa nya dataflöden för nya **[!UICONTROL SFTP beta]** mål.
>* Om du ännu inte har skapat några dataflöden till **[!UICONTROL SFTP]** mål, använd den nya **[!UICONTROL SFTP beta]** exportera filer till **[!UICONTROL SFTP]**.


![Bild av de två SFTP-målkorten i en sida vid sida-vy.](../../assets/catalog/cloud-storage/sftp/two-sftp-destination-cards.png)

Förbättringar i nya [!DNL SFTP] omfattar följande destinationskort:

* [Stöd för dataexport](/help/destinations/ui/export-datasets.md).
* Ytterligare [filnamnsalternativ](/help/destinations/ui/activate-batch-profile-destinations.md#scheduling).
* Möjlighet att ange anpassade filhuvuden i de exporterade filerna via [förbättrat mappningssteg](/help/destinations/ui/activate-batch-profile-destinations.md#mapping).
* [Möjlighet att anpassa formateringen i exporterade CSV-datafiler](/help/destinations/ui/batch-destinations-file-formatting-options.md).

## Översikt {#overview}

Skapa en utgående liveanslutning till SFTP-servern för att regelbundet exportera avgränsade datafiler från Adobe Experience Platform.

>[!IMPORTANT]
>
> Experience Platform stöder dataexport till SFTP-servrar, men de rekommenderade molnlagringsplatserna för dataexport är [!DNL Amazon S3] och [!DNL SFTP].

## Exportera typ och frekvens {#export-type-frequency}

Se tabellen nedan för information om exporttyp och frekvens för destinationen.

| Objekt | Typ | Anteckningar |
---------|----------|---------|
| Exporttyp | **[!UICONTROL Profile-based]** | Du exporterar alla medlemmar i ett segment tillsammans med önskade schemafält (till exempel: e-postadress, telefonnummer, efternamn), som du har valt på skärmen Välj profilattribut i [arbetsflöde för målaktivering](../../ui/activate-batch-profile-destinations.md#select-attributes). |
| Exportfrekvens | **[!UICONTROL Batch]** | Batchdestinationer exporterar filer till efterföljande plattformar i steg om tre, sex, åtta, tolv eller tjugofyra timmar. Läs mer om [gruppfilsbaserade mål](/help/destinations/destination-types.md#file-based). |

{style="table-layout:auto"}

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
>abstract="Du kan också bifoga den RSA-formaterade offentliga nyckeln för att lägga till kryptering till de exporterade filerna. Visa ett exempel på en korrekt formaterad nyckel i dokumentationslänken nedan."

>[!CONTEXTUALHELP]
>id="platform_destinations_connect_sftp_ssh"
>title="Privat SSH-nyckel"
>abstract="Den privata SSH-nyckeln måste vara formaterad som en Base64-kodad sträng och får inte vara lösenordsskyddad."

Om du väljer **[!UICONTROL Basic authentication]** skriv för att ansluta till din SFTP-plats:

![Grundläggande autentisering för SFTP-mål](../../assets/catalog/cloud-storage/sftp/stfp-basic-authentication.png)

* **[!UICONTROL Host]**: Adress till din SFTP-lagringsplats.
* **[!UICONTROL Username]**: Användarnamn för att logga in på din SFTP-lagringsplats.
* **[!UICONTROL Password]**: Lösenordet för att logga in på din SFTP-lagringsplats.
* **[!UICONTROL Encryption key]**: Du kan också bifoga den RSA-formaterade offentliga nyckeln för att lägga till kryptering till de exporterade filerna. Visa ett exempel på en korrekt formaterad krypteringsnyckel i bilden nedan.

   ![Bild som visar ett exempel på en korrekt formaterad PGP-nyckel i användargränssnittet](../../assets/catalog/cloud-storage/sftp/pgp-key.png)


Om du väljer **[!UICONTROL SFTP with SSH key]** autentiseringstyp för att ansluta till din SFTP-plats:

![SSH-nyckelautentisering för SFTP-mål](../../assets/catalog/cloud-storage/sftp/sftp-ssh-key-authentication.png)

* **[!UICONTROL Domain]**: Fyll i IP-adressen eller domännamnet för ditt SFTP-konto
* **[!UICONTROL Port]**: Den port som används av SFTP-lagringsplatsen;
* **[!UICONTROL Username]**: Användarnamn för att logga in på din SFTP-lagringsplats.
* **[!UICONTROL SSH Key]**: Den privata SSH-nyckeln som används för att logga in på din SFTP-lagringsplats. Den privata nyckeln måste vara formaterad som en Base64-kodad sträng och får inte vara lösenordsskyddad.
* **[!UICONTROL Encryption key]**: Du kan också bifoga den RSA-formaterade offentliga nyckeln för att lägga till kryptering till de exporterade filerna. Visa ett exempel på en korrekt formaterad krypteringsnyckel i bilden nedan.

   ![Bild som visar ett exempel på en korrekt formaterad PGP-nyckel i användargränssnittet](../../assets/catalog/cloud-storage/sftp/pgp-key.png)

### Destinationsinformation {#destination-details}

När du har upprättat autentiseringsanslutningen till SFTP-platsen anger du följande information för målet:

![Tillgänglig målinformation för SFTP-mål](../../assets/catalog/cloud-storage/sftp/sftp-destination-details.png)

* **[!UICONTROL Name]**: Ange ett namn som hjälper dig att identifiera destinationen i användargränssnittet i Experience Platform.
* **[!UICONTROL Description]**: Ange en beskrivning av destinationen.
* **[!UICONTROL Folder path]**: Ange sökvägen till mappen på SFTP-platsen dit filerna ska exporteras.
* **[!UICONTROL File type]**: väljer du vilket format Experience Platform ska använda för de exporterade filerna. Det här alternativet är bara tillgängligt för **[!UICONTROL SFTP beta]** mål. När du väljer [!UICONTROL CSV] kan du också [konfigurera filformateringsalternativ](../../ui/batch-destinations-file-formatting-options.md).
* **[!UICONTROL Compression format]**: välj den komprimeringstyp som Experience Platform ska använda för de exporterade filerna. Det här alternativet är bara tillgängligt för **[!UICONTROL SFTP beta]** mål.
* **[!UICONTROL Include manifest file]**: aktivera det här alternativet om du vill att exporten ska innehålla en manifestfil för JSON som innehåller information om exportplats, exportstorlek och mycket annat. Det här alternativet är bara tillgängligt för **[!UICONTROL SFTP beta]** mål.

## Aktivera segment till den här destinationen {#activate}

>[!IMPORTANT]
> 
>Om du vill aktivera data måste du ha **[!UICONTROL Manage Destinations]**, **[!UICONTROL Activate Destinations]**, **[!UICONTROL View Profiles]** och **[!UICONTROL View Segments]** [behörigheter för åtkomstkontroll](/help/access-control/home.md#permissions). Läs [åtkomstkontroll - översikt](/help/access-control/ui/overview.md) eller kontakta produktadministratören för att få de behörigheter som krävs.

Se [Aktivera målgruppsdata för att batchprofilera exportmål](../../ui/activate-batch-profile-destinations.md) om du vill ha instruktioner om hur du aktiverar målgruppssegment till det här målet.

## (Beta) Exportera datauppsättningar {#export-datasets}

Detta mål stöder datauppsättningsexporter. Fullständig information om hur du ställer in datauppsättningsexporter finns i [självstudiekurs om hur du exporterar datauppsättningar](/help/destinations/ui/export-datasets.md).

## Exporterade data {#exported-data}

För [!DNL SFTP] mål, Platform skapar en `.csv` filen på lagringsplatsen som du angav. Mer information om filerna finns i [Aktivera målgruppsdata för att batchprofilera exportmål](../../ui/activate-batch-profile-destinations.md) i segmentaktiveringssjälvstudiekursen.

## IP-adress tillåtelselista

Se [IP-adress tillåtelselista för SFTP-mål](ip-address-allow-list.md) om du behöver lägga till IP-adresser för Adobe i ett tillåtelselista.
