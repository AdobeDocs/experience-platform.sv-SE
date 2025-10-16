---
title: Översikt över Capillary Streaming Events
description: Lär dig att strömma data från Capillary till Experience Platform.
badge: Beta
exl-id: 3b8eb2f6-3b4a-4b91-89d4-b6d9027c6ab4
source-git-commit: 428aed259343f56a2bf493b40ff2388340fffb7b
workflow-type: tm+mt
source-wordcount: '530'
ht-degree: 0%

---

# [!DNL Capillary Streaming Events]

>[!AVAILABILITY]
>
>Källan [!DNL Capillary Streaming Events] är i betaversion. Läs [villkoren](../../home.md#terms-and-conditions) i källresursöversikten om du vill ha mer information om hur du använder betatecknade källor.

[!DNL Capillary Technologies] är en ledande lojalitets- och engagemangsplattform som är betrodd av över 300 varumärken runt om i världen. Använd [!DNL Capillary Streaming Events]-källan för att göra det möjligt för ditt företag att strömma kundprofiler, lojalitetsdata och transaktionshändelser från [!DNL Capillary] till Adobe Experience Platform. Anslut [!DNL Capillary]-källan för att aktivera personalisering i realtid, avancerad målgruppssegmentering och flerkanalskampanjer.

Genom att integrera [!DNL Capillary] med Experience Platform kan du:

* Synkronisera **förmånspunkter, nivåer och belöningar** i realtid.
* Skicka **transaktionsdata** till Experience Platform för analys och aktivering.
* Använd Real-Time CDP, Experience Platform och Adobe Journey Optimizer för segmentering, resesamordning och personalisering.

## Förhandskrav

Innan du ansluter [!DNL Capillary] till Adobe Experience Platform måste du ha följande:

* Ett giltigt **Adobe-organisations-ID** och åtkomst till en aktiverad Experience Platform-sandlåda.
* Du måste ha både behörighet **[!UICONTROL View Sources]** och behörighet **[!UICONTROL Manage Sources]** aktiverat för ditt konto för att kunna ansluta ditt [!DNL Capillary]-konto till Experience Platform. Kontakta produktadministratören för att få den behörighet som krävs. Mer information finns i [användargränssnittsguiden för åtkomstkontroll](../../../access-control/ui/overview.md).

### Skapa ett schema

Du måste skapa ett XDM-schema (Experience Data Model) för att beskriva en datauppsättning som kan lagra möjliga fält och datatyper som ska skickas från [!DNL Capillary].

1. Logga in på Adobe Experience Platform och gå till Experience Platform via din organisations inloggning.
2. I den vänstra navigeringspanelen väljer du **[!UICONTROL Schemas]** för att öppna arbetsytan i [!UICONTROL Schemas].
3. Välj **[!UICONTROL Create schema]** i det övre högra hörnet.
4. I dialogrutan Skapa schema väljer du mellan **[!UICONTROL Manual creation]** (lägg till fält och fältgrupper själv) eller **[!UICONTROL ML-assisted creation]** (överför en CSV-fil och använd maskininlärning för att generera ett rekommenderat schema).
5. Välj en basklass för ditt schema (t.ex. XDM Individual Profile, XDM ExperienceEvent eller Other). Om du väljer **[!UICONTROL Other]** kan du välja bland tillgängliga anpassade klasser eller standardklasser.
6. Ange ett användarvänligt namn och en beskrivning för ditt schema.
7. Använd Schemaredigeraren för att: Lägga till fältgrupper (återanvändbara fältblock), definiera enskilda fält (anpassa namn, datatyper och alternativ) och eventuellt skapa anpassade datatyper eller fältgrupper om befintliga inte passar dina behov.
8. Granska schemastrukturen på arbetsytan. Välj **[!UICONTROL Finish]** för att skapa schemat.
9. (Valfritt) Redigera fält, lägg till beskrivningar och justera fältgrupper efter behov i Schemaredigeraren.

Mer information om hur du skapar ett XDM-schema finns i guiden om att [skapa ett schema med schemaredigeraren](../../../xdm/tutorials/create-schema-ui.md).

### Skapa en datauppsättning

Därefter måste du skapa en datauppsättning som refererar till det schema du just skapade.

1. I Experience Platform-gränssnittet väljer du [!UICONTROL Datasets] i den vänstra navigeringen för att öppna arbetsytan i [!UICONTROL Datasets].
2. Välj **[!UICONTROL Create dataset]** längst upp till höger.
3. Välj **[!UICONTROL Create dataset from schema]** i alternativen för att skapa.
4. I listan söker du efter och väljer det XDM-schema som du skapade tidigare. När du har hittat ditt schema väljer du **[!UICONTROL Next]**.
5. Ange ett unikt, beskrivande namn för datauppsättningen.
6. Om du vill kan du lägga till en beskrivning som hjälper framtida användare att identifiera datauppsättningen.
7. Välj **[!UICONTROL Finish]** om du vill skapa datauppsättningen.

Mer information om hur du skapar en datauppsättning finns i [användargränssnittsguiden för datauppsättningar](../../../catalog/datasets/user-guide.md).

## Anslut [!DNL Capillary Streaming Events] till Experience Platform

När du har slutfört kravkonfigurationen för [!DNL Capillary] kan du läsa [[!DNL Capillary Streaming Events] självstudiekursen för användargränssnitt](../../tutorials/ui/create/loyalty/capillary.md) och lära dig hur du kan ansluta ditt konto och strömma data från [!DNL Capillary] till Experience Platform.
