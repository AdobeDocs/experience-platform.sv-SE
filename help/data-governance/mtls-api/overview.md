---
title: MTLS API-guide
description: Lär dig hur du använder API:t för mTLS-tjänsten för att på ett säkert sätt hämta och verifiera de offentliga certifikat som utfärdas av Adobe.
role: Developer
source-git-commit: f805d03ff2cd3a4f84ca8068023d83986f8bdfbb
workflow-type: tm+mt
source-wordcount: '196'
ht-degree: 0%

---

# API-översikt för MTLS-tjänst

Använd API:t för MTLS-tjänsten för att på ett säkert sätt hämta offentliga certifikat som utfärdats av Adobe för organisationens program. Detta API säkerställer att datautbytet mellan era kunder och Adobe Experience Platform autentiseras och krypteras, vilket ger ytterligare ett säkerhetslager. Genom att externt verifiera certifikatens äkthet kan du öka förtroendet och skydda känslig information.

## Offentligt certifikat

Ett offentligt certifikat är ett digitalt dokument som används för att autentisera identiteten på en server eller klient i säker kommunikation. I samband med mTLS Service API säkerställer dessa certifikat att datautbyten med Adobe Experience Platform autentiseras och krypteras. När du hämtar och verifierar dessa certifikat via API bekräftas deras äkthet, vilket förbättrar säkerheten och tillförlitligheten för dina datatransaktioner och skyddar känslig information. Om du vill lära dig hur du hämtar ditt offentliga certifikat kan du läsa [slutpunktshandboken](./public-certificate-endpoint.md) och lära dig hur du ringer.

## Nästa steg

Om du vill börja ringa anrop med MTLS Service API:t läser du [kom igång-guiden](./getting-started.md) för viktig information om obligatoriska huvuden, läsning av exempel-API-anrop och mycket mer.
