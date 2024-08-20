---
title: Borttagningar i identitetstjänsten
description: I det här dokumentet finns en översikt över de olika mekanismer som du kan använda för att ta bort dina identitetsdata i Experience Platform och för att skapa klarhet om hur identitetsdiagram kan påverkas.
exl-id: 0619d845-71c1-4699-82aa-c6436815d5b3
source-git-commit: 2a2e3fcc4c118925795951a459a2ed93dfd7f7d7
workflow-type: tm+mt
source-wordcount: '1194'
ht-degree: 0%

---

# Borttagningar i identitetstjänsten

Adobe Experience Platform Identity Service genererar identitetsdiagram genom att på ett deterministiskt sätt länka identiteter mellan olika enheter och system för en enskild person. Identitetsdiagramlänkar upprättas när två eller flera markerade identiteter tas emot inom samma datarad.

Identitetsdiagram utnyttjas av kundprofilen i realtid för att skapa en heltäckande och unik bild av era kundattribut och -beteenden, så att ni kan leverera slagkraftiga, personliga digitala upplevelser i realtid till människor, och inte till enheter.

I det här dokumentet finns en översikt över de olika mekanismer som du kan använda för att ta bort dina identitetsdata i Experience Platform och för att skapa klarhet om hur identitetsdiagram kan påverkas.

## Komma igång

Dokumentet nedan refererar till följande funktioner i Experience Platform:

* [Identitetstjänst](../home.md): Få en bättre bild av enskilda kunder och deras beteende genom att skapa en bro mellan identiteter på olika enheter och system.
   * [Identitetsdiagram](./identity-graph-viewer.md): Ett identitetsdiagram är en karta över relationer mellan olika identiteter för en viss kund, som ger dig en visuell representation av hur kunden interagerar med varumärket i olika kanaler.
   * [Identitetsnamnutrymmen](./namespaces.md): Identitetsnamnutrymmen är en komponent i identitetstjänsten som fungerar som indikatorer för det sammanhang som en identitet relateras till. De skiljer till exempel på värdet&quot;name<span>@email.com&quot; som e-postadress eller&quot;443522&quot; som ett numeriskt CRMID.
* [Katalogtjänst](../../catalog/home.md): Utforska datalinje, metadata, filbeskrivningar, kataloger och datauppsättningar i datasjön.
* [Datahygien](../../hygiene/home.md): Hantera dina lagrade konsumentdata genom att schemalägga utgångsdatum för automatiska datauppsättningar eller ta bort enskilda poster från en datauppsättning eller alla datauppsättningar.
* [Adobe Experience Platform Privacy Service](../../privacy-service/home.md): Hantera kundförfrågningar om åtkomst, avanmälan från försäljning eller borttagning av personuppgifter mellan Adobe Experience Cloud-program.
* [Kundprofil i realtid](../../profile/home.md): Tillhandahåller en enhetlig kundprofil i realtid baserad på aggregerade data från flera källor.

## Ta bort en identitet

Med en begäran om borttagning av en identitet kan du ta bort en identitet i ett diagram, vilket resulterar i att länkar som är kopplade till en enskild användaridentitet som är kopplad till ett identitetsnamnutrymme tas bort. Du kan använda mekanismer som tillhandahålls av [Privacy Service](../../privacy-service/home.md) för användningsfall som kundförfrågningar för borttagning av data och efterlevnad av sekretessbestämmelser som den allmänna dataskyddsförordningen (GDPR).

I avsnitten nedan beskrivs de mekanismer som du kan använda för att ta bort enstaka identiteter i Experience Platform.

### Ta bort en identitet i Privacy Servicen

Privacy Service behandlar kundförfrågningar om åtkomst, avanmälan från försäljning eller radering av personuppgifter enligt sekretessbestämmelser såsom Allmänna dataskyddsförordningen (GDPR) och California Consumer Privacy Act (CCPA). Med Privacy Service kan du skicka jobbbegäranden med API:t eller användargränssnittet. När Experience Platform tar emot en begäran om borttagning från Privacy Servicen skickar Platform en bekräftelse till Privacy Servicen om att begäran har tagits emot och att data som påverkas har markerats för borttagning. Borttagningen av den enskilda identiteten baseras på det angivna namnutrymmet och/eller ID-värdet. Dessutom tas alla sandlådor som är kopplade till en viss organisation bort. Mer information finns i handboken om [bearbetning av sekretessförfrågningar i identitetstjänsten](../privacy.md).

Tabellen nedan innehåller en beskrivning av borttagningen av enstaka identiteter i Privacy Servicen:

| Ta bort en identitet | Integritetstjänst |
| --- | --- |
| Godkända användningsfall | Endast förfrågningar om dataintegritet (GDPR, CCPA). |
| Beräknad fördröjning | Dagar till veckor |
| Tjänster som påverkas | Genom att ta bort en identitet i Privacy Service kan du välja om data ska tas bort från identitetstjänsten, kundprofilen i realtid eller datavjön. |
| Borttagningsmönster | Ta bort en identitet från identitetstjänsten. |

{style="table-layout:auto"}

## Borttagning av datauppsättning

I följande avsnitt beskrivs de mekanismer som kan användas för att ta bort datauppsättningar och associerade identitetslänkar i Experience Platform.

### Borttagning av datauppsättning i katalogtjänsten

Du kan använda katalogtjänsten för att skicka begäranden om borttagning av datauppsättningar. Mer information om hur du tar bort datauppsättningar med katalogtjänsten finns i guiden om att [ta bort objekt med hjälp av katalogtjänstens API](../../catalog/api/delete-object.md). Du kan också använda användargränssnittet för plattformen för att skicka begäranden om borttagning av datauppsättningar. Mer information finns i användarhandboken för [datauppsättningar](../../catalog/datasets/user-guide.md#delete-a-dataset).

### Utgångsdatum för datauppsättning i Datahygien

Med arbetsytan [[!UICONTROL Data Hygiene] ](../../hygiene/ui/overview.md) i Adobe Experience Platform-gränssnittet kan du schemalägga förfallodatum för datauppsättningar. När en datauppsättning når sitt förfallodatum startar datasjön, identitetstjänsten och kundprofilen i realtid separata processer för att ta bort datauppsättningens innehåll från sina respektive tjänster. Mer information finns i guiden om att [hantera förfallodatum för datauppsättningar med arbetsytan [!UICONTROL Data Hygiene]](../../hygiene/ui/dataset-expiration.md).

Tabellen nedan innehåller en beskrivning av skillnaderna mellan borttagning av datauppsättningar i katalogtjänsten och datahygien:

| Borttagning av datauppsättning | Katalogtjänst | Datahygien |
| --- | --- | --- |
| Godkända användningsfall | Ta bort fullständiga datauppsättningar och tillhörande identitetsinformation i Platform. | Hantering av data som lagras i Experience Platform. |
| Beräknad fördröjning | Dagar | Dagar |
| Tjänster som påverkas | Borttagning av datauppsättningar via katalogtjänsten tar bort data från identitetstjänsten, kundprofilen i realtid och datasjön. | Borttagning av datauppsättningar via datahygien tar bort data från identitetstjänsten, kundprofilen i realtid och datasjön. |
| Borttagningsmönster | Ta bort länkade identiteter från identitetstjänsten som upprättats av en viss datauppsättning. | Ta bort länkade identiteter från identitetstjänsten som upprättats av en viss datauppsättning, baserat på förfalloschema. |

{style="table-layout:auto"}

## Olika tillstånd för identitetsdiagram efter borttagning

Alla borttagningar av identitetsdiagram leder till att länkarna mellan två eller flera identiteter tas bort, enligt begäran om borttagning. Vid borttagning av datauppsättningar tas alla identitetslänkar som upprättats av den angivna datauppsättningen bort, men de kan ta bort identiteter från diagram. För enstaka identitetsavgränsningar tas identitetslänkar bort för den angivna identiteten och identitetsvärdet tas därför bort från alla identitetsdiagram. Identiteter utan en enda länkning till en annan identitet lagras inte i identitetstjänsten.

Nedan visas en översikt över de potentiella konsekvenser som borttagningar kan ha för identitetsgrafernas tillstånd.

| Identitetsdiagramstatus | Beskrivning |
| --- | --- |
| Delvis uppdatering | En partiell uppdatering av ett diagram inträffar när minst två identiteter förblir länkade i ett diagram efter att en borttagningsbegäran har bearbetats. Efter borttagningen kan de återstående identitetslänkarna vara anslutna till varandra eller delas upp i två eller flera separata diagram beroende på vilka identiteter som togs bort. |
| Fullständig borttagning | Ett diagram måste ha minst två länkade identiteter för att kunna finnas. Om en borttagningsbegäran leder till att alla befintliga länkar i ett diagram tas bort, tas diagrammet bort helt. |
| Ingen ändring | Ett diagram påverkas inte om en viss borttagningsbegäran innehåller en identitet eller datauppsättning som inte är associerad med någon medlem i diagrammet. Dessutom uppdateras inte ett diagram även om borttagningsbegäran tar bort en länk mellan en datauppsättning eller en kombination av identitetsdatauppsättning, eftersom länken upprättades av en annan länk som inte togs bort. Det innebär att om det finns en länk i två olika datauppsättningar kommer diagrammet inte att uppdateras eftersom bara en av datauppsättningarna tas bort. |

{style="table-layout:auto"}

## Nästa steg

Det här dokumentet innehåller de olika mekanismer som du kan använda för att ta bort identiteter och datauppsättningar på Experience Platform. I det här dokumentet beskrivs också hur identitets- och datauppsättningsborttagningar kan påverka identitetsdiagram. Mer information om identitetstjänsten finns i [Översikt över identitetstjänsten](../home.md).

<!--

You can use [Data hygiene](../hygiene/home.md) for data cleansing, removing anonymous data, or data minimization for the data that you have collected.

### Single identity deletion in the [!UICONTROL Data Hygiene] workspace

The [[!UICONTROL Data Hygiene] workspace](../hygiene/ui/overview.md) in the Platform UI allows you to delete consumer records that are participating in Identity Service and Real-Time Customer Profile. For a comprehensive guide on using the [!UICONTROL Data Hygiene] workspace, see the tutorial on [deleting consumer records](../hygiene/ui/record-delete.md).

The table below provides a breakdown of differences between single identity deletion in Privacy Service and Data hygiene:

| Single identity deletion | Privacy Service | Data hygiene |
| --- | --- | --- |
| Accepted use cases | Data privacy requests (GDPR, CCPA) only. | Management of data stored in Experience Platform. |
| Estimated latency | Days to weeks | Days |
| Services impacted | Single identity deletion in Privacy Service allows you to select whether data will be deleted from Identity Service, Real-Time Customer Profile, or data lake. | Single identity deletion in Data hygiene deletes the selected data across Identity Service, Real-Time Customer Profile, and data lake. |
| Deletion patterns | Delete an identity from Identity Service. | Delete an identity from Identity Service. |

-->
