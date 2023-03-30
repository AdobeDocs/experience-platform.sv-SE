---
title: Felmeddelanden för flödestjänst
description: Lär dig mer om de felmeddelanden du kan stöta på när du använder Flow Service för källor.
source-git-commit: 10edb5dfd9ce99b69cf5bb014f4903942c9bff3e
workflow-type: tm+mt
source-wordcount: '1698'
ht-degree: 0%

---

# Felmeddelanden för Flow Service

Flow Service används för att samla in och centralisera kunddata från olika källor inom Platform. Tjänsten tillhandahåller ett användargränssnitt och RESTful API som gör att du enkelt kan konfigurera källanslutningar till olika dataleverantörer. Dessa källanslutningar gör att du kan autentisera dina tredjepartssystem, ange tider för att få tillgång till dem och hantera dataöverföringshastigheten.

Det här dokumentet innehåller en katalog med felmeddelanden, beskrivningar och förslag på lösningar för Flow Service.

## Internt valideringsfel i Flow Service

I följande tabell visas felen gällande intern validering i Flow Service.

| Felkod | Titel | Detaljerat meddelande |
| --- | --- | --- |
| `1100-400` | Ogiltig begäran | Begäran kunde inte behandlas. Fel från flödesprovider: Inte berättigad till den här åtgärden. |
| `1101-404` | Resursen hittades inte | Det gick inte att hitta den begärda resursen. Fel från flödesprovider: Resursen med angivet ID finns inte. |
| `1102-500` | Internt fel | Ett internt fel har inträffat. Försök igen. Kontakta kundsupport om problemet kvarstår. |
| `1103-503` | Tjänsten är inte tillgänglig | Tjänsten är inte tillgänglig för tillfället. Försök igen. Kontakta kundsupport om problemet kvarstår. |
| `1104-504` | Tidsgräns för gateway | En gateway-timeout har inträffat. Försök igen. Kontakta kundsupport om problemet kvarstår. |
| `1400-500` | Internt fel | Ett internt fel har inträffat. Försök igen. Kontakta kundsupport om problemet kvarstår. |
| `1401-400` | Ogiltig begäran | Parametrarna limit och count kan inte anges tillsammans i samma begäran. Ange antingen bara gräns- eller räkningsparametern och försök igen. |
| `1402-400` | Ogiltig begäran | Åtgärden &quot;finalize&quot; stöds bara för providerbegäranden. |
| `1403-400` | Huvudet saknas | Rubriken If-Match saknas i begäran. Ange rubriken och försök igen. |
| `1404-412` | Versionen matchar inte | Den angivna versionen v1 matchar inte den aktuella versionen på entiteten cc01fc2c-0000-0200. Kontrollera att den angivna versionen matchar den aktuella versionen för entiteten och försök igen. |
| `1405-400` | Ogiltig begäran | Begärandetexten får inte vara null eller tom. Ange en begärandetext och försök igen. |
| `1406-400` | Ogiltig begäran | Det går inte att använda underåtgärden progress med andra underåtgärder. Uppdatera listan över underåtgärder och försök igen. |
| `1407-400` | Ogiltig begäran | Statusen misslyckades kan inte användas med `progress` subOp. Ta bort `progress` subOp eller använd status=&#39;inProgress&#39; och försök igen. |
| `1408-400` | Ogiltig begäran | Procent slutfört ska vara 100 för slutförda eller misslyckade lägen. Uppdatera procentandelen färdigt och försök igen. |
| `1409-400` | Ogiltig begäran | Det går inte att använda åtgärden &#39;finalize&#39; i det aktuella läget. Uppdatera åtgärden och försök igen. |
| `1410-400` | Ogiltig begäran | `State` tillåts inte i begäran om att skapa flöde. |
| `1411-400` | Ogiltig begäran | Det gick inte att hämta entityId. Ogiltig begäran togs emot med sökvägen baseConnections/123. |
| `1412-400` | Ogiltig begäran | Ogiltig mappningsversion i begäran. Ange korrekt mappningsversion. |
| `1413-400` | Ogiltig begäran | Angivet spec-ID är ogiltigt. Ange ett giltigt spec-ID och försök igen. |
| `1414-400` | Ogiltig begäran | Det går inte att uppdatera anslutningsspecifikationen för en anslutning. |
| `1415-400` | Ogiltig begäran | Det gick inte att hitta auth-specifikationen authConnection för anslutningsspecifikationen ID ba6e206f-f233-ab16. |
| `1416-400` | Ogiltig begäran | Det går endast att använda Delete eller Update för anslutning med aktiverat, inaktiverat eller initierat läge. |
| `1417-400` | Ogiltig begäran | Ta bort eller uppdatera anslutningar i `initializing` tillstånd tillåts inte med UserToken. |
| `1418-400` | Ogiltig begäran | Det går inte att ta bort basanslutningen med ID 35dcaad3-122a-4278 eftersom basanslutningen används i ett eller flera flöden. Se till att motsvarande flöden tas bort innan du tar bort en basanslutning. |
| `1419-400` | Ogiltig begäran | Fel vid validering av mappning med ID 45d90285d2d249acb87a72a2f12f7401, version 0. Detta kan bero på otillräcklig behörighet för mappade fält. Kontrollera mappningen eller kontakta administratören. |
| `1420-400` | Ogiltig begäran | Det går inte att uppdatera den aktuella inaktiveringsstatusen. |
| `1421-400` | Ogiltig begäran | Det går inte att övergå till den aktuella statusuppdateringen. |
| `1422-400` | Ogiltig begäran | Inaktiveringen av åtgärden kan inte tillämpas på det aktuella läget {state}. Uppdatera åtgärden och försök igen. |
| `1423-400` | Ogiltig begäran | Ett ohanterat field baseSpec angavs i ConnectionSpecFiltering. Uppdatera fältet {field} och försök igen. |
| `1424-400` | Ogiltig begäran | OrderBy stöds inte med korssandlådefråga. |
| `1425-400` | Ogiltig begäran | Ett fel uppstod vid matchning av schema i måldatauppsättningen 64ef1a3c0ef med schema i mappningen 91ac5a2c0eb. Schema med samma ID och version måste användas i både mappnings- och måldatamängd. |
| `1426-400` | Ogiltig begäran | Användartoken har inte behörighet att skapa/uppdatera anslutningsspecifikationen. Kontrollera att användarens token är auktoriserad och försök igen. |
| `1427-400` | Ogiltig begäran | Användartoken har inte behörighet att skapa/uppdatera flödeskörningar. Kontrollera att användarens token är auktoriserad och försök igen. |
| `1428-400` | Ogiltig begäran | Predecessor flow run not found with id aa6a206f-f233-4c2d. |
| `1429-400` | Ogiltig begäran | Det gick inte att hitta föregående flöde med ID a6a206f-f233-4c2d. |
| `1430-400` | Ogiltig begäran | Flödet hittades inte med ID a6a206f-f233-4c2d. |
| `1431-400` | Ogiltig begäran | En tom matris av typen &quot;fields&quot; tillåts inte i principen. |
| `1432-400` | Ogiltig begäran | Den angivna sorteringsordningen är inte korrekt, använd + för stigande ordning och - för fallande ordning i fieldName. |
| `1433-400` | Ogiltig begäran | Felaktigt fält= #id skickades i orderBy. Exempel är +name, -name, name. |
| `1434-400` | Ogiltig begäran | Åtgärden move stöds inte. Använd någon av de åtgärdstyper som stöds och försök igen. |
| `1435-400` | Ogiltig begäran | Underåtgärden &#39;reverse&#39; som inte stöds har tagits emot. Använd någon av underåtgärdstyperna som stöds och försök igen. |
| `1436-400` | Ogiltig begäran | En PROGRESS som inte stöds togs emot för aktivering av åtgärd. |
| `1437-400` | Ogiltig begäran | Statusvärdet &#39;started&#39; som inte stöds har tagits emot. Uppdatera statusvärdet och försök igen. |
| `1438-400` | Ogiltig begäran | Samlingsåtgärden Average som inte stöds har tagits emot. |
| `1439-400` | Resursen hittades inte | Den begärda flödesresursen 3f4ae131-b384-4e73 hittades inte. Kontrollera resurs-ID:t innan du försöker igen. |
| `1440-400` | Ogiltig begäran | Operatorn &#39;~&#39; är inte implementerad. |
| `1441-400` | Ogiltig begäran | Sammanställningsfunktionen Average har inte implementerats. |
| `1442-400` | Ogiltig begäran | Aggregering tillåts inte för fält-ID. |
| `1443-400` | Ogiltig begäran | Operatorn &#39;&lt;=&#39; tillåts inte för flera värden. |
| `1444-400` | Ogiltig begäran | Flödet 3f4ae131-b384-4e73 är inte i det förväntade tillståndet som väntar. |
| `1445-400` | Ogiltig begäran | Anslutningsfunktionen PATCH är inte aktiverad. |
| `1446-400` | Ogiltig begäran | Flödes-ID:t får inte vara null eller tomt. Uppdatera flödes-ID och försök igen. |
| `1447-400` | Ogiltig begäran | Aktiva flöden med ID a6a206f-f233-4c2d hittades. |
| `1448-400` | Ogiltig begäran | Operator >= stöds inte för fält-ID. |
| `1449-400` | Ogiltig begäran | Ogiltiga fältanslutningar i filterparametrar. |
| `1450-400` | Ogiltig begäran | Ogiltig operator!> i filterparametrar. |
| `1451-400` | Ogiltig begäran | Ogiltiga parametrar för testParam har angetts i frågeparametrar. |
| `1452-400` | Ogiltig begäran | Ogiltigt värde 1676643256,1676643210 för fältet createdAt. |
| `1453-400` | Ogiltig begäran | Ogiltigt frågevärde skapatAt== angivet i frågeparam. |
| `1454-400` | Ogiltig begäran | En ohanterad filtervärdetyp har angetts. |
| `1455-400` | Ogiltig begäran | Ett fel uppstod vid validering av korrigeringsinstruktionerna: Fältet &quot;keyThatDoesNotExist&quot; saknas. |
| `1456-400` | Ogiltig begäran | Borttagning av tillstånd är inte ett giltigt värde. Tillåtna värden är [aktiverad, inaktiverad, initiera]. |
| `1457-400` | Ogiltig begäran | Det går inte att använda åtgärdsuppdatering när läget har tagits bort. |
| `1458-400` | Ogiltig begäran | Det går inte att använda borttagning av åtgärd i lägets borttagning-slutförande. |

{style="table-layout:auto"}


## Verifieringsfel för användartoken för auktorisering

I följande tabell visas felen gällande verifiering av användartoken för auktorisering

| Felkod | Titel | Detaljerat meddelande |
| --- | --- | --- |
| `2000-401` | Ogiltig auktoriseringstoken | Auktoriseringstoken har inte åtkomst till den här organisationen eller så finns inte organisationen. Kontrollera att organisationen finns eller kontakta administratören för att få åtkomst. |
| `2001-401` | Huvudet saknas eller är tomt | Rubriken x-gw-ims-org-id saknas eller är tom. Uppdatera rubrikvärdet och försök igen. |
| `2002-401` | Huvudet saknas | Rubriken x-gw-ims-org-id saknas i begäran. Uppdatera rubrikvärdet och försök igen. |
| `2100-404` | Sandlådan hittades inte | Det gick inte att hitta sandlådan med namnet &#39;dev&#39;. Kontrollera att namnet på sandlådan är korrekt och försök igen. |
| `2101-404` | Sandlådan hittades inte | Det gick inte att hitta sandlådan med namnet &#39;dev&#39;. Fel från API:t för sandlådehantering: Sandlådan med namnet &#39;dev&#39; finns inte. Kontrollera om resursen finns. |
| `2102-500` | Hämta sandlåda efter namnfel | Det gick inte att hämta en sandlåda med namnet &#39;dev&#39;. Fel från API:t för sandlådehantering: Något gick fel. Försök igen. |
| `2103-404` | Sandlådan hittades inte | Det gick inte att hitta sandlådan med ID 8da3ef09-b469-404a och name dev. Kontrollera att ID- och sandlådenamnvärdena är korrekta och försök igen. |
| `2104-500` | Hämta sandlåda efter identifierarfel | Ett problem uppstod när en sandlåda med ID &#39;8da3ef09-b469-404a&#39; och namnet &#39;dev&#39; skulle hämtas. Fel från API:t för sandlådehantering: Något gick fel. Försök igen. |
| `2105-400` | Huvudet saknas | Rubriken x-sandbox-name saknas i begäran. Lägg till rubriken i begäran och försök igen. |
| `2106-404` | Hämta standardsandlådefel | Det gick inte att hitta standardinformationen för sandlådan. |
| `2107-500` | Hämta standardsandlådefel | Det gick inte att hämta en standardsandlåda. Fel från API:t för sandlådehantering: Något gick fel. Försök igen. |
| `2108-500` | Hämta fel för aktiva sandlådor | Det gick inte att hämta en aktiv sandlåda. Fel från API:t för sandlådehantering: Något gick fel. Försök igen. |
| `2110-400` | Rubriker tillåts inte | Rubriken x-sandbox-id tillåts inte med användartoken. Uppdatera sidhuvudet och försök igen. |
| `2111-403` | Rubriker med begränsat värde | Rubriken x-sandbox-name med värdet * är begränsad med användar-token. Uppdatera rubriken och värdet och försök igen. |
| `2112-400` | Rubriker med ett annat värde tillåts inte | Båda rubrikerna x-sandbox-name och x-sandbox-id måste ha värdet * för korsfrågor. Uppdatera rubrikerna och försök igen. |
| `2113-400` | Rubriker med ett värde tillåts inte | Rubrikerna x-sandbox-id och x-sandbox-name med värdet * tillåts inte för begäran. Uppdatera rubrikerna och försök igen. |
| `2114-400` | Tom token | En tom token har angetts. Ange en token och försök igen. |
| `2115-400` | Ogiltig token | Ogiltig token har angetts. Ange en giltig token och försök igen. |
| `2116-500` | Internt fel | Ett internt fel uppstod vid offlineavkodning av innehavartoken för omfångsupplösning. |
| `2117-500` | Internt fel | Ett internt fel uppstod när behörighetskontrollen för användaren kontrollerades. Försök igen. Kontakta kundsupport om problemet kvarstår. |
| `2118-403` | Behörighet saknas | Behörighetsskrivningen saknas. Kontakta administratören för att lösa behörigheterna och försök igen. |
| `2119-400` | Frågeparametern saknas | Begärandekontexten innehåller inte den obligatoriska frågeparametern specId. Ange den saknade frågeparametern och försök igen. |
| `2120-403` | Förbjuden | Du har inte tillräcklig behörighet för att utföra åtgärden. Kontakta administratören för att lösa behörigheterna och försök igen. |
| `2121-403` | Förbjuden | Behörighetshanteraren nekas för resursens Enterprise Source. Kontakta administratören för att lösa behörigheterna och försök igen. |
| `2200-500` | Fel vid begäran om extern tjänst | Ett problem uppstod när katalogtjänsten anropades för att verifiera schemat. |
| `2250-500` | Fel vid begäran om extern tjänst | Det uppstod ett problem när tjänsten Data Prep anropades för validering av mappningen. |

{style="table-layout:auto"}
