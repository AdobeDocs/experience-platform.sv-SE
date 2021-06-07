---
solution: Experience Platform
title: Datamodell för detaljhandeln
topic-legacy: overview
description: Se en standardiserad datamodell för detaljhandeln som är kompatibel med Experience Data Model (XDM) för användning i Adobe Experience Platform.
exl-id: 40cbb243-668b-4280-815f-1f94a06b6b87
source-git-commit: 9c5a4e064af0b46ff30b41afef71ca2fd3503a82
workflow-type: tm+mt
source-wordcount: '476'
ht-degree: 0%

---

# [!UICONTROL Retail] branschdatamodell

Följande enhetsrelationsdiagram representerar en standardiserad datamodell för detaljhandeln. Den europeiska referensdosen presenteras avsiktligt på ett avnormaliserat sätt och med hänsyn till hur data lagras i Adobe Experience Platform.

Använd följande förklaring för att tolka denna ERD:

* Varje entitet som visas i är baserad på en underliggande [XDM-klass (Experience Data Model)](../composition.md#class).
* För en given entitet representerar varje rad som är markerad med **fet** en fältgrupp eller en datatyp, med de relevanta fält som anges nedan i oförändrad text.
* De viktigaste fälten för en viss enhet markeras med rött.
* Alla egenskaper som kan användas för att identifiera enskilda kunder markeras som&quot;identitet&quot;, med en av dessa egenskaper markerad som&quot;primär identitet&quot;.
* Enhetsrelationer markeras som icke-beroende eftersom cookie-baserade händelser ofta inte kan avgöra vem eller vilka personer som gjorde transaktionen.

![](../../images/industries/retail.png)

>[!NOTE]
>
>Experience Event-entiteten innehåller ett fält av typen &quot;_ID&quot;, som representerar det unika identifierarattributet (`_id`) som tillhandahålls av klassen XDM ExperienceEvent. Mer information om vad som förväntas för det här värdet finns i referensdokumentet på [XDM ExperienceEvent](../../classes/experienceevent.md).

## [!UICONTROL Retail] användningsfall

Följande tabell visar de rekommenderade klasserna och schemafältgrupperna för flera vanliga användningsfall.

| Användningsfall | Rekommenderade klasser och fältgrupper |
| --- | --- |
| Kombinera online- och offlinedatakällor och matcha enhets- och online-/offlineidentitet för att tillhandahålla en helhetsbaserad rapportering för flerkanals- och enhetsövergripande attribuering. | <ul><li>**[XDM ExperienceEvent](../../classes/experienceevent.md)**:<ul><li>[Handelsinformation](../../field-groups/event/commerce-details.md)</li><li>[Webbinformation](../../field-groups/event/web-details.md)</li></ul></li><li>**Product**  (anpassad klass)\*:<ul><li>Produkt (anpassad fältgrupp)\*</li></ul></li></ul> |
| Tillhandahåll målinriktade och personaliserade upplevelser för olika segment för att öka intäkterna och bidra till att stärka plattformen i flerkanalsmarknadsföring. | <ul><li>**[XDM ExperienceEvent](../../classes/experienceevent.md)**:<ul><li>[Information om kampanjmarknadsföring](../../field-groups/event/campaign-marketing-details.md)</li><li>[Kanalinformation](../../field-groups/event/channel-details.md)</li><li>[Handelsinformation](../../field-groups/event/commerce-details.md)</li><li>[Miljöinformation](../../field-groups/event/environment-details.md)</li><li>[Webbinformation](../../field-groups/event/web-details.md)</li></ul></li><li>**[Individuell XDM-profil](../../classes/individual-profile.md)**:<ul><li>[Demografiska detaljer](../../field-groups/profile/demographic-details.md)</li><li>[Kontaktinformation, privat](../../field-groups/profile/personal-contact-details.md)</li><li>[Kontaktinformation, arbete](../../field-groups/profile/work-contact-details.md)</li></ul></li></ul> |
| Analysera multitouch-attribuering för att förbättra marknadsföringens effektivitet. | <ul><li>**[XDM ExperienceEvent](../../classes/experienceevent.md)**:<ul><li>[Information om kampanjmarknadsföring](../../field-groups/event/campaign-marketing-details.md)</li><li>[Kanalinformation](../../field-groups/event/channel-details.md)</li><li>[Handelsinformation](../../field-groups/event/commerce-details.md)</li></ul></li><li>**[Individuell XDM-profil](../../classes/individual-profile.md)**:<ul><li>[Demografiska detaljer](../../field-groups/profile/demographic-details.md)</li></ul></li></ul> |
| Förbättra e-postrelevansen genom förbättrad segmentering mellan män och kvinnor. | <ul><li>**[XDM ExperienceEvent](../../classes/experienceevent.md)**:<ul><li>[Handelsinformation](../../field-groups/event/commerce-details.md)</li></ul></li><li>**[Individuell XDM-profil](../../classes/individual-profile.md)**:<ul><li>[Demografiska detaljer](../../field-groups/profile/demographic-details.md)</li></ul></li><li>**Product**  (anpassad klass)\*:<ul><li>Produkt (anpassad fältgrupp)\*</li></ul></li></ul> |
| Öka lojalitetsdata (partnerdata) för att öka relevant produktinformation över webben, e-post och digitala marknadsföringskanaler. | <ul><li>**[XDM ExperienceEvent](../../classes/experienceevent.md)**:<ul><li>[Webbinformation](../../field-groups/event/web-details.md)</li></ul></li><li>**[Individuell XDM-profil](../../classes/individual-profile.md)**:<ul><li>[Demografiska detaljer](../../field-groups/profile/demographic-details.md)</li><li>[Förmånsinformation](../../field-groups/profile/loyalty-details.md)</li></ul></li><li>**Product**  (anpassad klass)\*:<ul><li>Produkt (anpassad fältgrupp)\*</li></ul></li></ul> |
| Återmarknadsför övergivna kundvagnar via automatiserade och personaliserade e-postmeddelanden. | <ul><li>**[XDM ExperienceEvent](../../classes/experienceevent.md)**:<ul><li>[Handelsinformation](../../field-groups/event/commerce-details.md)</li><li>[Webbinformation](../../field-groups/event/web-details.md)</li></ul></li><li>**Product**  (anpassad klass)\*:<ul><li>Produkt (anpassad fältgrupp)\*</li></ul></li></ul> |

{style=&quot;table-layout:auto&quot;}

*\*Medan en standardproduktklass planeras för en framtida release måste produktscheman i stället byggas med en anpassad klass. Du måste därför manuellt skapa strukturen för schemaklassen samt strukturen för de fältgrupper som du lägger till i den. Mer information finns i avsnittet [skapa en anpassad klass](../../ui/resources/classes.md#create) i gränssnittshandboken för XDM.*.
