---
title: Relaterade konton i Real-Time CDP B2B Edition
type: Documentation
description: En översikt och mer information om kontofunktionen i Experience Platform Real-Time CDP B2B.
feature: Get Started, Profiles, B2B
badgeB2B: label="B2B Edition" type="Informative" url="https://helpx.adobe.com/legal/product-descriptions/real-time-customer-data-platform-b2b-edition-prime-and-ultimate-packages.html newtab=true"
exl-id: 37fd2cdb-87c0-4e5e-9599-ad4f397f7c28
source-git-commit: db57fa753a3980dca671d476521f9849147880f1
workflow-type: tm+mt
source-wordcount: '435'
ht-degree: 3%

---

# Relaterade konton i Real-Time CDP B2B Edition

## Översikt {#overview}

B2B-företag har ofta sin kundinformation lagrad i flera system, där alla bara innehåller partiella eller till och med motstridiga data för samma verkliga affärsenhet. Detta skapar en stor utmaning i att få en korrekt bild av kunderna och minskar därmed effektiviteten och effektiviteten i B2B-marknadsförings- och säljsatsningarna.

| ID | Namn | Webbplats | Bransch | Läge | Telefon | Har öppen affärsmöjlighet med belopp > `$1 million` |
|---|---|---|---|---|---|---|
| 1 | Acme | acme.com | Programvara | CA | (408)536-6000 |   |
| 2 | Acme | acm.com | Programvara | CA | 4085366000 | x |
| 3 | Acme Inc |   |   | CA | (408)5366000 |   |
| 4 | Acme Consulting Service | `http://www.acme.com/consulting` | Technology Consulting | NY | (212)471-0904 | x |
| 5 | Acme IT |   |   | CA |   |   |

{style="table-layout:auto"}

Med relaterade konton [!DNL Real-Time CDP B2B] visar nu en lista över konton som liknar det konto du bläddrar i.

![Skärm som visar relaterade konton i användargränssnittet för Experience Platform.](/help/rtcdp/b2b-ai-ml-services/assets/related-accounts-in-ui.png)

Använd den här funktionen om du vill visa relaterade kontoprofiler för en kontoprofil i användargränssnittet för Experience Platform och sedan inkludera de relaterade kontona i segmentdefinitionerna för att bredda din räckvidd eller tillämpa bredare kriterier i dina segment.

## Aktivera tjänsten för relaterade konton {#enable}

Aktivera tjänsten genom att välja **[!UICONTROL Profiles]** i sidlisten följt av **[!UICONTROL Settings]**.

![Markeringsprofiler och inställningar för användargränssnittet i Experience Platform.](../assets/../b2b-ai-ml-services/assets/related-account-settings.png)

Markera växlingsknappen bredvid [!UICONTROL Enable related accounts] för att aktivera tjänsten och sedan välja **[!UICONTROL Save]**.

![Skärmmarkeringen för kontoinställningar visar hur du växlar och sparar.](../assets/../b2b-ai-ml-services/assets/related-account-toggle.png)

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
