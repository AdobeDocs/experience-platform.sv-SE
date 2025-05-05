---
title: Relaterade konton i Real-Time CDP B2B Edition
type: Documentation
description: En översikt och mer information om kontofunktionen i Experience Platform Real-Time CDP B2B.
feature: Get Started, Profiles, B2B
badgeB2B: label="B2B Edition" type="Informative" url="https://helpx.adobe.com/se/legal/product-descriptions/real-time-customer-data-platform-b2b-edition-prime-and-ultimate-packages.html newtab=true"
exl-id: 37fd2cdb-87c0-4e5e-9599-ad4f397f7c28
source-git-commit: 82535ec3ac2dd27e685bb591fdf661d3ab5dd2c9
workflow-type: tm+mt
source-wordcount: '429'
ht-degree: 2%

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

Med relaterade konton visar [!DNL Real-Time CDP B2B] nu en lista över konton som liknar det konto du bläddrar i.

![Skärm med relaterade konton i användargränssnittet för Experience Platform.](/help/rtcdp/b2b-ai-ml-services/assets/related-accounts-in-ui.png)

Använd den här funktionen om du vill visa relaterade kontoprofiler för en kontoprofil i användargränssnittet i Experience Platform och sedan inkludera de relaterade kontona i segmentdefinitionerna för att bredda din räckvidd eller tillämpa bredare kriterier i dina målgrupper.

## Aktivera tjänsten för relaterade konton {#enable}

Om du vill aktivera tjänsten väljer du **[!UICONTROL Profiles]** i sidofältet följt av **[!UICONTROL Settings]**.

![Användargränssnittet för Experience Platform markerar profiler och inställningar.](../assets/../b2b-ai-ml-services/assets/related-account-settings.png)

Markera växlingsknappen bredvid [!UICONTROL Enable related accounts] för att aktivera tjänsten och välj sedan **[!UICONTROL Save]**.

![Skärmen Kontoinställningar visar växlingen och sparandet.](../assets/../b2b-ai-ml-services/assets/related-account-toggle.png)

## Så fungerar det {#how-it-works}

Maskininlärningsjobb som körs dagligen använder en hierarkisk algoritm för att gruppera liknande kontoprofiler i grupper baserat på tre faktorer:

* Länk till överordnat konto
* Webbdomän
* Kontonamn

Efter ett slutfört bearbetningsjobb taggas varje medlem i kontoprofilgruppen med listan Relaterade konton. Du kan visa listan på fliken **Relaterade konton** på sidan Kontoprofil och använda relaterade konton i segmentdefinitioner.

Mer information om [profilanrikningsrelaterade kontojobb](/help/dataflows/ui/b2b/monitor-profile-enrichment.md) finns i dokumentationen.

## Visa relaterade konton {#how-to-view}

Du kan visa relaterade konton för ett konto som du surfar på i användargränssnittet för Experience Platform.

Mer information om [hur du hittar relaterade konton i användargränssnittet](/help/rtcdp/accounts/account-profile-ui-guide.md#related-accounts-tab) finns i dokumentationen.

## Så här kan du använda relaterade konton {#how-to-use}

Du kan använda konton och relaterade konton i segmenteringen. Beslutet om ni ska använda relaterade konton i era segmentdefinitioner beror på ert marknadsföringsexempel. Ni kan till exempel använda relaterade konton för e-postmarknadsföring eller annonskampanjer där ni kan acceptera en lägre noggrannhet i utbyte mot en större räckvidd.

Se ett [exempel på segmentering](/help/rtcdp/segmentation/b2b.md#related-accounts) som använder relaterade konton.
