---
keywords: e-post;E-post;e-postadresser;oraclets svarsmål
title: Oraclena svarssystemanslutning
description: Responsys är ett e-postmarknadsföringsverktyg för företag för flerkanalskampanjer som Oraclet erbjuder för att personalisera interaktioner över e-post, mobiler, displayannonsering och sociala medier.
exl-id: 70f2f601-afee-4315-bf7a-ed2c92397ebe
translation-type: tm+mt
source-git-commit: 29b4eaca06e2f1032584a0b4720490934a6e1fa7
workflow-type: tm+mt
source-wordcount: '570'
ht-degree: 0%

---

# [!DNL Oracle Responsys] anslutning

## Översikt {#overview}

[Responsys ](https://www.oracle.com/cx/marketing/campaign-management/) är ett verktyg för e-postmarknadsföring i storföretag för flerkanalskampanjer som erbjuds av  [!DNL Oracle] att personalisera interaktioner i e-post, mobiler, displayannonsering och sociala medier.

Om du vill skicka segmentdata till [!DNL Oracle Responsys] måste du först [ansluta till målet](#connect-destination) i Adobe Experience Platform och sedan [konfigurera en dataimport](#import-data-into-responsys) från lagringsplatsen till [!DNL Oracle Responsys].

## Exporttyp {#export-type}

**Profilbaserat**  - du exporterar alla medlemmar i ett segment tillsammans med önskade schemafält (till exempel: e-postadress, telefonnummer, efternamn), som du väljer på skärmen Välj attribut i arbetsflödet [ för ](../../ui/activate-destinations.md#select-attributes)målaktivering.

## IP-adress tillåtelselista {#allow-list}

När du konfigurerar e-postmarknadsföringsmål med SFTP-lagring rekommenderar Adobe att du lägger till vissa IP-intervall till tillåtelselista.

Se [IP-adressen tillåtelselista för molnlagringsdestinationer](../cloud-storage/ip-address-allow-list.md) om du behöver lägga till IP-adresser för Adobe i tillåtelselista.

## Anslutningsmål {#connect-destination}

I **[!UICONTROL Connections]** > **[!UICONTROL Destinations]** väljer du [!DNL Oracle Responsys] och sedan **[!UICONTROL Connect destination]**.

![Anslut till svar](../../assets/catalog/email-marketing/oracle-responsys/catalog.png)

I steget **[!UICONTROL Account]** väljer du **[!UICONTROL Existing Account]** och en av dina befintliga anslutningar om du tidigare har konfigurerat en anslutning till molnlagringsmålet. Du kan också välja **[!UICONTROL New Account]** för att konfigurera en ny anslutning. Fyll i autentiseringsuppgifterna för ditt konto och välj **[!UICONTROL Connect to destination]**. För [!DNL Oracle Responsys] kan du välja mellan **[!UICONTROL SFTP with Password]** och **[!UICONTROL SFTP with SSH Key]**.

![Connect Responsys-konto](../../assets/catalog/email-marketing/oracle-responsys/connection-type.png)

Fyll i informationen nedan, beroende på din anslutningstyp, och välj **[!UICONTROL Configure]**.

- För **[!UICONTROL SFTP with Password]**-anslutningar måste du ange [!UICONTROL Domain], [!UICONTROL Port], [!UICONTROL Username] och [!UICONTROL Password].
- För **[!UICONTROL SFTP with SSH Key]**-anslutningar måste du ange [!UICONTROL Domain], [!UICONTROL Port], [!UICONTROL Username] och [!UICONTROL SSH Key].

Du kan även bifoga den RSA-formaterade offentliga nyckeln för att lägga till kryptering med PGP/GPG till dina exporterade filer under **[!UICONTROL Key]**-avsnittet. Din offentliga nyckel måste skrivas som en [!DNL Base64]-kodad sträng.

![Fyll i svarsinformation](../../assets/catalog/email-marketing/oracle-responsys/account-info.png)

I steget **[!UICONTROL Authentication]** ska du fylla i relevant information för destinationen enligt nedan:
- **[!UICONTROL Name]**: Välj ett relevant namn för destinationen.
- **[!UICONTROL Description]**: Ange en beskrivning för destinationen.
- **[!UICONTROL Folder Path]**: Ange sökvägen till lagringsplatsen där Plattform ska placera dina exportdata som CSV-filer eller tabbavgränsade filer.
- **[!UICONTROL File Format]**:  **** CSVor  **TAB_DELIMITED**. Välj vilket filformat som ska exporteras till lagringsplatsen.
- **[!UICONTROL Marketing actions]**: Marknadsföringsåtgärder anger för vilken metod data ska exporteras till målet. Du kan välja bland Adobe-definierade marknadsföringsåtgärder eller skapa en egen marknadsföringsåtgärd. Mer information om marknadsföringsåtgärder finns i [Översikt över dataanvändningsprinciper](../../../data-governance/policies/overview.md).

<!--

Commenting out Amazon S3 bucket part for now until support is clarified

- **[!UICONTROL Bucket name]**: Your Amazon S3 bucket, where Platform will deposit the data export. Your input must be between 3 and 63 characters long. Must begin and end with a letter or number. Must contain only lowercase letters, numbers, or hyphens ( - ). Must not be formatted as an IP address (for example, 192.100.1.1).

-->

![Grundläggande information om svar](../../assets/catalog/email-marketing/oracle-responsys/basic-information.png)

Klicka på **[!UICONTROL Create destination]** när du har fyllt i fälten ovan. Målet är nu anslutet och du kan [aktivera segment](../../ui/activate-destinations.md) till målet.

## Aktivera segment {#activate-segments}

Mer information om arbetsflödet för segmentaktivering finns i [Aktivera profiler och segment till ett mål](../../ui/activate-destinations.md).

## Målattribut {#destination-attributes}

När du [aktiverar segment](../../ui/activate-destinations.md) till målet [!DNL Oracle Responsys] rekommenderar Adobe att du väljer en unik identifierare i ditt [unionsschema](../../../profile/home.md#profile-fragments-and-union-schemas). Välj den unika identifieraren och eventuella andra XDM-fält som du vill exportera till målet. Mer information finns i [Välja vilka schemafält som ska användas som målattribut i de exporterade filerna](./overview.md#destination-attributes).

## Exporterade data {#exported-data}

För [!DNL Oracle Responsys]-mål skapar Platform en tabbavgränsad `.txt`- eller `.csv`-fil på den angivna lagringsplatsen. Mer information om filerna finns i [E-postmarknadsföringsmål och molnlagringsmål](../../ui/activate-destinations.md#esp-and-cloud-storage) i självstudiekursen om segmentaktivering.

## Konfigurera dataimport till [!DNL Oracle Responsys] {#import-data-into-responsys}

När du har anslutit [!DNL Platform] till din SFTP-lagring måste du konfigurera dataimporten från din lagringsplats till [!DNL Oracle Responsys]. Mer information om hur du gör detta finns i [Importera kontakter eller konton](https://docs.oracle.com/cloud/latest/marketingcs_gs/OMCEA/Connect_WizardUpload.htm) i [!DNL Oracle Responsys Help Center].
