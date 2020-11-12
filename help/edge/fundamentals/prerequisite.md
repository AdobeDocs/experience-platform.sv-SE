---
title: Krav för att använda Adobe Experience Platform Web SDK
seo-title: Krav för att använda Adobe Experience Platform Web SDK
description: Krav för att använda Adobe Experience Platform Web SDK
seo-description: Krav för att använda Adobe Experience Platform Web SDK
keywords: 1st-party domain;CNAME;schema;create schema;launch;aep web sdk extension;extension;configuration id;configuration tool;data element;create data element;XDM Object;sendEvent;send Event;
translation-type: tm+mt
source-git-commit: 930e98502294cfd4ce86188246b6c33eb0744634
workflow-type: tm+mt
source-wordcount: '189'
ht-degree: 0%

---


# Krav för att använda Adobe Experience Platform Web SDK

Om du vill använda denna SDK måste du först:

- Etablera din organisation för den här funktionen. (Om du vill komma med på väntelistan kontaktar du din CSM (Certified software manager).)
- Ha en [förstapartsdomän (CNAME)](https://docs.adobe.com/content/help/en/core-services/interface/ec-cookies/cookies-first-party.html) aktiverad. Om du redan har en CNAME för Adobe Analytics bör du använda den. Testning under utveckling fungerar utan CNAME, men du behöver en innan du går till produktion.

>[!IMPORTANT]
>
>**Observera att från och med 11/10/20 har CNAME-implementeringar från första part en 7-dagars utgång på alla Safari-webbläsare och mobila iOS-enheter.**

- Var berättigad till Adobe Experience Platform. Om du inte har köpt Adobe Experience Platform kommer Adobe att förse dig med Experience Platform Data Services Foundation för användning med SDK utan extra kostnad.
- Använd den senaste versionen av Visitor ID-tjänsten.
