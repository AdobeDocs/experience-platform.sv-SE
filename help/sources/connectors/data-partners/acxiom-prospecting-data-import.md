---
title: Acxiom Prospecting Data Import
description: Lär dig hur du ansluter Acxiom Prospecting Data till Adobe Experience Platform och Adobe Real-Time Customer Data Platform med användargränssnittet.
exl-id: 6df674d9-c14b-42ea-a287-5377484e567d
source-git-commit: e402a58f51de49b26f9d279cebf551ec11e4698f
workflow-type: tm+mt
source-wordcount: '540'
ht-degree: 0%

---

# [!DNL Acxiom Prospecting Data Import]

Adobe Experience Platform har stöd för inmatning av data från ett datapartnerprogram. Stöd för data- och identitetspartners omfattar [!DNL Acxiom Prospecting Data Import].

[!DNL Acxiom]s Prospecting Data Import för Adobe Real-Time Customer Data Platform är en process för att leverera de mest produktiva målgrupperna för potentiella kunder. [!DNL Acxiom] tar Real-Time CDP egna data via en säker export och kör dessa data via ett prisbelönt hygien- och identitetsupplösningssystem. En datafil som kan användas som en undertryckningslista skapas. Den här datafilen matchas sedan mot databasen [!DNL Acxiom Global], vilket gör att listan över potentiella kunder kan anpassas för import.

Du kan använda källan [!DNL Acxiom] för att hämta och mappa svar från tjänsten [!DNL Acxiom] för potentiell kund med [!DNL Amazon S3] som släpppunkt.

![acxiom-prospekting-workflow](../../images/tutorials/create/acxiom-prospect-suppression-data-sourcing/acxiom-prospecting.png)

Läs dokumentet nedan om du vill ha information om hur du kan konfigurera ditt [!DNL Acxiom Prospecting Data Import]-källkonto.

## Förhandskrav

Om du vill komma åt din bucket på Experience Platform måste du ange giltiga värden för följande autentiseringsuppgifter:

| Autentiseringsuppgifter | Beskrivning |
| --- | --- |
| [!DNL Acxiom] autentiseringsnyckel | Autentiseringsnyckeln. Du kan hämta värdet från [!DNL Acxiom]-teamet. |
| [!DNL Amazon S3] åtkomstnyckel | Åtkomstnyckel-ID för din bucket. Du kan hämta värdet från [!DNL Acxiom]-teamet. |
| [!DNL Amazon S3] hemlig nyckel | Det hemliga nyckel-ID:t för din bucket. Du kan hämta värdet från [!DNL Acxiom]-teamet. |
| Buckennamn | Det här är din bucket där filer delas. Du kan hämta värdet från [!DNL Acxiom]-teamet. |

## IP-adress tillåtelselista

Innan du kan använda källanslutningar måste du lägga till de IP-adresser som krävs för din region på tillåtelselista. Om du inte lägger till de här IP-adresserna kanske källanslutningarna inte fungerar som de ska eller så kan fel uppstå. Detaljerade instruktioner och en lista över IP-adresser som ska tillåtas finns på sidan [IP-adressen tillåtelselista ](../../ip-address-allow-list.md).

### Konfigurera behörigheter i Experience Platform

Du måste ha både behörighet **[!UICONTROL View Sources]** och behörighet **[!UICONTROL Manage Sources]** aktiverat för ditt konto för att kunna ansluta ditt [!DNL Acxiom Prospecting Data Import]-konto till Experience Platform. Kontakta produktadministratören för att få den behörighet som krävs. Mer information finns i [användargränssnittsguiden för åtkomstkontroll](../../../access-control/abac/ui/permissions.md).

## Namnbegränsningar för filer och kataloger

De begränsningar som anges nedan måste beaktas när du namnger molnlagringsfilen eller -katalogen:

- Katalog- och filkomponentnamn får inte innehålla fler än 255 tecken.
- Katalog- och filnamn får inte sluta med ett snedstreck (`/`). Den tas bort automatiskt om den anges.
- Följande reserverade URL-tecken måste ha escape-konverterats: `! ' ( ) ; @ & = + $ , % # [ ]`
- Följande tecken tillåts inte: `" \ / : | < > * ?`.
- Ogiltiga URL-sökvägstecken tillåts inte. Kodpunkter som `\uE000` är inte giltiga Unicode-tecken, men de är giltiga i NTFS-filnamn. Dessutom tillåts inte vissa ASCII- eller Unicode-tecken, som kontrolltecken (0x00 till 0x1F, \u0081 osv.). Information om regler som styr Unicode-strängar i HTTP/1.1 finns i [RFC 2616, Section 2.2: Basic Rules](https://www.ietf.org/rfc/rfc2616.txt) och [RFC 3987](https://www.ietf.org/rfc/rfc3987.txt).
- Följande filnamn tillåts inte: LPT1, LPT2, LPT3, LPT4, LPT5, LPT6, LPT7, LPT8, LPT9, COM1, COM2, COM3, COM4, COM5, COM6, COM7, COM8, COM9, PRN, AUX, NUL, CON, CLOCK$, punkttecken (.) och två punkttecken (. .).

## Nästa steg

Genom att läsa det här dokumentet har du slutfört de nödvändiga inställningarna för att kunna överföra data från ditt [!DNL Acxiom]-konto till Experience Platform. Du kan nu fortsätta med guiden om att [ansluta [!DNL Acxiom Prospecting Data Import] till Experience Platform via användargränssnittet](../../tutorials/ui/create/data-partners/acxiom-prospecting-data-import.md).
