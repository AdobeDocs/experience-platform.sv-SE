---
title: Acxiom Prospecting Data Import
description: Lär dig hur du ansluter Acxiom Prospecting Data till Adobe Experience Platform och Adobe Real-time Customer Data Platform med användargränssnittet.
badge: Beta
source-git-commit: 64975ccb6a44730489427cef745f3dbce5bcedf1
workflow-type: tm+mt
source-wordcount: '532'
ht-degree: 0%

---

# [!DNL Acxiom Prospecting Data Import]

>[!NOTE]
>
>The [!DNL Acxiom Prospecting Data Import] källan är i betaversion. Läs [källöversikt](../../home.md#terms-and-conditions) om du vill ha mer information om hur du använder betamärkta källor.

Adobe Experience Platform har stöd för inmatning av data från ett datapartnerprogram. Stöd för data- och identitetspartners innefattar [!DNL Acxiom Prospecting Data Import].

[!DNL Acxiom]Prospecting Data Import for Adobe Real-time Customer Data Platform är en process för att leverera de mest produktiva målgrupperna. [!DNL Acxiom] använder Real-Time CDP förstahandsdata via säker export och kör dessa data via ett prisbelönt hygien- och identitetshanteringssystem. En datafil som kan användas som en undertryckningslista skapas. Den här datafilen matchas sedan mot [!DNL Acxiom Global] databas, som gör det möjligt att anpassa listor med potentiella kunder för import.

Du kan använda [!DNL Acxiom] källa för att hämta och mappa svar från [!DNL Acxiom] tjänst för potentiell kund med [!DNL Amazon S3] som en släpppunkt.

## Förutsättningar

För att få åtkomst till din bucket på Experience Platform måste du ange giltiga värden för följande autentiseringsuppgifter:

| Autentiseringsuppgifter | Beskrivning |
| --- | --- |
| [!DNL Acxiom] autentiseringsnyckel | Autentiseringsnyckeln. Du kan hämta det här värdet från [!DNL Acxiom] team. |
| [!DNL Amazon S3] åtkomstnyckel | Åtkomstnyckel-ID för din bucket. Du kan hämta det här värdet från [!DNL Acxiom] team. |
| [!DNL Amazon S3] hemlig nyckel | Det hemliga nyckel-ID:t för din bucket. Du kan hämta det här värdet från [!DNL Acxiom] team. |
| Buckennamn | Det här är din bucket där filer delas. Du kan hämta det här värdet från [!DNL Acxiom] team. |

### Behörigheter

Du måste ha båda **[!UICONTROL View Sources]** och **[!UICONTROL Manage Sources]** behörigheter för ditt konto för att ansluta [!DNL Acxiom Prospecting Data Import] konto till Experience Platform. Kontakta produktadministratören för att få den behörighet som krävs. Mer information finns i [gränssnittsguide för åtkomstkontroll](../../../access-control/abac/ui/permissions.md).

## IP-adress tillåtelselista

En lista med IP-adresser måste läggas till tillåtelselista innan du kan arbeta med källanslutningar. Om du inte lägger till dina regionspecifika IP-adresser i tillåtelselista kan det leda till fel eller sämre prestanda när du använder källor. Se [IP-adress tillåtelselista](../../ip-address-allow-list.md) sida för mer information.

## Namnbegränsningar för filer och kataloger

De begränsningar som anges nedan måste beaktas när du namnger molnlagringsfilen eller -katalogen:

- Katalog- och filkomponentnamn får inte innehålla fler än 255 tecken.
- Katalog- och filnamn får inte sluta med ett snedstreck (`/`). Den tas bort automatiskt om den anges.
- Följande reserverade URL-tecken måste escape-konverteras: `! ' ( ) ; @ & = + $ , % # [ ]`
- Följande tecken tillåts inte: `" \ / : | < > * ?`.
- Ogiltiga URL-sökvägstecken tillåts inte. Kodpunkter som `\uE000`, som är giltigt i NTFS-filnamn, är inte giltiga Unicode-tecken. Dessutom tillåts inte vissa ASCII- eller Unicode-tecken, som kontrolltecken (0x00 till 0x1F, \u0081 osv.). Information om regler för Unicode-strängar i HTTP/1.1 finns i [RFC 2616, avsnitt 2.2: Grundregler](https://www.ietf.org/rfc/rfc2616.txt) och [RFC 3987](https://www.ietf.org/rfc/rfc3987.txt).
- Följande filnamn tillåts inte: LPT1, LPT2, LPT3, LPT4, LPT5, LPT6, LPT7, LPT8, LPT9, COM1, COM2, COM3, COM4, COM5, COM6, COM7, COM8, COM9, PRN, AUX, NUL, CON, CLOCK$, punkttecken (.) och två punkttecken (. .).

## Nästa steg

Genom att läsa det här dokumentet har du slutfört de nödvändiga inställningarna för att kunna hämta data från [!DNL Acxiom] konto till Experience Platform. Du kan nu fortsätta med guiden på [koppla [!DNL Acxiom Prospecting Data Import] till Experience Platform via användargränssnittet](../../tutorials/ui/create/data-partners/acxiom-prospecting-data-import.md).