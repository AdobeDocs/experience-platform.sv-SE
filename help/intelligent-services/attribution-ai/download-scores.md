---
keywords: Experience Platform;attribution ai;access scores;popular topics
solution: Experience Platform
title: Åtkomst till poäng i Attribution AI
topic: Accessing scores
translation-type: tm+mt
source-git-commit: 689b4c7a96856e1167ee435a6740fed006136256

---


# Åtkomst till poäng i Attribution AI

>[!IMPORTANT] Kontakta attributionai-support@adobe.com om du vill ha mer information om nedladdning av råpoäng för bulkexport av data.

Åtkomst till poäng för Attribution AI görs via Snowflake. För närvarande måste du skicka e-post till Adobes support på attributionai-support@adobe.com för att kunna konfigurera och ta emot inloggningsuppgifterna till ditt läsarkonto för Snowflake.

När Adobes support har bearbetat din begäran får du en URL för läsarkontot till Snowflake och motsvarande uppgifter nedan:

- Snöflinga URL
- Användarnamn
- Lösenord

>[!NOTE] Läsarkontot används för att fråga data med SQL-klienter, kalkylblad och BI-lösningar som stöder JDBC-anslutning.

När du har dina inloggningsuppgifter och URL-adresser kan du fråga modelltabellerna, antingen i Raw-format, aggregerat efter slutpunktsdatum eller konverteringsdatum.

## Hitta ditt schema i snöflake

Logga in på Snowflake med de angivna inloggningsuppgifterna. Klicka på fliken **Kalkylblad** i den övre vänstra navigeringen och navigera sedan till din databaskatalog i den vänstra panelen.

![Kalkylblad och navigering](./images/download-scores/edited_snowflake_1.png)

Klicka sedan på **Välj schema** i skärmens övre högra hörn. Bekräfta att du har markerat rätt databas i den port som visas. Klicka sedan på listrutan *Schema* och välj ett av scheman i listan. Du kan söka direkt från de poängtabeller som listas under det valda schemat.

![hitta ett schema](./images/download-scores/edited_snowflake_2.png)

## Hämta bakgrundsmusik

Kontakta attributionai-support@adobe.com om du vill ha mer information om nedladdning av råpoäng.

## Ansluta PowerBI till snöflake (valfritt)

Dina Snowflake-autentiseringsuppgifter kan användas för att skapa en anslutning mellan PowerBI Desktop- och Snowflake-databaser.

Skriv först in webbadressen för snöflake i rutan *Server* . Skriv sedan in &quot;XSMALL&quot; under *Lagerställe*. Ange sedan ditt användarnamn och lösenord.

![exempel på POWERBI](./images/download-scores/powerbi-snowflake.png)

När anslutningen har upprättats väljer du din Snowflake-databas och väljer sedan lämpligt schema. Du kan nu läsa in alla tabeller.

När du har valt ditt schema visas tabeller med dina attribueringspoäng.

| Tabell | Beskrivning |
| ----- | ----------- |
| APP_{APP_ID} | Råattribueringspoäng. |
| APP_{APP_ID}_BY_CONV_DATE | Raw-attribueringsmoment sammanställd på konverteringsdatumnivå. |
| APP_{APP_ID}_BY_TP_DATE | Raw-attribueringsmoment aggregerat på kontaktpunktsdatumnivå. |

## Nästa steg

I det här dokumentet beskrivs stegen som krävs för att fråga efter data och komma åt poäng för Attribution AI. Nu kan du fortsätta att söka bland de andra [intelligenta tjänsterna](../home.md) och guiderna som erbjuds.