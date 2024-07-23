---
title: Dela privata tilläggspaket i reaktors-API
description: Lär dig hur du tillåter andra företag att dela privata tilläggspaket i Reactor API.
source-git-commit: ea9a2bb00d3ce59e28ea4cda0d30945e77aa95cb
workflow-type: tm+mt
source-wordcount: '503'
ht-degree: 0%

---


# Dela privata tilläggspaket

>[!NOTE]
>
>Användare med behörigheten `develop_extensions` i tilläggets ägarorganisation kan skapa, lista och ta bort användningsauktoriseringar för tilläggspaketet. Användare i en auktoriserad organisation som har behörigheten `manage_properties` får endast lista användningsauktoriseringarna för tilläggspaket för sin organisation och uppdatera sin status till `accepted` om de vill använda tilläggspaketet, eller till `rejected` om de inte vill använda det.

Ägare till tilläggspaket kan ge andra företag tillstånd att använda sina privata versioner via Reactor API. En användningslicens för ett tilläggspaket beviljas varje godkänt företag och den här behörigheten gäller för alla aktuella och framtida privata versioner av paketet.

Den här guiden ger en översikt på hög nivå över hur du konfigurerar användningsauktoriseringar för tilläggspaket. Mer detaljerad vägledning om hur du hanterar auktoriseringar i Reactor API, inklusive exempel på JSON för en auktoriserings struktur, finns i [slutpunktshandboken för godkännande av tilläggspaketanvändning](../endpoints/extension-package-usage-authorizations.md).

## Skapa en auktorisering {#create-authorization}

Om du vill skapa en ny auktorisering måste du ha behörigheten `develop_extensions`. I följande exempel visas hur du kan skapa en användningsbehörighet för tilläggspaket för ett tilläggspaket med hjälp av `authorized_org_id` för det företag du vill auktorisera.

**API-format**

```http
POST /extension_packages/{EXTENSION_PACKAGE_ID}/extension_package_usage_authorizations
```

| Parameter | Beskrivning |
| --- | --- |
| `EXTENSION_PACKAGE_ID` | `ID` för tilläggspaketet som du vill skapa en auktorisering för. |

{style="table-layout:auto"}

**Begäran**

Följande begäran skapar en ny auktorisering för tilläggspaket för det angivna företaget.

```shell
curl -X POST \
  https://reactor.adobe.io/extension_packages/{EXTENSION_PACKAGE_ID}/extension_package_usage_authorizations \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H "Content-Type: application/vnd.api+json" \
  -d '{
        "data": {
          "attributes": {
            "authorized_org_id": "{ORG_ID}"
          },
          "type": "extension_package_usage_authorizations"
        }
      } 
```

| Egenskap | Beskrivning |
| --- | --- |
| `attributes.authorized_org_id` | `ID` för organisationen som du vill auktorisera. |

{style="table-layout:auto"}

Auktoriseringens ursprungliga tillstånd är i `pending_approval`-steget. Innan företaget använder tilläggspaketet måste det godkänna godkännandet. Företagets användare kan bläddra i det privata tilläggspaketet medan auktoriseringen väntar på godkännande, men de kan inte installera det och kan inte hitta det i sin tilläggskatalog.

## Godkänn en auktorisering {#approve-authorization}

Om du vill godkänna en auktorisering måste du ha behörigheten `manage_properties`. Som auktoriserat företag måste du skicka en PATCH-begäran till användningsauktoriseringen för tilläggspaketet, inklusive `ID` för auktoriseringen och ange statusen som `approved`.

**API-format**

```http
PATCH //extension_package_usage_authorizations/{EXTENSION_PACKAGE_USAGE_AUTHORIZATION_ID}
```

| Parameter | Beskrivning |
| --- | --- |
| `EXTENSION_PACKAGE_USAGE_AUTHORIZATION_ID` | `ID` för auktoriseringen som du vill godkänna. |

{style="table-layout:auto"}

**Begäran**

Följande PATCH-begäran ställer in `state` för en auktorisering till `approved`.

```shell
curl -X PATCH \
  https://reactor.adobe.io/extension_package_usage_authorizations/{EXTENSION_PACKAGE_USAGE_AUTHORIZATION_ID} \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-Api-Key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H "Content-Type: application/vnd.api+json" \
  -d '{
        "data": {
          "attributes": {
	          "state": "approved"
	        },
	        "id": ":extension_package_usage_authorization_id",
	        "type": "extension_package_usage_authorizations"
        }
      }
```

När auktoriseringen har godkänts som auktoriserat företag kan du nu installera tilläggspaketet på dina egenskaper.

>[!NOTE]
>
>Om auktoriseringen inte godkänns kommer det auktoriserade företaget inte att kunna använda tilläggspaketet.

## Ta bort en auktorisering {#delete-authorization}

Som ägare av ett tilläggspaket kan du återkalla behörigheten när som helst genom att ta bort behörigheten för användning av tilläggspaketet. Detta förhindrar att det auktoriserade företaget visar privata versioner av tilläggspaketet i katalogen och installerar det på sina egenskaper. Installerade privata versioner fortsätter dock att fungera som förväntat efter borttagningen.

**API-format**

```http
DELETE //extension_package_usage_authorizations/{EXTENSION_PACKAGE_USAGE_AUTHORIZATION_ID}
```

| Parameter | Beskrivning |
| --- | --- |
| `EXTENSION_PACKAGE_USAGE_AUTHORIZATION_ID` | `ID` för auktoriseringen som du vill ta bort. |

{style="table-layout:auto"}

**Begäran**

Följande DELETE-begäran tar bort behörigheten för ett företag.

```shell
curl -X DELETE \
  https://reactor.adobe.io/extension_package_usage_authorizations/{EXTENSION_PACKAGE_USAGE_AUTHORIZATION_ID} \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-Api-Key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H "Content-Type: application/vnd.api+json" \
```
