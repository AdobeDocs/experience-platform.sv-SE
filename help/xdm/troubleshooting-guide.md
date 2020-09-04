---
keywords: Experience Platform;home;popular topics;;XDM;XDM system;XDM individual profile;XDM ExperienceEvent;XDM Experience Event;experienceEvent;experience eventExperience event;XDM Experience Event;XDM ExperienceEvent;;experience data model;Experience data model;Experience Data Model;data model;Data Model;schema;troubleshooting;FAQ;faq;Union schema;UNION PROFILE;union profile
solution: Experience Platform
title: Felsökningsguide för Experience Data Model (XDM)
description: Det här dokumentet innehåller svar på vanliga frågor om Experience Data Model (XDM) System samt en felsökningsguide för vanliga fel.
topic: troubleshooting
translation-type: tm+mt
source-git-commit: 2a528c705a7aa610f57047be39be1ce9886ce44c
workflow-type: tm+mt
source-wordcount: '1852'
ht-degree: 0%

---


# [!DNL Experience Data Model] (XDM) Felsökningsguide för system

Det här dokumentet innehåller svar på vanliga frågor om [!DNL Experience Data Model] (XDM) System samt en felsökningsguide för vanliga fel. För frågor och felsökning som rör andra tjänster i Adobe Experience Platform, se felsökningsguiden för [Experience Platform](../landing/troubleshooting.md).

**[!DNL Experience Data Model](XDM)** är en öppen källkodsspecifikation som definierar standardiserade scheman för kundupplevelsehantering. Metoden som [!DNL Experience Platform] byggs på, **XDM System**, används för att göra [!DNL Experience Data Model] scheman tillgängliga för [!DNL Platform] tjänster. I **[!DNL Schema Registry]** finns ett användargränssnitt och ett RESTful-API för att komma åt **[!DNL Schema Library]** innehållet [!DNL Experience Platform]. Mer information finns i [XDM-dokumentationen](home.md) .

## Vanliga frågor och svar 

Nedan följer en lista med svar på vanliga frågor om XDM-system och användning av [!DNL Schema Registry] API:t.

### Hur lägger jag till fält i ett schema?

Du kan lägga till fält i ett schema med hjälp av en mixin. Varje blandning är kompatibel med en eller flera klasser, vilket gör att mixin kan användas i alla scheman som implementerar en av dessa kompatibla klasser. Adobe Experience Platform erbjuder flera branschblandningar med sina egna fördefinierade fält, men du kan lägga till egna fält i ett schema genom att skapa nya mixiner med API:t eller användargränssnittet.

Mer information om hur du skapar nya mixiner i API:t finns i [Skapa ett mixin](api/create-mixin.md) -dokument i utvecklarhandboken för [!DNL Schema Registry] API. Om du använder användargränssnittet läser du i [schemaredigerarens självstudiekurs](./tutorials/create-schema-ui.md).

### Vilket är det bästa användningsområdet för blandningar och datatyper?

[Blandningar](./schema/composition.md#mixin) är komponenter som definierar ett eller flera fält i ett schema. Blandningar styr hur deras fält visas i schemats hierarki och visar därför samma struktur i varje schema som de ingår i. Blandningar är bara kompatibla med specifika klasser, som identifieras av deras `meta:intendedToExtend` attribut.

[Datatyper](./schema/composition.md#data-type) kan även innehålla ett eller flera fält för ett schema. Till skillnad från blandningar begränsas datatyperna inte till en viss klass. Detta gör datatyper till ett mer flexibelt alternativ för att beskriva vanliga datastrukturer som kan återanvändas i flera scheman med potentiellt olika klasser.

### Vilket unikt ID har ett schema?

Alla [!DNL Schema Registry] resurser (scheman, mixins, datatyper, klasser) har en URI som fungerar som ett unikt ID för referens- och sökningsändamål. När du visar ett schema i API:t finns det på den översta nivån `$id` och i `meta:altId` attributen.

Mer information finns i avsnittet om [schemaidentifiering](api/getting-started.md#schema-identification) i utvecklarhandboken för [!DNL Schema Registry] API.

### När börjar ett schema förhindra att ändringar bryts?

Du kan göra ändringar i ett schema så länge det aldrig har använts för att skapa en datauppsättning eller aktiverats för användning i [[!DNL-kundprofil i realtid]](../profile/home.md). När ett schema har använts för att skapa en datauppsättning eller aktiverats för användning med [!DNL Real-time Customer Profile], kommer reglerna för [schemautveckling](schema/composition.md#evolution) att tillämpas strikt av systemet.

### Vilken är den maximala storleken för en lång fälttyp?

En lång fälttyp är ett heltal med en maximal storlek på 53 (+1) bitar, vilket ger den ett möjligt intervall mellan -9007199254740992 och 900719925474092. Detta beror på en begränsning av hur JavaScript-implementeringar av JSON representerar långa heltal.

Mer information om fälttyper finns i avsnittet [Definiera XDM-fälttyper](api/appendix.md#field-types) i utvecklarhandboken för [!DNL Schema Registry] API.

### Hur definierar jag identiteter för mitt schema?

I [!DNL Experience Platform]används identiteter för att identifiera ett ämne (vanligtvis en enskild person) oavsett vilka datakällor som tolkas. De definieras i scheman genom att nyckelfält markeras som&quot;Identitet&quot;. Vanliga fält för identitet är e-postadress, telefonnummer, [[!DNL Experience Cloud ID (ECID)]](https://docs.adobe.com/content/help/sv-SE/id-service/using/home.html), CRM ID och andra unika ID-fält.

Fält kan markeras som identiteter med antingen API:t eller användargränssnittet.

#### Definiera identiteter i API:t

I API:t etableras identiteter genom att skapa identitetsbeskrivningar. Identitetsbeskrivare signalerar att en viss egenskap för ett schema är en unik identifierare.

Identitetsbeskrivare skapas av en POST-begäran till slutpunkten /descriptors. Om det lyckas får du ett HTTP Status 201 (Skapad) och ett svarsobjekt med information om den nya beskrivningen.

Mer information om hur du skapar identitetsbeskrivningar i API:t finns i dokumentet om [beskrivningar](api/descriptors.md) i [!DNL Schema Registry] utvecklarhandboken.

#### Definiera identiteter i användargränssnittet

Öppna schemat i Schemaredigeraren och klicka på det fält i redigerarens avsnitt som du vill markera som en identitet. **[!UICONTROL Structure]** Klicka i kryssrutan **[!UICONTROL Field Properties]** till höger **[!UICONTROL Identity]** .

Mer information om hur du hanterar identiteter i användargränssnittet finns i avsnittet om [att definiera identitetsfält](./tutorials/create-schema-ui.md#identity-field) i schemaredigerarens självstudiekurs.

### Behöver mitt schema en primär identitet?

Primära identiteter är valfria eftersom scheman kan ha 0 eller 1 av dem. Ett schema måste dock ha en primär identitet för att schemat ska kunna aktiveras för användning i [!DNL Real-time Customer Profile]. Mer information finns i [identitetsdelen](./tutorials/create-schema-ui.md#identity-field) i schemaredigerarens självstudiekurs.

### Hur aktiverar jag ett schema för användning i [!DNL Real-time Customer Profile]?

Scheman är aktiverade för användning i [[!DNL Real-time Customer Profile]](../profile/home.md) genom att en &quot;union&quot;-tagg läggs till, som finns i schemats `meta:immutableTags` -attribut. Du [!DNL Profile] kan aktivera ett schema för användning med API:t eller användargränssnittet.

#### Aktivera ett befintligt schema för [!DNL Profile] användning av API

Gör en PATCH-begäran om att uppdatera schemat och lägga till attributet som en array som innehåller värdet &quot;union&quot;. `meta:immutableTags` Om uppdateringen lyckas visas det uppdaterade schemat som nu innehåller unionstaggen.

Mer information om hur du använder API:t för att aktivera ett schema för användning i [!DNL Real-time Customer Profile]finns i dokumentet om [fackföreningar](./api/unions.md) i [!DNL Schema Registry] utvecklarhandboken.

#### Aktivera ett befintligt schema för [!DNL Profile] användning av användargränssnittet

I [!DNL Experience Platform]klickar du på **[!UICONTROL Schemas]** i den vänstra navigeringen och väljer namnet på schemat som du vill aktivera i listan med scheman. Klicka sedan på till höger om redigeraren under **[!UICONTROL Schema Properties]** för **[!UICONTROL Profile]** att aktivera den.


Mer information finns i avsnittet om [användning i kundprofilen](./tutorials/create-schema-ui.md#profile) i realtid i [!UICONTROL Schema Editor] självstudiekursen.

### Kan jag redigera ett unionsschema direkt?

Unionsscheman är skrivskyddade och genereras automatiskt av systemet. De kan inte redigeras direkt. Unionsscheman skapas för en viss klass när en&quot;union&quot;-tagg läggs till i schemat som implementerar den klassen.

Mer information om fackföreningar i XDM finns i avsnittet om [fackföreningar](./api/unions.md) i utvecklarhandboken för [!DNL Schema Registry] API.

### Hur ska jag formatera min datafil för att importera data till mitt schema?

[!DNL Experience Platform] använder datafiler i antingen [!DNL Parquet] - eller JSON-format. Innehållet i dessa filer måste överensstämma med det schema som datauppsättningen refererar till. Mer information om de bästa sätten att mata in datafiler finns i översikten över [batchimporten](../ingestion/home.md).

## Fel och felsökning

Här följer en lista med felmeddelanden som du kan stöta på när du arbetar med [!DNL Schema Registry] API:t.

### Objektet hittades inte

```json
{
    "type": "/placeholder/type/uri",
    "status": 404,
    "title": "NotFoundError",
    "detail": "Object https://ns.adobe.com/incorrectTenantId/schemas/ee067e31b08514d21e2b82577813409d 
      with version 1 not found"
}
```

Det här felet visas när systemet inte kan hitta en viss resurs. Resursen kan ha tagits bort eller så är sökvägen i API-anropet ogiltig. Kontrollera att du har angett en giltig sökväg för API-anropet innan du försöker igen. Du kanske vill kontrollera att du har angett rätt ID för resursen och att sökvägen har rätt namn tillsammans med rätt behållare (global eller klientorganisation).

Mer information om hur du skapar sökvägar i API:t finns i avsnitten om [behållar](./api/getting-started.md#container) - och [schemaidentifiering](api/getting-started.md#schema-identification) i [!DNL Schema Registry] utvecklarhandboken.

### Titeln måste vara unik

```json
{
    "type": "/placeholder/type/uri",
    "status": 400,
    "title": "BadRequestError",
    "detail": "Title must be unique. An object 
      https://ns.adobe.com/{TENANT_ID}/schemas/26f6833e55db1dd8308aa07a64f2042d 
      already exists with the same title."
}
```

Det här felmeddelandet visas när du försöker skapa en resurs med en titel som redan används av en annan resurs. Titlar måste vara unika för alla resurstyper. Om du till exempel försöker skapa en blandning med en titel som redan används av ett schema, visas det här felet.

### Anpassade fält måste använda ett fält på den översta nivån

```json
{
    "type": "/placeholder/type/uri",
    "status": 400,
    "title": "BadRequestError",
    "detail": "For custom fields, you must use a top level field named _{TENANT_ID}
       and all the other fields must be defined under it"
}
```

Det här felmeddelandet visas när du försöker skapa en ny blandning med felnamngivna fält. Blandningar som definieras av din IMS-organisation måste namnge sina fält med en `TENANT_ID` för att undvika konflikter med andra bransch- och leverantörsresurser. Detaljerade exempel på lämpliga datastrukturer för blandningar finns i dokumentet om hur du [skapar ett mixin](api/create-mixin.md) -avsnitt i utvecklarhandboken för [!DNL Schema Registry] API.


### [!DNL Real-time Customer Profile] fel

Följande felmeddelanden är kopplade till åtgärder som används för att aktivera scheman för [!DNL Real-time Customer Profile]. Mer information finns i avsnittet [Fackföreningar](./api/unions.md) i utvecklarhandboken för [!DNL Schema Registry] API.

#### Schemat ska vara giltigt för att aktivera profildatamängder

```json
{
    "type": "/placeholder/type/uri",
    "status": 400,
    "title": "BadRequestError",
    "detail": "To enable profile datasets the schema should be valid"
}
```

Det här felmeddelandet visas när du försöker aktivera en profildatauppsättning för ett schema som inte har aktiverats för [!DNL Real-time Customer Profile]. Kontrollera att schemat innehåller en unionstagg innan du aktiverar datauppsättningen.

#### Det måste finnas en referensidentitetsbeskrivning

```json
{
    "type": "/placeholder/type/uri",
    "status": 400,
    "title": "BadRequestError",
    "detail": "For a schema to be able to participate in union, if any of its 
      property is associated with a xdm:descriptorOneToOne descriptor, there must 
      be a xdm:descriptorReferenceIdentity descriptor for that property"
}
```

Det här felmeddelandet visas när du försöker aktivera ett schema för [!DNL Profile] och en av dess egenskaper innehåller en relationsbeskrivare utan någon referensidentitetsbeskrivare. Lös det här felet genom att lägga till en beskrivare för referens-ID i schemafältet i fråga.

#### Namnutrymmena för referensbeskrivningsfältet och målschemat måste matcha

```json
{
    "type": "/placeholder/type/uri",
    "status": 400,
    "title": "BadRequestError",
    "detail": "If both schemas from an already defined xdm:descriptorOneToOne 
      descriptor are promoted to union, and if there is a primary identity on one of 
      the schemas from the xdm:descriptorOneToOne descriptor, the 
      xdm:identityNamespace of the sourceSchema's descriptorReferenceIdentity and the 
      xdm:namespace field of the xdm:descriptorIdentity for the destinationSchema must 
      match"
}
```

Om du vill aktivera scheman som innehåller relationsbeskrivningar som ska användas i [!DNL Profile]måste källfältets namnutrymme och målfältets primära namnutrymme vara samma. Det här felmeddelandet visas när du försöker aktivera ett schema som innehåller ett omatchat namnutrymme för dess referensidentitetsbeskrivning. Kontrollera att `xdm:namespace` värdet för målschemats identitetsfält matchar värdet för `xdm:identityNamespace` egenskapen i källfältets beskrivare för referens-ID för att lösa problemet.

En lista över identitetsnamnutrymmeskoder som stöds finns i avsnittet om [standardnamnutrymmen](../identity-service/namespaces.md) i översikten över identitetsnamnutrymmet.

### Acceptera rubrikfel

De flesta GET-begäranden i API:t kräver en Accept-rubrik för att systemet ska kunna avgöra hur svaret ska formateras. [!DNL Schema Registry] Nedan följer en lista över vanliga fel som är kopplade till huvudet Acceptera. En lista över kompatibla Acceptera rubriker för olika API-begäranden finns i motsvarande avsnitt i utvecklarhandboken för [schemaregister](api/getting-started.md).

#### Parametern Godkänn sidhuvud krävs

```json
{
    "type": "/placeholder/type/uri",
    "status": 406,
    "title": "NotAcceptableError",
    "detail": "Accept header parameter is required"
}
```

Det här felmeddelandet visas när en Accept-rubrik saknas i en API-begäran. Se till att en Accept-rubrik inkluderas innan du försöker igen.

#### Okänt accepterande media har angetts

```json
{
    "type": "/placeholder/type/uri",
    "status": 406,
    "title": "NotAcceptableError",
    "detail": "Unknown Accept media supplied: xed+json"
}
```

Det här felmeddelandet visas när en Accept-rubrik är ogiltig. Kontrollera att du har angett ett accepteringshuvud som är kompatibelt med den API-begäran du försöker göra innan du försöker igen.

#### Okänt format för Acceptera är tillgängligt

```json
{
    "type": "/placeholder/type/uri",
    "status": 406,
    "title": "NotAcceptableError",
    "detail": "Unknown Accept format available "
}
```

Det här felmeddelandet visas när sidhuvudet Godkänn har angetts felaktigt vid sökning efter en beskrivning. Kontrollera att du har angett något av de [godkända rubrikerna för beskrivare](./api/descriptors.md) korrekt innan du försöker igen.

#### Versionen måste anges i sidhuvudet Godkänn

```json
{
    "type": "/placeholder/type/uri",
    "status": 400,
    "title": "BadRequestError",
    "detail": "version must be supplied in the accept header. Example: 
      application/vnd.adobe.xed-full-notext+json; version=1"
}
```

Det här felmeddelandet visas när ett versionsnummer inte har inkluderats i huvudet Godkänn. Vissa element som scheman kräver att en version anges när du söker efter enskilda instanser. Ett Accept-huvud som innehåller ett versionsnummer ser ut ungefär så här:

```plaintext
application/vnd.adobe.xed+json; version=1
```

En lista över vilka sidhuvuden som stöds finns i avsnittet [Acceptera sidhuvud](api/getting-started.md#accept) i [!DNL Schema Registry] utvecklarhandboken.

#### Versionen får inte anges i sidhuvudet Godkänn

```json
{
    "type": "/placeholder/type/uri",
    "status": 400,
    "title": "BadRequestError",
    "detail": "version must not be supplied in the accept header. Example: 
      application/vnd.adobe.xed-full+json"
}
```

Om du försöker ta med en version i rubriken Acceptera när du listar (GET) resurser visas det här felet. Versioner krävs bara när en sökbegäran görs på en enskild resurs. Ta bort versionen från sidhuvudet Godkänn för att åtgärda felet.