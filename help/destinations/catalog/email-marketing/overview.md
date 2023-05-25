---
keywords: e-post;E-post;e-post;e-postadresser
title: Översikt över destinationer för e-postmarknadsföring
type: Tutorial
description: Med ESP (Email Service Providers) kan ni hantera era e-postmarknadsföringsaktiviteter, t.ex. för att skicka e-postkampanjer. Lär dig vilka ESP:er som stöds som Experience Platform-mål.
exl-id: e07f8c5a-0424-4de5-810f-3d5711ef4606
source-git-commit: 152786e5e994a88b19ca7af8815b33be5a732852
workflow-type: tm+mt
source-wordcount: '374'
ht-degree: 2%

---

# Översikt över destinationer för e-postmarknadsföring {#email-marketing-destinations}

## Översikt {#overview}

Med ESP (Email Service Providers) kan du hantera dina e-postmarknadsföringsaktiviteter, som att skicka e-postkampanjer med reklam. Adobe Experience Platform kan integreras med ESP:er genom att ni kan aktivera segment för e-postmarknadsföring.

## E-postmarknadsföringsmål som stöds {#supported-destinations}

Adobe Experience Platform har stöd för följande e-postmarknadsföringsmål:

* [Adobe Campaign](adobe-campaign.md)
* [Adobe Campaign Managed Cloud Services](adobe-campaign-managed-services.md)
* [Intressekategorier för e-postmeddelanden](mailchimp-interest-categories.md)
* [(API) Oracle Eloqua](oracle-eloqua-api.md)
* [(API) [!DNL Salesforce Marketing Cloud]](salesforce-marketing-cloud-exact-target.md)
* [(Filer) Oraclet Eloqua](oracle-eloqua.md)
* [(Filer) [!DNL Salesforce Marketing Cloud]](salesforce-marketing-cloud.md)
* [[!DNL Salesforce Marketing Cloud Account Engagement]](salesforce-marketing-cloud-account-engagement.md)
* [Oraclets svar](oracle-responsys.md)
* [SendGrid](sendgrid.md)

## Anslut till ett nytt mål för e-postmarknadsföring {#connect-destination}

För att kunna skicka segment till e-postmarknadsföringsmål för era kampanjer måste Platform först ansluta till destinationen. Se [självstudiekurs om att skapa mål](../../ui/connect-destination.md) för detaljerad information om hur du konfigurerar ett nytt mål.

## Bästa tillvägagångssätt när ni aktiverar målgrupper för e-postmarknadsföring {#best-practices}

### Identitetsurval {#identity}

Adobe rekommenderar att du väljer en unik identifierare från [union](../../../profile/home.md#profile-fragments-and-union-schemas). Det här är fältet som dina användaridentiteter är avaktiverade i. Oftast är det här fältet e-postadressen, men det kan också vara ett lojalitetsprogram-ID eller ett telefonnummer. I tabellen nedan finns de vanligaste unika identifierarna och deras XDM-fält i schemat.

| Unik identifierare | XDM-fält i Unified Schema |
|----------------- | ---------------------------|
| E-postadress | `personalEmail.address` |
| Telefon | `mobilePhone.number` |
| Förmånsprogram-ID | `Customer-defined XDM field` |

{style="table-layout:auto"}

### Andra målattribut {#other-destination-attributes}

Välj vilka andra fält du vill exportera till e-postmålet i fältet Schema. Några rekommenderade alternativ är:

| Schema | XDM-fält |
|------ | ---------|
| Förnamn | `person.name.firstName` |
| Efternamn | `person.name.lastName` |
| Telefon | `mobilePhone.number` |
| Adress, ort | `homeAddress.city` |
| Adresstillstånd | `homeAddress.stateProvince` |
| Adress Postnummer | `homeAddress.postalCode` |
| Födelsedag | `person.birthDayAndMonth` |
| Segmentmedlemskap | `segmentMembership.status` |

{style="table-layout:auto"}

## Aktivera segment för e-postmarknadsföringsmål {#activate}

Vissa e-postmarknadsföringsmål i katalogexportprofilerna på ett direktuppspelat sätt, via en API-integrering med målet.

Andra mål exporterar filer till en molnlagringsplats. När exporten är klar måste du importera data från molnlagringsplatsen till ditt e-postmarknadsföringsmål.

Följ länkarna i [e-postmarknadsföringsmål som stöds](#supported-destinations) om du vill veta hur du aktiverar segment för varje e-postmarknadsföringsmål.

## Ytterligare resurser {#additional-resources}

* [Aktivera målgruppsdata för att batchprofilera exportmål](../../ui/activate-batch-profile-destinations.md)
* [Skapa e-postmarknadsföringsmål och aktivera data med API:t för Flow Service](../../api/connect-activate-batch-destinations.md)
