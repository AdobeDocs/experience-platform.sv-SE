---
title: Merkury Enterprise Identity Resolution Source Overview
description: Lär dig hur du ansluter Merkury Enterprise Identity Resolution till Adobe Experience Platform via användargränssnittet.
badge: Beta
hide: true
hidefromtoc: true
source-git-commit: bf6a3422d9af6eaa4f3f4a8a573dc587b3cfdbd5
workflow-type: tm+mt
source-wordcount: '498'
ht-degree: 0%

---

# [!DNL Merkury Enterprise Identity Resolution]

>[!NOTE]
>
>The [!DNL Merkury Enterprise Identity Resolution] källan är i betaversion. Läs [källöversikt](../../home.md#terms-and-conditions) om du vill ha mer information om hur du använder betamärkta källor.

Adobe Experience Platform har stöd för inmatning av data från ett datapartnerprogram. Stöd för datapartners innefattar [!DNL Merkury Enterprise Identity Resolution].

Du kan använda [!DNL Merkury] av [!DNL Merkle] för att identifiera fler digitala besökare - även utan att använda cookies - och leverera relevanta och personaliserade upplevelser som era kunder behöver.

Du kan använda **person-ID** som en del av [!DNL Merkury] för att kombinera allt som organisationen känner till om en individ i en enda heltäckande profil. Dessa uppgifter kan vara:

- digitala beteenden
- köpinställningar
- Identifiera information som namn, e-postadress, fysisk adress eller enhets-ID.

Du kan formatera inkapslade data som XDM (Experience Data Model) JSON, XDM Parquet eller avgränsat. Varje steg i processen är integrerat i källorna

![En illustration av databearbetningsarbetsflödet för Merkury-källan.](../../images/tutorials/create/merkury-enterprise-identity-resolution-assets/architecture.png)

## IP-adress tillåtelselista

En lista med IP-adresser måste läggas till tillåtelselista innan du kan arbeta med källanslutningar. Om du inte lägger till dina regionspecifika IP-adresser i tillåtelselista kan det leda till fel eller sämre prestanda när du använder källor. Se [IP-adress tillåtelselista](../../ip-address-allow-list.md) sida för mer information.

## Namnbegränsningar för filer och kataloger

Nedan följer en lista över begränsningar som du måste ta hänsyn till när du namnger molnlagringsfilen eller -katalogen.

- Katalog- och filkomponentnamn får inte innehålla fler än 255 tecken.
- Katalog- och filnamn får inte sluta med ett snedstreck (`/`). Den tas bort automatiskt om den anges.
- Följande reserverade URL-tecken måste escape-konverteras: `! ' ( ) ; @ & = + $ , % # [ ]`
- Följande tecken tillåts inte: `" \ / : | < > * ?`.
- Ogiltiga URL-sökvägstecken tillåts inte. Kodpunkter som `\uE000`, som är giltigt i NTFS-filnamn, är inte giltiga Unicode-tecken. Dessutom tillåts inte vissa ASCII- eller Unicode-tecken, som kontrolltecken (0x00 till 0x1F, \u0081 osv.). Information om regler för Unicode-strängar i HTTP/1.1 finns i [RFC 2616, avsnitt 2.2: Grundregler](https://www.ietf.org/rfc/rfc2616.txt) och [RFC 3987](https://www.ietf.org/rfc/rfc3987.txt).
- Följande filnamn tillåts inte: LPT1, LPT2, LPT3, LPT4, LPT5, LPT6, LPT7, LPT8, LPT9, COM1, COM2, COM3, COM4, COM5, COM6, COM7, COM8, COM9, PRN, AUX, NUL, CON, CLOCK$, punkttecken (.) och två punkttecken (. .).

## Förutsättningar

Du måste uppfylla följande krav innan du kan börja använda [!DNL Merkury] källa:

- Du måste fylla i [!DNL Merkury] konfigurera med [!DNL Merkury] team.
- Du måste hämta dina inloggningsuppgifter (åtkomstnyckel, hemlig nyckel och bucket-namn) från din [!DNL Merkury] team. 

>[!NOTE]
>
>En filsökväg som `myBucket/folder/subfolder/subsubfolder/abc.csv` kan leda till att du endast får åtkomst `subsubfolder/abc.csv`. Om du vill komma åt undermappen kan du ange parametern bucket som myBucket och mappenPath som mapp/undermapp för att säkerställa att filsökningen startar vid undermappen i stället för `subsubfolder/abc.csv`.

## Nästa steg

Genom att läsa det här dokumentet har du slutfört nödvändiga inställningar för att kunna hämta data från [!DNL Merkury] konto till Experience Platform. Du kan nu fortsätta med guiden på [koppla [!DNL Merkury] till Experience Platform via användargränssnittet](../../tutorials/ui/create/data-partners/merkury.md).
