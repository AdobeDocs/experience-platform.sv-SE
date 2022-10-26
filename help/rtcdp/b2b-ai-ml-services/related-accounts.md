---
title: Relaterade konton i Real-Time CDP B2B Edition
type: Documentation
description: En översikt och mer information om kontofunktionen i Experience Platform Real-Time CDP B2B.
exl-id: 37fd2cdb-87c0-4e5e-9599-ad4f397f7c28
source-git-commit: 14e3eff3ea2469023823a35ee1112568f5b5f4f7
workflow-type: tm+mt
source-wordcount: '386'
ht-degree: 4%

---

# Relaterade konton i Real-Time CDP B2B Edition

## Översikt {#overview}

B2B-företag har ofta sin kundinformation lagrad i flera system, där alla bara innehåller partiella eller till och med motstridiga data för samma verkliga affärsenhet. Detta skapar en stor utmaning i att få en korrekt bild av kunderna och minskar därmed effektiviteten och effektiviteten i B2B-marknadsförings- och säljsatsningarna.

| ID | Namn | Webbplats | Bransch | Läge | Telefon | Har öppen affärsmöjlighet med belopp > `$1 million` |
|---|---|---|---|---|---|---|
| 1 | Acme | acme.com | Mjukvara | CA | (408)536-6000 |  |
| 2 | Acme | acm.com | Mjukvara | CA | 4085366000 | x |
| 3 | Acme Inc |  |  | CA | (408)5366000 |  |
| 4 | Acme Consulting Service | `http://www.acme.com/consulting` | Technology Consulting | NY | (212)471-0904 | x |
| 5 | Acme IT |  |  | CA |  |  |

{style=&quot;table-layout:auto&quot;}

Med relaterade konton [!DNL Real-Time CDP B2B] visar nu en lista över konton som liknar det konto du bläddrar i.

![Skärm som visar relaterade konton i användargränssnittet för Experience Platform.](/help/rtcdp/b2b-ai-ml-services/assets/related-accounts-in-ui.png)

Använd den här funktionen om du vill visa relaterade kontoprofiler för en kontoprofil i användargränssnittet för Experience Platform och sedan inkludera de relaterade kontona i segmentdefinitionerna för att bredda din räckvidd eller tillämpa bredare kriterier i dina segment.

## Så fungerar det {#how-it-works}

Maskininlärningsjobb som körs dagligen använder en hierarkisk algoritm för att gruppera liknande kontoprofiler i grupper baserat på tre faktorer:

* Länk till överordnat konto
* Webbdomän
* Kontonamn

Efter ett slutfört bearbetningsjobb taggas varje medlem i kontoprofilgruppen med listan Relaterade konton. Du kan visa listan i **Relaterade konton** på sidan Kontoprofil och använd de relaterade kontona i segmentdefinitioner.

Mer information om [profilanrikningsrelaterade kontojobb](/help/dataflows/ui/b2b/monitor-profile-enrichment.md).

## Visa relaterade konton {#how-to-view}

Du kan visa relaterade konton för ett konto som du surfar på i användargränssnittet för Experience Platform.

Mer information om [söka efter relaterade konton i användargränssnittet](/help/rtcdp/accounts/account-profile-ui-guide.md#related-accounts-tab).

## Så här kan du använda relaterade konton {#how-to-use}

Du kan använda konton och relaterade konton i segmenteringen. Beslutet om ni ska använda relaterade konton i era segmentdefinitioner beror på ert marknadsföringsexempel. Ni kan till exempel använda relaterade konton för e-postmarknadsföring eller annonskampanjer där ni kan acceptera en lägre noggrannhet i utbyte mot en större räckvidd.

Se en [segmenteringsexempel](/help/rtcdp/segmentation/b2b.md#related-accounts) som använder relaterade konton.
