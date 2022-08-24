---
keywords: Experience Platform;hem;populära ämnen;källor;kopplingar;källkopplingar;källor sdk;sdk;SDK
title: Skicka din källa
topic-legacy: overview
description: I följande dokument beskrivs hur du testar och verifierar en ny källa med hjälp av API:t för Flow Service och integrerar en ny källa med självbetjäningskällor (Batch SDK).
exl-id: 9e945ba1-51b6-40a9-b92f-e0a52b3f92fa
source-git-commit: 4d7799b01c34f4b9e4a33c130583eadcfdc3af69
workflow-type: tm+mt
source-wordcount: '826'
ht-degree: 0%

---

# Skicka din källa

Det sista steget mot att integrera din nya källa till Adobe Experience Platform med självbetjäningskällor (Batch SDK) är att testa källan för verifiering. När det är klart kan du sedan skicka in din nya källfil genom att kontakta Adobe.

Följande dokument innehåller anvisningar om hur du testar och felsöker källan med [[!DNL Flow Service] API](https://www.adobe.io/experience-platform-apis/references/flow-service/).

## Komma igång

* Mer information om hur du kan anropa API:er för plattformar finns i handboken [komma igång med plattforms-API:er](../../../landing/api-guide.md).
* Mer information om hur du genererar autentiseringsuppgifter för plattforms-API:er finns i självstudiekursen om [autentisera och komma åt Experience Platform API:er](../../../landing/api-authentication.md).
* Mer information om hur du konfigurerar [!DNL Postman] för plattforms-API:er, se självstudiekursen om [konfigurera utvecklarkonsolen och [!DNL Postman]](../../../landing/postman.md).
* Ladda ned [Självserverad källverifieringssamling och -miljö här](../assets/sdk-verification.zip) och följ stegen nedan.

## Testa källan

Om du vill testa källan måste du köra [Insamling och miljö för verifiering av självserverkällor](../assets/sdk-verification.zip) på [!DNL Postman] samtidigt som du tillhandahåller rätt miljövariabler som hör till källan.

För att kunna börja testa måste du först konfigurera samlingen och miljön på [!DNL Postman]. Ange sedan det ID för anslutningsspecifikationen som du vill testa.

### Ange `authSpecName`

När du har angett ditt anslutningsspecifikations-ID måste du ange `authSpecName` som du använder för din basanslutning. Beroende på vad du väljer kan det vara antingen `OAuth 2 Refresh Code` eller  `Basic Authentication`. När du har angett `authSpecName`måste du sedan inkludera de nödvändiga inloggningsuppgifterna i din miljö. Om du till exempel anger `authSpecName` as `OAuth 2 Refresh Code`måste du ange de autentiseringsuppgifter som krävs för OAuth 2, som `host` och `accessToken`.

### Ange `sourceSpec`

När du har lagt till parametrar för autentiseringsspecifikation måste du lägga till de egenskaper som krävs från källspecifikationen. Du hittar de obligatoriska egenskaperna i `sourceSpec.spec.properties`. När det gäller [!DNL MailChimp Members] I exemplet nedan är den enda obligatoriska egenskapen `listId`, vilket betyder `listId` och det motsvarar ditt ID-värde [!DNL Postman] miljö.

```json
"spec": {
  "$schema": "http://json-schema.org/draft-07/schema#",
  "type": "object",
  "description": "Define user input parameters to fetch resource values.",
  "properties": {
    "listId": {
      "type": "string",
      "description": "listId for which members need to fetch."
    }
  }
}
```

När du har angett parametrarna för autentisering och källspecifikation kan du börja fylla i resten av dina miljövariabler. Se tabellen nedan för referens:

>[!NOTE]
>
>Alla exempelvariabler nedan är platshållarvärden som du måste uppdatera, förutom `flowSpecificationId` och `targetConnectionSpecId`, som är fasta värden.

| Parameter | Beskrivning | Exempel |
| --- | --- | --- |
| `x-api-key` | En unik identifierare som används för att autentisera anrop till API:er för Experience Platform. Se självstudiekursen om [autentisera och komma åt Experience Platform API:er](../../../landing/api-authentication.md) om du vill ha information om hur du hämtar `x-api-key`. | `c8d9a2f5c1e03789bd22e8efdd1bdc1b` |
| `x-gw-ims-org-id` | En företagsenhet som kan äga eller licensiera produkter och tjänster och ge åtkomst till sina medlemmar. Se självstudiekursen om [konfigurera utvecklarkonsolen och [!DNL Postman]](../../../landing/postman.md) för instruktioner om hur du hämtar `x-gw-ims-org-id` information. | `ABCEH0D9KX6A7WA7ATQE0TE@adobeOrg` |
| `authorizationToken` | Den auktoriseringstoken som krävs för att slutföra anrop till Experience Platform API:er. Se självstudiekursen om [autentisera och komma åt Experience Platform API:er](../../../landing/api-authentication.md) om du vill ha information om hur du hämtar `authorizationToken`. | `Bearer authorizationToken` |
| `schemaId` | För att källdata ska kunna användas i Platform måste ett målschema skapas för att strukturera källdata efter dina behov. Detaljerade anvisningar om hur du skapar ett XDM-målschema finns i självstudiekursen om [skapa ett schema med API](../../../xdm/api/schemas.md). | `https://ns.adobe.com/{TENANT_ID}.schemas.0ef4ce0d390f0809fad490802f53d30b` |
| `schemaVersion` | Den unika version som motsvarar ditt schema. | `application/vnd.adobe.xed-full-notext+json; version=1` |
| `schemaAltId` | The `meta:altId` som returneras tillsammans med  `schemaId` när du skapar ett nytt schema. | `_{TENANT_ID}.schemas.0ef4ce0d390f0809fad490802f53d30b` |
| `dataSetId` | Detaljerade anvisningar om hur du skapar en måldatauppsättning finns i självstudiekursen om [skapa en datauppsättning med API](../../../catalog/api/create-dataset.md). | `5f3c3cedb2805c194ff0b69a` |
| `mappings` | Mappningsuppsättningar kan användas för att definiera hur data i ett källschema mappas till data i ett målschema. Detaljerade anvisningar om hur du skapar en mappning finns i självstudiekursen om [skapa en mappningsuppsättning med API](../../../data-prep/api/mapping-set.md). | `[{"destinationXdmPath":"person.name.firstName","sourceAttribute":"email.email_id","identity":false,"version":0},{"destinationXdmPath":"person.name.lastName","sourceAttribute":"email.activity.action","identity":false,"version":0}]` |
| `mappingId` | Det unika ID som motsvarar din mappningsuppsättning. | `bf5286a9c1ad4266baca76ba3adc9366` |
| `connectionSpecId` | Anslutningsspecifikations-ID som motsvarar källan. Detta är det ID som du skapade efter [skapa en ny anslutningsspecifikation](./create.md). | `2e8580db-6489-4726-96de-e33f5f60295f` |
| `flowSpecificationId` | Flödesspecifikation-ID för `RestStorageToAEP`. **Detta är ett fast värde**. | `6499120c-0b15-42dc-936e-847ea3c24d72` |
| `targetConnectionSpecId` | Målanslutnings-ID för den datasjön där inmatade data landar. **Detta är ett fast värde**. | `c604ff05-7f1a-43c0-8e18-33bf874cb11c` |
| `verifyWatTimeInSecond` | Det angivna tidsintervallet som ska följas när en flödeskörning slutförs. | `40` |
| `startTime` | Starttiden för dataflödet. Starttiden måste formateras i unix-tid. | `1597784298` |

När du har angett alla dina miljövariabler kan du börja köra samlingen med [!DNL Postman] gränssnitt. I [!DNL Postman] väljer du ellipserna (**...**) bredvid [!DNL Sources SSSs Verification Collection] och sedan markera **Kör samling**.

![runner](../assets/runner.png)

The [!DNL Runner] -gränssnittet visas så att du kan konfigurera körningsordningen för dataflödet. Välj **Kör SSS-verifieringssamling** för att köra samlingen.

>[!NOTE]
>
>Du kan inaktivera **Ta bort flöde** i checklistan för körningsordning om du föredrar att använda kontrollpanelen för källövervakning i plattformsgränssnittet. När du är klar med testningen måste du dock se till att testflödena tas bort.

![run-collection](../assets/run-collection.png)

## Skicka din källa

När källan är klar med hela arbetsflödet kan du kontakta Adobe och skicka in källan för integrering.
