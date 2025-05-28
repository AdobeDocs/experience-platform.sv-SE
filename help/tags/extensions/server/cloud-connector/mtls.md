---
title: mTLS (Mutual Transport Layer Security) - översikt
description: Lär dig hur du kan använda mTLS för att säkert hämta offentliga certifikat som utfärdats av Adobe för händelsevidarebefordran.
exl-id: e8ee8655-213d-4d2a-93d4-d62824b53b1d
source-git-commit: ab16cc3f70ec54460c7c4834e665c828d75d4d9e
workflow-type: tm+mt
source-wordcount: '605'
ht-degree: 0%

---

# Översikt över säkerhet för lager för ömsesidig transport ([!DNL mTLS])

Bind certifikat för ömsesidigt transportskikt ([!DNL mTLS]) i [!UICONTROL Environments UI] för att ta kontroll över säkerheten för tillägget. Certifikatet [!DNL mTLS] är en digital autentiseringsuppgift som bevisar identiteten på en server eller klient i säker kommunikation. När du använder tjänst-API:t [!DNL mTLS] hjälper dessa certifikat dig att verifiera och kryptera din interaktion med Adobe Experience Platform Event Forwarding. Denna process skyddar inte bara dina data, utan säkerställer även att alla anslutningar kommer från en betrodd partner.

## Implementera [!DNL mTLS] i en ny miljö {#implement-mtls}

Konfigurera miljön för händelsevidarebefordran för att säkerställa att dina biblioteksbyggen distribueras korrekt till gränsnätverket. Under installationen kan du välja det värdalternativ som bäst passar dina distributionsbehov. Ett [!DNL mTLS]-certifikat läggs också automatiskt till i den nya miljön för säker kommunikation.

Om du vill skapa en ny miljö väljer du fliken **[!UICONTROL Environments]** i den vänstra panelen i egenskaperna för vidarebefordran av händelser och väljer sedan **[!UICONTROL Add Environment]**.

![Egenskaper för vidarebefordran av händelser visar befintliga miljöer, markering [!UICONTROL Add Environment].](../../../images/extensions/server/cloud-connector/add-environment.png)

På nästa sida väljer du den miljö som du vill använda för den här konfigurationen. Det finns tre tillgängliga miljöer:

>[!NOTE]
>
>En egenskap är begränsad till en utveckling, en mellanlagring och en produktionsmiljö.

| Miljö | Beskrivning |
| --- | --- |
| Utveckling | Utvecklingsmiljön är till för att teammedlemmar ska kunna testa bibliotek eller ändringar i händelsevidarebefordran. |
| Mellanlagring | Mellanlagringsmiljön är valfri och tillåter att godkända teammedlemmar testar och godkänner ett bibliotek innan det publiceras. |
| Produktion | Produktionsmiljön används för produktionsdata i realtid. |

![Miljön väljer skärm och [!UICONTROL Select] markeras för utveckling.](../../../images/extensions/server/cloud-connector/select-environment.png)

Ange en **[!UICONTROL Name]** på sidan **[!UICONTROL Create Environment]** och välj ***Adobe Managed*** i listrutan **[!UICONTROL Select Host]**. **[!UICONTROL Certificate]** har ***lagts till automatiskt***. Välj slutligen **[!UICONTROL Save]**.

![Sidan Skapa utvecklingsmiljö, som markerar [!UICONTROL Name], [!UICONTROL Select Host] och [!UICONTROL Save].](../../../images/extensions/server/cloud-connector/create-environment.png)

Miljön har skapats och du återgår till fliken **[!UICONTROL Environments]** som visar den nya miljön.

![Fliken [!UICONTROL Environments] som markerar utvecklingsmiljön.](../../../images/extensions/server/cloud-connector/new-environment-created.png)

## Visa information om miljöcertifikat {#view-certificate}

Om du vill visa certifikatinformation för en miljö väljer du fliken **[!UICONTROL Environments]** i den vänstra panelen i egenskaperna för vidarebefordran av händelser och väljer sedan miljön för att visa information.

Följande certifikatinformation visas:

| Fältnamn | Beskrivning |
| --- | --- |
| Certifikat | Uppgifter om certifikatet, som omfattar<ul><li>**Namn**: Namnet på certifikatet.</li><li>**Skapad**: Datumet då certifikatet skapades.</li><li>**Status**: Certifikatets aktuella status:<ul><li>**Aktuell**: Certifikatet används aktivt.</li><li>**Föråldrad**: Certifikatet används inte men har inte gått ut ännu. Den kan fortfarande väljas för användning.</li><li>**Utgånget**: Certifikatet har upphört att gälla, är nedtonat och inte längre tillgängligt för användning.</li></ul></ul> |
| Upphör | Det datum då certifikatet upphör att gälla. |
| Variabelnamn | Variabelnamnet för certifikatet. |
| Status | Certifikatets aktuella status:<ul><li>**Depolyed**: Certifikatet har distribuerats och är aktivt.</li><li>**Distribuerar**: Certifikatet distribueras.</li><li>**Behöver distribueras**: Den här statusen visas när ett föråldrat certifikat har valts.</li></ul> |

![Sidan Redigera utvecklingsmiljö där [!UICONTROL Certificate] information markeras.](../../../images/extensions/server/cloud-connector/certificate-details.png)

### Välj och distribuera ett föråldrat certifikat {#deploy-obsolete-certificate}

Om du vill använda ett föråldrat certifikat går du till fliken **[!UICONTROL Environments]** i den vänstra panelen i egenskaperna för vidarebefordran av händelser och väljer sedan miljön för att visa informationen om certifikatet.

![Fliken [!UICONTROL Environments] som markerar utvecklingsmiljön.](../../../images/extensions/server/cloud-connector/new-environment-created.png)

Välj ett föråldrat certifikat i listrutan **[!UICONTROL Certificate]** och välj sedan **[!UICONTROL Save]**.

![Sidan Redigera utvecklingsmiljö, markera [!UICONTROL Certificate] i listrutan med föråldrat certifikat och Spara markerad.](../../../images/extensions/server/cloud-connector/obsolete-certificate.png)

Om du vill distribuera certifikatet väljer du **[!UICONTROL Save and deploy]** i dialogrutan **[!UICONTROL Deploy Certificate]**.

![Distribuera certifikatdialogruta med Spara och distribuera markerat.](../../../images/extensions/server/cloud-connector/obsolete-certificate-deploy.png)


## Nästa steg {#next-steps}

I det här dokumentet visades hur du skapar en miljö för egenskapen för händelsevidarebefordran, lägger till ett certifikat och använder ett föråldrat certifikat. Mer information om [!DNL mTLS]-certifikaten finns i [[!DNL mTLS] Översikt över tjänst-API:t](../../../../data-governance/mtls-api/overview.md)

Mer information om hur du använder [!DNL mTLS]-certifikat i reglerna för händelsevidarebefordran finns i översikten för [Cloud Connector-tillägget](../cloud-connector/overview.md/#mtls-rules).
