---
title: Scheman i Real-time Customer Data Platform B2B Edition (beta)
description: En översikt över XDM-schemats (Experience Data Model) roll i Real-time Customer Data Platform B2B Edition.
exl-id: 3b18d377-108f-443f-86ae-dc7537cf9013
source-git-commit: 6f421a8ae77318ca2598d640cf7e27ea485ec9db
workflow-type: tm+mt
source-wordcount: '219'
ht-degree: 0%

---

# Scheman i Real-time Customer Data Platform B2B Edition (beta)

>[!IMPORTANT]
>
>Real-time Customer Data Platform B2B Edition är för närvarande i betaversion. Dokumentationen och funktionerna kan komma att ändras.

Real-time Customer Data Platform B2B Edition innehåller flera standardprogram [XDM-klasser (Experience Data Model)](../../xdm/schema/composition.md#class) som samlar in information om viktiga B2B-datatjänster, som konton, möjligheter, kampanjer med mera. Dessutom kan ni med CDP B2B Edition i realtid definiera många-till-ett-relationer mellan dessa scheman så att de kan delta i avancerad segmenteringsanvändning.

Följande standardklasser finns i CDP B2B Edition i realtid:

* [XDM Business Account](../../xdm/classes/b2b/business-account.md)
* [XDM Business Account Person Relation](../../xdm/classes/b2b/business-account-person-relation.md)
* [XDM Business Campaign](../../xdm/classes/b2b/business-campaign.md)
* [XDM Business Campaign-medlemmar](../../xdm/classes/b2b/business-campaign-members.md)
* [XDM - affärsmöjlighet](../../xdm/classes/b2b/business-opportunity.md)
* [XDM - affärsmöjlighet, personrelation](../../xdm/classes/b2b/business-opportunity-person-relation.md)
* [XDM Business Marketing List](../../xdm/classes/b2b/business-marketing-list.md)
* [XDM Business Marketing List-medlemmar](../../xdm/classes/b2b/business-marketing-list-members.md)

Anvisningar om hur du skapar en många-till-ett-relation mellan två scheman finns i självstudiekursen om [definiera B2B-schemarelationer](../../xdm/tutorials/relationship-b2b.md).

Om du använder en B2B-källanslutning kan du använda ett verktyg för att automatiskt generera nödvändiga scheman och relationerna mellan dem. Se guiden [B2B-namnutrymmen](../../sources/connectors/adobe-applications/marketo/marketo-namespaces.md) i källdokumentationen för mer information.
