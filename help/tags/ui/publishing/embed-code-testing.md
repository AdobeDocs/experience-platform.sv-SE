---
title: Testa inbäddningskoder med Adobe Experience Platform Debugger
description: Lär dig hur du använder Platform Debugger för att lokalt testa olika inbäddningskoder för Adobe Experience Platform på din webbplats.
exl-id: ae6183b9-0d25-49d0-b0e9-f8b5ba58ab33
source-git-commit: d81c4c8630598597ec4e253ef5be9f26c8987203
workflow-type: tm+mt
source-wordcount: '478'
ht-degree: 0%

---

# Testa inbäddningskoder med Adobe Experience Platform Debugger

>[!NOTE]
>
>Adobe Experience Platform Launch har omklassificerats som en serie datainsamlingstekniker i Adobe Experience Platform. Som ett resultat av detta har flera terminologiska förändringar införts i produktdokumentationen. I följande [dokument](../../term-updates.md) finns en konsoliderad referens till de ändrade terminologin.

När du gör ändringar i kodbiblioteksbyggen i Adobe Experience Platform bör du testa dessa ändringar innan du distribuerar bygget till din produktionsmiljö. Om du inte har någon dedikerad staging- eller utvecklingsmiljö för webbplatsen kan du använda Adobe Experience Platform Debugger för att lokalt testa olika inbäddningskoder på webbplatsen.

## Förhandskrav

Den här självstudiekursen kräver en fungerande förståelse för hur du använder miljöer och bäddar in koder för taggar. Mer information finns i [miljööversikten](./environments.md).

Den här självstudien kräver även att du har installerat webbläsartillägget Platform Debugger. Felsökningsprogrammet för plattformen är tillgängligt för Chrome webbläsare. Använd följande länk för att installera tillägget innan du startar självstudiekursen:

* [Felsökning för Chrome](https://chrome.google.com/webstore/detail/adobe-experience-platform/bfnnokhpnncpkdmbokanobigaccjkpob)

## Open Platform Debugger på din webbplats

Använd valfri webbläsare och navigera till webbplatsen och öppna tillägget för plattformsfelsökning. Den webbplats som Platform Debugger är ansluten till visas längst ned i fönstret. Om taggar för närvarande körs på din plats visas den på fliken [!UICONTROL Summary].

![](./images/embed-code-testing/summary.png)

>[!NOTE]
>
>Om plattformsfelsökaren inte ansluter från början kan du behöva läsa in webbläsarfliken som visar webbplatsen igen innan du försöker igen.

## Ersätt inbäddningskoder

När plattformsfelsökaren har anslutit till webbplatsen väljer du **[!UICONTROL Launch]** i den vänstra navigeringen. Här kan du se information om den biblioteksbygge som för närvarande körs på din plats, inklusive dess miljö och tillhörande tillägg. Här väljer du **[!UICONTROL Configuration]** om du vill visa kontroller för att hantera inbäddningskoder.

![](./images/embed-code-testing/launch-tab.png)

Under [!UICONTROL Page Embed Codes] visas den inbäddningskod som används för din webbplats. Välj **[!UICONTROL Actions]** till höger om inbäddningskoden och välj sedan **[!UICONTROL Replace]**.

![](./images/embed-code-testing/replace.png)

En pover visas som uppmanar dig att ange en inbäddningskod som ersätter den aktuella koden med. Observera att om du ersätter inbäddningskoden med hjälp av plattformsfelsökaren ändras inte den inbäddningskod som distribuerats på din plats. I stället ersätter den bara den inbäddade koden som körs lokalt så att du kan testa och felsöka implementeringen av den.

Klistra in den inbäddningskod som du vill testa i textrutan och välj sedan **[!UICONTROL Apply]**.

![](./images/embed-code-testing/paste-code.png)

Fliken **[!UICONTROL Configuration]** visas igen och visar att den inbäddade koden har ersatts med den som du angav. Du kan nu använda webbläsaren för att se om den inbäddningskod som du testar fungerar som förväntat.

![](./images/embed-code-testing/code-replaced.png)

## Nästa steg

I den här självstudien beskrivs hur du lokalt byter inbäddningskoder för testning med hjälp av plattformsfelsökaren. Mer information om de olika funktionerna finns i [dokumentationen för plattformsfelsökning](../../../debugger/home.md).
