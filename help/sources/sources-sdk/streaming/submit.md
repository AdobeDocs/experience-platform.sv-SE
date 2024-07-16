---
title: Testa och skicka in din Source
description: I följande dokument beskrivs hur du testar och verifierar en ny källa med API:t för Flow Service och integrerar en ny källa med självbetjäningskällor (Streaming SDK).
exl-id: 2ae0c3ad-1501-42ab-aaaa-319acea94ec2
badge: Beta
source-git-commit: 256857103b4037b2cd7b5b52d6c5385121af5a9f
workflow-type: tm+mt
source-wordcount: '1236'
ht-degree: 0%

---

# Testa och skicka källan

>[!NOTE]
>
>SDK för självbetjäningsströmning för källor är i betaversion. Läs [källöversikten](../../home.md#terms-and-conditions) om du vill ha mer information om hur du använder betatecknade källor.

De sista stegen för att integrera din nya källa till Adobe Experience Platform med självbetjäningskällor (Streaming SDK) är att testa och skicka den nya källan. När du har slutfört anslutningsspecifikationen och uppdaterat specifikationen för direktuppspelningsflödet kan du börja testa källans funktionalitet antingen via API:t eller gränssnittet. När det är klart kan du sedan skicka in din nya källfil genom att kontakta Adobe.

Följande dokument innehåller steg om hur du testar och felsöker källan med [[!DNL Flow Service] API](https://www.adobe.io/experience-platform-apis/references/flow-service/).

## Komma igång

* Mer information om hur du kan anropa plattforms-API:er finns i guiden [Komma igång med plattforms-API:er](../../../landing/api-guide.md).
* Mer information om hur du genererar autentiseringsuppgifter för plattforms-API:er finns i självstudiekursen om [autentisering och åtkomst av Experience Platform API:er](../../../landing/api-authentication.md).
* Information om hur du konfigurerar [!DNL Postman] för plattforms-API:er finns i självstudiekursen [Konfigurera utvecklarkonsol och [!DNL Postman]](../../../landing/postman.md).
* Om du vill ha hjälp med testnings- och felsökningsprocessen kan du hämta verifieringssamlingen och miljön för [självbetjänade källor här](../assets/sdk-verification.zip) och följa stegen som beskrivs nedan.

## Testa källan med API:t

Om du vill testa källan med API:t måste du köra verifieringssamlingen och miljön ](../assets/sdk-verification.zip) för [!DNL Postman]-källor med [självbetjäning, samtidigt som du anger lämpliga miljövariabler som hör till källan.

Om du vill börja testa måste du först konfigurera samlingen och miljön på [!DNL Postman]. Ange sedan det ID för anslutningsspecifikationen som du vill testa.

>[!NOTE]
>
>Alla exempelvariabler nedan är platshållarvärden som du måste uppdatera, förutom för `flowSpecificationId` och `targetConnectionSpecId`, som är fasta värden.

| Parameter | Beskrivning | Exempel |
| --- | --- | --- |
| `x-api-key` | En unik identifierare som används för att autentisera anrop till API:er för Experience Platform. I självstudiekursen om [autentisering och åtkomst av Experience Platform API:er](../../../landing/api-authentication.md) finns mer information om hur du hämtar din `x-api-key`. | `c8d9a2f5c1e03789bd22e8efdd1bdc1b` |
| `x-gw-ims-org-id` | En företagsenhet som kan äga eller licensiera produkter och tjänster och ge åtkomst till sina medlemmar. Se självstudiekursen [Konfigurera utvecklarkonsolen och [!DNL Postman]](../../../landing/postman.md) för instruktioner om hur du hämtar din `x-gw-ims-org-id`-information. | `ABCEH0D9KX6A7WA7ATQE0TE@adobeOrg` |
| `authorizationToken` | Den auktoriseringstoken som krävs för att slutföra anrop till Experience Platform API:er. I självstudiekursen om [autentisering och åtkomst av Experience Platform API:er](../../../landing/api-authentication.md) finns mer information om hur du hämtar din `authorizationToken`. | `Bearer authorizationToken` |
| `schemaId` | För att källdata ska kunna användas i Platform måste ett målschema skapas för att strukturera källdata efter dina behov. Detaljerade steg om hur du skapar ett mål-XDM-schema finns i självstudiekursen [Skapa ett schema med API:t](../../../xdm/api/schemas.md). | `https://ns.adobe.com/{TENANT_ID}.schemas.0ef4ce0d390f0809fad490802f53d30b` |
| `schemaVersion` | Den unika version som motsvarar ditt schema. | `application/vnd.adobe.xed-full-notext+json; version=1` |
| `schemaAltId` | `meta:altId` som returneras tillsammans med `schemaId` när ett nytt schema skapas. | `_{TENANT_ID}.schemas.0ef4ce0d390f0809fad490802f53d30b` |
| `dataSetId` | Detaljerade steg om hur du skapar en måldatauppsättning finns i självstudiekursen [Skapa en datauppsättning med API:t](../../../catalog/api/create-dataset.md). | `5f3c3cedb2805c194ff0b69a` |
| `mappings` | Mappningsuppsättningar kan användas för att definiera hur data i ett källschema mappas till data i ett målschema. Detaljerade anvisningar om hur du skapar en mappning finns i självstudiekursen [om hur du skapar en mappningsuppsättning med API:t](../../../data-prep/api/mapping-set.md). | `[{"destinationXdmPath":"person.name.firstName","sourceAttribute":"email.email_id","identity":false,"version":0},{"destinationXdmPath":"person.name.lastName","sourceAttribute":"email.activity.action","identity":false,"version":0}]` |
| `mappingId` | Det unika ID som motsvarar din mappningsuppsättning. | `bf5286a9c1ad4266baca76ba3adc9366` |
| `connectionSpecId` | Anslutningsspecifikations-ID som motsvarar källan. Detta är det ID som du genererade efter [att du har skapat en ny anslutningsspecifikation](./create.md). | `2e8580db-6489-4726-96de-e33f5f60295f` |
| `flowSpecificationId` | Flödesspecifikation-ID för `GenericStreamingAEP`. **Det här är ett fast värde**. | `e77fde5a-22a8-11ed-861d-0242ac120002` |
| `targetConnectionSpecId` | Målanslutnings-ID för den datasjön där inmatade data landar. **Det här är ett fast värde**. | `c604ff05-7f1a-43c0-8e18-33bf874cb11c` |
| `verifyWatTimeInSecond` | Det angivna tidsintervallet som ska följas när en flödeskörning slutförs. | `40` |
| `startTime` | Starttiden för dataflödet. Starttiden måste formateras i unix-tid. | `1597784298` |

När du har angett alla dina miljövariabler kan du börja köra samlingen med gränssnittet [!DNL Postman]. I gränssnittet [!DNL Postman] markerar du ellipserna (**..**) bredvid [!DNL Sources SSSs Verification Collection] och väljer sedan **Kör samlingen**.

![runner](../assets/runner.png)

Gränssnittet [!DNL Runner] visas så att du kan konfigurera körningsordningen för dataflödet. Välj **Kör SSS-verifieringssamling** för att köra samlingen.

>[!NOTE]
>
>Du kan inaktivera **Ta bort flöde** från checklistan för körningsordning om du föredrar att använda kontrollpanelen för källövervakning i plattformsgränssnittet. När du är klar med testningen måste du dock se till att testflödena tas bort.

![run-collection](../assets/run-collection.png)

## Testa källan med användargränssnittet

Om du vill testa källan i användargränssnittet går du till källkatalogen för organisationens sandlåda i användargränssnittet för plattformen. Här ser du att din nya källa visas under kategorin *Direktuppspelning*.

När din nya källa nu är tillgänglig i din sandlåda måste du följa arbetsflödet för källor för att testa funktionerna. Börja genom att välja **[!UICONTROL Set up]**.

![Källkatalogen som visar den nya direktuppspelningskällan.](../assets/testing/catalog-test.png)

[!UICONTROL Add data]-steget visas. Om du vill testa att källan kan direktuppspela data använder du den vänstra sidan av gränssnittet för att överföra [ett exempel på JSON-data](../assets/testing/raw.json.zip). När data har överförts uppdateras den högra sidan av gränssnittet till en förhandsgranskning av datahierarkin. Välj **[!UICONTROL Next]** om du vill fortsätta.

![Stegen för att lägga till data i källarbetsflödet där du kan överföra och förhandsgranska dina data innan de hämtas.](../assets/testing/add-data-test.png)

På sidan [!UICONTROL Dataflow detail] kan du välja om du vill använda en befintlig datauppsättning eller en ny datauppsättning. Under den här processen kan du även konfigurera dina data så att de hämtas till profilen och aktivera inställningar som [!UICONTROL Error diagnostics] och [!UICONTROL Partial ingestion].

Om du vill testa väljer du **[!UICONTROL New dataset]** och anger ett namn på utdatauppsättningen. Under det här steget kan du även ange en valfri beskrivning för att lägga till ytterligare information till datauppsättningen. Välj sedan ett schema att mappa till med alternativet [!UICONTROL Advanced search] eller genom att bläddra igenom listan med befintliga scheman i listrutan. När du har valt ett schema anger du ett namn och en beskrivning för dataflödet.

När du är klar väljer du **[!UICONTROL Next]**.

![Dataflödets detaljsteg i källarbetsflödet.](../assets/testing/dataflow-details-test.png)

Steg [!UICONTROL Mapping] visas, och du får ett gränssnitt för att mappa källfälten från källschemat till rätt mål-XDM-fält i målschemat.

Plattformen ger intelligenta rekommendationer för automatiskt mappade fält baserat på det målschema eller den datamängd du valt. Du kan justera mappningsreglerna manuellt så att de passar dina användningsfall. Beroende på dina behov kan du välja att mappa fält direkt eller använda förinställningsfunktioner för data för att omvandla källdata för att härleda beräknade eller beräknade värden. Mer information om hur du använder mappningsgränssnittet och beräkningsfälten finns i [Användargränssnittshandboken för dataförinställningar](../../../data-prep/ui/mapping.md)

När källdata har mappats väljer du **[!UICONTROL Next]**.

![Mappningssteget för källarbetsflödet.](../assets/testing/mapping-test.png)

Steg **[!UICONTROL Review]** visas, så att du kan granska det nya dataflödet innan det skapas. Informationen är grupperad i följande kategorier:

* **[!UICONTROL Connection]**: Visar ditt kontonamn, typ av källa och annan information som är specifik för den strömmande molnlagringskällan som du använder.
* **[!UICONTROL Assign dataset and map fields]**: Visar måldatauppsättningen och målschemat som du använder för dataflödet.

När du har granskat dataflödet väljer du **[!UICONTROL Finish]** och tillåt en tid innan dataflödet skapas.

![Granskningssteget för källarbetsflödet.](../assets/testing/review-test.png)

Slutligen måste du hämta dataflödets slutpunkt för direktuppspelning. Den här slutpunkten används för att prenumerera på din webkrok, vilket gör att strömningskällan kan kommunicera med Experience Platform. Om du vill hämta strömningsslutpunkten går du till sidan [!UICONTROL Dataflow activity] i det dataflöde som du just skapade och kopierar slutpunkten längst ned på panelen [!UICONTROL Properties].

![Slutpunkten för direktuppspelning i dataflödesaktivitet.](../assets/testing/endpoint-test.png)

## Skicka din källa

När källan är klar med hela arbetsflödet kan du kontakta din Adobe-representant och skicka in källan för integrering mellan andra Experience Platform-organisationer.
