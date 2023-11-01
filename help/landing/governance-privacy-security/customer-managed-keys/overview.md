---
title: Kundhanterade nycklar i Adobe Experience Platform
description: Lär dig hur du konfigurerar egna krypteringsnycklar för data som lagras i Adobe Experience Platform.
exl-id: cd33e6c2-8189-4b68-a99b-ec7fccdc9b91
source-git-commit: e300e57df998836a8c388511b446e90499185705
workflow-type: tm+mt
source-wordcount: '752'
ht-degree: 0%

---

# Kundhanterade nycklar i Adobe Experience Platform

Data som lagras på Adobe Experience Platform krypteras i vila med hjälp av systemnivånycklar. Om du använder ett program som är byggt på plattformen kan du välja att använda dina egna krypteringsnycklar istället, vilket ger dig större kontroll över datasäkerheten.

>[!NOTE]
>
>Data i Adobe Experience Platform datasjön och Profile Store krypteras med CMK. Dessa betraktas som era primära datalager.

Det här dokumentet ger en översikt på hög nivå över processen för att aktivera funktionen för kundhanterade nycklar (CMK) i Platform, och den information som krävs för att slutföra dessa steg.

>[!NOTE]
>
>För Customer Journey Analytics-kunder, följ instruktionerna i [Customer Journey Analytics dokumentation](https://experienceleague.adobe.com/docs/analytics-platform/using/cja-privacy/cmk.html).

## Förutsättningar

Visa och gå till [!UICONTROL Encryption] i Adobe Experience Platform måste du ha skapat en roll och tilldelat [!UICONTROL Manage Customer Managed Key] behörighet till den rollen. Alla användare som har [!UICONTROL Manage Customer Managed Key] behörighet kan aktivera CMK för sin organisation.

Mer information om hur du tilldelar roller och behörigheter i Experience Platform finns i [konfigurera behörighetsdokumentation](https://experienceleague.adobe.com/docs/platform-learn/getting-started-for-data-architects-and-data-engineers/configure-permissions.html).

Om du vill aktivera CMK måste du [!DNL Azure] Nyckelvalv måste konfigureras med följande inställningar:

* [Aktivera rensningsskydd](https://learn.microsoft.com/en-us/azure/key-vault/general/soft-delete-overview#purge-protection)
* [Aktivera mjuk borttagning](https://learn.microsoft.com/en-us/azure/key-vault/general/soft-delete-overview)
* [Konfigurera åtkomst med [!DNL Azure] rollbaserad åtkomstkontroll](https://learn.microsoft.com/en-us/azure/role-based-access-control/)

Läs den länkade dokumentationen för att få en bättre förståelse för processen.

## Processsammanfattning {#process-summary}

CMK ingår i hälso- och sjukvårdsskölden och i skölden för skydd av privatlivet och säkerhet från Adobe. När din organisation har köpt en licens för något av dessa erbjudanden kan du påbörja en engångsprocess för att konfigurera funktionen.

>[!WARNING]
>
>När du har konfigurerat CMK kan du inte återgå till systemhanterade nycklar. Du ansvarar för att hantera dina nycklar på ett säkert sätt och ge åtkomst till dina Key Vault-, Key- och CMK-appar i [!DNL Azure] för att förhindra att dataåtkomsten går förlorad.

Processen är följande:

1. [Konfigurera en [!DNL Azure] Key Vault](./azure-key-vault-config.md) baserat på organisationens policyer, och sedan [generera en krypteringsnyckel](./azure-key-vault-config.md#generate-a-key) som till slut kommer att delas med Adobe.
1. Konfigurera CMK-appen med [!DNL Azure] via antingen [API-samtal](./api-set-up.md#register-app) eller [UI](./ui-set-up.md#register-app).
1. Skicka ditt krypteringsnyckel-ID till Adobe och starta aktiveringsprocessen för funktionen antingen [i användargränssnittet](./ui-set-up.md#send-to-adobe) eller med [API-anrop](./api-set-up.md#send-to-adobe).
1. Kontrollera statusen för konfigurationen för att verifiera om CMK har aktiverats [i användargränssnittet](./ui-set-up.md#check-status) eller med [API-anrop](./api-set-up.md#check-status).

När konfigurationen är klar krypteras alla data som är inbyggda i Platform i alla sandlådor med hjälp av [!DNL Azure] nyckelinställningar. Om du vill använda CMK använder du [!DNL Microsoft Azure] funktioner som kan vara en del av [offentligt förhandsvisningsprogram](https://azure.microsoft.com/en-ca/support/legal/preview-supplemental-terms/).

## Återkalla åtkomst {#revoke-access}

Om du vill återkalla plattformsåtkomst till dina data kan du ta bort den användarroll som är associerad med programmet från nyckelvalvet i [!DNL Azure].

>[!WARNING]
>
>Om du inaktiverar nyckelvalvet, tangenten eller CMK-appen kan det leda till en förändring. När nyckelvalvet, nyckeln eller CMK-appen är inaktiverad och data inte längre är tillgängliga i Platform, kommer eventuella åtgärder som rör dessa data inte längre att vara möjliga. Se till att du förstår vilka konsekvenser det kan få om plattformsåtkomst återkallas längre fram i kedjan innan du gör några ändringar i konfigurationen.

När du har tagit bort tangentåtkomsten eller inaktiverat/tagit bort nyckeln från [!DNL Azure] nyckelvalv, det kan ta från några minuter till 24 timmar att sprida den här konfigurationen till primära datalager. Plattformsarbetsflödena omfattar även cachelagrade och tillfälliga datalager som krävs för prestanda och centrala programfunktioner. Spridningen av CMK-spärrning via sådana cachelagrade och tillfälliga butiker kan ta upp till sju dagar enligt deras arbetsflöden för databehandling. Detta innebär till exempel att kontrollpanelen Profil behåller och visar data från sitt cache-datalager och tar sju dagar att förfalla data som lagras i cache-datalager som en del av uppdateringscykeln. Samma tidsfördröjning gäller för data som ska bli tillgängliga igen när åtkomsten till programmet återaktiveras.

>[!NOTE]
>
>Det finns två användningsspecifika undantag för sju dagars datauppsättning som förfaller på icke-primära (cachelagrade/tillfälliga) data. Mer information om dessa funktioner finns i respektive dokumentation.<ul><li>[Adobe Journey Optimizer URL Shortener](https://experienceleague.adobe.com/docs/journey-optimizer/using/sms/sms-configuration.html#message-preset-sms)</li><li>[Kantprojektioner](https://experienceleague.adobe.com/docs/experience-platform/profile/home.html#edge-projections)</li></ul>

## Nästa steg

Börja med [konfigurera en [!DNL Azure] Key Vault](./azure-key-vault-config.md) och [generera en krypteringsnyckel](./azure-key-vault-config.md#generate-a-key) att dela med Adobe.
