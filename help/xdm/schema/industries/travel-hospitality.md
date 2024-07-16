---
solution: Experience Platform
title: Resor och turism - branschdatamodell ERD
description: Visa en datamodell (ERD) som beskriver en standardiserad datamodell för rese- och turismbranschen som är kompatibel med Experience Data Model (XDM) för användning i Adobe Experience Platform.
exl-id: 4d454160-9066-4702-815b-9509942f709e
source-git-commit: 5caa4c750c9f786626f44c3578272671d85b8425
workflow-type: tm+mt
source-wordcount: '442'
ht-degree: 0%

---

# [!UICONTROL Travel and hospitality] branschdatamodell - ERD

Följande enhetsrelationsdiagram representerar en standardiserad datamodell för rese- och turismbranschen. Den europeiska referensdosen presenteras avsiktligt på ett avnormaliserat sätt och med hänsyn till hur data lagras i Adobe Experience Platform.

>[!NOTE]
>
>Den rekommenderade referensmetoden är en rekommendation för hur du ska modellera dina data för det här användningsexemplet. Om du vill använda den här datamodellen i Platform måste du själv skapa de rekommenderade scheman och deras relationer. Mer information finns i guiderna för att hantera [scheman](../../ui/resources/schemas.md) och [relationer](../../tutorials/relationship-ui.md) i användargränssnittet.

Använd följande förklaring för att tolka denna ERD:

* Varje entitet som visas i är baserad på en underliggande [XDM-klass (Experience Data Model)](../composition.md#class).
* För en given entitet representerar varje rad som är markerad med **bold** en fältgrupp eller en datatyp, med de relevanta fält som anges nedan i oformaterad text.
* De viktigaste fälten för en viss enhet markeras med rött.
* Alla egenskaper som kan användas för att identifiera enskilda kunder markeras som&quot;identitet&quot;, med en av dessa egenskaper markerad som&quot;primär identitet&quot;.
* Enhetsrelationer markeras som icke-beroende eftersom cookie-baserade händelser ofta inte kan avgöra vem eller vilka personer som gjorde transaktionen.

![](../../images/industries/travel-hospitality.png)

>[!NOTE]
>
>Experience Event-entiteten innehåller ett _ID-fält, som representerar det unika identifierarattributet (`_id`) som tillhandahålls av klassen XDM ExperienceEvent. Mer information om vad som förväntas för det här värdet finns i referensdokumentet på [XDM ExperienceEvent](../../classes/experienceevent.md).

## [!UICONTROL Travel and hospitality] användningsfall

Följande tabell visar de rekommenderade klasserna och schemafältgrupperna för flera vanliga användningsområden för rese- och turismbranschen.

| Användningsfall | Rekommenderade klasser och fältgrupper |
| --- | --- |
| Merförsäljning av matsalar och andra bofasta attraktioner till marknadsgäster och gäster med kommande hotellbokningar. | <ul><li>**[XDM ExperienceEvent](../../classes/experienceevent.md)**:<ul><li>[Reservationsinformation](../../field-groups/event/reservation-details.md)</li><li>[Bokföringsreservation](../../field-groups/event/lodging-reservation.md)</li><li>[Reservation för matsalar](../../field-groups/event/dining-reservation.md)</li></ul></li><li>**[XDM-individuell profil](../../classes/individual-profile.md)**:<ul><li>[Demografisk information](../../field-groups/profile/demographic-details.md)</li><li>[Information om personlig kontakt](../../field-groups/profile/personal-contact-details.md)</li><li>[Information om arbetskontakt](../../field-groups/profile/work-contact-details.md)</li></ul></li></ul> |
| Merförsäljning av matsalar och andra bofasta attraktioner till marknadsgäster och gäster med kommande hotellbokningar. | <ul><li>**[XDM ExperienceEvent](../../classes/experienceevent.md)**:<ul><li>[Reservationsinformation](../../field-groups/event/reservation-details.md)</li><li>[Reservation för matsalar](../../field-groups/event/dining-reservation.md)</li></ul></li><li>**[XDM-individuell profil](../../classes/individual-profile.md)**:<ul><li>[Demografisk information](../../field-groups/profile/demographic-details.md)</li><li>[Information om personlig kontakt](../../field-groups/profile/personal-contact-details.md)</li><li>[Information om arbetskontakt](../../field-groups/profile/work-contact-details.md)</li><li>[Förmånsinformation](../../field-groups/profile/loyalty-details.md)</li></ul></li></ul> |
| Merförsäljning av hotell och andra bofasta attraktioner till marknadsgäster och gäster med kommande hotellbokningar. | <ul><li>**[XDM ExperienceEvent](../../classes/experienceevent.md)**:<ul><li>[Reservationsinformation](../../field-groups/event/reservation-details.md)</li><li>[Bokföringsreservation](../../field-groups/event/lodging-reservation.md)</li></ul></li><li>**[XDM-individuell profil](../../classes/individual-profile.md)**:<ul><li>[Demografisk information](../../field-groups/profile/demographic-details.md)</li><li>[Information om personlig kontakt](../../field-groups/profile/personal-contact-details.md)</li><li>[Information om arbetskontakt](../../field-groups/profile/work-contact-details.md)</li><li>[Förmånsinformation](../../field-groups/profile/loyalty-details.md)</li></ul></li></ul> |
| Merförsäljning av flyg och andra boendeattraktioner till marknadsgäster och gäster med kommande hotellbokningar. | <ul><li>**[XDM ExperienceEvent](../../classes/experienceevent.md)**:<ul><li>[Reservationsinformation](../../field-groups/event/reservation-details.md)</li><li>[Flygreservation](../../field-groups/event/flight-reservation.md)</li></ul></li><li>**[XDM-individuell profil](../../classes/individual-profile.md)**:<ul><li>[Demografisk information](../../field-groups/profile/demographic-details.md)</li><li>[Information om personlig kontakt](../../field-groups/profile/personal-contact-details.md)</li><li>[Information om arbetskontakt](../../field-groups/profile/work-contact-details.md)</li><li>[Förmånsinformation](../../field-groups/profile/loyalty-details.md)</li></ul></li></ul> |

{style="table-layout:auto"}
