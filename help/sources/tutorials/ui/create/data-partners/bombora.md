---
title: Koppla Bombora-återgivning till Experience Platform med användargränssnittet
description: Lär dig hur du ansluter Bombora Intent till Experience Platform
hide: true
hidefromtoc: true
source-git-commit: 81a615b9826ed69bb050cae9c074a4e457ba128a
workflow-type: tm+mt
source-wordcount: '356'
ht-degree: 0%

---

# Anslut [!DNL Bombora Intent] till Experience Platform med användargränssnittet

Läs den här vägledningen när du vill lära dig hur du ansluter ditt [!DNL Bombora Intent]-konto till Adobe Experience Platform med användargränssnittet.

## Kom igång

Den här självstudiekursen kräver en fungerande förståelse av följande komponenter i Experience Platform:

* [Real-Time CDP B2B edition](../../../../../rtcdp/b2b-overview.md): Real-Time CDP B2B edition är särskilt utformat för marknadsförare som använder en tjänstmodell som bygger på business-to-business. Den sammanför data från flera källor och kombinerar dem i en enda vy över personer och kontoprofiler. Tack vare dessa enhetliga data kan marknadsförarna inrikta sig exakt på specifika målgrupper och engagera dessa målgrupper i alla tillgängliga kanaler.
* [Källor](../../../../home.md): Med Experience Platform kan data hämtas från olika källor samtidigt som du kan strukturera, etikettera och förbättra inkommande data med hjälp av Experience Platform tjänster.
* [Sandlådor](../../../../../sandboxes/home.md): Experience Platform tillhandahåller virtuella sandlådor som partitionerar en enda Experience Platform-instans till separata virtuella miljöer för att utveckla och utveckla program för digitala upplevelser.

## Navigera i källkatalogen

I plattformsgränssnittet väljer du **[!UICONTROL Sources]** i den vänstra navigeringen för att komma åt arbetsytan i [!UICONTROL Sources]. Du kan välja lämplig kategori i katalogen till vänster på skärmen. Du kan också hitta den källa du vill arbeta med med med sökalternativet.

Välj **[!DNL Bombora Intent]** under kategorin *[!UICONTROL B2B]* och välj sedan **[!UICONTROL Set up]**.

>[!TIP]
>
>Källor i källkatalogen visar alternativet **[!UICONTROL Set up]** när en angiven källa ännu inte har något autentiserat konto. När det finns ett autentiserat konto ändras det här alternativet till **[!UICONTROL Add data]**.



## Använd ett befintligt konto {#existing}

## Skapa ett nytt konto {#create}

## Ange information om dataflöde {#provide-dataflow-details}

>[!CONTEXTUALHELP]
>id="platform_sources_bombora_domain"
>title="Domänkälla"
>abstract="Adobe använder XDM accountOrganization.website, men det kan finnas kunder som använder anpassade fält för sina respektive webbplatser. Därför måste du se till att domänkällan är det domän-/webbplatsfält som matchar dina Bombora-kontoposter mot Experience Platform-konton."

## Schemalägg dataflöde {#schedule-dataflow}

>[!CONTEXTUALHELP]
>id="platform_sources_bombora_schedule"
>title="Schemalägg ditt dataflöde"
>abstract="Bombora släpper data en gång i veckan på måndag morgon klockan 17:00 UTC. Därför måste du konfigurera starttiden för ditt intag efter 17:00 UTC. Dessutom måste du bekräfta tiden det tar att få tag på Bombora eftersom de kan ändra deras schema när de släpper filer till Adobe."


## Granska dataflöde {#review-dataflow}
