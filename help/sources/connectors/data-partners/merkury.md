---
title: Merkury Enterprise Identity Resolution Source - översikt
description: Lär dig hur du ansluter Merkury Enterprise Identity Resolution till Adobe Experience Platform via användargränssnittet.
exl-id: c5eaa561-d620-4c82-bce1-972d0a422c3f
source-git-commit: e402a58f51de49b26f9d279cebf551ec11e4698f
workflow-type: tm+mt
source-wordcount: '486'
ht-degree: 0%

---

# [!DNL Merkury Enterprise Identity Resolution]

Adobe Experience Platform har stöd för inmatning av data från ett datapartnerprogram. Stöd för datapartners är [!DNL Merkury Enterprise Identity Resolution].

Du kan använda [!DNL Merkury] av [!DNL Merkle] för att identifiera fler digitala besökare - även utan att använda cookies - och leverera relevanta och personaliserade upplevelser som kunderna behöver.

Du kan använda **person-ID** som en del av [!DNL Merkury]-källan för att kombinera allt som din organisation känner till om en individ till en enda heltäckande profil. Dessa uppgifter kan vara:

- Digitala beteenden
- Köpinställningar
- Identifiera information som namn, e-postadress, fysisk adress eller enhets-ID.

Du kan formatera inkapslade data som XDM (Experience Data Model) JSON, XDM Parquet eller avgränsat. Varje steg i processen är integrerat i källorna

![En illustration av arbetsflödet för databearbetning för Merkury-källan.](../../images/tutorials/create/merkury-enterprise-identity-resolution-assets/architecture.png)

## IP-adress tillåtelselista

Innan du kan använda källanslutningar måste du lägga till de IP-adresser som krävs för din region på tillåtelselista. Om du inte lägger till de här IP-adresserna kanske källanslutningarna inte fungerar som de ska eller så kan fel uppstå. Detaljerade instruktioner och en lista över IP-adresser som ska tillåtas finns på sidan [IP-adressen tillåtelselista ](../../ip-address-allow-list.md).

## Namnbegränsningar för filer och kataloger

Nedan följer en lista över begränsningar som du måste ta hänsyn till när du namnger molnlagringsfilen eller -katalogen.

- Katalog- och filkomponentnamn får inte innehålla fler än 255 tecken.
- Katalog- och filnamn får inte sluta med ett snedstreck (`/`). Den tas bort automatiskt om den anges.
- Följande reserverade URL-tecken måste ha escape-konverterats: `! ' ( ) ; @ & = + $ , % # [ ]`
- Följande tecken tillåts inte: `" \ / : | < > * ?`.
- Ogiltiga URL-sökvägstecken tillåts inte. Kodpunkter som `\uE000` är inte giltiga Unicode-tecken, men de är giltiga i NTFS-filnamn. Dessutom tillåts inte vissa ASCII- eller Unicode-tecken, som kontrolltecken (0x00 till 0x1F, \u0081 osv.). Information om regler som styr Unicode-strängar i HTTP/1.1 finns i [RFC 2616, Section 2.2: Basic Rules](https://www.ietf.org/rfc/rfc2616.txt) och [RFC 3987](https://www.ietf.org/rfc/rfc3987.txt).
- Följande filnamn tillåts inte: LPT1, LPT2, LPT3, LPT4, LPT5, LPT6, LPT7, LPT8, LPT9, COM1, COM2, COM3, COM4, COM5, COM6, COM7, COM8, COM9, PRN, AUX, NUL, CON, CLOCK$, punkttecken (.) och två punkttecken (. .).

## Förhandskrav

Du måste uppfylla följande krav innan du kan börja använda källan [!DNL Merkury]:

- Du måste slutföra konfigurationen av [!DNL Merkury] med ditt [!DNL Merkury]-team.
- Du måste hämta dina autentiseringsuppgifter (åtkomstnyckel, hemlig nyckel och bucket-namn) från ditt [!DNL Merkury]-team. 

>[!NOTE]
>
>En filsökväg som `myBucket/folder/subfolder/subsubfolder/abc.csv` kan leda till att du bara får åtkomst till `subsubfolder/abc.csv`. Om du vill komma åt undermappen kan du ange parametern bucket som myBucket och mappenPath som mapp/undermapp för att säkerställa att filsökningen startar vid undermappen i stället för `subsubfolder/abc.csv`.

## Nästa steg

Genom att läsa det här dokumentet har du slutfört nödvändiga inställningar för att kunna överföra data från ditt [!DNL Merkury]-konto till Experience Platform. Du kan nu fortsätta med guiden om att [ansluta [!DNL Merkury] till Experience Platform via användargränssnittet](../../tutorials/ui/create/data-partners/merkury.md).
