---
solution: Experience Platform
title: Datamodell ERD för telekombranschen
description: Visa ett entitetsrelationsdiagram (ERD) som beskriver en standardiserad datamodell för telekombranschen som är kompatibel med Experience Data Model (XDM) för användning i Adobe Experience Platform.
exl-id: 96f267ce-a177-4384-a512-841c89d942ba
source-git-commit: 60c0bd62b4effaa161c61ab304718ab8c20a06e1
workflow-type: tm+mt
source-wordcount: '381'
ht-degree: 0%

---

# [!UICONTROL Telecommunications] ERD för branschdatamodell

Följande enhetsrelationsdiagram representerar en standardiserad datamodell för telekombranschen. Den europeiska referensdosen presenteras avsiktligt på ett avnormaliserat sätt och med hänsyn till hur data lagras i Adobe Experience Platform.

>[!NOTE]
>
>Den rekommenderade referensmetoden är en rekommendation för hur du ska modellera dina data för det här användningsexemplet. Om du vill använda den här datamodellen i Platform måste du själv skapa de rekommenderade scheman och deras relationer. Visa guiderna för hantering [scheman](../../ui/resources/schemas.md) och [relationer](../../tutorials/relationship-ui.md) i användargränssnittet om du vill ha mer information.

Använd följande förklaring för att tolka denna ERD:

* Varje enhet som visas i är baserad på ett underliggande [Klassen Experience Data Model (XDM)](../composition.md#class).
* För en given entitet är varje rad markerad i **fet** representerar en fältgrupp eller en datatyp, med de relevanta fält som anges nedan i oformaterad text.
* De viktigaste fälten för en viss enhet markeras med rött.
* Alla egenskaper som kan användas för att identifiera enskilda kunder markeras som&quot;identitet&quot;, med en av dessa egenskaper markerad som&quot;primär identitet&quot;.
* Enhetsrelationer markeras som icke-beroende eftersom cookie-baserade händelser ofta inte kan avgöra vem eller vilka personer som gjorde transaktionen.


![](../../images/industries/telecom.png)

>[!NOTE]
>
>Händelseentiteten i Experience innehåller fältet &quot;_ID&quot;, som representerar den unika identifieraren (`_id`)-attribut från klassen XDM ExperienceEvent. Se referensdokumentet på [XDM ExperienceEvent](../../classes/experienceevent.md) om du vill ha mer information om vad som förväntas för det här värdet.

## [!UICONTROL Telecommunications] användningsfall

Följande tabell visar de rekommenderade klasserna och schemafältgrupperna för flera vanliga användningsområden för telekombranschen.

| Användningsfall | Rekommenderade klasser och fältgrupper |
| --- | --- |
| Förstå kunder som är bra kandidater för merförsäljning eller korsförsäljning baserat på deras nuvarande innehav och deras surfbeteende. | <ul><li>**[XDM ExperienceEvent](../../classes/experienceevent.md)**:<ul><li>[[!UICONTROL Upsell Details]](../../field-groups/event/upsell-details.md)</li><li>[[!UICONTROL Upgrade Details]](../../field-groups/event/upgrade-details.md)</li></ul></li><li>**[[!UICONTROL XDM Individual Profile]](../../classes/individual-profile.md)**:<ul><li>[[!UICONTROL Telecom Subscription]](../../field-groups/profile/telecom-subscription.md)</li><li>[[!UICONTROL Demographic Details]](../../field-groups/profile/demographic-details.md)</li><li>[[!UICONTROL Personal Contact Details]](../../field-groups/profile/personal-contact-details.md)</li></ul></li></ul> |
| Återmarknadsför övergivna varukorgar genom relevanta annonser och automatiserade personaliserade e-postmeddelanden. Utelämna annonser när de konverteras. | <ul><li>**[XDM ExperienceEvent](../../classes/experienceevent.md)**:<ul><li>[[!UICONTROL Commerce Details]](../../field-groups/event/upsell-details.md) (För att fånga upp kundvagnsöverläggningar)</li></ul></li><li>**[[!UICONTROL XDM Individual Profile]](../../classes/individual-profile.md)**:<ul><li>[[!UICONTROL Telecom Subscription]](../../field-groups/profile/telecom-subscription.md)</li><li>[[!UICONTROL Demographic Details]](../../field-groups/profile/demographic-details.md)</li><li>[[!UICONTROL Personal Contact Details]](../../field-groups/profile/personal-contact-details.md)</li></ul></li></ul> |
| När en kund markeras som trolig att försvinna (baserat på en medarbetarinteraktion eller en automatiserad maskininlärningsalgoritm) skickar du kundinformationen till digitala och icke-digitala kanaler. | <ul><li>**[XDM ExperienceEvent](../../classes/experienceevent.md)**:<ul><li>[[!UICONTROL Campaign Marketing Details]](../../field-groups/event/campaign-marketing-details.md)</li><li>[[!UICONTROL Channel Details]](../../field-groups/event/channel-details.md)</li><li>En anpassad fältgrupp som innehåller anpassat innehåll</li></ul></li><li>**[[!UICONTROL XDM Individual Profile]](../../classes/individual-profile.md)**:<ul><li>[[!UICONTROL Demographic Details]](../../field-groups/profile/demographic-details.md)</li><li>[[!UICONTROL Personal Contact Details]](../../field-groups/profile/personal-contact-details.md)</li></ul></li></ul> |

{style=&quot;table-layout:auto&quot;}
