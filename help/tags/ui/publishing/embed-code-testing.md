---
title: Testa inbäddningskoder med Adobe Experience Platform Debugger
description: Lär dig hur du använder Platform Debugger för att lokalt testa olika inbäddningskoder för Adobe Experience Platform på din webbplats.
source-git-commit: 7e27735697882065566ebdeccc36998ec368e404
workflow-type: tm+mt
source-wordcount: '506'
ht-degree: 0%

---

# Testa inbäddningskoder med Adobe Experience Platform Debugger

>[!NOTE]
>
>Adobe Experience Platform Launch har omklassificerats som en serie datainsamlingstekniker i Adobe Experience Platform. Som ett resultat av detta har flera terminologiska förändringar införts i produktdokumentationen. Se följande [dokument](../../term-updates.md) för en konsoliderad referens till terminologiska ändringar.

När du gör ändringar i kodbiblioteksbyggen i Adobe Experience Platform bör du testa dessa ändringar innan du distribuerar bygget till din produktionsmiljö. Om du inte har någon dedikerad staging- eller utvecklingsmiljö för webbplatsen kan du använda Adobe Experience Platform Debugger för att lokalt testa olika inbäddningskoder på webbplatsen.

## Förutsättningar

Den här självstudiekursen kräver en fungerande förståelse för hur du använder miljöer och bäddar in koder i användargränssnittet för datainsamling. Mer information finns i [miljööversikten](./environments.md).

Den här självstudien kräver även att du har installerat webbläsartillägget Platform Debugger. Felsökningsprogrammet för plattformen är bara tillgängligt för Chrome- och Firefox-webbläsare. Använd någon av följande länkar för att installera tillägget innan du startar självstudiekursen:

* [Felsökning för plattformen för Chrome](https://chrome.google.com/webstore/detail/adobe-experience-platform/bfnnokhpnncpkdmbokanobigaccjkpob)
* [Felsökning för plattformen i Firefox](https://addons.mozilla.org/en-US/firefox/addon/adobe-experience-platform-dbg/)

## Open Platform Debugger på din webbplats

Använd valfri webbläsare och navigera till webbplatsen och öppna tillägget för plattformsfelsökning. Den webbplats som Platform Debugger är ansluten till visas längst ned i fönstret. Om taggar för närvarande körs på din plats visas den på fliken [!UICONTROL Summary].

![](./images/embed-code-testing/summary.png)

>[!NOTE]
>
>Om plattformsfelsökaren inte ansluter från början kan du behöva läsa in webbläsarfliken som visar webbplatsen igen innan du försöker igen.

## Ersätt inbäddningskoder

När plattformsfelsökaren har anslutit till webbplatsen väljer du **[!UICONTROL Launch]** i den vänstra navigeringen. Här kan du se information om den biblioteksbygge som körs på din plats, inklusive dess miljö och tillhörande tillägg. Här väljer du **[!UICONTROL Configuration]** för att visa kontroller för hantering av inbäddningskoder.

![](./images/embed-code-testing/launch-tab.png)

Under [!UICONTROL Page Embed Codes] visas den inbäddningskod som används på din plats. Välj **[!UICONTROL Actions]** till höger om inbäddningskoden och välj sedan **[!UICONTROL Replace]**.

![](./images/embed-code-testing/replace.png)

En pover visas som uppmanar dig att ange en inbäddningskod som ersätter den aktuella koden med. Observera att om du ersätter inbäddningskoden med hjälp av plattformsfelsökaren ändras inte den inbäddningskod som distribuerats på din plats. I stället ersätter den bara den inbäddade koden som körs lokalt så att du kan testa och felsöka implementeringen av den.

Klistra in den inbäddningskod som du vill testa i den angivna textrutan och välj sedan **[!UICONTROL Apply]**.

![](./images/embed-code-testing/paste-code.png)

Fliken **[!UICONTROL Configuration]** visas igen, vilket visar att den aktiva inbäddningskoden har ersatts med den som du angav. Du kan nu använda webbläsaren för att se om den inbäddningskod som du testar fungerar som förväntat.

![](./images/embed-code-testing/code-replaced.png)

## Nästa steg

I den här självstudien beskrivs hur du lokalt byter inbäddningskoder för testning med hjälp av plattformsfelsökaren. Mer information om de olika funktionerna finns i [dokumentationen för plattformsfelsökning](https://experienceleague.adobe.com/docs/debugger/using-v2/experience-cloud-debugger.html).
