---
keywords: Experience Platform;hem;populära ämnen;identitet;Identitet;XDM-diagram;identitetstjänst;Identitetstjänst
solution: Experience Platform
title: Översikt över identitetstjänsten
description: Adobe Experience Platform identitetstjänst hjälper er att få en bättre bild av era kunder och deras beteende genom att skapa en bro mellan identiteter på olika enheter och system, så att ni kan leverera slagkraftiga, personliga digitala upplevelser i realtid.
exl-id: a22dc3f0-3b7d-4060-af3f-fe4963b45f18
source-git-commit: 3fe94be9f50d64fc893b16555ab9373604b62e59
workflow-type: tm+mt
source-wordcount: '1554'
ht-degree: 0%

---

# Adobe Experience Platform Identity Service

För att kunna leverera relevanta digitala upplevelser behöver ni en heltäckande och korrekt representation av de verkliga enheter som utgör er kundbas.

Organisationer och företag har idag en stor mängd olika datauppsättningar: dina enskilda kunder representeras av en mängd olika identifierare. Kunden kan länkas till olika webbläsare (Safari, Google Chrome), maskinvaruenheter (telefoner, bärbara datorer) och andra personidentifierare (CRM-ID:n, e-postkonton). Detta skapar en osammanhängande bild av kunden.

Du kan lösa dessa problem med Adobe Experience Platform Identity Service och dess funktioner:

* Generera en **identitetsdiagram** som knyter samman olika identiteter och därmed ger er en visuell representation av hur en kund interagerar med ert varumärke i olika kanaler.
* Skapa ett diagram för kundprofil i realtid, som sedan används för att skapa en heltäckande bild av kunden genom att sammanfoga attribut och beteenden.
* Utför validering och felsökning med olika verktyg.

Det här dokumentet innehåller en översikt över identitetstjänsten och hur du kan använda dess funktioner i Experience Platform.

## Terminologi {#terminology}

Läs följande tabell för att få en sammanfattning av nyckeltermerna innan du börjar lära dig mer om identitetstjänsten:

| Term | Definition |
| --- | --- |
| Identitet | En identitet är data som är unika för en enhet. Vanligtvis är detta ett objekt i verkligheten, till exempel en enskild person, en maskinvaruenhet eller en webbläsare (representeras av en cookie). En fullständigt kvalificerad identitet består av två delar: en **namnutrymme för identitet** och **identitetsvärde**. |
| Namnutrymme för identitet | Ett identitetsnamnutrymme är kontexten för en viss identitet. Ett namnutrymme för `Email` kan motsvara **julien<span>@acme.com**. På samma sätt är namnutrymmet `Phone` kan motsvara `555-555-1234`. Mer information finns i [Översikt över namnutrymmet identity](./features/namespaces.md) |
| Identitetsvärde | Ett identitetsvärde är en sträng som representerar en faktisk entitet och kategoriseras i identitetstjänsten via ett namnutrymme. Exempelvis identitetsvärdet (sträng) **julien<span>@acme.com** kan kategoriseras som en `Email` namnutrymme. |
| Identitetstyp | En identitetstyp är en komponent i ett identitetsnamnutrymme. Identitetstypen anger om identitetsdata är länkade i ett identitetsdiagram eller inte. |
| Länk | En länk eller en länkning är en metod för att fastställa att två olika identiteter representerar samma enhet. En länk mellan &quot;`Email` = julien<span>@acme.com och &quot;`Phone` = 555-555-1234&quot; betyder att båda identiteterna representerar samma enhet. Detta tyder på att kunden som interagerat med ert varumärke både med juliens e-postadress<span>@acme.com och telefonnumret 555-555-1234 är samma. |
| Identitetstjänst | Identitetstjänsten är en tjänst i Experience Platform som länkar (eller bryter länkar) identiteter för att underhålla identitetsdiagram. |
| Identitetsdiagram | Identitetsdiagrammet är en samling identiteter som representerar en enskild kund. Mer information finns i guiden [med identitetsdiagramvisningsprogrammet](./features/identity-graph-viewer.md). |
| Kundprofil i realtid | Kundprofilen i realtid är en tjänst inom Adobe Experience Platform som: <ul><li>Sammanfogar profilfragment för att skapa en profil utifrån ett identitetsdiagram.</li><li>Segmentprofiler så att de sedan kan skickas till målet för aktiveringar.</li></ul> |
| Profil | En profil är en representation av ett ämne, en organisation eller en individ. En profil består av fyra element: <ul><li>Attribut: attribut innehåller information som namn, ålder eller kön.</li><li>Beteende: beteenden ger information om aktiviteterna för en viss profil. Ett profilbeteende kan till exempel avgöra om en viss profil söker efter sandaler eller t-shirts.</li><li>Identiteter: För en sammanfogad profil innehåller detta information om alla identiteter som är associerade med personen. Identiteter kan klassificeras i tre kategorier: Person (CRMID, email, phone), device (IDFA, GAID) och cookie (ECID, AAID).</li><li>Målgruppsmedlemskap: De grupper där profilen tillhör (lojala användare, användare som bor i Kalifornien osv.)</li></ul> |

{style="table-layout:auto"}

## Vad är identitetstjänsten?

![Identitetssammanfogning på plattform](./images/identity-service-stitching.png)

I B2C-sammanhang (Business-To-Customer) interagerar kunderna med ert företag och skapar en relation med ert varumärke. En typisk kund kan vara aktiv i valfritt antal system i organisationens datainfrastruktur. Alla kunder kan vara aktiva i e-handels-, lojalitets- och helpdesk-systemen. Samma kund kan även anlita både anonymt eller via autentiserade medier på ett antal olika enheter.

Tänk på följande kundresa:

* Julien har skapat ett konto på din e-handelswebbplats och beställt några artiklar tidigare. Julien använder vanligtvis sin egen bärbara dator för att handla och loggar in på sitt konto med användningstiden.
* Men under ett av hennes besök på er webbplats använder hon en surfplatta för att söka efter sandaler. Under den här sessionen loggar hon varken in eller lägger en order eftersom hon använde en annan enhet.
* I det här skedet representeras Juliens verksamhet i två olika profiler:
   * Hennes första profil är hennes inloggnings-ID för e-handel. Den här profilen används när hon använder en kombination av användarnamn och lösenord för att autentisera sin session på din e-handelsplats. Den här profilen identifieras av en identifierare för olika enheter.
   * Hennes andra profil är hennes surfplatta. Den här profilen skapades när hon har bläddrat anonymt på din e-handelsplats med en surfplatta utan att logga in på sitt konto. Den här profilen identifieras av en cookie-identifierare.
* Senare återupptar Julien sin surfsession. Men den här gången loggar hon in på sitt konto. Därför relaterar identitetstjänsten nu Juliens aktivitet på surfplattor till hennes inloggnings-ID för e-handel.
* Om du går vidare kan målinnehållet återspegla Juliens fullständiga profil, inköpshistorik och anonyma webbläsaraktivitet.

>[!IMPORTANT]
>
>Ni kan använda identitetstjänsten för att länka samman identiteter och samla en fullständig bild av kunden som annars skulle kunna vara spridd över olika system.

## Vad gör identitetstjänsten?

Identitetstjänsten utför följande åtgärder för att utföra sitt uppdrag:

* Skapa egna namnutrymmen som passar organisationens behov.
* Skapa, uppdatera och visa identitetsdiagram.
* Ta bort identiteter baserat på datauppsättningar.
* Ta bort identiteter för att säkerställa efterlevnad av gällande bestämmelser.

## Så här länkar identitetstjänsten identiteter

En länk mellan två identiteter skapas när identitetsnamnutrymmet och identitetsvärdena matchar.

En vanlig inloggningshändelse **skickar två identiteter** till Experience Platform:

* Identifieraren (till exempel ett CRM-ID) som representerar en autentiserad användare.
* Webbläsaridentifieraren (t.ex. ett ECID) som representerar webbläsaren.

Titta på följande exempel:

* Du loggar in med kombinationen användarnamn och lösenord till en e-handelswebbplats med din bärbara dator. Den här händelsen kvalificerar dig som en autentiserad användare, så identitetstjänsten känner igen ditt CRM-ID.
* Din användning av en webbläsare för att komma åt e-handelsplatsen känns också igen som en händelse av Identity Service. Den här händelsen representeras i identitetstjänsten via ett ECID.
* Bakom kulisserna bearbetar Identity Service de två händelserna som: `CRM_ID:ABC, ECID:123`.
   * CRM-ID: ABC är det namnutrymme och värde som representerar dig som autentiserad användare.
   * ECID: 123 är namnutrymmet och värdet som representerar webbläsaranvändningen på din bärbara dator.
* Om du sedan loggar in med samma inloggningsuppgifter på samma e-handelswebbplats, men använder webbläsaren på telefonen i stället för webbläsaren på din bärbara dator, registreras ett nytt ECID i identitetstjänsten.
* Bakom kulisserna bearbetar Identity Service den nya händelsen som `{CRM_ID:ABC, ECID:456}`, där CRM_ID: ABC representerar ditt autentiserade kund-ID och ECID:456 representerar webbläsaren på din mobila enhet.

Med tanke på scenarierna ovan upprättar identitetstjänsten en länk mellan `{CRM_ID:ABC, ECID:123}`, samt `{CRM_ID:ABC, ECID:456}`. Detta resulterar i ett identitetsdiagram där du&quot;äger&quot; tre identiteter: en för personidentifierare (CRM ID) och två för cookie-identifierare (ECID).

Mer information finns i guiden [hur identitetstjänsten länkar identiteter](./features/identity-linking-logic.md).

## Identitetsdiagram

Ett identitetsdiagram är en karta över relationer mellan olika identitetsnamnutrymmen, som gör att du kan visualisera och bättre förstå vilka kundidentiteter som sammanfogas, och hur. Läs självstudiekursen om [med identitetsdiagramvisningsprogrammet](./features/identity-graph-viewer.md) för mer information.

Följande video är avsedd att ge stöd för din förståelse av identiteter och identitetsdiagram.

>[!VIDEO](https://video.tv.adobe.com/v/27841?quality=12&learn=on)

## Förstå identitetstjänstens roll i Experience Platform infrastruktur

Identitetstjänsten spelar en viktig roll inom Experience Platform. Några av dessa viktiga integreringar är:

* [Scheman](../xdm/home.md): I ett givet schema gör de schemafält som är markerade som identiteter att identitetsdiagram kan skapas.
* [Datauppsättningar](../catalog/datasets/overview.md): När en datauppsättning aktiveras för inmatning i kundprofilen i realtid genereras identitetsdiagram från datauppsättningen, eftersom datauppsättningen har minst två fält som är markerade som identitet.
* [Web SDK](../edge/home.md): Web SDK skickar upplevelsehändelser till Adobe Experience Platform, och identitetstjänsten genererar ett diagram när det finns två eller fler identiteter i händelsen.
* [Kundprofil i realtid](../profile/home.md): Innan attribut och händelser för en viss profil sammanfogas kan kundprofilen i realtid referera till identitetsdiagrammet. Mer information finns i guiden [förstå relationen mellan identitetstjänsten och kundprofilen i realtid](./identity-and-profile.md).
* [Destinationer](../destinations/home.md): Destinationer kan skicka profilinformation till andra system baserat på ett identitetsnamnutrymme, t.ex. hashad e-post.
* [Segmentmatchning](../segmentation/ui/segment-match/overview.md): Segmentmatchning matchar två profiler i två olika sandlådor som har samma id-namnutrymme och identitetsvärde.
* [Privacy Service](../privacy-service/home.md): Om borttagningsbegäran innehåller `identity`kan den angivna kombinationen av namnutrymme och identitetsvärde tas bort från identitetstjänsten med hjälp av funktionen för behandling av sekretessförfrågningar i Privacy Servicen.

