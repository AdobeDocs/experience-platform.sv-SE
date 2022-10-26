---
title: Scheman i Real-time Customer Data Platform B2B Edition
description: En översikt över XDM-schemats (Experience Data Model) roll i Adobe Real-time Customer Data Platform B2B Edition.
exl-id: 3b18d377-108f-443f-86ae-dc7537cf9013
source-git-commit: 14e3eff3ea2469023823a35ee1112568f5b5f4f7
workflow-type: tm+mt
source-wordcount: '237'
ht-degree: 0%

---

# Scheman i Real-time Customer Data Platform B2B Edition

Adobe Real-time Customer Data Platform B2B Edition innehåller flera standardprogram [XDM-klasser (Experience Data Model)](../../xdm/schema/composition.md#class) som samlar in information om viktiga B2B-datatjänster, som konton, möjligheter, kampanjer med mera. Dessutom kan du med Real-Time CDP B2B Edition definiera många-till-ett-relationer mellan dessa scheman så att de kan delta i avancerad segmenteringsanvändning.

>[!IMPORTANT]
>
>Du måste ha tillgång till Real-Time CDP B2B Edition för att B2B-scheman ska kunna delta i [Kundprofil i realtid](../../profile/home.md).

Följande standardklasser finns i Real-Time CDP B2B Edition:

* [XDM Business Account](../../xdm/classes/b2b/business-account.md)
* [XDM Business Account Person Relation](../../xdm/classes/b2b/business-account-person-relation.md)
* [XDM Business Campaign](../../xdm/classes/b2b/business-campaign.md)
* [XDM Business Campaign-medlemmar](../../xdm/classes/b2b/business-campaign-members.md)
* [XDM - affärsmöjlighet](../../xdm/classes/b2b/business-opportunity.md)
* [XDM - affärsmöjlighet, personrelation](../../xdm/classes/b2b/business-opportunity-person-relation.md)
* [XDM Business Marketing List](../../xdm/classes/b2b/business-marketing-list.md)
* [XDM Business Marketing List-medlemmar](../../xdm/classes/b2b/business-marketing-list-members.md)

Om du vill veta hur scheman passar in i ditt B2B-arbetsflöde kan du läsa [självstudiekurs från början till slut](../b2b-tutorial.md).

Anvisningar om hur du skapar en många-till-ett-relation mellan två scheman finns i självstudiekursen om [definiera B2B-schemarelationer](../../xdm/tutorials/relationship-b2b.md).

Om du använder en B2B-källanslutning kan du använda ett verktyg för att automatiskt generera nödvändiga scheman och relationerna mellan dem. Se guiden [B2B-namnutrymmen](../../sources/connectors/adobe-applications/marketo/marketo-namespaces.md) i källdokumentationen för mer information.
