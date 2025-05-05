---
title: Scheman i Real-time Customer Data Platform B2B Edition
description: En översikt över XDM-schemats (Experience Data Model) roll i Adobe Real-time Customer Data Platform B2B Edition.
feature: Get Started, Data Management, Schemas
badgeB2B: label="B2B Edition" type="Informative" url="https://helpx.adobe.com/se/legal/product-descriptions/real-time-customer-data-platform-b2b-edition-prime-and-ultimate-packages.html newtab=true"
exl-id: 3b18d377-108f-443f-86ae-dc7537cf9013
source-git-commit: db57fa753a3980dca671d476521f9849147880f1
workflow-type: tm+mt
source-wordcount: '229'
ht-degree: 0%

---

# Scheman i Real-time Customer Data Platform B2B Edition

Adobe Real-time Customer Data Platform B2B Edition innehåller flera standardklasser [i Experience Data Model (XDM)](../../xdm/schema/composition.md#class) som samlar in information om viktiga B2B-datatabeller, som konton, affärsmöjligheter, kampanjer med mera. Dessutom kan du med Real-Time CDP B2B Edition definiera många-till-ett-relationer mellan dessa scheman så att de kan delta i avancerad segmenteringsanvändning.

>[!IMPORTANT]
>
>Du måste ha tillgång till Real-Time CDP B2B Edition för att B2B-scheman ska kunna delta i [kundprofilen i realtid](../../profile/home.md).

Följande standardklasser finns i Real-Time CDP B2B Edition:

* [XDM Business Account](../../xdm/classes/b2b/business-account.md)
* [XDM Business Account Person Relation](../../xdm/classes/b2b/business-account-person-relation.md)
* [XDM Business Campaign](../../xdm/classes/b2b/business-campaign.md)
* [XDM Business Campaign-medlemmar](../../xdm/classes/b2b/business-campaign-members.md)
* [XDM - affärsmöjlighet](../../xdm/classes/b2b/business-opportunity.md)
* [XDM - affärsmöjlighet, personrelation](../../xdm/classes/b2b/business-opportunity-person-relation.md)
* [XDM Business Marketing List](../../xdm/classes/b2b/business-marketing-list.md)
* [XDM Business Marketing List-medlemmar](../../xdm/classes/b2b/business-marketing-list-members.md)

Mer information om hur scheman passar in i ditt B2B-arbetsflöde finns i [den kompletta självstudiekursen](../b2b-tutorial.md).

Anvisningar om hur du skapar en många-till-ett-relation mellan två scheman finns i självstudiekursen [om hur du definierar B2B-schemarelationer](../../xdm/tutorials/relationship-b2b.md).

Om du använder en B2B-källanslutning kan du använda ett verktyg för att automatiskt generera nödvändiga scheman och relationerna mellan dem. Mer information finns i guiden om [B2B-namnutrymmen](../../sources/connectors/adobe-applications/marketo/marketo-namespaces.md) i källdokumentationen.
