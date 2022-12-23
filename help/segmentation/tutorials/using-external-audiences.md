---
keywords: Experience Platform;hem;populära ämnen
solution: Experience Platform
title: Importera och använda externa målgrupper
description: Följ den här självstudiekursen för att lära dig hur du använder externa målgrupper med Adobe Experience Platform.
topic-legacy: tutorial
exl-id: 56fc8bd3-3e62-4a09-bb9c-6caf0523f3fe
source-git-commit: 681418b4198c2b1303fda937c3ffc60dad21b672
workflow-type: tm+mt
source-wordcount: '1582'
ht-degree: 0%

---

# Importera och använda externa målgrupper

Adobe Experience Platform har stöd för import av externa målgrupper, som sedan kan användas som komponenter för en ny segmentdefinition. Det här dokumentet innehåller en självstudiekurs om hur du konfigurerar Experience Platform för att importera och använda externa målgrupper.

## Komma igång

Den här självstudiekursen kräver en fungerande förståelse för de olika [!DNL Adobe Experience Platform] tjänster som används för att skapa målgruppssegment. Innan du börjar med den här självstudiekursen bör du läsa dokumentationen för följande tjänster:

- [Segmenteringstjänst](../home.md): Gör att ni kan bygga målgruppssegment utifrån kundprofildata i realtid.
- [Kundprofil i realtid](../../profile/home.md): Ger en enhetlig konsumentprofil i realtid baserad på aggregerade data från flera källor.
- [Experience Data Model (XDM)](../../xdm/home.md): Det standardiserade ramverk som Platform använder för att organisera kundupplevelsedata. För att utnyttja segmenteringen på bästa sätt bör du se till att dina data är inmatade som profiler och händelser enligt [bästa praxis för datamodellering](../../xdm/schema/best-practices.md).
- [Datauppsättningar](../../catalog/datasets/overview.md): Konstruktionen för lagring och hantering av databeständighet i Experience Platform.
- [Direktinmatning](../../ingestion/streaming-ingestion/overview.md): Hur Experience Platform importerar och lagrar data från klient- och serverenheter i realtid.

### Segmentdata kontra segmentmetadata

Innan du börjar importera och använda externa målgrupper är det viktigt att förstå skillnaden mellan segmentdata och segmentmetadata.

Segmentdata avser de profiler som uppfyller kriterierna för att kvalificera segment, och är därför en del av målgruppen.

Metadata för segment är information om själva segmentet, som innehåller namn, beskrivning, uttryck (om tillämpligt), datum då segmentet skapades, datum för senaste ändring och ett ID. ID:t länkar segmentmetadata till de enskilda profiler som uppfyller segmentkvalificeringen och är en del av den slutliga målgruppen.

| Segmentdata | Segmentmetadata |
| ------------ | ---------------- |
| Profiler som uppfyller kraven för segment | Information om själva segmentet |

## Skapa ett identitetsnamnutrymme för den externa målgruppen

Det första steget för att använda externa målgrupper är att skapa ett identitetsnamnutrymme. Med identitetsnamnutrymmen kan plattformen associera varifrån ett segment kommer.

Följ instruktionerna i [guide för identitetsnamnutrymme](../../identity-service/namespaces.md#manage-namespaces). När du skapar ditt identitetsnamnutrymme lägger du till källinformationen i identitetsnamnutrymmet och markerar dess [!UICONTROL Type] som **[!UICONTROL Non-people identifier]**.

![Identifieraren för icke-människa markeras på spärrformen för identitetsnamnutrymmet.](../images/tutorials/external-audiences/identity-namespace-info.png)

## Skapa ett schema för segmentmetadata

När du har skapat ett identitetsnamnutrymme måste du skapa ett nytt schema för det segment som du ska skapa.

Börja med att välja **[!UICONTROL Schemas]** i det vänstra navigeringsfältet, följt av **[!UICONTROL Create schema]** i det övre högra hörnet av arbetsytan Scheman. Här väljer du **[!UICONTROL Browse]** om du vill se ett fullständigt urval av tillgängliga schematyper.

![Både Skapa schema och Bläddra är markerade.](../images/tutorials/external-audiences/create-schema-browse.png)

Eftersom du skapar en segmentdefinition, som är en fördefinierad klass, väljer du **[!UICONTROL Use existing class]**. Nu väljer du **[!UICONTROL Segment definition]** klass, följt av **[!UICONTROL Assign class]**.

![Segmentdefinitionsklassen är markerad.](../images/tutorials/external-audiences/assign-class.png)

Nu när schemat har skapats måste du ange vilket fält som ska innehålla segment-ID:t. Det här fältet bör markeras som primär identitet och tilldelas de namnutrymmen som du skapade tidigare.

![Kryssrutorna för att markera det markerade fältet som primär identitet markeras i Schemaredigeraren.](../images/tutorials/external-audiences/mark-primary-identifier.png)

När du har markerat `_id` som primär identitet väljer du schemats titel, följt av växlingens etikett **[!UICONTROL Profile]**. Välj **[!UICONTROL Enable]** för att aktivera schemat för [!DNL Real-time Customer Profile].

![Växlingen för att aktivera schemat för profilen är markerad i Schemaredigeraren.](../images/tutorials/external-audiences/schema-profile.png)

Det här schemat är nu aktiverat för profilen, med den primära identifieringen tilldelad till det icke-personliga ID-namnområdet som du skapade. Detta innebär att segmentmetadata som importeras till plattformen med det här schemat kommer att importeras till profilen utan att sammanfogas med andra personrelaterade profildata.

## Skapa en datauppsättning för schemat

När du har konfigurerat schemat måste du skapa en datauppsättning för segmentets metadata.

Om du vill skapa en datauppsättning följer du instruktionerna i [användarhandbok för datauppsättning](../../catalog/datasets/user-guide.md#create). Du bör följa **[!UICONTROL Create dataset from schema]** med det schema som du skapade tidigare.

![Schemat som du vill basera din datauppsättning på markeras.](../images/tutorials/external-audiences/select-schema.png)

När du har skapat datauppsättningen fortsätter du att följa instruktionerna i [användarhandbok för datauppsättning](../../catalog/datasets/user-guide.md#enable-profile) för att aktivera den här datauppsättningen för kundprofil i realtid.

![Växlingen för att aktivera schemat för profilen är markerad på aktivitetssidan för datauppsättning.](../images/tutorials/external-audiences/dataset-profile.png)

## Konfigurera och importera målgruppsdata

När datauppsättningen är aktiverad kan data nu skickas till plattformen antingen via användargränssnittet eller med Experience Platform API:er. Du kan importera dessa data antingen via en batch- eller direktuppspelningsanslutning.

### Infoga data med en batchanslutning

Om du vill skapa en batchanslutning kan du följa instruktionerna i det generiska [användargränssnittshandbok för lokal filöverföring](../../sources/tutorials/ui/create/local-system/local-file-upload.md). En fullständig lista över tillgängliga källor som du kan använda importdata med finns i [källöversikt](../../sources/home.md).

### Importera data via en direktuppspelningsanslutning

Om du vill skapa en direktuppspelningsanslutning följer du instruktionerna i [API, genomgång](../../sources/tutorials/api/create/streaming/http.md) eller [Självstudiekurs om användargränssnitt](../../sources/tutorials/ui/create/streaming/http.md).

När du har skapat en direktuppspelningsanslutning får du tillgång till din unika slutpunkt för direktuppspelning som du kan skicka data till. Läs mer om hur du skickar data till dessa slutpunkter i [självstudiekurs om att direktuppspela postdata](../../ingestion/tutorials/streaming-record-data.md#ingest-data).

![Slutpunkten för direktuppspelning för direktuppspelningsanslutningen markeras på sidan med källinformation.](../images/tutorials/external-audiences/get-streaming-endpoint.png)

## Struktur för målgruppsmetadata

När du har skapat en anslutning kan du nu importera dina data till plattformen.

Ett exempel på den externa målgruppens nyttolastmetadata visas nedan:

```json
{
    "header": {
        "schemaRef": {
            "id": "https://ns.adobe.com/{TENANT_ID}/schemas/{SCHEMA_ID}",
            "contentType": "application/vnd.adobe.xed-full+json;version=1"
        },
        "imsOrgId": "{ORG_ID}",
        "datasetId": "{DATASET_ID}",
        "source": {
            "name": "Sample External Audience"
        }
    },
    "body": {
        "xdmMeta": {
            "schemaRef": {
                "id": "https://ns.adobe.com/{TENANT_ID}/schemas/{SCHEMA_ID}",
                "contentType": "application/vnd.adobe.xed-full+json;version=1"
            }
        },
        "xdmEntity": {
            "_id": "{SEGMENT_ID}",
            "description": "Sample description",
            "identityMap": {
                "{IDENTITY_NAMESPACE}": [{
                    "id": "{}"
                }]
            },
            "segmentName" : "{SEGMENT_NAME}",
            "segmentStatus": "ACTIVE",
            "version": "1.0"
        }
    }
}
```

| Egenskap | Beskrivning |
| -------- | ----------- |
| `schemaRef` | Schemat **måste** hänvisar till det tidigare skapade schemat för segmentmetadata. |
| `datasetId` | Datauppsättnings-ID **måste** referera till den tidigare skapade datauppsättningen för det schema du just skapade. |
| `xdmEntity._id` | ID:t **måste** referera till samma segment-ID som du använder som extern målgrupp. |
| `xdmEntity.identityMap` | Detta avsnitt **måste** innehåller den identitetsetikett som användes när det namnutrymme som skapades tidigare skapades. |
| `{IDENTITY_NAMESPACE}` | Detta är etiketten för det identitetsnamnutrymme som skapades tidigare. Om du till exempel anropar ditt identitetsnamnutrymme &quot;externalAudience&quot;, använder du det som nyckel för arrayen. |
| `segmentName` | Namnet på det segment som du vill att den externa målgruppen ska segmenteras av. |

## Skapa segment med importerade målgrupper

När de importerade målgrupperna har konfigurerats kan de användas som en del av segmenteringsprocessen. Om du vill hitta externa målgrupper går du till segmentbyggaren och väljer **[!UICONTROL Audiences]** i **[!UICONTROL Fields]** -avsnitt.

![Den externa målgruppsväljaren i segmentbyggaren markeras.](../images/tutorials/external-audiences/external-audiences.png)

## Nästa steg

Nu när ni kan använda externa målgrupper i era segment kan ni använda segmentverktyget för att skapa segment. Läs mer om hur du skapar segment i [självstudiekurs om hur du skapar segment](./create-a-segment.md).

## Bilaga

Förutom att använda importerade externa målgruppsmetadata och använda dem för att skapa segment, kan du även importera externa segmentmedlemskap till plattformen.

### Ställ in ett externt målschema för segmentmedlemskap

Börja med att välja **[!UICONTROL Schemas]** i det vänstra navigeringsfältet, följt av **[!UICONTROL Create schema]** i det övre högra hörnet av arbetsytan Scheman. Här väljer du **[!UICONTROL XDM Individual Profile]**.

![Området XDM Individual Profile är markerat.](../images/tutorials/external-audiences/create-schema-profile.png)

Nu när schemat har skapats måste du lägga till fältgruppen för segmentmedlemskap som en del av schemat. Välj [!UICONTROL Segment Membership Details], följt av [!UICONTROL Add field groups].

![Fältgruppen Information om segmentmedlemskap är markerad.](../images/tutorials/external-audiences/segment-membership-details.png)

Kontrollera dessutom att schemat är markerat för **[!UICONTROL Profile]**. För att kunna göra detta måste du markera ett fält som primär identitet.

![Växlingen för att aktivera schemat för profilen är markerad i Schemaredigeraren.](../images/tutorials/external-audiences/external-segment-profile.png)

### Konfigurera datauppsättningen

När du har skapat schemat måste du skapa en datauppsättning.

Om du vill skapa en datauppsättning följer du instruktionerna i [användarhandbok för datauppsättning](../../catalog/datasets/user-guide.md#create). Du bör följa **[!UICONTROL Create dataset from schema]** med det schema som du skapade tidigare.

![Schemat som du använder för att skapa databasen markeras.](../images/tutorials/external-audiences/select-schema.png)

När du har skapat datauppsättningen fortsätter du att följa instruktionerna i [användarhandbok för datauppsättning](../../catalog/datasets/user-guide.md#enable-profile) för att aktivera den här datauppsättningen för kundprofil i realtid.

![Växlingen för att aktivera schemat för profilen är markerad i arbetsflödet för att skapa datauppsättningar.](../images/tutorials/external-audiences/dataset-profile.png)

## Ställ in och importera externa data för målgruppsmedlemskap

När datauppsättningen är aktiverad kan data nu skickas till plattformen antingen via användargränssnittet eller med Experience Platform API:er. Du kan importera dessa data antingen via en batch- eller direktuppspelningsanslutning.

### Infoga data med en batchanslutning

Om du vill skapa en batchanslutning kan du följa instruktionerna i det generiska [användargränssnittshandbok för lokal filöverföring](../../sources/tutorials/ui/create/local-system/local-file-upload.md). En fullständig lista över tillgängliga källor som du kan använda importdata med finns i [källöversikt](../../sources/home.md).

### Importera data via en direktuppspelningsanslutning

Om du vill skapa en direktuppspelningsanslutning följer du instruktionerna i [API, genomgång](../../sources/tutorials/api/create/streaming/http.md) eller [Självstudiekurs om användargränssnitt](../../sources/tutorials/ui/create/streaming/http.md).

När du har skapat en direktuppspelningsanslutning får du tillgång till din unika slutpunkt för direktuppspelning som du kan skicka data till. Läs mer om hur du skickar data till dessa slutpunkter i [självstudiekurs om att direktuppspela postdata](../../ingestion/tutorials/streaming-record-data.md#ingest-data).

![Slutpunkten för direktuppspelning för direktuppspelningsanslutningen markeras på sidan med källinformation.](../images/tutorials/external-audiences/get-streaming-endpoint.png)

## Segmentmedlemsstruktur

När du har skapat en anslutning kan du nu importera dina data till plattformen.

Ett exempel på nyttolasten för det externa målgruppsmedlemskapet visas nedan:

```json
{
    "header": {
        "schemaRef": {
            "id": "https://ns.adobe.com/{TENANT_ID}/schemas/{SCHEMA_ID}",
            "contentType": "application/vnd.adobe.xed-full+json;version=1"
        },
        "imsOrgId": "{ORG_ID}",
        "datasetId": "{DATASET_ID}",
        "source": {
            "name": "Sample External Audience Membership"
        }
    },
    "body": {
        "xdmMeta": {
            "schemaRef": {
                "id": "https://ns.adobe.com/{TENANT_ID}/schemas/{SCHEMA_ID}",
                "contentType": "application/vnd.adobe.xed-full+json;version=1"
            }
        },
        "xdmEntity": {
            "_id": "{UNIQUE_ID}",
            "description": "Sample description",
            "{TENANT_NAME}": {
                "identities": {
                    "{SCHEMA_IDENTITY}": "sample-id"
                }
            },
            "personId" : "sample-name",
            "segmentMembership": {
                "{IDENTITY_NAMESPACE}": {
                    "{EXTERNAL_IDENTITY}": {
                        "status": "realized",
                        "lastQualificationTime": "2022-03-14T:00:00:00Z"
                    }
                }
            }
        }
    }
}
```

| Egenskap | Beskrivning |
| -------- | ----------- |
| `schemaRef` | Schemat **måste** hänvisar till det tidigare skapade schemat för segmentmedlemskapsdata. |
| `datasetId` | Datauppsättnings-ID **måste** hänvisa till den tidigare skapade datauppsättningen för det medlemsschema som du just skapade. |
| `xdmEntity._id` | Ett lämpligt ID som används för att unikt identifiera posten i datauppsättningen. |
| `{TENANT_NAME}.identities` | Det här avsnittet används för att koppla fältgruppen för anpassade identiteter till de användare som du tidigare importerat. |
| `segmentMembership.{IDENTITY_NAMESPACE}` | Detta är etiketten för det anpassade identitetsnamnutrymmet som skapades tidigare. Om du till exempel anropar ditt identitetsnamnutrymme &quot;externalAudience&quot;, använder du det som nyckel för arrayen. |