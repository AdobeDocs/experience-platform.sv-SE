---
title: Salesforce Marketing Cloud Source - översikt
description: Lär dig hur du ansluter Salesforce Marketing Cloud till Adobe Experience Platform med hjälp av API:er eller användargränssnittet.
exl-id: 2177d68c-0cef-4031-a0e7-8bf22ee2e70b
last-substantial-update: 2025-05-17T00:00:00Z
source-git-commit: 0c0a58df4beae499008e52c118b40bed86ff0596
workflow-type: tm+mt
source-wordcount: '664'
ht-degree: 0%

---

# [!DNL Salesforce Marketing Cloud]

>[!WARNING]
>
>[!DNL Salesforce Marketing Cloud]-källan kommer att bli inaktuell i januari 2026. En ny källa kommer att släppas senare i år som ett alternativ. När den nya källan har släppts måste du planera migreringen till den nya källan genom att skapa nya kontoanslutningar och dataflöden före utgången av januari 2026.

Med [!DNL Salesforce Marketing Cloud] kan ni hantera och automatisera kundengagemang för e-post, mobiler, sociala medier och annonser - allt från en enda plattform. Med verktyg som Email Studio, Journey Builder och Audience Builder kan ni skapa personaliserade kampanjer och kundresor som är skräddarsydda efter er målgrupp.

Du kan använda källan [!DNL Salesforce Marketing Cloud] för att ansluta ditt konto och överföra dina data till Adobe Experience Platform.

## Förhandskrav

Innan du kan ansluta din [!DNL Salesforce Marketing Cloud]-källa till Experience Platform måste du se till att följande **behörighetsomfattningar** har tilldelats din [!DNL Salesforce Marketing Cloud]-klient-ID och kombination av klienthemlighet:

* `campaign_read`
* `list_and_subscribers_read`

Du kan begära omfång genom att anropa `v2/userinfo`-resursen för API:t [!DNL Salesforce Marketing Cloud]. I dokumentet [[!DNL Salesforce Marketing Cloud] Behörighetsintervall för API-integrering](<https://developer.salesforce.com/docs/marketing/marketing-cloud/guide/data-access-permissions.html>) finns mer information om hur du begär och jämför omfattningar.

Mer information om omfattningar inklusive en lista över deras relaterade behörigheter och beteenden finns i det här [[!DNL Salesforce Marketing Cloud] REST API-dokumentet](<https://developer.salesforce.com/docs/marketing/marketing-cloud/guide/rest-permissions-and-scopes.html>).

>[!IMPORTANT]
>
>Inläsning av anpassade objekt stöds för närvarande inte av källintegreringen [!DNL Salesforce Marketing Cloud].

### IP-adress tillåtelselista

Du måste lägga till regionspecifika IP-adresser i tillåtelselista innan du kan ansluta dina källor till Experience Platform. Mer information finns i guiden om att [tillåtslista IP-adresser för att ansluta till Experience Platform](../../ip-address-allow-list.md).

>[!WARNING]
>
>Om du inte lägger till de nödvändiga IP-adresserna i tillåtelselista kommer ditt [!DNL Salesforce Marketing Cloud]-konto inte att ansluta till Experience Platform.

### Autentisera till Experience Platform på Azure {#azure}

Du måste ange värden för följande autentiseringsuppgifter för att kunna ansluta [!DNL Salesforce Marketing Cloud] till Experience Platform på [!DNL Azure].

| Autentiseringsuppgifter | Beskrivning |
| --- | --- |
| Värd | Programmets värdserver. Detta är ofta din underdomän. **Obs!** När du anger ditt `host`-värde måste du ange `{subdomain}.rest.marketingcloudapis.com`. Om din värd-URL till exempel är `https://acme-ab12c3d4e5fg6hijk7lmnop8qrst.auth.marketingcloudapis.com/` måste du ange `acme-ab12c3d4e5fg6hijk7lmnop8qrst.rest.marketingcloudapis.com/` som värdvärde. |
| Klient-ID | Klient-ID som är associerat med ditt [!DNL Salesforce Marketing Cloud]-program. |
| Klienthemlighet | Klienthemligheten som är associerad med ditt [!DNL Salesforce Marketing Cloud]-program. |
| Anslutningsspecifikation-ID | Anslutningsspecifikationen **för** innehåller anslutningsegenskaperna för en datakälla. Detta innehåller information som autentiseringsspecifikationer och krav för att skapa både **base** - och **source** -anslutningar. För [!DNL Salesforce Marketing Cloud] är anslutningsspec-ID: `ea1c2a08-b722-11eb-8529-0242ac130003`. **Obs!** Den här autentiseringsuppgiften behövs bara när du ansluter via API:er. |

### Autentisera till Experience Platform på Amazon Web Services (AWS) {#aws}

>[!AVAILABILITY]
>
>Detta avsnitt gäller implementeringar av Experience Platform som körs på Amazon Web Services (AWS). Experience Platform som körs på AWS är för närvarande tillgängligt för ett begränsat antal kunder. Mer information om den Experience Platform-infrastruktur som stöds finns i [Experience Platform översikt över flera moln](../../../landing/multi-cloud.md).

Du måste ange värden för följande autentiseringsuppgifter för att kunna ansluta [!DNL Salesforce Marketing Cloud] till Experience Platform på AWS.

| Autentiseringsuppgifter | Beskrivning |
| --- | --- |
| Underdomän | Den unika delen av [!DNL Salesforce Marketing Cloud]-instansens URL som används för att skapa API-slutpunkter. |
| Klient-ID | En offentlig identifierare för programmet som genereras när du skapar ett installerat paket i [!DNL Salesforce Marketing Cloud] |
| Klienthemlighet | En konfidentiell nyckel som är kopplad till ditt klient-ID, som också genereras i det installerade paketet. |
| Anslutningsspecifikation-ID | Anslutningsspecifikationen **för** innehåller anslutningsegenskaperna för en datakälla. Detta innehåller information som autentiseringsspecifikationer och krav för att skapa både **base** - och **source** -anslutningar. För [!DNL Salesforce Marketing Cloud] är anslutningsspec-ID: `ea1c2a08-b722-11eb-8529-0242ac130003`. **Obs!** Den här autentiseringsuppgiften behövs bara när du ansluter via API:er. |

Mer information finns i [[!DNL Salesforce] dokumentationen om åtkomsttoken för server-till-server-integreringar](https://developer.salesforce.com/docs/marketing/marketing-cloud/guide/access-token-s2s.html).

## Anslut [!DNL Salesforce Marketing Cloud] till Experience Platform med API:er

Dokumentationen nedan innehåller information om hur du ansluter [!DNL Salesforce Marketing Cloud] till Experience Platform med API:er:

* [Anslut [!DNL Salesforce Marketing Cloud] till Experience Platform med API:t för Flow Service](../../tutorials/api/create/marketing-automation/salesforce-marketing-cloud.md)
* [Utforska datatabeller med API:t för Flow Service](../../tutorials/api/explore/tabular.md)
* [Skapa ett dataflöde för en källa för automatiserad marknadsföring med API:t för Flow Service](../../tutorials/api/collect/marketing-automation.md)

## Anslut [!DNL Salesforce Marketing Cloud] till Experience Platform med användargränssnittet

Dokumentationen nedan innehåller information om hur du ansluter [!DNL Salesforce Marketing Cloud] till Experience Platform med användargränssnittet:

* [Anslut [!DNL Salesforce Marketing Cloud] till Experience Platform i användargränssnittet](../../tutorials/ui/create/marketing-automation/salesforce-marketing-cloud.md)
* [Skapa ett dataflöde för en källanslutning för automatiserad marknadsföring i användargränssnittet](../../tutorials/ui/dataflow/marketing-automation.md)
