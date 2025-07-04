---
title: Konfigurera ett Azure Key Vault för kundhanterade nycklar
description: Lär dig hur du skapar ett nytt Enterprise-konto med Azure, eller använder ett befintligt Enterprise-konto och skapar nyckelvalvet.
role: Developer
feature: Privacy
exl-id: 670e3ca3-a833-4b28-9ad4-73685fa5d74d
source-git-commit: c920f78363ee5f040964dbd3a0d0815474094b07
workflow-type: tm+mt
source-wordcount: '675'
ht-degree: 0%

---

# Konfigurera ett [!DNL Azure]-nyckelvalv för kundhanterade nycklar

Kundhanterade nycklar (CMK) har stöd för nycklar från både [!DNL Microsoft Azure] nyckelvalv och AWS [!DNL Key Management Service (KMS)]. Om din implementering finns på [!DNL Azure] följer du stegen nedan för att skapa ett nyckelvalv. Information om implementeringar på AWS finns i [AWS KMS-konfigurationsguiden](../aws/configure-kms.md).

>[!IMPORTANT]
>
>Endast HSM-nivåerna Standard, Premium och Managed för [!DNL Azure] Key Vault stöds. [!DNL Azure Dedicated HSM] och [!DNL Azure Payments HSM] stöds inte. Mer information om tjänster för nyckelhantering finns i [[!DNL Azure] dokumentationen](https://learn.microsoft.com/en-us/azure/security/fundamentals/key-management#azure-key-management-services).

>[!NOTE]
>
>Dokumentationen nedan beskriver bara de grundläggande stegen för att skapa nyckelvalvet. Utanför den här vägledningen bör du konfigurera nyckelvalvet enligt din organisations policyer.

Logga in på portalen [!DNL Azure] och använd sökfältet för att hitta **[!DNL Key vaults]** i listan över tjänster.

![Sökfunktionen i [!DNL Microsoft Azure] med [!DNL Key vaults] markerad i sökresultaten.](../../../images/governance-privacy-security/customer-managed-keys/access-key-vaults.png)

Sidan **[!DNL Key vaults]** visas när du har valt tjänsten. Välj **[!DNL Create]** härifrån.

![Kontrollpanelen [!DNL Key vaults] i [!DNL Microsoft Azure] med [!DNL Create] markerad.](../../../images/governance-privacy-security/customer-managed-keys/create-key-vault.png)

Fyll i grundläggande information för nyckelvalvet med hjälp av det angivna formuläret, inklusive ett namn och en tilldelad resursgrupp.

>[!WARNING]
>
>De flesta alternativ kan lämnas som standardvärden, men **se till att du aktiverar alternativen för mjuk borttagning och tömning**. Om du inte aktiverar de här funktionerna kan du riskera att förlora åtkomsten till dina data om nyckelvalvet tas bort.
>
>![Arbetsflödet [!DNL Microsoft Azure] [!DNL Create a Key Vault] med mjuk borttagning och rensningsskydd markerat.](../../../images/governance-privacy-security/customer-managed-keys/basic-config.png)

Här fortsätter du med arbetsflödet för att skapa nyckelvalv och konfigurerar de olika alternativen enligt din organisations policyer.

När du har kommit till steget **[!DNL Review + create]** kan du granska informationen om nyckelvalvet medan det går igenom valideringen. När valideringen har slutförts väljer du **[!DNL Create]** för att slutföra processen.

![Microsoft Azure Key Valults Review och create page with Create selected.](../../../images/governance-privacy-security/customer-managed-keys/finish-creation.png)

## Konfigurera åtkomst {#configure-access}

Aktivera sedan Azure-rollbaserad åtkomstkontroll för ditt nyckelvalv. Välj **[!DNL Access configuration]** i avsnittet [!DNL Settings] i den vänstra navigeringen och markera sedan **[!DNL Azure role-based access control]** för att aktivera inställningen. Det här steget är viktigt eftersom CMK-appen senare måste associeras med en Azure-roll. Tilldelning av en roll dokumenteras i både arbetsflödena [API](./api-set-up.md#assign-to-role) och [UI](./ui-set-up.md#assign-to-role).

![Kontrollpanelen [!DNL Microsoft Azure] med [!DNL Access configuration] och [!DNL Azure role-based access control] markerade.](../../../images/governance-privacy-security/customer-managed-keys/access-configuration.png)

## Konfigurera nätverksalternativ {#configure-network-options}

Om nyckelvalvet är konfigurerat för att begränsa offentlig åtkomst till vissa virtuella nätverk eller inaktivera allmän åtkomst helt måste du bevilja [!DNL Microsoft] ett brandväggsundantag.

Välj **[!DNL Networking]** i den vänstra navigeringen. Markera kryssrutan **[!DNL Allow trusted Microsoft services to bypass this firewall]** under **[!DNL Firewalls and virtual networks]** och välj sedan **[!DNL Apply]**.

>[!NOTE]
>
>Om ditt nyckelvalv använder begränsad nätverksåtkomst rekommenderar Adobe att du lägger till följande statiska IP-adress: `20.88.123.53`. Genom att lägga till den här IP-adressen kan Adobe-tjänster övervaka anslutningen mer effektivt och tillhandahålla varningar på plattformen när åtkomstproblem upptäcks.
>
>Mer information om när du ska tillåtslista Adobe IP-adress, hur aviseringar fungerar och hur du ska svara på meddelanden om nyckelåtkomstfel finns i [Konfigurera aviseringar och IP-åtkomst för Azure CMK](./alerts-and-ip-access.md).
>
>Om ditt nyckelvalv redan har konfigurerats för att tillåta offentlig nätverksåtkomst krävs ingen ytterligare åtgärd.

![Fliken [!DNL Networking] i [!DNL Microsoft Azure] med [!DNL Networking] och [!DNL Allow trusted Microsoft surfaces to bypass this firewall] undantag markerat.](../../../images/governance-privacy-security/customer-managed-keys/networking.png)

### Generera en nyckel {#generate-a-key}

När du har skapat ett nyckelvalv kan du generera en ny nyckel. Navigera till fliken **[!DNL Keys]** och välj **[!DNL Generate/Import]**.

![Fliken [!DNL Keys] i [!DNL Azure] med [!DNL Generate import] markerat.](../../../images/governance-privacy-security/customer-managed-keys/view-keys.png)

Använd det angivna formuläret för att ange ett namn för nyckeln och välj antingen **RSA** eller **RSA-HSM** som nyckeltyp. För [!DNL Azure]-värdbaserade implementeringar måste **[!DNL RSA key size]** vara minst **3072** bitar, vilket krävs för [!DNL Azure Cosmos DB]. [!DNL Azure Data Lake Storage] är även kompatibel med RSA 3027.

>[!NOTE]
>
>Kom ihåg namnet som du anger för nyckeln, eftersom det krävs för att skicka nyckeln till Adobe.

Använd de återstående kontrollerna för att konfigurera nyckeln som du vill generera eller importera efter behov. När du är klar väljer du **[!DNL Create]**.

![Kontrollpanelen [!DNL Create a key] med [!DNL 3072] bitar markerade.](../../../images/governance-privacy-security/customer-managed-keys/configure-key.png)

Den konfigurerade nyckeln visas i listan med nycklar för valvet.

![Arbetsytan [!DNL Keys] med nyckelnamnet markerat.](../../../images/governance-privacy-security/customer-managed-keys/key-added.png)

## Nästa steg

Om du vill fortsätta med engångsinstallationen av funktionen Kundhanterade nycklar följer du konfigurationsguiden för din plattforms värdmiljö:

- Använd installationsguiderna för [ API ](./api-set-up.md) eller [UI](./ui-set-up.md) för [!DNL Azure].
- Information om AWS finns i [AWS Konfigurera KMS-guiden](../aws/configure-kms.md) och [UI-installationsguiden](../aws/ui-set-up.md).
