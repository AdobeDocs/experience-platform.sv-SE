---
title: Målgruppslivscykel i Experience Platform och direktuppspelningsmål
description: Läs om hur målgruppsnamn och målmappningar från Experience Platform återspeglas i målplattformarna för direktuppspelning.
source-git-commit: 6b4dfa714e078fb5b97900811aade081ffef0d78
workflow-type: tm+mt
source-wordcount: '467'
ht-degree: 1%

---


# Målgruppens livscykel på direktuppspelningsmål

På den här sidan beskrivs hur målgruppsuppdateringar och mappningar i Experience Platform synkroniseras med målplattformar för direktuppspelning. När du ändrar målgruppsnamn eller tar bort målgruppsmappningar i Experience Platform varierar beteendet beroende på målplattformens funktioner.

Det är viktigt att du förstår dessa skillnader för att kunna hantera målgruppernas livscykler och se till att målplattformarna speglar målgruppernas aktuella status i Experience Platform.

## Spridningsbeteende för målgruppsnamn {#audience-name-propagation}

När du aktiverar en målgrupp till ett direktuppspelat mål skickas målgruppsnamnet till målplatsen under den första aktiveringen. Beteendet för uppdatering av målgruppsnamn varierar dock beroende på mål:

* **[Destinationer som stöder uppdatering av målgruppsnamn](#name-update-supported)**: Om du ändrar ett målgruppsnamn i Experience Platform kommer det uppdaterade namnet automatiskt att spridas till dessa mål.
* **[Destinationer som inte stöder uppdatering av målgruppsnamn](#name-update-not-supported)**: Om du ändrar ett målgruppsnamn i Experience Platform kommer målplatsen att fortsätta använda det ursprungliga namnet från den första aktiveringen.

### Destinationer som stöder uppdatering av målgruppsnamn {#name-update-supported}

Följande mål för direktuppspelning stöder automatisk uppdatering av målgruppsnamn när du ändrar målgruppsnamn i Experience Platform:

* [Acxiom Audience Connection](../catalog/advertising/acxiom-audience-connection.md)
* [Adobe Campaign Managed Cloud](../catalog/email-marketing/adobe-campaign-managed-services.md)
* [Advertising Cloud DSP](../catalog/advertising/adobe-advertising-cloud-connection.md)
* [Bombora](../catalog/advertising/bombora.md)
* [Criteo](../catalog/advertising/criteo.md)
* [Demandbase](../catalog/advertising/demandbase.md)
* [Demandbase-användare](../catalog/advertising/demandbase-people.md)
* [Experience Cloud-målgrupper](../catalog/adobe/experience-cloud-audiences.md)
* [Anpassad målgrupp för Facebook](../catalog/social/facebook.md)
* [Gainsight PX](../catalog/analytics/gainsight-px.md)
* [LINJE](../catalog/mobile-engagement/line.md)
* [(Företag) LinkedIn Matched Audience](../catalog/social/linkedin-b2b.md)
* [LinkedIn Matched Audience](../catalog/social/linkedin.md)
* [(Äldre) (V2) Marketo Engage](../catalog/adobe/marketo-engage.md)
* [PubMatic Connect](../catalog/advertising/pubmatic.md)
* [SendGrid](../catalog/email-marketing/sendgrid.md)
* [Snap Inc](../catalog/advertising/snap-inc.md)
* [TikTok](../catalog/social/tiktok.md)
* [Twitter-anpassade målgrupper](../catalog/social/twitter.md)
* [Yahoo DataX](../catalog/advertising/datax.md)

### Destinationer som inte stöder uppdatering av målgruppsnamn {#name-update-not-supported}

För mål som inte anges ovan förblir målgruppsnamnen statiska efter den första aktiveringen. Om du behöver uppdatera ett målgruppsnamn för dessa destinationer måste du:

1. Skapa en ny publik i Experience Platform med det namn man önskar
2. Aktivera den nya målgruppen för målet

>[!TIP]
>
>Undvik förvirring genom att använda beskrivande målgruppsnamn från den första aktiveringen, särskilt när du aktiverar till mål som inte stöder uppdatering av målgruppsnamn.

## Destinationer som stöder målgruppsborttagning {#support-removal}

När du tar bort (tar bort mappning) en målgrupp från ett direktuppspelningsmål försöker Experience Platform ta bort motsvarande målgrupp från målplattformen. Alla mål har dock inte stöd för den här funktionen.

Följande mål för direktuppspelning stöder automatisk målgruppsborttagning när du tar bort mappningen för en målgrupp från målet:

* [(API) Oracle Eloqua](../catalog/email-marketing/oracle-eloqua-api.md)
* [(Företag) LinkedIn Matched Audience](../catalog/social/linkedin-b2b.md)
* [(Äldre) (V2) Marketo Engage](../catalog/adobe/marketo-engage.md)
* [Adobe Advertising Cloud DSP](../catalog/advertising/adobe-advertising-cloud-connection.md)
* [Målgrupper för Bombora-konto](../catalog/advertising/bombora.md)
* [Criteo](../catalog/advertising/criteo.md)
* [Experience Cloud-målgrupper](../catalog/adobe/experience-cloud-audiences.md)
* [Facebook](../catalog/social/facebook.md)
* [Gainsight PX](../catalog/analytics/gainsight-px.md)
* [HubSpot](../catalog/crm/hubspot.md)
* [LINJE](../catalog/mobile-engagement/line.md)
* [LinkedIn-matchade målgrupper](../catalog/social/linkedin.md)
* [LiveRamp - Distribution](../catalog/advertising/liveramp-distribution.md)
* [Intressekategorier för e-postmeddelanden](../catalog/email-marketing/mailchimp-interest-categories.md)
* [PubMatic Connect](../catalog/advertising/pubmatic.md)
* [Salesforce Marketing Cloud Account Engagement](../catalog/email-marketing/salesforce-marketing-cloud-account-engagement.md)
* [SendGrid](../catalog/email-marketing/sendgrid.md)
* [Snap Inc](../catalog/advertising/snap-inc.md)
* [TikTok](../catalog/social/tiktok.md)
* [Twitter-anpassade målgrupper](../catalog/social/twitter.md)
* [Yahoo DataX](../catalog/advertising/datax.md)

### Destinationer som inte stöder målgruppsborttagning

För mål som inte listas ovan tas mappningen endast bort när du tar bort en målgrupp från målet. Målgruppen på målplattformen är aktiv tills du tar bort den manuellt på partnerplattformen.
