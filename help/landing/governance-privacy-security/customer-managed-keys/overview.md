---
title: Kundhanterade nycklar i Adobe Experience Platform
description: Lär dig hur du konfigurerar egna krypteringsnycklar för data som lagras i Adobe Experience Platform.
role: Developer
feature: Privacy
exl-id: cd33e6c2-8189-4b68-a99b-ec7fccdc9b91
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '1102'
ht-degree: 0%

---

# Kundhanterade nycklar i Adobe Experience Platform

Data som lagras på Adobe Experience Platform krypteras i vila med hjälp av systemnivånycklar. Om du använder ett program som är byggt på Experience Platform kan du välja att använda dina egna krypteringsnycklar istället, vilket ger dig större kontroll över datasäkerheten.

>[!AVAILABILITY]
>
>Adobe Experience Platform stöder Customer Managed Keys (CMK) för både Microsoft Azure och Amazon Web Services (AWS). Experience Platform som körs på AWS är för närvarande tillgängligt för ett begränsat antal kunder. Om implementeringen körs på AWS kan du välja att använda nyckelhanteringstjänsten (KMS) för Experience Platform-datakryptering. Mer information om den infrastruktur som stöds finns i [Experience Platform översikt över flera moln](https://experienceleague.adobe.com/en/docs/experience-platform/landing/multi-cloud).
>
>Mer information om hur du skapar och hanterar krypteringsnycklar i AWS KMS finns i [AWS KMS-krypteringsguiden](./aws/configure-kms.md). Information om Azure-implementeringar finns i [konfigurationsguiden för Azure Key Vault](./azure/azure-key-vault-config.md).

>[!NOTE]
>
>För [!DNL Azure] värdbaserade Experience Platform-instanser krypteras kundprofildata som lagras i Experience Platform [!DNL Azure Data Lake] och profilarkivet [!DNL Azure Cosmos DB] exklusivt med CMK när de har aktiverats. Nyckelåterkallning i primära datalager kan ta mellan **några minuter och 24 timmar** och **upp till 7 dagar** för tillfälliga eller sekundära datalager. Mer information finns i [konsekvenserna av att återkalla nyckelåtkomstavsnittet](#revoke-access).

Det här dokumentet innehåller en översikt på hög nivå över processen för att aktivera funktionen för kundhanterade nycklar (CMK) i Experience Platform i hela [!DNL Azure] och AWS, tillsammans med den information som krävs för att slutföra dessa steg.

>[!NOTE]
>
>För Customer Journey Analytics-kunder följer du instruktionerna i [Customer Journey Analytics-dokumentationen](https://experienceleague.adobe.com/docs/analytics-platform/using/cja-privacy/cmk.html).

## Förhandskrav

Om du vill aktivera CMK måste plattformens värdmiljö ([!DNL Azure] eller AWS) uppfylla specifika konfigurationskrav:

### Allmänna krav

Om du vill visa och komma åt avsnittet [!UICONTROL Encryption] i Adobe Experience Platform måste du ha skapat en roll och tilldelat behörigheten [!UICONTROL Manage Customer Managed Key] till den rollen.  Alla användare med behörigheten [!UICONTROL Manage Customer Managed Key] kan aktivera CMK för sin organisation.

Mer information om hur du tilldelar roller och behörigheter i Experience Platform finns i [Konfigurera behörigheter](https://experienceleague.adobe.com/docs/platform-learn/getting-started-for-data-architects-and-data-engineers/configure-permissions.html).

### Azure-specifika krav

För Azure-värdbaserade implementeringar konfigurerar du [!DNL Azure]-nyckelvalvet med följande inställningar:

- [Aktivera rensningsskydd](https://learn.microsoft.com/en-us/azure/key-vault/general/soft-delete-overview#purge-protection)
- [Aktivera mjuk borttagning](https://learn.microsoft.com/en-us/azure/key-vault/general/soft-delete-overview)
- [Konfigurera åtkomst med  [!DNL Azure] rollbaserad åtkomstkontroll](https://learn.microsoft.com/en-us/azure/role-based-access-control/)

### AWS-specifika förutsättningar

För implementeringar som hanteras av AWS konfigurerar du din AWS-miljö enligt följande:

- Kontrollera att du har behörighet att hantera krypteringsnycklar med hjälp av AWS Identity and Access Management (IAM). Mer information finns i [IAM-principer för AWS KMS](https://docs.aws.amazon.com/kms/latest/developerguide/iam-policies.html).
- Konfigurera AWS KMS med stöd för CMK. Läs [AWS KMS-krypteringsguiden](./aws/configure-kms.md).

## Processsammanfattning {#process-summary}

Customer Managed Keys (CMK) erbjuds genom Adobe Healthcare Shield och Privacy and Security Shield. På Azure stöds CMK för både hälso- och sjukvårdssköld och sköld för skydd av privatlivet och säkerheten. På AWS stöds CMK endast för skölden för skydd av privatlivet och säkerheten och är inte tillgängligt för hälso- och sjukvårdsskölden. När organisationen har köpt en licens för något av dessa alternativ kan du påbörja engångskonfigurationsprocessen för att aktivera CMK.

>[!WARNING]
>
>När du har konfigurerat CMK kan du inte återgå till systemhanterade nycklar. Du ansvarar för att hantera dina nycklar på ett säkert sätt så att du inte förlorar åtkomsten till dina data.

Processen är följande:

### För Azure {#azure-process-summary}

1. [Konfigurera ett [!DNL Azure] nyckelvalv](./azure/azure-key-vault-config.md) baserat på din organisations principer och [generera sedan en krypteringsnyckel](./azure/azure-key-vault-config.md#generate-a-key) som du kan dela med Adobe.
1. Konfigurera CMK-appen med din [!DNL Azure]-klientorganisation genom antingen [API-anrop](./azure/api-set-up.md#register-app) eller [användargränssnittet](./azure/ui-set-up.md#register-app).
1. Skicka ditt krypteringsnyckel-ID till Adobe och starta aktiveringsprocessen för funktionen, antingen [ i användargränssnittet](./azure/ui-set-up.md#send-to-adobe) eller med ett [API-anrop](./azure/api-set-up.md#send-to-adobe).
1. Kontrollera konfigurationsstatusen för att verifiera om CMK har aktiverats, antingen [ i användargränssnittet ](./azure/ui-set-up.md#check-status) eller med ett [API-anrop](./azure/api-set-up.md#check-status).

När installationsprocessen är klar för Azure-värdbaserade Experience Platform-instanser krypteras alla data som är inskrivna i Experience Platform över alla sandlådor med hjälp av nyckelkonfigurationen för [!DNL Azure]. Om du vill använda CMK använder du [!DNL Microsoft Azure]-funktioner som kan ingå i deras [allmänna förhandsvisningsprogram](https://azure.microsoft.com/en-ca/support/legal/preview-supplemental-terms/).

### För AWS {#aws-process-summary}

1. [Konfigurera AWS KMS](./aws/configure-kms.md) genom att konfigurera en krypteringsnyckel som ska delas med Adobe.
2. Följ de AWS-specifika instruktionerna i [installationsguiden för användargränssnittet](./aws/ui-set-up.md).
3. Verifiera konfigurationen för att bekräfta att Experience Platform-data är krypterade med AWS värdnyckel.

<!--  Pending: or [API setup guide]() -->

När installationsprocessen är klar för Experience Platform-instanser som ligger på AWS krypteras alla data som är inskrivna i Experience Platform över alla sandlådor med hjälp av konfigurationen för AWS Key Management Service (KMS). Om du vill använda CMK på AWS använder du AWS nyckelhanteringstjänst för att skapa och hantera dina krypteringsnycklar i enlighet med organisationens säkerhetskrav.

## Konsekvenser av återkallande av nyckelåtkomst {#revoke-access}

Om du återkallar eller inaktiverar åtkomsten till Key Vault-, key- eller CMK-appen i Azure eller krypteringsnyckeln i AWS kan det leda till allvarliga störningar, som bland annat kan leda till att dina Experience Platform-åtgärder inte fungerar som de ska. När tangenterna har inaktiverats kan data i Experience Platform bli oåtkomliga, och alla åtgärder längre fram i kedjan som är beroende av dessa data kommer inte att fungera. Det är viktigt att förstå effekterna i efterföljande led till fullo innan du gör några ändringar i dina nyckelkonfigurationer.

Om du vill återkalla Experience Platform-åtkomst till dina data i [!DNL Azure] tar du bort den användarroll som är associerad med programmet från nyckelvalvet. För AWS kan du inaktivera nyckeln eller uppdatera policyn. Detaljerade instruktioner om AWS-processen finns i avsnittet [om nyckelspärr](./aws/ui-set-up.md#key-revocation).


### Spridningstidslinjer {#propagation-timelines}

När nyckelåtkomsten har återkallats från nyckelvalvet [!DNL Azure] kommer ändringarna att spridas enligt följande:

| **Lagringstyp** | **Beskrivning** | **Tidslinje** |
|---|---|---|
| Primära datalager | Inkluderar datalager (Azure Data Lake, AWS S3) och Azure Cosmos DB-profilarkiv. När nyckelåtkomsten har återkallats blir data oåtkomliga. | **några minuter till 24 timmar**. |
| Cachelagrade/tillfälliga datalager | Inkluderar sekundära datalager som används för prestanda och centrala programfunktioner. Effekten av nyckelspärrning fördröjs. | **Upp till 7 dagar**. |

Profilkontrollpanelen fortsätter till exempel att visa data från sin cache i upp till sju dagar innan data förfaller och uppdateras. På samma sätt tar det lika lång tid att återaktivera åtkomst till programmet för att återställa datatillgängligheten i alla dessa butiker.

>[!NOTE]
>
>Det kan ta lika lång tid att återaktivera åtkomst till programmet som att återställa datatillgängligheten i dessa butiker.

>[!TIP]
>
>Det finns två användningsspecifika undantag för sju dagars datauppsättning som förfaller på icke-primära (cachelagrade/tillfälliga) data. Mer information om dessa funktioner finns i respektive dokumentation.<ul><li>[Adobe Journey Optimizer URL Shortener](https://experienceleague.adobe.com/docs/journey-optimizer/using/sms/sms-configuration.html#message-preset-sms)</li><li>[Edge Projection](https://experienceleague.adobe.com/docs/experience-platform/profile/home.html#edge-projections)</li></ul>

## Nästa steg

Så här startar du processen:

- För Azure: Börja med [att konfigurera ett  [!DNL Azure] nyckelvalv](./azure/azure-key-vault-config.md) och [generera en krypteringsnyckel](./azure/azure-key-vault-config.md#generate-a-key) som ska delas med Adobe.
- För AWS: [Konfigurera AWS KMS](./aws/configure-kms.md) och kontrollera att IAM- och KMS-konfigurationerna är korrekta innan du fortsätter till installationsguiderna för användargränssnittet eller API.
