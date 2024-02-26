---
title: Konfigurera ett Azure Key Vault
description: Lär dig hur du skapar ett nytt Enterprise-konto med Azure, eller använder ett befintligt Enterprise-konto och skapar nyckelvalvet.
exl-id: 670e3ca3-a833-4b28-9ad4-73685fa5d74d
source-git-commit: 4f08e8fcc8d53b981af60226f1397a1d1ac4d8dc
workflow-type: tm+mt
source-wordcount: '561'
ht-degree: 0%

---

# Konfigurera en [!DNL Azure] Key Vault

Kundhanterade nycklar (CMK) stöder bara nycklar från en [!DNL Microsoft Azure] Key Vault. För att komma igång måste du arbeta med [!DNL Azure] om du vill skapa ett nytt Enterprise-konto eller använda ett befintligt Enterprise-konto och följa stegen nedan för att skapa nyckelvalvet.

>[!IMPORTANT]
>
>Endast nivåerna Standard, Premium och Managed HSM för [!DNL Azure] Nyckelvalv stöds. [!DNL Azure Dedicated HSM] och [!DNL Azure Payments HSM] stöds inte. Se [[!DNL Azure] dokumentation](https://learn.microsoft.com/en-us/azure/security/fundamentals/key-management#azure-key-management-services) för mer information om nyckelhanteringstjänster.

>[!NOTE]
>
>Dokumentationen nedan beskriver bara de grundläggande stegen för att skapa nyckelvalvet. Utanför den här vägledningen bör du konfigurera nyckelvalvet enligt din organisations policyer.

Logga in på [!DNL Azure] portalen och använd sökfältet för att hitta **[!DNL Key vaults]** i förteckningen över tjänster.

![Sökfunktionen i [!DNL Microsoft Azure] med [!DNL Key vaults] markerat i sökresultaten.](../../images/governance-privacy-security/customer-managed-keys/access-key-vaults.png)

The **[!DNL Key vaults]** visas när du har valt tjänsten. Välj **[!DNL Create]**.

![The [!DNL Key vaults] instrumentpanel i [!DNL Microsoft Azure] med [!DNL Create] markerad.](../../images/governance-privacy-security/customer-managed-keys/create-key-vault.png)

Fyll i grundläggande information för nyckelvalvet med hjälp av det angivna formuläret, inklusive ett namn och en tilldelad resursgrupp.

>[!WARNING]
>
>De flesta alternativ kan lämnas som standardvärden, men **se till att du aktiverar alternativen för mjuk borttagning och tömning av skydd**. Om du inte aktiverar de här funktionerna kan du riskera att förlora åtkomsten till dina data om nyckelvalvet tas bort.
>
>![The [!DNL Microsoft Azure] [!DNL Create a Key Vault] arbetsflöde med mjuk borttagning och rensningsskydd markerat.](../../images/governance-privacy-security/customer-managed-keys/basic-config.png)

Här fortsätter du med arbetsflödet för att skapa nyckelvalv och konfigurerar de olika alternativen enligt din organisations policyer.

När du har kommit fram till **[!DNL Review + create]** kan du granska informationen om nyckelvalvet medan det går igenom valideringen. När valideringen är klar väljer du **[!DNL Create]** för att slutföra processen.

![Microsoft Azure Key Valults Review och create page with Create marked.](../../images/governance-privacy-security/customer-managed-keys/finish-creation.png)

## Konfigurera åtkomst {#configure-access}

Aktivera sedan Azure-rollbaserad åtkomstkontroll för ditt nyckelvalv. Välj **[!DNL Access configuration]** i [!DNL Settings] i den vänstra navigeringen väljer du **[!DNL Azure role-based access control]** för att aktivera inställningen. Det här steget är viktigt eftersom CMK-appen senare måste associeras med en Azure-roll. Tilldela en roll finns dokumenterad i båda [API](./api-set-up.md#assign-to-role) och [UI](./ui-set-up.md#assign-to-role) arbetsflöden.

![The [!DNL Microsoft Azure] kontrollpanel med [!DNL Access configuration] och [!DNL Azure role-based access control] markerad.](../../images/governance-privacy-security/customer-managed-keys/access-configuration.png)

## Konfigurera nätverksalternativ {#configure-network-options}

Om nyckelvalvet är konfigurerat för att begränsa offentlig åtkomst till vissa virtuella nätverk eller inaktivera allmän åtkomst helt måste du bevilja [!DNL Microsoft] ett brandväggsundantag.

Välj **[!DNL Networking]** i den vänstra navigeringen. Under **[!DNL Firewalls and virtual networks]** markerar du kryssrutan **[!DNL Allow trusted Microsoft services to bypass this firewall]** väljer **[!DNL Apply]**.

![The [!DNL Networking] flik för [!DNL Microsoft Azure] med [!DNL Networking] och [!DNL Allow trusted Microsoft surfaces to bypass this firewall] undantag markerat.](../../images/governance-privacy-security/customer-managed-keys/networking.png)

### Generera en nyckel {#generate-a-key}

När du har skapat ett nyckelvalv kan du generera en ny nyckel. Navigera till **[!DNL Keys]** och markera **[!DNL Generate/Import]**.

![The [!DNL Keys] flik för [!DNL Azure] med [!DNL Generate import] markerad.](../../images/governance-privacy-security/customer-managed-keys/view-keys.png)

Använd det angivna formuläret för att ange ett namn för nyckeln och välj antingen **RSA** eller **RSA-HSM** för nyckeltypen. Som ett minimum är **[!DNL RSA key size]** måste vara minst **3072** bitar efter behov av [!DNL Cosmos DB]. [!DNL Azure Data Lake Storage] är också kompatibelt med RSA 3027.

>[!NOTE]
>
>Kom ihåg namnet som du anger för nyckeln, eftersom det krävs för att skicka nyckeln till Adobe.

Använd de återstående kontrollerna för att konfigurera nyckeln som du vill generera eller importera efter behov. När du är klar väljer du **[!DNL Create]**.

![The [!DNL Create a key] kontrollpanel med [!DNL 3072] bitar markerade.](../../images/governance-privacy-security/customer-managed-keys/configure-key.png)

Den konfigurerade nyckeln visas i listan med nycklar för valvet.

![The [!DNL Keys] arbetsyta med nyckelnamnet markerat.](../../images/governance-privacy-security/customer-managed-keys/key-added.png)

## Nästa steg

Om du vill fortsätta med engångsprocessen för att konfigurera funktionen för kundhanterade nycklar fortsätter du med antingen [API](./api-set-up.md) eller [UI](./ui-set-up.md) kundhanterade nycklar, inställningsguider.
