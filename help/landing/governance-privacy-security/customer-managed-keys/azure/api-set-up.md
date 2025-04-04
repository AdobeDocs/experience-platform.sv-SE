---
title: Konfigurera kundhanterade nycklar för Azure med API:t
description: Lär dig hur du konfigurerar din CMK-app med din Azure-klient och skickar ditt krypteringsnyckel-ID till Adobe Experience Platform.
role: Developer
feature: API, Privacy
exl-id: c9a1888e-421f-4bb4-b4c7-968fb1d61746
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '1023'
ht-degree: 0%

---

# Konfigurera och konfigurera kundhanterade nycklar för Azure med API:t

Det här dokumentet innehåller de Azure-specifika instruktionerna för att aktivera kundhanterade nycklar (CMK) i Adobe Experience Platform med API:t. Instruktioner om hur du slutför den här processen med användargränssnittet för Azure-värdbaserade Experience Platform-instanser finns i [UI CMK-konfigurationsdokumentet](./ui-set-up.md).

Instruktioner som är specifika för AWS finns i [AWS installationsguide](../aws/ui-set-up.md).

## Förhandskrav

Om du vill visa och gå till avsnittet [!UICONTROL Encryption] i Adobe Experience Platform måste du ha skapat en roll och tilldelat behörigheten [!UICONTROL Manage Customer Managed Key] till den rollen. Alla användare som har behörigheten [!UICONTROL Manage Customer Managed Key] kan aktivera CMK för sin organisation.

Mer information om hur du tilldelar roller och behörigheter i Experience Platform finns i [Konfigurera behörigheter](https://experienceleague.adobe.com/docs/platform-learn/getting-started-for-data-architects-and-data-engineers/configure-permissions.html).

Om du vill aktivera CMK för Azure-värdbaserade Experience Platform-instanser måste [[!DNL Azure] nyckelvalvet konfigureras](./azure-key-vault-config.md) med följande inställningar:

* [Aktivera rensningsskydd](https://learn.microsoft.com/en-us/azure/key-vault/general/soft-delete-overview#purge-protection)
* [Aktivera mjuk borttagning](https://learn.microsoft.com/en-us/azure/key-vault/general/soft-delete-overview)
* [Konfigurera åtkomst med  [!DNL Azure] rollbaserad åtkomstkontroll](https://learn.microsoft.com/en-us/azure/role-based-access-control/)
* [Konfigurera ett  [!DNL Azure] nyckelvalv](./azure-key-vault-config.md)

## Konfigurera CMK-appen {#register-app}

När du har konfigurerat nyckelvalvet är nästa steg att registrera CMK-programmet som ska länka till din [!DNL Azure]-klient.

### Komma igång

Om du registrerar CMK-appen måste du anropa Experience Platform API:er. Mer information om hur du samlar in de autentiseringsrubriker som krävs för att ringa dessa anrop finns i [autentiseringsguiden för Experience Platform API](../../../api-authentication.md).

Autentiseringsguiden innehåller anvisningar om hur du skapar ett eget unikt värde för begärandehuvudet `x-api-key`, men alla API-åtgärder i den här handboken använder det statiska värdet `acp_provisioning` i stället. Du måste dock fortfarande ange dina egna värden för `{ACCESS_TOKEN}` och `{ORG_ID}`.

I alla API-anrop som visas i den här handboken används `platform.adobe.io` som rotsökväg, som är standard för VA7-regionen. Om din organisation använder en annan region måste `platform` följas av ett bindestreck och regionkoden som tilldelats din organisation: `nld2` för NLD2 eller `aus5` för AUS5 (till exempel: `platform-aus5.adobe.io`). Om du inte känner till organisationens region kontaktar du systemadministratören.

### Hämta en autentiserings-URL {#fetch-authentication-url}

Om du vill starta registreringsprocessen skickar du en GET-begäran till slutpunkten för programregistrering för att hämta den autentiserings-URL som krävs för din organisation.

**Begäran**

```shell
curl -X GET \
  https://platform.adobe.io/data/infrastructure/manager/byok/app-registration \ 
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: acp_provisioning' \
  -H 'x-gw-ims-org-id: {ORG_ID}'
```

**Svar**

Ett lyckat svar returnerar en `applicationRedirectUrl`-egenskap som innehåller autentiserings-URL:en.

```json
{
    "id": "byok",
    "name": "acpebae9422Caepcmkmultitenantapp",
    "applicationUri": "https://adobe.com/acpebae9422Caepcmkmultitenantapp",
    "applicationId": "e463a445-c6ac-4ca2-b36a-b5146fcf6a52",
    "applicationRedirectUrl": "https://login.microsoftonline.com/common/oauth2/authorize?response_type=code&client_id=e463a445-c6ac-4ca2-b36a-b5146fcf6a52&redirect_uri=https://adobe.com/acpebae9422Caepcmkmultitenantapp&scope=user.read"
}
```

Kopiera och klistra in adressen `applicationRedirectUrl` i en webbläsare för att öppna en autentiseringsdialogruta. Välj **[!DNL Accept]** om du vill lägga till CMK-programtjänstens huvudnamn i din [!DNL Azure]-innehavare.

![En dialogruta för Microsoft-behörighetsbegäran med [!UICONTROL Accept] markerad.](../../../images/governance-privacy-security/customer-managed-keys/app-permission.png)

### Tilldela CMK-appen till en roll {#assign-to-role}

När autentiseringsprocessen är slutförd går du tillbaka till [!DNL Azure]-nyckelvalvet och väljer **[!DNL Access control]** i den vänstra navigeringen. Här väljer du **[!DNL Add]** följt av **[!DNL Add role assignment]**.

![Microsoft Azure-instrumentpanelen med [!DNL Add] och [!DNL Add role assignment] markerade.](../../../images/governance-privacy-security/customer-managed-keys/add-role-assignment.png)

På nästa skärm får du en uppmaning om att välja en roll för uppdraget. Välj **[!DNL Key Vault Crypto Service Encryption User]** innan du väljer **[!DNL Next]** för att fortsätta.

>[!NOTE]
>
>Om du har nivån [!DNL Managed-HSM Key Vault] måste du välja användarrollen **[!DNL Managed HSM Crypto Service Encryption User]**.

![Microsoft Azure-instrumentpanelen med [!DNL Key Vault Crypto Service Encryption User] markerad.](../../../images/governance-privacy-security/customer-managed-keys/select-role.png)

På nästa skärm väljer du **[!DNL Select members]** för att öppna en dialogruta i den högra listen. Använd sökfältet för att hitta tjänstens huvudnamn för CMK-programmet och markera det i listan. När du är klar väljer du **[!DNL Save]**.

>[!NOTE]
>
>Om du inte kan hitta ditt program i listan har ditt huvudnamn inte godkänts i din klientorganisation. Om du vill vara säker på att du har rätt behörigheter kan du samarbeta med [!DNL Azure]-administratören eller -representanten.

## Aktivera krypteringsnyckelkonfigurationen i Experience Platform {#send-to-adobe}

När du har installerat CMK-appen på [!DNL Azure] kan du skicka din krypteringsnyckel till Adobe. Välj **[!DNL Keys]** i den vänstra navigeringen, följt av namnet på nyckeln som du vill skicka.

![Microsoft Azure-instrumentpanelen med objektet [!DNL Keys] och nyckelnamnet markerat.](../../../images/governance-privacy-security/customer-managed-keys/select-key.png)

Välj den senaste versionen av nyckeln så visas informationssidan. Här kan du välja att konfigurera tillåtna åtgärder för nyckeln.

>[!IMPORTANT]
>
>De åtgärder som minst krävs för nyckeln är behörigheterna **[!DNL Wrap Key]** och **[!DNL Unwrap Key]**. Du kan inkludera [!DNL Encrypt], [!DNL Decrypt], [!DNL Sign] och [!DNL Verify] om du vill.

Fältet **[!UICONTROL Key Identifier]** visar URI-identifieraren för nyckeln. Kopiera det här URI-värdet för användning i nästa steg.

![Nyckelinformation för Microsoft Azure-instrumentpanelen med avsnitten [!DNL Permitted operations] och kopieringsnyckel markerade.](../../../images/governance-privacy-security/customer-managed-keys/copy-key-url.png)

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
| `name` | Ett namn för konfigurationen. Se till att du kommer ihåg det här värdet eftersom det krävs för att kontrollera konfigurationsstatus i ett [senare steg](#check-status). Värdet är skiftlägeskänsligt. |
| `type` | Konfigurationstypen. Måste anges till `BYOK_CONFIG`. |
| `imsOrgId` | Ditt organisations-ID. Detta ID måste vara samma värde som anges under rubriken `x-gw-ims-org-id`. |
| `configData` | Den här egenskapen innehåller följande information om konfigurationen:<ul><li>`providerType`: Måste anges till `AZURE_KEYVAULT`.</li><li>`keyVaultKeyIdentifier`: Nyckelvalvs-URI som du kopierade [tidigare](#send-to-adobe).</li></ul> |

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

Om du vill kontrollera statusen för konfigurationsbegäran kan du göra en GET-begäran.

**Begäran**

Du måste lägga till `name` för konfigurationen som du vill kontrollera till sökvägen (`config1` i exemplet nedan) och inkludera en `configType`-frågeparameter som är inställd på `BYOK_CONFIG`.

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

Attributet `status` kan ha ett av fyra värden med följande betydelse:

1. `RUNNING`: Verifierar att Experience Platform kan komma åt nyckel- och nyckelvalvet.
1. `UPDATE_EXISTING_RESOURCES`: Nyckelvalvet och nyckelnamnet läggs till i datalagret över alla sandlådor i organisationen.
1. `COMPLETED`: Nyckelvalvet och nyckelnamnet har lagts till i datalagret.
1. `FAILED`: Ett problem har uppstått, huvudsakligen relaterat till nyckeln, nyckelvalvet eller konfigurationen av multi-tenant-appar.

## Nästa steg

Genom att utföra ovanstående steg har du aktiverat CMK för din organisation. För Azure-värdbaserade Experience Platform-instanser krypteras och dekrypteras data som är inkapslade i primära datalager med nycklarna i [!DNL Azure]-nyckelvalvet.

Mer information om datakryptering i Adobe Experience Platform finns i [krypteringsdokumentationen](../../encryption.md).
