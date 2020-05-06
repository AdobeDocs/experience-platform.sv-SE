---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Felsökning av direktuppspelning
topic: troubleshooting
translation-type: tm+mt
source-git-commit: 0eecd802fc8d0ace3a445f3f188a7f095b97d0c8
workflow-type: tm+mt
source-wordcount: '1046'
ht-degree: 0%

---


# Felsökningsguide för direktuppspelning

Det här dokumentet ger svar på vanliga frågor om direktuppspelning på Adobe Experience Platform. Om du har frågor och felsökning som rör andra plattformstjänster, inklusive de som hittas i alla plattforms-API:er, kan du läsa felsökningsguiden för [Experience Platform](../../landing/troubleshooting.md).

Adobe Experience Platform Data Inghit tillhandahåller RESTful-API:er som ni kan använda för att importera data till Experience Platform. Inkapslade data används för att uppdatera enskilda kundprofiler i nära realtid, så att ni kan leverera personaliserade, relevanta upplevelser över flera kanaler. Läs översikten över [](../home.md) datainmatning om du vill ha mer information om tjänsten och de olika användningsmetoderna. Anvisningar om hur du använder API:er för direktuppspelning av inmatning finns i översikten över [direktuppspelning](../streaming-ingestion/overview.md).

## Vanliga frågor

Nedan följer en lista med svar på vanliga frågor om direktuppspelning.

### Hur vet jag att nyttolasten jag skickar är korrekt formaterad?

Datainmatning utnyttjar XDM-scheman (Experience Data Model) för att validera formatet för inkommande data. Om du skickar data som inte följer strukturen i ett fördefinierat XDM-schema, kommer det att leda till att importen misslyckas. Mer information om XDM och hur det används i Experience Platform finns i [XDM-systemöversikten](../../xdm/home.md).

Direktuppspelningsinmatning har stöd för två valideringslägen: synkron och asynkron. Varje verifieringsmetodhanterare misslyckades med data på olika sätt.

**Synkron validering** bör användas under utvecklingsprocessen. Poster som inte godkänns vid validering tas bort och returnerar ett felmeddelande om varför de misslyckades (till exempel: &quot;Ogiltigt XDM-meddelandeformat&quot;).

**Asynkron validering** ska användas i produktionen. Alla felformaterade data som inte godkänns vid validering skickas till datasjön som en misslyckad batchfil, där de kan hämtas senare för ytterligare analys.

Mer information om synkron och asynkron validering finns i [översikt](../quality/streaming-validation.md)över direktuppspelningsvalidering. Anvisningar om hur du visar batchar som inte kan valideras finns i guiden om hur du [hämtar misslyckade batchar](../quality/retrieve-failed-batches.md).

### Kan jag validera nyttolasten för en begäran innan jag skickar den till plattformen?

Nyttolaster för begäranden kan bara utvärderas efter att de har skickats till plattformen. Vid synkron validering returnerar giltiga nyttolaster ifyllda JSON-objekt medan ogiltiga nyttolaster returnerar felmeddelanden. Under asynkron validering upptäcker och skickar tjänsten alla felformaterade data till datasjön där de senare kan hämtas för analys. Mer information finns i [verifieringsöversikten](../quality/streaming-validation.md) för direktuppspelning.

### Vad händer när synkron validering begärs på en kant som inte stöder det?

Om synkron validering inte stöds för den begärda platsen returneras ett 501-felsvar. Mer information om synkron validering finns i [strömningsvalideringsöversikten](../quality/streaming-validation.md) .

### Hur ser jag till att data bara samlas in från betrodda källor?

Experience Platform har stöd för säker datainsamling. När autentiserad datainsamling är aktiverad måste klienterna skicka en JSON Web Token (JWT) och deras IMS Organization ID som begärandehuvuden. Mer information om hur du skickar autentiserade data till Platform finns i guiden om [autentiserad datainsamling](../tutorials/create-authenticated-streaming-connection.md).

### Vilken fördröjning har direktuppspelning av data till kundprofilen i realtid?

Direktuppspelade händelser återspeglas i allmänhet i kundprofilen i realtid på mindre än 60 sekunder. Faktiska latenser kan variera beroende på datavolym, meddelandestorlek och bandbreddsbegränsningar.

### Kan jag inkludera flera meddelanden i samma API-begäran?

Du kan gruppera flera meddelanden inom en och samma nyttolast för begäran och strömma dem till plattformen. När det används på rätt sätt är gruppering av flera meddelanden i en enda begäran ett utmärkt sätt att optimera dataåtgärderna. Läs självstudiekursen om hur du [skickar flera meddelanden i en begäran](../tutorials/streaming-multiple-messages.md) om mer information.

### Hur vet jag om de data jag skickar tas emot?

Alla data som skickas till plattformen (utan fel eller på annat sätt) lagras som gruppfiler innan de lagras i datauppsättningar. Batchernas bearbetningsstatus visas i den datauppsättning de skickades till.

Du kan verifiera om data har importerats korrekt genom att kontrollera datauppsättningsaktiviteten med användargränssnittet [för](https://platform.adobe.com)Experience Platform. Klicka på **Datauppsättningar** till vänster för att visa en lista med datauppsättningar. Markera den datauppsättning som du direktuppspelar till i den lista som visas för att öppna aktivitetssidan för *datauppsättningen* och visa alla batchar som har skickats under en vald tidsperiod. Mer information om hur du använder Experience Platform för att övervaka dataströmmar finns i guiden om [övervakning av dataflöden](../quality/monitor-data-flows.md)för direktuppspelning.

Om dina data inte kunde importera och du vill återställa dem från Platform, kan du hämta de misslyckade batcharna genom att skicka deras ID:n till API:t för [dataåtkomst][Data Access Service API]. Mer information finns i guiden om hur du [hämtar misslyckade batchar](../quality/retrieve-failed-batches.md) .

### Varför är mina strömmande data inte tillgängliga i datasjön?

Det finns många orsaker till varför batchimporten inte kan nå datasjön, till exempel ogiltig formatering, saknade data eller systemfel. Om du vill ta reda på varför din batch misslyckades måste du hämta gruppen med API:t för [datainmatningstjänsten][Data Ingestion Service] och visa information om den. Detaljerade steg för hur du hämtar en misslyckad batch finns i guiden om hur du [hämtar misslyckade batchar](../quality/retrieve-failed-batches.md).

### Hur tolkar jag det svar som returnerats för API-begäran?

Du kan tolka ett svar genom att först kontrollera serverns svarskod för att avgöra om din begäran accepterades. Om en svarskod returneras kan du granska `responses` arrayobjektet för att fastställa statusen för uppgiften att få en fråga.

En slutförd API-begäran med ett meddelande returnerar statuskoden 200. En slutförd (eller delvis slutförd) API-begäran för gruppmeddelanden returnerar statuskod 207.

Följande JSON är ett exempelsvarsobjekt för en API-begäran med två meddelanden: ett lyckades och ett misslyckades. Meddelanden som kan direktuppspelas returnerar en `xactionId` egenskap. Meddelanden som inte direktuppspelas returnerar en `statusCode` egenskap och ett svar `message` med mer information.

```JSON
{
    "inletId": "9b0cb233972f3b0092992284c7353f5eead496218e8441a79b25e9421ea127f5",
    "batchId": "1565638336649:1750:244",
    "receivedTimeMs": 1565638336705,
    "responses": [
        {
            "xactionId": "1565650704337:2124:92:3"
        },
        {
            "statusCode": 400,
            "message": "inletId: [9b0cb233972f3b0092992284c7353f5eead496218e8441a
                79b25e9421ea127f5] 
                imsOrgId: [{IMS_ORG}] 
                Message has unknown xdm format"
        }
    ]
}
```

### Varför tas inte mina skickade meddelanden emot av kundprofilen i realtid?

Om kundprofilen i realtid avvisar ett meddelande beror det troligtvis på felaktig identitetsinformation. Detta kan bero på att ett ogiltigt värde eller namnutrymme har angetts för en identitet.

Det finns två typer av identitetsnamnutrymmen: standard och anpassad. När du använder anpassade namnutrymmen måste du kontrollera att namnutrymmet har registrerats i identitetstjänsten. Mer information om hur du använder standardnamnutrymmen och anpassade namnutrymmen finns i Översikt över [](../../identity-service/namespaces.md) identitetsnamn.

Du kan använda användargränssnittet [för](https://platform.adobe.com) Experience Platform för att få mer information om varför ett meddelande inte kunde hämtas. Klicka på **Övervakning** i den vänstra navigeringen och visa sedan fliken _Direktuppspelning från början till slut_ för att se meddelandebatchar som direktuppspelats under en viss tidsperiod.