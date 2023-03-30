---
title: Felmeddelanden för källor
description: Lär dig mer om de felmeddelanden du kan stöta på när du använder Flow Service för källor.
source-git-commit: 10edb5dfd9ce99b69cf5bb014f4903942c9bff3e
workflow-type: tm+mt
source-wordcount: '3192'
ht-degree: 0%

---

# Felmeddelanden för källor

Det här dokumentet innehåller en katalog med felmeddelanden, beskrivningar och förslag på lösningar för källor.

## Allmänna fel

| Felkod | Titel | Detaljerat meddelande |
| --- | --- | --- |
| `1000-400` | Felaktig begäran | Begäran är ogiltig. Kontrollera begäran och försök igen. |
| `1001-401` | Obehörig | Användaren är obehörig. Kontakta administratören för att få åtkomst till resursen. |
| `1002-403` | Förbjuden | Den begärda åtgärden är inte tillåten. Kontrollera den begärda åtgärden och försök igen. |
| `1003-404` | Resursen hittades inte | Det gick inte att hitta den begärda resursen. Kontrollera den angivna begäran och försök igen. |
| `1004-415` | Medietypen stöds inte | Angivet nyttolastformat stöds inte. Kontrollera din förfrågan och försök igen. |
| `1005-500` | Internt fel | Ett internt fel har inträffat. Försök igen och kontakta kundsupport om problemet kvarstår. |
| `1006-408` | Timeout för begäran | Ett fel uppstod när begäran bearbetades. Tidsgränsen för begäran har överskridits. Försök igen och kontakta kundsupport om problemet kvarstår. |
| `1007-400` | Ogiltig rubrikparameter | En ogiltig rubrikparameter: {headerName} har tagits emot. Kontrollera rubrikparametrarna och försök igen. |
| `1008-401` |  | Ogiltig auktoriseringstoken | Auktoriseringstoken har inte åtkomst till den här organisationen eller så finns inte organisationen. Kontrollera att organisationen finns eller kontakta administratören för att få åtkomst. |
| `1009-403` | ID för IMS-organisation saknas eller är tomt | Organisations-ID-begärandehuvudet saknas eller är tomt. Uppdatera rubrikvärdet och försök igen. |
| `1010-500` | Ogiltigt detaljmeddelande | Parametern i det detaljerade meddelandet har inte angetts korrekt. Kontrollera parametern i det detaljerade meddelandet och försök igen. |
| `1011-503` | Tjänsten är inte tillgänglig | Tjänsten är inte tillgänglig för tillfället. Försök igen och kontakta kundsupport om problemet kvarstår. |
| `1012-504` | Tidsgräns för gateway | En gateway-timeout har inträffat. Försök igen och kontakta kundsupport om problemet kvarstår. |
| `1013-412` | Förhandsvillkoret misslyckades | Villkoret som definieras av rubrikerna If-Unmodified-Since eller If-None-Match uppfylls inte. Kontrollera och försök igen. |
| `1014-400` | Ogiltig begäran Ogiltigt argument | Begäran kunde inte behandlas. {detailedMessage} |

## Ramverksfel

| Felkod | Titel | Detaljerat meddelande |
| --- | --- | --- |
| `1100-400` | Felaktig begäran | Begäran kunde inte behandlas. {detailedMessage} |
| `1101-500` | Internt fel | Ett internt fel har inträffat. Försök igen och kontakta kundsupport om problemet kvarstår. |
| `1102-404` | Resursen hittades inte | Det gick inte att hitta den begärda resursen. {detailedMessage} |
| `1103-503` | Tjänsten är inte tillgänglig | Tjänsten är inte tillgänglig för tillfället. Försök igen och kontakta kundsupport om problemet kvarstår. |
| `1104-504` | Tidsgräns för gateway | En gateway-timeout har inträffat. Försök igen och kontakta kundsupport om problemet kvarstår. |
| `1105-401` | Obehörig | Användaren är obehörig. {detailedMessage} |
| `1106-403` | Förbjuden | Den begärda åtgärden är inte tillåten. {detailedMessage} |
| `1107-412` | Förhandsvillkoret misslyckades | Villkoret som definieras av rubrikerna If-Unmodified-Since eller If-None-Match uppfylls inte. {detailedMessage} |

## Krypteringsfel

| Felkod | Titel | Detaljerat meddelande |
| --- | --- | --- |
| `1200-500` | Internt fel | Ett internt fel har inträffat. Försök igen och kontakta kundsupport om problemet kvarstår. |
| `1201-400` | Felaktig begäran | flowId får inte vara null eller tomt. Ange ett giltigt flowId i begäran och försök igen. |
| `1202-400` | Felaktig begäran | publicKeyId saknas i flödets transformations={transformations}. Ange publicKeyId i begäran och försök igen. |
| `1203-400` | Felaktig begäran | Krypteringsnyckeln finns inte mot keyID={keyID} i flödets transformations={transformations}. Kontrollera ditt nyckel-ID och försök igen. |
| `1204-400` | Felaktig begäran | Den angivna krypteringsalgoritmen är ogiltig. Ange en giltig krypteringsalgoritm och försök igen. |
| `1205-400` | Felaktig begäran | Lösenfrasen saknas i parameteravsnittet i den angivna begäran. Ange passPhrase i parametrar och försök igen. |

## REST API-fel

| Felkod | Titel | Detaljerat meddelande |
| --- | --- | --- |
| `1300-400` | Felaktig begäran | Korrigeringsanslutningsbegäran stöds inte för {connectorType}-kopplingen. Kontrollera den angivna begäran och försök igen. |
| `1301-400` | Felaktig begäran | Angiven authSpecType-parameter: {authSpecType} stöds inte. Ange en giltig autentiseringstyp och försök igen. |
| `1302-400` | Felaktig begäran | Angiven autentiseringstyp = {authType} stöds inte för koppling={connectorType}. Ange en giltig autentiseringstyp för den angivna kopplingen. |
| `1303-400` | Felaktig begäran | Det gick inte att koda URL:en med de angivna auth-parametrarna eftersom URL-kodning inte stöds för {value}. Kontrollera dina auth-parametrar och försök igen. |
| `1304-400` | Felaktig begäran | Det obligatoriska fältet {field} har inte angetts. Ange {field} och försök igen. |
| `1305-400` | Felaktig begäran | Den angivna anslutningstypen = {connectorType} stöds inte för den här åtgärden. |
| `1306-400` | Felaktig begäran | Målanslutningen kan inte vara null när målanslutningens spec-ID verifieras. Kontrollera den angivna begäran och försök igen. |
| `1307-400` | Felaktig begäran | Målanslutningens spec-ID är inte giltigt={targetConnectionSpecId}. Det tillåtna värdet är: `c604ff05-7f1a-43c0-8e18-33bf874cb11c`. |
| `1308-400` | Felaktig begäran | Begäran kunde inte behandlas. Felmeddelande: {msftErrorMessage} |
| `1309-400` | Felaktig begäran | Den angivna krypteringsomvandlingen är ogiltig eftersom {requiredParam} saknas i parametrarna. Ange {requiredParam} och försök igen. |
| `1310-400` | Felaktig begäran | Angivet publicKeyId i parametrarna har gått ut. Ange ett giltigt publicKeyId och försök igen. |
| `1311-400` | Felaktig begäran | Det publicKeyId som angetts i parametrar är ogiltigt. Ange ett giltigt publicKeyId och försök igen. |
| 1312-400 | Felaktig begäran | Det angivna parametervärdet {paramValue} är inte en giltig indata för egenskapen={requestParam}. Ange ett giltigt parametervärde och försök igen. |
| `1313-400` | Felaktig begäran | Sökvägsattributet {attribute} finns inte. Kontrollera att attributet finns och försök igen. |
| `1314-400` | Felaktig begäran | En komplex sökväg har angetts, men är inte tillåten. Kontrollera att ingen komplex sökväg har angetts och försök igen. |
| `1315-400` | Felaktig begäran | Den angivna sökvägen {path} ska peka på en array med poster. Kontrollera att den angivna sökvägen pekar på arkivmatrisen med poster och försök igen. |
| `1316-400` | Felaktig begäran | De angivna sidnumreringsparametrarna får inte vara tomma. Ange giltiga sidnumreringsparametrar och försök igen. |
| `1317-400` | Felaktig begäran | De angivna schemaparametrarna är tomma men får inte vara tomma. Ange giltiga schemaparametrar och försök igen. |
| `1318-400` | Felaktig begäran | {combinedMessage}. Kontrollera den angivna begäran och försök igen. |
| `1319-400` | Felaktig begäran | {param} ska ingå i den överordnade samlingen. Ange {param} i den överordnade samlingen och försök igen. |
| `1320-400` | Felaktig begäran | {idType} får inte vara null eller tom. Ange en giltig {idType} och försök igen. |
| `1321-400` | Felaktig begäran | Längden på {idType} ska vara en, den angivna storleken är {size}. Ange en giltig storlek och försök igen. |
| `1322-400` | Felaktig begäran | Källanslutningen får inte vara null för att skapa schemareferensen. Ange en giltig källanslutning och försök igen. |
| `1323-400` | Felaktig begäran | {entity} får inte vara null eller tom i källanslutningen: {sourceConnection}. Ange en giltig {entity} och försök igen. |
| `1324-400` | Felaktig begäran | Målanslutningen kan inte vara null när datauppsättnings-ID extraheras. Ange en giltig målanslutning och försök igen. |
| `1325-400` | Felaktig begäran | Parametern dataSetId får inte vara null eller tom i målanslutningen: {TargetConnection}. Ange en giltig dataSetId-parameter och försök igen. |
| `1326-400` | Felaktig begäran | Källanslutningen får inte vara null när källformatet hämtas. Ange en giltig källanslutning och försök igen. |
| `1327-400` | Felaktig begäran | Formatet för källdata som anges={sourceFormat} i SourceConnection stöds inte. Tillåtna värden är: {values}. Ange tillåtna värden och försök igen. |
| `1328-400` | Felaktig begäran | Mappningsomformningen kan inte vara null när {param} extraheras. Ange giltig mappningsomvandling och försök igen. |
| `1329-400` | Felaktig begäran | Param: {param} får inte vara null eller tom i den angivna begäran. Ange en giltig {param} och försök igen. |
| `1330-400` | Felaktig begäran | Inga kolumner hittades för tabellen {tableName}. Ange ett giltigt tabellnamn och försök igen. |
| `1331-400` | Felaktig begäran | Kolumnavgränsaren får inte innehålla fler än ett tecken i SourceConnection: {sourceConnection}. Ange en giltig kolumnavgränsare och försök igen. |
| `1332-400` | Felaktig begäran | Källanslutningsbegäran med connectionSpecId: {connectionSpecId} kan inte ha ett baseConnectionId. Ta bort baseConnectionId och försök igen. |
| `1333-400` | Dåliga krav | flowRunAction={flowRunAction} stöds inte för källa med spec id={specId}. Ange en giltig flödeskörningsåtgärd och försök igen. |
| `1334-400` | Felaktig begäran | Frågeparam: {param} får inte vara tom. Ange en giltig {param} och försök igen. |
| `1335-400` | Felaktig begäran | Ett fel uppstod när filterparametrarna för utforskande serialiserades. Kontrollera din filterparam-begäran och försök igen. |
| `1336-400` | Felaktig begäran | Utforska anslutningen stöds inte för anslutningsspec-ID: {connectionSpecId}. Ange det anslutningsspec-ID som stöds och försök igen. |
| `1337-400` | Felaktig begäran | {QueryParam} får inte vara tom för objectType={objectType}. Ange en giltig {QueryParam} och försök igen. |
| `1338-400` | Felaktig begäran | Anslutnings-ID:t {connectionType} får inte vara null i flowRequest. Ange ett giltigt anslutnings-ID för {connectionType} i flowRequest. |
| `1339-400` | Felaktig begäran | Formatet på organisationen={imsOrg} som angavs i begäran är ogiltigt. Ange ett giltigt organisations-ID och försök igen. |
| `1340-400` | Felaktig begäran | Ett fel uppstod när {time} parsades. Kontrollera tidsformatet i begäran och försök igen. |
| `1341-400` | Felaktig begäran | Angiven ODI Json är tom. Ange en giltig ODI Json och försök igen. |
| `1342-400` | Felaktig begäran | Dls:folder-segmentet i odi.json saknar definitioner. Ange lämpliga definitioner i &#39;odi.json&#39; och försök igen. |
| `1343-400` | Felaktig begäran | Både dls:entityReferences och dls:partitionSpec i odi.json saknar definitioner. Ange lämpliga definitioner i &#39;odi.json&#39; och försök igen. |
| `1344-400` | Felaktig begäran | Definitionen för dls:partitionSpec i odi.json är ogiltig eftersom fler än en partitionSpecics hittades. Ange lämpliga definitioner i &#39;odi.json&#39; och försök igen. |
| `1345-400` | Felaktig begäran | Definitioner saknas i ett eller flera segment i banor: &#39;dls:partitionSpec/dls:fileFormat&#39;, &#39;dls:partitionSpec/dls:partitionTemplate&#39;,&#39;dls:partitionSpec/dls:fileFormat/@type&#39;, &#39;dls:partitionSpec/dls:fileFormat/dls:csvDelimiters&#39; i &#39;odi.json&#39;. Ange lämpliga definitioner i &#39;odi.json&#39; och försök igen. |
| `1346-400` | Felaktig begäran | Definitionen &#39;@type&#39; i &#39;dls:fileFormat&#39; i &#39;odi.json&#39; är ogiltig. Ange lämpliga definitioner i &#39;odi.json&#39; och försök igen. |
| `1347-400` | Felaktig begäran | Definitionen dls:csvDelimiters i odi.json stöds inte. Följande csvDelimiters stöds: [&#39;,&#39;]. Ange lämpliga definitioner i &#39;odi.json&#39; och försök igen. |
| `1348-400` | Felaktig begäran | Ett fel uppstod vid deserialisering av dls:entityReferences. Kontrollera att data har ett giltigt format och försök igen. |
| `1349-400` | Felaktig begäran | De angivna filterparametrarna är ogiltiga. Ange giltiga filterparametrar och försök igen. |
| `1350-400` | Felaktig begäran | Ingen operator har angetts för filter vid källan. Ange en giltig filterbegäran med lämplig operator och försök igen. |
| `1351-400` | Felaktig begäran | Den angivna operatorn {operator} stöds inte för filter vid källan för den här kopplingen. Ange en giltig operator och försök igen. |
| `1352-400` | Felaktig begäran | Den angivna operatorn {operator} kan inte mappas till någon systemspecifik operator som stöds för {ql}. Ange en giltig operator och försök igen. |
| `1353-400` | Felaktig begäran | Filtret vid källan stöds ännu inte för {connectorType}-kopplingen. Kontrollera vilka anslutningar som stöds i dokumentationen: https://experienceleague.adobe.com/docs/experience-platform/sources/api-tutorials/filter.html. |
| `1354-400` | Felaktig begäran | Frågespråket {ql} stöds ännu inte för filter vid källan. Ange ett giltigt frågespråk och försök igen. |
| `1355-400` | Felaktig begäran | Den angivna filtertypen är ogiltig. Den filtertyp som stöds är: PQL. Ange en giltig filtertyp och försök igen. |
| `1356-400` | Felaktig begäran | Angivet filterformat är ogiltigt. Filterformatet som stöds är: pql/json. Ange ett giltigt filterformat och försök igen. |
| `1357-400` | Felaktig begäran | Det angivna filtret är ogiltigt. Värdet måste ha detaljerade filter. Ange ett giltigt filter och försök igen. |
| `1358-400` | Felaktig begäran | Den angivna parametern objectType är ogiltig. Ange en giltig objectType och försök igen. |
| `1359-400` | Felaktig begäran | Param {param} saknas i begäran. Ange en giltig {param} och försök igen. |
| `1360-400` | Felaktig begäran | Starttiden kan inte anges i det förflutna. Ange en giltig starttid och försök igen. |
| `1361-400` | Felaktig begäran | Intervall tillåts inte med engångsintag. Ta bort intervall eller ändra frekvens och försök sedan igen. |
| `1362-400` | Felaktig begäran | Intervallet får inte vara mindre än {minInterval}. Ange ett giltigt intervallvärde och försök igen. |
| `1363-400` | Felaktig begäran | Intervall {interval} tillåts inte med frekvens: {frequency}. Ange ett giltigt intervallvärde och försök igen. |
| `1364-400` | Felaktig begäran | Bakgrundsfyllningsflaggan tillåts inte när frekvensen är inställd på ett. Ta bort bakgrundsfyllningsflaggan när frekvensen är inställd på en gång och försök igen. |
| `1365-400` | Felaktig begäran | Sökvägen {path} som anges i ops är ogiltig. Ange en giltig sökväg {path} och försök igen. |
| `1366-400` | Felaktig begäran | Starttiden har passerat och uppdateringsåtgärden tillåts inte längre. |
| `1367-400` | Felaktig begäran | Deltakolumnen krävs vid kopieringsomvandling när en CRM-koppling skapas. Ange delta-kolumnen och försök igen. |
| `1368-400` | Felaktig begäran | Läge tillåts inte i flödesbegäran. Kontrollera din begäran och försök igen. |
| `1369-400` | Felaktig begäran | Deltakolumnen i kopieringsomformningen tillåts inte när frekvensen anges till en gång. Ta bort deltakolumnen och försök igen. |
| `1370-400` | Felaktig begäran | Det gick inte att hämta källkolumnerna för inmatning eftersom mappningsomvandlingen saknas. Lägg till mappningsomvandlingen och försök igen. |
| `1371-400` | Felaktig begäran | Identifieringen av filegenskaper stöds inte för {connectorType}-kopplingen. Ange filegenskaperna manuellt. |
| `1372-400` | Felaktig begäran | Den aktuella åtgärden tillåts inte. Utforska via anslutningsspecifikation tillåts inte för anslutningsspecifikation ID={connectionSpecId}. |
| `1373-400` | Felaktig begäran | flowSpecType saknas i begäran. Ange en giltig flowSpecType och försök igen. |
| `1374-400` | Felaktig begäran | De angivna frågeparametrarna är ogiltiga. Du kan inte ha flaggan determineProperties och användardefinierade egenskaper i samma begäran. Korrigera din begäran och försök igen. |
| `1375-400` | Felaktig begäran | Det gick inte att identifiera filegenskaperna. Ange egenskaper manuellt. |
| `1376-400` | Felaktig begäran | Identifieringen av filegenskaper stöds inte för anslutningsspec id={connectionSpecId}. Ange filegenskaperna manuellt. |
| `1377-400` | Felaktig begäran | Angiven värdeparam är null och kan inte jämföras med operatorn {operator}. Ange en giltig värdeparam och försök igen. |
| `1378-400` | Felaktig begäran | Det uppstod ett fel när indatakolumnen {column} verifierades för filter vid källan. Kolumnnamnet måste vara en giltig kolumn i tabellen. Ange ett giltigt kolumnnamn och försök igen. |
| `1379-400` | Felaktig begäran | Ett fel uppstod när indata {value} för filtret vid källan verifierades. Kolumnen DataType vid källan är {columnDataType} och värdet DataType [Sträng] matchar inte. Ange ett giltigt {value} och försök igen. |
| `1380-400` | Felaktig begäran | Det gick inte att skapa flödeskörning. Felmeddelande: {message} |
| `1381-400` | Felaktig begäran | WindowEndTime={endTime} får inte vara före Window StartTime={startTime}. Ange en giltig sluttid och försök igen. |
| `1382-400` | Felaktig begäran | Deltakolumnen ska matcha värdet i flödets Kopiera-omformningar. Ange en giltig delta-kolumn och försök igen. |
| `1383-400` | Felaktig begäran | Deltakolumnen saknas i de parametrar som tagits emot för att skapa en flödeskörning. Ange delta-kolumnen i parametrar och försök igen. |
| `1384-400` | Felaktig begäran | Parametrarna={params} som anges för att skapa flödeskörning är ogiltiga eller tomma. Ange giltiga parametrar och försök igen. |
| `1385-400` | Felaktig begäran | Angiven connectorType={connectorType} stöds inte för att skapa flödeskörningar. Ange en giltig connectorType och försök igen. |
| `1386-400` | Felaktig begäran | flowId={flowId} med scheduleParams frequency={frequency} stöds inte för att skapa flödeskörningar. Ange en giltig frekvens och försök igen. |
| `1387-400` | Felaktig begäran | flowRunId={flowRunId} är i ett ogiltigt tillstånd={state} för återutlösande åtgärder. Försök igen om en stund och kontakta kundsupport om problemet kvarstår. |
| `1388-400` | Felaktig begäran | Flödet={flow} är i tillståndet={state} och kan inte aktiveras igen. Flödet måste vara i aktiverat läge för att kunna aktiveras igen. |
| `1389-400` | Felaktig begäran | Ett fel uppstod när den tillhandahållna base64-kodade strängen parsades. Ange en giltig kodad filtersträng och försök igen. |
| `1390-400` | Felaktig begäran | Operatorn not kan inte ha fler än en jämförelse. Ange ett giltigt antal jämförelser och försök igen. |
| `1391-400` | Felaktig begäran | Det gick inte att parsa SchemaMetaData i sourceConnection för Id={sourceConnectionId}. Kontrollera schemaMetaData i din begäran och försök igen. |
| `1392-400` | Felaktig begäran | Det gick inte att parsa transformeringar i flödesbegäran för flowId={flowId}. Kontrollera omformningarna i din begäran och försök igen. |
| `1393-400` | Felaktig begäran | Den angivna parametern {parameter} är null eller tom. Ange en giltig {parameter} och försök igen. |
| `1394-400` | Felaktig begäran | Det lägsta värdet för en parameter, {parameter}, är ett. Ange en giltig {parameter} och försök igen. |
| `1395-400` | Felaktig begäran | Källanslutningen som hittades i flödet är antingen null eller tom. Ange en giltig källanslutning i flödet och försök igen. |
| `1396-400` | Felaktig begäran | Det gick inte att hitta något matchande format. Ange ett matchande format och försök igen. |
| `1397-400` | Felaktig begäran | Angiven frekvens: {frequency} är ogiltig. Ange en giltig frekvens och försök igen. |
| `1398-400` | Felaktig begäran | Den angivna åtgärden: {action} stöds inte. Kontrollera åtgärden och försök igen. |
| `1399-400` | Felaktig begäran | Det gick inte att hitta en giltig requestFileType. Ange en giltig requestFileType och försök igen. |
| `1400-400` | Felaktig begäran | Den angivna parametern templateType är ogiltig. Ange en giltig malltyp och försök igen. |
| `1401-400` | Felaktig begäran | Den angivna flödeskörningsåtgärden={flowRunAction} stöds inte. Ange en giltig flödeskörningsåtgärd och försök igen. |
| `1402-500` | Internt fel | Ett internt fel har inträffat. Försök igen och kontakta kundsupport om problemet kvarstår. |
| `1403-400` | Felaktig begäran | Starttiden har passerat och du kan inte längre ändra frekvensen till en gång. |
| `1404-400` | Felaktig begäran | Starttiden har passerat och du kan inte längre uppdatera bakåtfyllnad. |

## Undantag för flödestjänst (1600-1699)

| Felkod | Titel | Detaljerat meddelande |
| --- | --- | --- |
| `1600-400` | Felaktig begäran | Begäran kunde inte behandlas. {detailedMessage} |
| `1601-500` | Internt fel | Ett internt fel har inträffat. Försök igen och kontakta kundsupport om problemet kvarstår. |
| `1602-404` | Resursen hittades inte | Det gick inte att hitta den begärda resursen. {detailedMessage} |
| `1603-503` | Tjänsten är inte tillgänglig | Tjänsten är inte tillgänglig för tillfället. Försök igen. Kontakta kundsupport om problemet kvarstår. |
| `1604-504` | Tidsgräns för gateway | En gateway-timeout har inträffat. Försök igen. Kontakta kundsupport om problemet kvarstår. |
| `1605-401` | Obehörig | Användaren är obehörig. {detailedMessage} |
| `1606-403` | Förbjuden | Den begärda åtgärden är inte tillåten. {detailedMessage} |
| `1607-412` | Förhandsvillkoret misslyckades | Villkoret som definieras av rubrikerna If-Unmodified-Since eller If-None-Match uppfylls inte. {detailedMessage} |

## Fel i datallandningszon

| Felkod | Titel | Detaljerat meddelande |
| --- | --- | --- |
| `1700-500` | Internt fel | Ett internt fel har inträffat. Försök igen och kontakta kundsupport om problemet kvarstår. |
| `1701-400` | Felaktig begäran | Den angivna landningszonen är inaktiv. Aktivera landningszonen och försök igen. |
| `1702-400` | Felaktig begäran | SAS-typen={sasType} som anges för landningszonen tillåts inte. Ange en giltig SAS och försök igen. |
| `1703-400` | Felaktig begäran | Det är inte tillåtet att uppdatera autentiseringsuppgifter. |
| `1704-400` | Felaktig begäran | Nycklarna som returnerades för storageAccountName={accountName} i subscriptionId={subscriptionId} och resourceGroupName={resourceGroupName} har fel format. Kontrollera din begäran och försök igen. Kontakta supporten om problemet kvarstår. |
| `1705-400` | Felaktig begäran | Angiven åtgärd för datalandningszon stöds inte. Ange en giltig åtgärd och försök igen. |
| `1706-400` | Felaktig begäran | Konfigurationen för tillåtna aktiveringar är inte korrekt konfigurerad för landningszon={landingZoneType}. Försök igen och kontakta kundsupport om problemet kvarstår. |
| `1707-400` | Felaktig begäran | Det gick inte att starta tjänsten eftersom landningszonens konfiguration inte får vara null eller tom. Kontrollera att landningszonens konfiguration inte är null och försök igen. |
| `1708-400` | Felaktig begäran | Behållarkonfigurationen får inte vara null i landingZoneType={landingZoneType}. Kontrollera att behållarkonfigurationen inte är null och försök igen. |
| `1709-400` | Felaktig begäran | SAS-informationen får inte vara null för {tokenConfig} i landingZoneType={landingZoneType}. Ange en giltig SAS i konfigurationen och försök igen. |
| `1710-400` | Felaktig begäran | Angiven landningszon av typen: {landingZoneUseCase} stöds inte. Ange en giltig landningszonstyp och försök igen. |
| `1711-400` | Felaktig begäran | SAS-informationen hittades inte för den angivna datalandningszonen av typen: {landingZoneUseCase}. Kontrollera om SAS-information finns för den angivna landningszonstypen. |
| `1712-400` | Felaktig begäran | Angiven åtgärd för landningszon: {actionType} tillåts inte. Ange en giltig åtgärd för datalandningszon och försök igen. |
| `1713-400` | Felaktig begäran | {OperationType} tillåts inte för angiven {tokenType}. Kontrollera din begäran och försök igen. |
| `1714-400` | Felaktig begäran | clientId={clientId} får inte utföra den här åtgärden. Kontrollera din begäran med behörigheter och försök igen. |