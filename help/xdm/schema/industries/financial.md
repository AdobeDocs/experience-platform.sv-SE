---
solution: Experience Platform
title: ERD för datamodell för finanssektorn
description: Visa ett enhetsrelationsdiagram (ERD) som beskriver en standardiserad datamodell för banksektorn, finanssektorn och försäkringssektorn (BFSI). Den här datamodellen är kompatibel med Experience Data Model (XDM) för användning i Adobe Experience Platform.
exl-id: 2e8f6b2a-10e7-4394-b45f-c03db0f25400
source-git-commit: 60c0bd62b4effaa161c61ab304718ab8c20a06e1
workflow-type: tm+mt
source-wordcount: '364'
ht-degree: 0%

---

# [!UICONTROL Financial services] ERD för branschdatamodell

Följande företagsrelationsdiagram representerar en standardiserad datamodell för banksektorn, finanssektorn och försäkringssektorn. Den europeiska referensdosen presenteras avsiktligt på ett avnormaliserat sätt och med hänsyn till hur data lagras i Adobe Experience Platform.

>[!NOTE]
>
>Den rekommenderade referensmetoden är en rekommendation för hur du ska modellera dina data för det här användningsexemplet. Om du vill använda den här datamodellen i Platform måste du själv skapa de rekommenderade scheman och deras relationer. Visa guiderna för hantering [scheman](../../ui/resources/schemas.md) och [relationer](../../tutorials/relationship-ui.md) i användargränssnittet om du vill ha mer information.

Använd följande förklaring för att tolka denna ERD:

* Varje enhet som visas i är baserad på ett underliggande [Klassen Experience Data Model (XDM)](../composition.md#class).
* För en given entitet är varje rad markerad i **fet** representerar en fältgrupp eller en datatyp, med de relevanta fält som anges nedan i oformaterad text.
* De viktigaste fälten för en viss enhet markeras med rött.
* Alla egenskaper som kan användas för att identifiera enskilda kunder markeras som&quot;identitet&quot;, med en av dessa egenskaper markerad som&quot;primär identitet&quot;.
* Enhetsrelationer markeras som icke-beroende eftersom cookie-baserade händelser ofta inte kan avgöra vem eller vilka personer som gjorde transaktionen.

![](../../images/industries/financial.png)

>[!NOTE]
>
>Händelseentiteten i Experience innehåller fältet &quot;_ID&quot;, som representerar den unika identifieraren (`_id`)-attribut från klassen XDM ExperienceEvent. Se referensdokumentet på [XDM ExperienceEvent](../../classes/experienceevent.md) om du vill ha mer information om vad som förväntas för det här värdet.

## [!UICONTROL Financial services] användningsfall

Följande tabell visar de rekommenderade klasserna och schemafältgrupperna för flera vanliga fall av ekonomiskt bruk.

| Användningsfall | Rekommenderade klasser och fältgrupper |
| --- | --- |
| Driv personalisering i stor skala för de segment du föredrar genom insikter i flerkanalsrapportering och automatisera resor för att öka registreringen till ett belöningsprogram som passar dig bäst. | <ul><li>**[[!UICONTROL Product]](../../classes/product.md)**:<ul><li>[[!UICONTROL Product Category]](../../field-groups/product/product-category.md)</li></ul></li><li>**[[!UICONTROL XDM ExperienceEvent]](../../classes/experienceevent.md)**:<ul><li>[[!UICONTROL Card Actions]](../../field-groups/event/card-actions.md)</li><li>[[!UICONTROL Quote Request Details]](../../field-groups/event/quote-request-details.md)</li><li>[[!UICONTROL Deposit Details]](../../field-groups/event/deposit-details.md)</li><li>[[!UICONTROL Channel Details]](../../field-groups/event/channel-details.md)</li><li>[[!UICONTROL Balance Transfers]](../../field-groups/event/balance-transfers.md)</li></ul></li><li>**[[!UICONTROL XDM Individual Profile]](../../classes/individual-profile.md)**:<ul><li>[[!UICONTROL Demographic Details]](../../field-groups/profile/demographic-details.md)</li><li>[[!UICONTROL Personal Contact Details]](../../field-groups/profile/personal-contact-details.md)</li><li>[[!UICONTROL Loyalty Details]](../../field-groups/profile/loyalty-details.md)</li></ul></li></ul> |
| Optimera personalisering över flera kanaler, både online och offline. | <ul><li>**[[!UICONTROL Product]](../../classes/product.md)**:<ul><li>[[!UICONTROL Product Category]](../../field-groups/product/product-category.md)</li></ul></li><li>**[[!UICONTROL XDM ExperienceEvent]](../../classes/experienceevent.md)**:<ul><li>[[!UICONTROL Channel Details]](../../field-groups/event/channel-details.md)</li></ul></li><li>**[[!UICONTROL XDM Individual Profile]](../../classes/individual-profile.md)**:<ul><li>[[!UICONTROL Demographic Details]](../../field-groups/profile/demographic-details.md)</li><li>[[!UICONTROL Personal Contact Details]](../../field-groups/profile/personal-contact-details.md)</li><li>[[!UICONTROL Loyalty Details]](../../field-groups/profile/loyalty-details.md)</li></ul></li></ul> |
| Få nya intäktsmöjligheter genom att använda insikter från flerkanalsbeteendeanalyser, identifiera mönster för produktanvändning som kan leda till nya produkterbjudanden. | <ul><li>**[[!UICONTROL Policy]](../../classes/policy.md)**</li><li>**[[!UICONTROL Product]](../../classes/product.md)**:<ul><li>[[!UICONTROL Product Category]](../../field-groups/product/product-category.md)</li></ul></li><li>**[[!UICONTROL XDM ExperienceEvent]](../../classes/experienceevent.md)**:<ul><li>[[!UICONTROL Card Actions]](../../field-groups/event/card-actions.md)</li><li>[[!UICONTROL Support Site Search]](../../field-groups/event/support-site-search.md)</li><li>[[!UICONTROL Deposit Details]](../../field-groups/event/deposit-details.md)</li><li>[[!UICONTROL Channel Details]](../../field-groups/event/channel-details.md)</li></ul></li><li>**[[!UICONTROL XDM Individual Profile]](../../classes/individual-profile.md)**:<ul><li>[[!UICONTROL Demographic Details]](../../field-groups/profile/demographic-details.md)</li><li>[[!UICONTROL Personal Contact Details]](../../field-groups/profile/personal-contact-details.md)</li><li>[[!UICONTROL Loyalty Details]](../../field-groups/profile/loyalty-details.md)</li></ul></li></ul> |
