---
keywords: Experience Platform;home;popular topics;streaming
solution: Experience Platform
title: Felsökning av direktuppspelning
topic: troubleshooting
translation-type: tm+mt
source-git-commit: bf99b08a1093a815687cc06372407949e170a0b3
workflow-type: tm+mt
source-wordcount: '987'
ht-degree: 0%

---


# Felsökningsguide för direktuppspelning

Det här dokumentet innehåller svar på vanliga frågor om direktuppspelning på Adobe Experience Platform. Om du har frågor och felsökning som rör andra [!DNL Platform] tjänster, inklusive de som hittas i alla [!DNL Platform] API:er, kan du läsa felsökningsguiden [för](../../landing/troubleshooting.md)Experience Platform.

Adobe Experience Platform [!DNL Data Ingestion] tillhandahåller RESTful-API:er som du kan använda för att importera data till [!DNL Experience Platform]. Inkapslade data används för att uppdatera enskilda kundprofiler i nära realtid, så att ni kan leverera personaliserade, relevanta upplevelser över flera kanaler. Läs översikten över [](../home.md) datainmatning om du vill ha mer information om tjänsten och de olika användningsmetoderna. Anvisningar om hur du använder API:er för direktuppspelning av inmatning finns i översikten över [direktuppspelning](../streaming-ingestion/overview.md).

## Vanliga frågor och svar 

Nedan följer en lista med svar på vanliga frågor om direktuppspelning.

### Hur vet jag att nyttolasten jag skickar är korrekt formaterad?

[!DNL Data Ingestion] använder [!DNL Experience Data Model] XDM-scheman för att validera formatet för inkommande data. Om du skickar data som inte följer strukturen i ett fördefinierat XDM-schema, kommer det att leda till att importen misslyckas. Mer information om XDM och hur det används i [!DNL Experience Platform]finns i [XDM-systemöversikten](../../xdm/home.md).

Direktuppspelningsinmatning har stöd för två valideringslägen: synkron och asynkron. Varje verifieringsmetodhanterare misslyckades med data på olika sätt.

**Synkron validering** bör användas under utvecklingsprocessen. Poster som inte godkänns vid validering tas bort och returnerar ett felmeddelande om varför de misslyckades (till exempel: &quot;Ogiltigt XDM-meddelandeformat&quot;).

**Asynkron validering** ska användas i produktionen. Alla felformaterade data som inte godkänns vid validering skickas till användaren [!DNL Data Lake] som en misslyckad batchfil, där de kan hämtas senare för ytterligare analys.

Mer information om synkron och asynkron validering finns i [översikt](../quality/streaming-validation.md)över direktuppspelningsvalidering. Anvisningar om hur du visar batchar som inte kan valideras finns i guiden om hur du [hämtar misslyckade batchar](../quality/retrieve-failed-batches.md).

### Kan jag validera nyttolasten för en begäran innan jag skickar den till [!DNL Platform]?

Nyttolaster för begäranden kan bara utvärderas efter att de har skickats till [!DNL Platform]. Vid synkron validering returnerar giltiga nyttolaster ifyllda JSON-objekt medan ogiltiga nyttolaster returnerar felmeddelanden. Under asynkron validering upptäcker och skickar tjänsten alla felformaterade data till den plats där de senare kan hämtas för analys [!DNL Data Lake] . Mer information finns i [verifieringsöversikten](../quality/streaming-validation.md) för direktuppspelning.

### Vad händer när synkron validering begärs på en kant som inte stöder det?

Om synkron validering inte stöds för den begärda platsen returneras ett 501-felsvar. Mer information om synkron validering finns i [strömningsvalideringsöversikten](../quality/streaming-validation.md) .

### Hur ser jag till att data bara samlas in från betrodda källor?

[!DNL Experience Platform] har stöd för säker datainsamling. När autentiserad datainsamling är aktiverad måste klienterna skicka en JSON Web Token (JWT) och deras IMS Organization ID som begärandehuvuden. Mer information om hur du skickar autentiserade data till [!DNL Platform]finns i guiden om [autentiserad datainsamling](../tutorials/create-authenticated-streaming-connection.md).

### Vilken fördröjning har strömmande data för [!DNL Real-time Customer Profile]?

Direktuppspelade händelser återspeglas i allmänhet på [!DNL Real-time Customer Profile] mindre än 60 sekunder. Faktiska latenser kan variera beroende på datavolym, meddelandestorlek och bandbreddsbegränsningar.

### Kan jag inkludera flera meddelanden i samma API-begäran?

Du kan gruppera flera meddelanden inom en enskild nyttolast för begäran och strömma dem till [!DNL Platform]. När det används på rätt sätt är gruppering av flera meddelanden i en enda begäran ett utmärkt sätt att optimera dataåtgärderna. Läs självstudiekursen om hur du [skickar flera meddelanden i en begäran](../tutorials/streaming-multiple-messages.md) om mer information.

### Hur vet jag om de data jag skickar tas emot?

Alla data som skickas till [!DNL Platform] (utan fel eller på annat sätt) lagras som gruppfiler innan de lagras i datauppsättningar. Batchernas bearbetningsstatus visas i den datauppsättning de skickades till.

Du kan verifiera om data har importerats genom att kontrollera datauppsättningsaktiviteten med [användargränssnittet](https://platform.adobe.com)i Experience Platform. Klicka **[!UICONTROL Datasets]** i den vänstra navigeringen för att visa en lista med datauppsättningar. Markera den datauppsättning som du direktuppspelar till i den lista som visas för att öppna dess *[!UICONTROL Dataset activity]* sida och visa alla batchar som har skickats under en vald tidsperiod. Mer information om hur du använder [!DNL Experience Platform] för att övervaka dataströmmar finns i guiden om [övervakning av dataflöden](../quality/monitor-data-flows.md)för direktuppspelning.

Om dina data inte kunde importera och du vill återställa dem från [!DNL Platform]kan du hämta de misslyckade batcharna genom att skicka deras ID:n till [!DNL Data Access API]. Mer information finns i guiden om hur du [hämtar misslyckade batchar](../quality/retrieve-failed-batches.md) .

### Varför är mina strömmande data inte tillgängliga i datasjön?

Det finns många anledningar till att batchimporten kanske inte når servern, till exempel ogiltig formatering, saknade data eller systemfel. [!DNL Data Lake] Om du vill ta reda på varför din batch misslyckades måste du hämta gruppen med hjälp av [!DNL Data Ingestion Service API] och visa information om den. Detaljerade steg för hur du hämtar en misslyckad batch finns i guiden om hur du [hämtar misslyckade batchar](../quality/retrieve-failed-batches.md).

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

### Varför tas mina skickade meddelanden inte emot av [!DNL Real-time Customer Profile]?

Om ett meddelande [!DNL Real-time Customer Profile] avvisas beror det troligtvis på felaktig identitetsinformation. Detta kan bero på att ett ogiltigt värde eller namnutrymme har angetts för en identitet.

Det finns två typer av identitetsnamnutrymmen: standard och anpassad. När du använder anpassade namnutrymmen måste du kontrollera att namnutrymmet har registrerats i [!DNL Identity Service]. Mer information om hur du använder standardnamnutrymmen och anpassade namnutrymmen finns i Översikt över [](../../identity-service/namespaces.md) identitetsnamn.

Du kan använda för [!DNL Experience Platform UI](https://platform.adobe.com) att se mer information om varför ett meddelande inte kunde hämtas. Klicka **[!UICONTROL Monitoring]** i den vänstra navigeringen och visa sedan _[!UICONTROL Streaming end-to-end]_fliken för att se meddelandebatchar som direktuppspelats under en vald tidsperiod.