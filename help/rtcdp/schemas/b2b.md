---
title: Scheman i Real-Time Customer Data Platform B2B edition
description: En översikt över XDM-schemats (Experience Data Model) roll i Adobe Real-Time Customer Data Platform B2B edition.
feature: Get Started, Data Management, Schemas
badgeB2B: label="B2B edition" type="Informative" url="https://experienceleague.adobe.com/docs/experience-platform/rtcdp/intro/rtcdp-intro/overview.html?lang=sv-SE#rtcdp-editions" newtab=true
exl-id: 3b18d377-108f-443f-86ae-dc7537cf9013
source-git-commit: 5998adf98aa7250864983d7e4e629921633e1a1c
workflow-type: tm+mt
source-wordcount: '842'
ht-degree: 0%

---

# Scheman i Real-Time Customer Data Platform B2B edition

Adobe Real-Time Customer Data Platform B2B edition innehåller flera [XDM-klasser (Experience Data Model)](../../xdm/schema/composition.md#class) som är standard och som samlar in information om viktiga B2B-datatabeller, som konton, affärsmöjligheter, kampanjer med mera. Dessutom kan du med Real-Time CDP B2B edition definiera många-till-ett-relationer mellan dessa scheman så att de kan delta i avancerad segmenteringsanvändning.

>[!IMPORTANT]
>
>B2B-scheman är tillgängliga för användning i Experience Platform-program (till exempel i [Customer Journey Analytics B2B edition](https://experienceleague.adobe.com/sv/docs/analytics-platform/using/cja-overview/cja-b2b/cja-b2b-edition)). <br/>Du måste dock ha tillgång till Real-Time CDP B2B edition för att (profiler i) B2B-scheman ska kunna delta i [kundprofilen i realtid](../../profile/home.md).

Följande standardklasser finns i Real-Time CDP B2B edition:

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


Följande tabell innehåller information om de underliggande inställningarna för B2B-scheman.

>[!NOTE]
>
>Rulla åt vänster/höger för att visa hela innehållet i tabellen.

| Schemanamn | Basklass | Fältgrupper | [!DNL Profile] i schemat | Primär identitet | Namnutrymme för primär identitet | Sekundär identitet | Namnutrymme för sekundär identitet | Relation | Anteckningar |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| B2B-konto | [XDM Business Account](../../xdm/classes/b2b/business-account.md) | XDM Business Account Details | Aktiverad | `accountKey.sourceKey` i basklassen | B2B-konto | `extSourceSystemAudit.externalKey.sourceKey` i basklassen | B2B-konto | <ul><li>`accountParentKey.sourceKey` i fältgruppen XDM Business Account Details</li><li>Målegenskap: `/accountKey/sourceKey`</li><li>Typ: en-till-en</li><li>Referensschema: B2B-konto</li><li>Namnutrymme: B2B-konto</li></ul> |  |
| B2B-person | [Individuell XDM-profil](../../xdm/classes/individual-profile.md) | <ul><li>Information om XDM Business Person</li><li>XDM Business Person Components</li><li>IdentityMap</li><li>Information om samtycke och inställningar</li></ul> | Aktiverad | `b2b.personKey.sourceKey` i fältgruppen XDM Business Person Details | B2B-person | <ol><li>`extSourceSystemAudit.externalKey.sourceKey` av fältgruppen XDM Business Person Details</li><li>`workEmail.address` av fältgruppen XDM Business Person Details</ol></li> | <ol><li>B2B-person</li><li>E-post</li></ol> | <ul><li>`personComponents.sourceAccountKey.sourceKey` av fältgruppen XDM Business Person Components</li><li>Typ: Flera till ett</li><li>Referensschema: B2B-konto</li><li>Namnutrymme: B2B-konto</li><li>Destinationsegenskap: accountKey.sourceKey</li><li>Relationsnamn från aktuellt schema: Konto</li><li>Relationsnamn från referensschema: Personer</li></ul> |  |
| B2B-säljprojekt | [XDM-affärsmöjlighet](../../xdm/classes/b2b/business-opportunity.md) | Information om affärsmöjligheter i XDM | Aktiverad | `opportunityKey.sourceKey` i basklassen | B2B-säljprojekt | `extSourceSystemAudit.externalKey.sourceKey` i basklassen | B2B-säljprojekt | <ul><li>`accountKey.sourceKey` i basklassen</li><li>Typ: Flera till ett</li><li>Referensschema: B2B-konto</li><li>Namnutrymme: B2B-konto</li><li>Målegenskap: `accountKey.sourceKey`</li><li>Relationsnamn från aktuellt schema: Konto</li><li>Relationsnamn från referensschema: Affärsmöjligheter</li></ul> |  |
| Personrelation för B2B-säljprojekt | [XDM-affärsmöjlighet, personrelation](../../xdm/classes/b2b/business-opportunity-person-relation.md) | Ingen | Aktiverad | `opportunityPersonKey.sourceKey` i basklassen | Personrelation för B2B-säljprojekt | | | **Första relationen**<ul><li>`personKey.sourceKey` i basklassen</li><li>Typ: Flera till ett</li><li>Referensschema: B2B-person</li><li>Namnutrymme: B2B-person</li><li>Destinationsegenskap: b2b.personKey.sourceKey</li><li>Relationsnamn från aktuellt schema: Person</li><li>Relationsnamn från referensschema: Affärsmöjligheter</li></ul>**Andra relationen**<ul><li>`opportunityKey.sourceKey` i basklassen</li><li>Typ: Flera till ett</li><li>Referensschema: B2B-säljprojekt </li><li>Namnutrymme: B2B-säljprojekt </li><li>Målegenskap: `opportunityKey.sourceKey`</li><li>Relationsnamn från aktuellt schema: Möjlighet</li><li>Relationsnamn från referensschema: Personer</li></ul> |  |
| B2B-kampanj | [XDM Business Campaign](../../xdm/classes/b2b/business-campaign.md) | Information om XDM Business Campaign | Aktiverad | `campaignKey.sourceKey` i basklassen | B2B-kampanj | | | | |
| B2B-kampanjmedlem | [XDM Business Campaign-medlemmar](../../xdm/classes/b2b/business-campaign-members.md) | Information om XDM Business Campaign-medlem | Aktiverad | `ccampaignMemberKey.sourceKey` i basklassen | B2B-kampanjmedlem | | | **Första relationen**<ul><li>`personKey.sourceKey` i basklassen</li><li>Typ: Flera till ett</li><li>Referensschema: B2B-person</li><li>Namnutrymme: B2B-person</li><li>Målegenskap: `b2b.personKey.sourceKey`</li><li>Relationsnamn från aktuellt schema: Person</li><li>Relationsnamn från referensschema: Kampanjer</li></ul>**Andra relationen**<ul><li>`campaignKey.sourceKey` i basklassen</li><li>Typ: Flera till ett</li><li>Referensschema: B2B-kampanj</li><li>Namnutrymme: B2B-kampanj</li><li>Målegenskap: `campaignKey.sourceKey`</li><li>Relationsnamn från aktuellt schema: Kampanj</li><li>Relationsnamn från referensschema: Personer</li></ul> |  |
| B2B-marknadsföringslista | [XDM Business Marketing List](../../xdm/classes/b2b/business-marketing-list.md) | Ingen | Aktiverad | `marketingListKey.sourceKey` i basklassen | B2B-marknadsföringslista | Ingen | Ingen | Ingen | Statisk lista har inte synkroniserats från [!DNL Salesforce] och har därför ingen sekundär identitet. |
| B2B Marketing List-medlem | [XDM Business Marketing List-medlemmar](../../xdm/classes/b2b/business-marketing-list-members.md) | Ingen | Aktiverad | `marketingListMemberKey.sourceKey` i basklassen | B2B Marketing List-medlem | Ingen | Ingen | **Första relationen**<ul><li>`PersonKey.sourceKey` i basklassen</li><li>Typ: Flera till ett</li><li>Referensschema: B2B-person</li><li>Namnutrymme: B2B-person</li><li>Målegenskap: `b2b.personKey.sourceKey`</li><li>Relationsnamn från aktuellt schema: Person</li><li>Relationsnamn från referensschema: Marknadsföringslistor</li></ul>**Andra relationen**<ul><li>`marketingListKey.sourceKey` i basklassen</li><li>Typ: Flera till ett</li><li>Referensschema: B2B-marknadsföringslista</li><li>Namnområde: B2B-marknadsföringslista</li><li>Målegenskap: `marketingListKey.sourceKey`</li><li>Relationsnamn från aktuellt schema: Marknadsföringslista</li><li>Relationsnamn från referensschema: Personer</li></ul> | Den statiska listmedlemmen har inte synkroniserats från [!DNL Salesforce] och har därför ingen sekundär identitet. |
| B2B-konto, personrelation | [XDM Business Account Person Relation](../../xdm/classes/b2b/business-account-person-relation.md) | Identitetskarta | Aktiverad | `accountPersonKey.sourceKey` i basklassen | B2B-konto, personrelation | Ingen | Ingen | **Första relationen**<ul><li>`personKey.sourceKey` i basklassen</li><li>Typ: Flera till ett</li><li>Referensschema: B2B-person</li><li>Namnutrymme: B2B-person</li><li>Målegenskap: `b2b.personKey.SourceKey`</li><li>Relationsnamn från aktuellt schema: Personer</li><li>Relationsnamn från referensschema: Konto</li></ul>**Andra relationen**<ul><li>`accountKey.sourceKey` i basklassen</li><li>Typ: Flera till ett</li><li>Referensschema: B2B-konto</li><li>Namnutrymme: B2B-konto</li><li>Målegenskap: `accountKey.sourceKey`</li><li>Relationsnamn från aktuellt schema: Konto</li><li>Relationsnamn från referensschema: Personer</li></ul> |  |

{style="table-layout:auto"}

