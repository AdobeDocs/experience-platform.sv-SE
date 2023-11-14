---
solution: Experience Platform
title: Datamodell för detaljhandeln
description: Se en standardiserad datamodell för detaljhandeln som är kompatibel med Experience Data Model (XDM) för användning i Adobe Experience Platform.
exl-id: 40cbb243-668b-4280-815f-1f94a06b6b87
source-git-commit: 5ceb261dbf1cac58d0cfe620875b8fa7c761abf2
workflow-type: tm+mt
source-wordcount: '456'
ht-degree: 1%

---

# [!UICONTROL Retail] branschdatamodell

Följande enhetsrelationsdiagram representerar en standardiserad datamodell för detaljhandeln. Den europeiska referensdosen presenteras avsiktligt på ett avnormaliserat sätt och med hänsyn till hur data lagras i Adobe Experience Platform.

>[!NOTE]
>
>Den rekommenderade referensmetoden är en rekommendation för hur du ska modellera dina data för det här användningsexemplet. Om du vill använda den här datamodellen i Platform måste du själv skapa de rekommenderade scheman och deras relationer. Visa guiderna för hantering [scheman](../../ui/resources/schemas.md) och [relationer](../../tutorials/relationship-ui.md) i användargränssnittet för mer information.

Använd följande förklaring för att tolka denna ERD:

* Varje enhet som visas i är baserad på ett underliggande [Klassen Experience Data Model (XDM)](../composition.md#class).
* För en given entitet är varje rad markerad i **fet** representerar en fältgrupp eller en datatyp, med de relevanta fält som anges nedan i oformaterad text.
* De viktigaste fälten för en viss enhet markeras med rött.
* Alla egenskaper som kan användas för att identifiera enskilda kunder markeras som&quot;identitet&quot;, med en av dessa egenskaper markerad som&quot;primär identitet&quot;.
* Enhetsrelationer markeras som icke-beroende eftersom cookie-baserade händelser ofta inte kan avgöra vem eller vilka personer som gjorde transaktionen.

![](../../images/industries/retail.png)

>[!NOTE]
>
>Händelseentiteten i Experience innehåller fältet &quot;_ID&quot;, som representerar den unika identifieraren (`_id`)-attribut från klassen XDM ExperienceEvent. Se referensdokumentet på [XDM ExperienceEvent](../../classes/experienceevent.md) för mer information om vad som förväntas för det här värdet.

## [!UICONTROL Retail] användningsfall

Följande tabell visar de rekommenderade klasserna och schemafältgrupperna för flera vanliga användningsfall.

| Användningsfall | Rekommenderade klasser och fältgrupper |
| --- | --- |
| Kombinera online- och offlinedatakällor och matcha enhets- och online-/offlineidentitet för att tillhandahålla en helhetsbaserad rapportering för flerkanals- och enhetsövergripande attribuering. | <ul><li>**[XDM ExperienceEvent](../../classes/experienceevent.md)**:<ul><li>[Handelsinformation](../../field-groups/event/commerce-details.md)</li><li>[Webbinformation](../../field-groups/event/web-details.md)</li></ul></li><li>**[Produkt](../../classes/product.md)**:<ul><li>[Produktkatalog](../../field-groups/product/product-catalog.md)</li><li>[Produktkategori](../../field-groups/product/product-category.md)</li></ul></li></ul> |
| Tillhandahåll målinriktade och personaliserade upplevelser för olika segment för att öka intäkterna och bidra till att stärka plattformen i flerkanalsmarknadsföring. | <ul><li>**[XDM ExperienceEvent](../../classes/experienceevent.md)**:<ul><li>[Information om kampanjmarknadsföring](../../field-groups/event/campaign-marketing-details.md)</li><li>[Kanalinformation](../../field-groups/event/channel-details.md)</li><li>[Handelsinformation](../../field-groups/event/commerce-details.md)</li><li>[Miljöinformation](../../field-groups/event/environment-details.md)</li><li>[Webbinformation](../../field-groups/event/web-details.md)</li></ul></li><li>**[Individuell XDM-profil](../../classes/individual-profile.md)**:<ul><li>[Demografiska detaljer](../../field-groups/profile/demographic-details.md)</li><li>[Kontaktinformation, privat](../../field-groups/profile/personal-contact-details.md)</li><li>[Kontaktinformation, arbete](../../field-groups/profile/work-contact-details.md)</li></ul></li></ul> |
| Analysera multitouch-attribuering för att förbättra marknadsföringens effektivitet. | <ul><li>**[XDM ExperienceEvent](../../classes/experienceevent.md)**:<ul><li>[Information om kampanjmarknadsföring](../../field-groups/event/campaign-marketing-details.md)</li><li>[Kanalinformation](../../field-groups/event/channel-details.md)</li><li>[Handelsinformation](../../field-groups/event/commerce-details.md)</li></ul></li><li>**[Individuell XDM-profil](../../classes/individual-profile.md)**:<ul><li>[Demografiska detaljer](../../field-groups/profile/demographic-details.md)</li></ul></li></ul> |
| Förbättra e-postrelevansen genom förbättrad segmentering mellan män och kvinnor. | <ul><li>**[XDM ExperienceEvent](../../classes/experienceevent.md)**:<ul><li>[Handelsinformation](../../field-groups/event/commerce-details.md)</li></ul></li><li>**[Individuell XDM-profil](../../classes/individual-profile.md)**:<ul><li>[Demografiska detaljer](../../field-groups/profile/demographic-details.md)</li></ul></li><li>**[Produkt](../../classes/product.md)**:<ul><li>[Produktkatalog](../../field-groups/product/product-catalog.md)</li><li>[Produktkategori](../../field-groups/product/product-category.md)</li></ul></li></ul> |
| Öka lojalitetsdata (partnerdata) för att öka relevant produktinformation över webben, e-post och digitala marknadsföringskanaler. | <ul><li>**[XDM ExperienceEvent](../../classes/experienceevent.md)**:<ul><li>[Webbinformation](../../field-groups/event/web-details.md)</li></ul></li><li>**[Individuell XDM-profil](../../classes/individual-profile.md)**:<ul><li>[Demografiska detaljer](../../field-groups/profile/demographic-details.md)</li><li>[Förmånsinformation](../../field-groups/profile/loyalty-details.md)</li></ul></li><li>**[Produkt](../../classes/product.md)**:<ul><li>[Produktkatalog](../../field-groups/product/product-catalog.md)</li><li>[Produktkategori](../../field-groups/product/product-category.md)</li></ul></li></ul> |
| Återmarknadsför övergivna varukorgar via automatiserade och personaliserade e-postmeddelanden. | <ul><li>**[XDM ExperienceEvent](../../classes/experienceevent.md)**:<ul><li>[Handelsinformation](../../field-groups/event/commerce-details.md)</li><li>[Webbinformation](../../field-groups/event/web-details.md)</li></ul></li><li>**[Produkt](../../classes/product.md)**:<ul><li>[Produktkatalog](../../field-groups/product/product-catalog.md)</li><li>[Produktkategori](../../field-groups/product/product-category.md)</li></ul></li></ul> |

{style="table-layout:auto"}
