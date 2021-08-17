---
keywords: e-post;E-post;e-post;e-postadresser
title: Översikt över destinationer för e-postmarknadsföring
type: Tutorial
description: Med ESP (Email Service Providers) kan ni hantera era e-postmarknadsföringsaktiviteter, t.ex. för att skicka e-postkampanjer.
exl-id: e07f8c5a-0424-4de5-810f-3d5711ef4606
source-git-commit: 802b1844bec1e577e978da5d5a69de87278c04b9
workflow-type: tm+mt
source-wordcount: '382'
ht-degree: 2%

---

# Översikt över destinationer för e-postmarknadsföring {#email-marketing-destinations}

## Översikt {#overview}

Med ESP (Email Service Providers) kan du hantera dina e-postmarknadsföringsaktiviteter, som att skicka e-postkampanjer med reklam. Adobe Experience Platform kan integreras med ESP:er genom att ni kan aktivera segment för e-postmarknadsföring.

Plattformen exporterar dina segment som `.csv`-filer och levererar dem till den plats du föredrar. Schemalägg dataimporten i din e-postmarknadsföringsplattform från den lagringsplats som är aktiverad i [!DNL Platform]. Processen för att importera data varierar för varje partner. Mer information finns i de enskilda destinationsartiklarna.

## E-postmarknadsföringsmål som stöds {#supported-destinations}

Adobe Experience Platform har stöd för följande e-postmarknadsföringsmål:

* [Adobe Campaign](adobe-campaign.md)
* [Oracle Eloqua](oracle-eloqua.md)
* [Oraclets svar](oracle-responsys.md)
* [Salesforce Marketing Cloud](salesforce-marketing-cloud.md)

## Anslut till ett nytt mål för e-postmarknadsföring {#connect-destination}

För att kunna skicka segment till e-postmarknadsföringsmål för era kampanjer måste Platform först ansluta till destinationen. Se självstudiekursen [när du skapar mål](../../ui/connect-destination.md) för mer information om hur du konfigurerar ett nytt mål.

## Bästa tillvägagångssätt när ni aktiverar målgrupper för e-postmarknadsföring {#best-practices}

### Identitetsurval {#identity}

Adobe rekommenderar att du väljer en unik identifierare i ditt [unionsschema](../../../profile/home.md#profile-fragments-and-union-schemas). Det här är fältet som dina användaridentiteter är avaktiverade i. Oftast är det här fältet e-postadressen, men det kan också vara ett lojalitetsprogram-ID eller ett telefonnummer. I tabellen nedan finns de vanligaste unika identifierarna och deras XDM-fält i schemat.

| Unik identifierare | XDM-fält i Unified Schema |
|----------------- | ---------------------------|
| E-postadress | `personalEmail.address` |
| Telefon | `mobilePhone.number` |
| Förmånsprogram-ID | `Customer-defined XDM field` |

### Andra målattribut

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

## Importera data från lagringsplatsen till målet {#import-data-into-destination}

Läs de enskilda målartiklarna för e-postmarknadsföring och lär dig hur du importerar data från din lagringsplats till destinationer:

* [Adobe Campaign](adobe-campaign.md)
* [Oracle Eloqua](oracle-eloqua.md)
* [Oraclets svar](oracle-responsys.md)
* [Salesforce Marketing Cloud](salesforce-marketing-cloud.md)

## Aktivera segment för e-postmarknadsföringsmål {#activate}

Instruktioner om hur du aktiverar segment för e-postmarknadsföringsmål finns i [Aktivera profiler och segment till en destination](../../ui/activate-destinations.md).

## Ytterligare resurser

* [Aktivera data till mål](../../ui/activate-destinations.md)
* [Skapa e-postmarknadsföringsmål och aktivera data med API:t för Flow Service](../../api/email-marketing.md)
