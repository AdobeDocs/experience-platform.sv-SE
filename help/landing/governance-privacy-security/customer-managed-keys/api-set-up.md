---
title: Konfigurera kundhanterade nycklar med API:t
description: Lär dig hur du konfigurerar din CMK-app med din Azure-klient och skickar ditt krypteringsnyckel-ID till Adobe Experience Platform.
source-git-commit: a0df05cde19e97d4abdad7abd19eafea8efe1096
workflow-type: tm+mt
source-wordcount: '1000'
ht-degree: 0%

---

# Konfigurera och konfigurera kundhanterade nycklar med API:t

I det här dokumentet beskrivs hur du aktiverar funktionen för kundhanterade nycklar (CMK) i Adobe Experience Platform med API:t. Instruktioner om hur du slutför den här processen med användargränssnittet finns i [Inställningsdokument för användargränssnittets CMK](./ui-set-up.md).

## Förutsättningar

Visa och gå till [!UICONTROL Encryption] i Adobe Experience Platform måste du ha skapat en roll och tilldelat [!UICONTROL Manage Customer Managed Key] behörighet till den rollen. Alla användare som har [!UICONTROL Manage Customer Managed Key] behörighet kan aktivera CMK för sin organisation.

Mer information om hur du tilldelar roller och behörigheter i Experience Platform finns i [konfigurera behörighetsdokumentation](https://experienceleague.adobe.com/docs/platform-learn/getting-started-for-data-architects-and-data-engineers/configure-permissions.html).

Om du vill aktivera CMK [[!DNL Azure] Nyckelvalv måste konfigureras](./azure-key-vault-config.md) med följande inställningar:

* [Aktivera rensningsskydd](https://learn.microsoft.com/en-us/azure/key-vault/general/soft-delete-overview#purge-protection)
* [Aktivera mjuk borttagning](https://learn.microsoft.com/en-us/azure/key-vault/general/soft-delete-overview)
* [Konfigurera åtkomst med [!DNL Azure] rollbaserad åtkomstkontroll](https://learn.microsoft.com/en-us/azure/role-based-access-control/)
* [Konfigurera en [!DNL Azure] Key Vault](./azure-key-vault-config.md)

## Konfigurera CMK-appen {#register-app}

När du har konfigurerat nyckelvalvet är nästa steg att registrera dig för CMK-programmet som ska länka till [!DNL Azure] tenant.

### Komma igång

Om du registrerar CMK-appen måste du anropa API:er för plattformen. Mer information om hur du samlar in de autentiseringsrubriker som krävs för att ringa dessa samtal finns i [Autentiseringsguide för plattforms-API](../../api-authentication.md).

Autentiseringsguiden innehåller instruktioner om hur du genererar ett eget unikt värde för den `x-api-key` begäranhuvud, används det statiska värdet för alla API-åtgärder i den här handboken `acp_provisioning` i stället. Du måste fortfarande ange dina egna värden för `{ACCESS_TOKEN}` och `{ORG_ID}`, dock.

I alla API-anrop som visas i den här handboken `platform.adobe.io` används som rotsökväg, som är standard för VA7-regionen. Om din organisation använder en annan region `platform` måste följas av ett bindestreck och regionkoden som tilldelats din organisation: `nld2` för NLD2 eller `aus5` för AUS5 (till exempel: `platform-aus5.adobe.io`). Om du inte känner till organisationens region kontaktar du systemadministratören.

### Hämta en autentiserings-URL {#fetch-authentication-url}

Om du vill starta registreringsprocessen skickar du en GET-förfrågan till slutpunkten för programregistreringen för att hämta den autentiserings-URL som krävs för din organisation.

**Begäran**

```shell
curl -X GET \
  https://platform.adobe.io/data/infrastructure/manager/byok/app-registration \ 
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: acp_provisioning' \
  -H 'x-gw-ims-org-id: {ORG_ID}'
```

**Svar**

Ett godkänt svar returnerar ett `applicationRedirectUrl` -egenskap som innehåller autentiserings-URL:en.

```json
{
    "id": "byok",
    "name": "acpebae9422Caepcmkmultitenantapp",
    "applicationUri": "https://adobe.com/acpebae9422Caepcmkmultitenantapp",
    "applicationId": "e463a445-c6ac-4ca2-b36a-b5146fcf6a52",
    "applicationRedirectUrl": "https://login.microsoftonline.com/common/oauth2/authorize?response_type=code&client_id=e463a445-c6ac-4ca2-b36a-b5146fcf6a52&redirect_uri=https://adobe.com/acpebae9422Caepcmkmultitenantapp&scope=user.read"
}
```

Kopiera och klistra in `applicationRedirectUrl` till en webbläsare för att öppna en autentiseringsdialogruta. Välj **[!DNL Accept]** för att lägga till CMK-programtjänstens huvudnamn i [!DNL Azure] tenant.

![En dialogruta för Microsoft-behörighetsbegäran med [!UICONTROL Accept] markerad.](../../images/governance-privacy-security/customer-managed-keys/app-permission.png)

### Tilldela CMK-appen till en roll {#assign-to-role}

När autentiseringsprocessen är klar går du tillbaka till [!DNL Azure] Nyckelvalv och välj **[!DNL Access control]** i den vänstra navigeringen. Välj **[!DNL Add]** följt av **[!DNL Add role assignment]**.

![Microsoft Azure-kontrollpanelen med [!DNL Add] och [!DNL Add role assignment] markerad.](../../images/governance-privacy-security/customer-managed-keys/add-role-assignment.png)

På nästa skärm får du en uppmaning om att välja en roll för uppdraget. Välj **[!DNL Key Vault Crypto Service Encryption User]** före markering **[!DNL Next]** för att fortsätta.

![Microsoft Azure-kontrollpanelen med [!DNL Key Vault Crypto Service Encryption User] markerad.](../../images/governance-privacy-security/customer-managed-keys/select-role.png)

Välj **[!DNL Select members]** för att öppna en dialogruta i den högra listen. Använd sökfältet för att hitta tjänstens huvudnamn för CMK-programmet och markera det i listan. När du är klar väljer du **[!DNL Save]**.

>[!NOTE]
>
>Om du inte kan hitta ditt program i listan har ditt huvudnamn inte godkänts i din klientorganisation. För att vara säker på att du har rätt behörigheter kan du arbeta med [!DNL Azure] administratör eller representant.

## Aktivera krypteringsnyckelkonfigurationen i Experience Platform {#send-to-adobe}

Efter installation av CMK-appen på [!DNL Azure]kan du skicka krypteringsnyckelns identifierare till Adobe. Välj **[!DNL Keys]** i den vänstra navigeringen, följt av namnet på den tangent som du vill skicka.

![Microsoft Azure-kontrollpanelen med [!DNL Keys] och nyckelnamnet är markerat.](../../images/governance-privacy-security/customer-managed-keys/select-key.png)

Välj den senaste versionen av nyckeln så visas informationssidan. Här kan du välja att konfigurera tillåtna åtgärder för nyckeln.

>[!IMPORTANT]
>
>De minsta åtgärder som krävs för nyckeln är **[!DNL Wrap Key]** och **[!DNL Unwrap Key]** behörigheter. Du kan inkludera [!DNL Encrypt], [!DNL Decrypt], [!DNL Sign]och [!DNL Verify] borde du vilja.

The **[!UICONTROL Key Identifier]** fältet visar URI-identifieraren för nyckeln. Kopiera det här URI-värdet för användning i nästa steg.

![Nyckelinformation för Microsoft Azure-instrumentpanelen med [!DNL Permitted operations] och kopieringsnyckelns URL-avsnitt är markerade.](../../images/governance-privacy-security/customer-managed-keys/copy-key-url.png)

När du har fått nyckelvalvs-URI:n kan du skicka den med en POST-begäran till CMK-konfigurationsslutpunkten.

>[!NOTE]
>
>Endast nyckelvalvet och nyckelnamnet lagras med Adobe, inte nyckelversionen.

**Begäran**

+++ En exempelbegäran om att skicka nyckelvalvs-URI till CMK-konfigurationsslutpunkten.

```shell
curl -X POST \
  https://platform.adobe.io/data/infrastructure/manager/customer/config \ 
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: acp_provisioning' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -d '{
        "name": "Config1",
        "type": "BYOK_CONFIG",
        "imsOrgId": "{ORG_ID}",
        "configData": {
          "providerType": "AZURE_KEYVAULT",
          "keyVaultKeyIdentifier": "https://adobecmkexample.vault.azure.net/keys/adobeCMK-key/7c1d50lo28234cc895534c00d7eb4eb4"
        }
      }'
```

| Egenskap | Beskrivning |
| --- | --- |
| `name` | Ett namn för konfigurationen. Se till att du kommer ihåg det här värdet eftersom det krävs för att kontrollera konfigurationsstatus på en [senare steg](#check-status). Värdet är skiftlägeskänsligt. |
| `type` | Konfigurationstypen. Måste anges till `BYOK_CONFIG`. |
| `imsOrgId` | Ditt organisations-ID. Detta ID måste ha samma värde som anges i `x-gw-ims-org-id` header. |
| `configData` | Den här egenskapen innehåller följande information om konfigurationen:<ul><li>`providerType`: Måste anges till `AZURE_KEYVAULT`.</li><li>`keyVaultKeyIdentifier`: Det nyckelvalv-URI som du kopierade [tidigare](#send-to-adobe).</li></ul> |

+++

**Svar**

+++ Det slutförda svaret returnerar information om konfigurationsjobbet.

```json
{
  "id": "4df7886b-a122-4391-880b-47888d5c5b92",
  "config": {
    "configData": {
      "keyVaultUri": "https://adobecmkexample.vault.azure.net",
      "keyVaultKeyIdentifier": "https://adobecmkexample.vault.azure.net/keys/adobeCMK-key/7c1d50lo28234cc895534c00d7eb4eb4",
      "keyVersion": "7c1d50lo28234cc895534c00d7eb4eb4",
      "keyName": "Config1",
      "providerType": "AZURE_KEYVAULT"
    },
    "name": "acpcf978863Aaepcmkmultitenantapp",
    "type": "BYOK_CONFIG",
    "imsOrgId": "{ORG_ID}",
    "status": "NEW"
  },
  "status": "CREATED"
}
```

+++

Jobbet bör slutföras inom några minuter.

## Verifiera konfigurationens status {#check-status}

Om du vill kontrollera statusen för konfigurationsbegäran kan du göra en GET-förfrågan.

**Begäran**

Du måste lägga till `name` för konfigurationen som du vill kontrollera till sökvägen (`config1` i exemplet nedan) och ta med en `configType` frågeparameter inställd på `BYOK_CONFIG`.

+++ Ett exempel på en begäran om att kontrollera statusen för konfigurationsbegäran.

```shell
curl -X GET \
  https://platform.adobe.io/data/infrastructure/manager/customer/config/config1?configType=BYOK_CONFIG \ 
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: acp_provisioning' \
  -H 'x-gw-ims-org-id: {ORG_ID}'
```

+++

**Svar**

+++ Det slutförda svaret returnerar jobbets status.

```json
{
  "name": "acpcf978863Aaepcmkmultitenantapp",
  "type": "BYOK_CONFIG",
  "status": "COMPLETED",
  "configData": {
    "keyVaultUri": "https://adobecmkexample.vault.azure.net",
    "keyVaultKeyIdentifier": "https://adobecmkexample.vault.azure.net/keys/adobeCMK-key/7c1d50lo28234cc895534c00d7eb4eb4",
    "keyVersion": "7c1d50lo28234cc895534c00d7eb4eb4",
    "keyName": "Config1",
    "providerType": "AZURE_KEYVAULT"
  },
  "imsOrgId": "{ORG_ID}",
  "subscriptionId": "cf978863-7325-47b1-8fd9-554b9fdb6c36",
  "id": "4df7886b-a122-4391-880b-47888d5c5b92",
  "rowType": "BYOK_KEY"
}
```

+++

The `status` -attribut kan ha ett av fyra värden med följande betydelse:

1. `RUNNING`: Verifierar att plattformen har åtkomst till nyckel- och nyckelvalvet.
1. `UPDATE_EXISTING_RESOURCES`: Nyckelvalvet och nyckelnamnet läggs till i datalagret över alla sandlådor i organisationen.
1. `COMPLETED`: Nyckelvalvet och nyckelnamnet har lagts till i datalagret.
1. `FAILED`: Ett problem uppstod, huvudsakligen relaterat till nyckeln, nyckelvalvet eller konfigurationen av multi-tenant-appar.

## Nästa steg

Genom att utföra ovanstående steg har du aktiverat CMK för din organisation. Data som hämtas till primära datalager krypteras och dekrypteras nu med nycklarna i [!DNL Azure] Key Vault. Mer information om datakryptering i Adobe Experience Platform finns i [krypteringsdokumentation](../encryption.md).
