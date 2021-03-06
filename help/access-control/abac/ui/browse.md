---
keywords: Experience Platform;hem;populära ämnen;åtkomstkontroll;attributbaserad åtkomstkontroll;ABAC
title: Attributbaserad åtkomstkontrollbläddring
description: Det här dokumentet innehåller information om hur du använder gränssnittet Behörigheter i Adobe Experience Cloud
exl-id: 39634bde-8858-44a6-b39a-776846654fc1
source-git-commit: c31855bff9d87133252c43e2f2f2fe1960c7b144
workflow-type: tm+mt
source-wordcount: '374'
ht-degree: 3%

---

# Behörighetsguide

>[!IMPORTANT]
>
>Attributbaserad åtkomstkontroll är för närvarande tillgänglig i en begränsad version för USA-baserade vårdkunder. Den här funktionen kommer att vara tillgänglig för alla Real-time Customer Data Platform-kunder när den släpps helt.

Behörigheter är det område i Adobe Experience Cloud där administratörer kan definiera användarroller och åtkomstprinciper för att hantera åtkomstbehörigheter för funktioner och objekt i ett produktprogram.

Med behörigheter kan du konfigurera:

* [Etiketter](./labels.md)
* [Behörigheter](./permissions.md)
* [Profiler](./permissions.md)
* [Roller](./roles.md)
* [Sandlådor](./sandboxes.md)
* [Användare](./users.md)

För att få åtkomst till attributbaserade åtkomstkontrollsbehörigheter för [!DNL Experience Cloud]måste du vara administratör för din organisation som har en prenumeration på [!DNL Experience Cloud]. Adobe stöder flexibla administratörshierarkier för dina organisationer, men du måste vara produktadministratör för Adobe Experience Platform för att kunna konfigurera behörigheter. Se Adobe Help Center artikel om [administrativa roller](https://helpx.adobe.com/enterprise/using/admin-roles.html) för mer information.

Om du inte har administratörsbehörighet kontaktar du systemadministratören för att få åtkomst.

När du har administratörsbehörighet går du till [Adobe Experience Cloud](https://experience.adobe.com/) och logga in med dina inloggningsuppgifter för Adobe. När du är inloggad visas **[!UICONTROL Overview]** visas för din organisation som du har administratörsbehörighet för. På den här sidan visas de produkter som din organisation prenumererar på, tillsammans med andra kontroller för att lägga till användare och administratörer i organisationen som helhet. Välj **[!UICONTROL Permissions]** för att öppna den attributbaserade åtkomstkontrollsarbetsytan för plattformsintegreringen.

![flac-select-product](../../images/flac-ui/flac-select-product.png)

Den attributbaserade åtkomstkontrollsarbetsytan för Adobe Experience Cloud visas på **[!UICONTROL Roles]** sida. På den här sidan kan du visa alla roller och hantera olika inställningar enligt beskrivningen i det här dokumentet.

>[!IMPORTANT]
>
>När din organisation har aktiverats för attributbaserad åtkomstkontroll kan du börja använda behörigheter på Adobe Experience Cloud i stället för produktprofiler i Adobe Admin Console för att hantera behörigheter för användare, funktioner, etiketter och andra resurser i din organisation.

![flash-select-roles](../../images/flac-ui/flac-select-roles.png)

Den här användarhandboken fokuserar på hur du använder [!DNL Experience Cloud] för att tilldela behörigheter för plattformen. Mer allmän information om navigering finns i [!DNL Admin Console], se [Användarhandbok för Admin Console](https://helpx.adobe.com/enterprise/using/admin-console.html).

## Nästa steg

När du har navigerat på arbetsytan för behörigheter fortsätter du till nästa steg till [skapa en ny roll](roles.md).
