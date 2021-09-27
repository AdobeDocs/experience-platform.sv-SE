---
title: Scheman i Real-time Customer Data Platform B2B Edition
description: En översikt över XDM-schemats (Experience Data Model) roll i kunddataplattformen B2B Edition i realtid.
source-git-commit: d83ad2870b6099d3c6359dcc7cd000ecad8a238f
workflow-type: tm+mt
source-wordcount: '218'
ht-degree: 0%

---

# Scheman i Real-time Customer Data Platform B2B Edition (beta)

>[!IMPORTANT]
>
>Real-time Customer Data Platform B2B Edition är för närvarande i betaversion. Dokumentationen och funktionerna kan komma att ändras.

Real-time Customer Data Platform B2B Edition innehåller flera [XDM-klasser (Experience Data Model)](../../xdm/schema/composition.md#class) som samlar in information om viktiga B2B-datatabeller, som konton, möjligheter, kampanjer med mera. Dessutom kan ni med CDP B2B Edition i realtid definiera många-till-ett-relationer mellan dessa scheman så att de kan delta i avancerad segmenteringsanvändning.

Följande standardklasser finns i CDP B2B Edition i realtid:

* [XDM Business Account](../../xdm/classes/b2b/business-account.md)
* [XDM Business Account Person Relation](../../xdm/classes/b2b/business-account-person-relation.md)
* [XDM Business Campaign](../../xdm/classes/b2b/business-campaign.md)
* [XDM Business Campaign-medlemmar](../../xdm/classes/b2b/business-campaign-members.md)
* [XDM - affärsmöjlighet](../../xdm/classes/b2b/business-opportunity.md)
* [XDM - affärsmöjlighet, personrelation](../../xdm/classes/b2b/business-opportunity-person-relation.md)
* [XDM Business Marketing List](../../xdm/classes/b2b/business-marketing-list.md)
* [XDM Business Marketing List-medlemmar](../../xdm/classes/b2b/business-marketing-list-members.md)

Anvisningar om hur du skapar en många-till-ett-relation mellan två scheman finns i självstudiekursen om [att definiera B2B-schemarelationer](../../xdm/tutorials/relationship-b2b.md).

Om du använder en B2B-källanslutning kan du använda ett verktyg för att automatiskt generera nödvändiga scheman och relationerna mellan dem. Mer information finns i guiden om [B2B-namnutrymmen](../../sources/connectors/adobe-applications/marketo/marketo-namespaces.md) i källdokumentationen.
