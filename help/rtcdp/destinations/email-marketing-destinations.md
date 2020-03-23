---
title: Destinationer för e-postmarknadsföring
seo-title: Destinationer för e-postmarknadsföring
description: Med ESP (Email Service Providers) kan ni hantera era e-postmarknadsföringsaktiviteter, t.ex. för att skicka e-postkampanjer.
seo-description: Med ESP (Email Service Providers) kan ni hantera era e-postmarknadsföringsaktiviteter, t.ex. för att skicka e-postkampanjer.
translation-type: tm+mt
source-git-commit: 463212a8fabb9dd5962b4d3f523a6f2d88bb1d9d

---


# E-postmarknadsföringsmål {#email-marketing-destinations}

Med ESP (Email Service Providers) kan du hantera dina e-postmarknadsföringsaktiviteter, som att skicka e-postkampanjer med reklam. Adobes kunddataplattform i realtid integreras med ESP:er genom att ni kan aktivera segment för e-postmarknadsföringsmål.

För att skicka segment till e-postmarknadsföringsmål för era kampanjer måste Adobe CDP i realtid först ansluta till destinationen.

Att ansluta till e-postmarknadsföringsmål är en process i tre steg. Varje steg beskrivs längre ned på den här sidan.

Anslut till antingen Amazon S3 eller SFTP i det anslutande målflödet som beskrivs i avsnittet nedan. CDP exporterar dina segment som `.csv` eller `.txt` filer i realtid och levererar dem till den plats du önskar. Schemalägg dataimporten på er e-postmarknadsföringsplattform från den lagringsplats som är aktiverad i CDP i realtid. Processen för att importera data varierar för varje partner. Mer information finns i de enskilda destinationsartiklarna.

## Steg 1 - Anslut mål {#connect-destination}

1. I **[!UICONTROL Connections > Destinations]** väljer du det mål för e-postmarknadsföring som du vill ansluta till och sedan **[!UICONTROL Connect destination]**.

   ![Anslut till mål](/help/rtcdp/destinations/assets/connect-destination.png)

2. Välj lagringsplats **[!UICONTROL Connection type]** i Anslutningsguiden. Du kan välja mellan **Amazon S3**, **SFTP med lösenord** och **SFTP med SSH-nyckel**. Fyll i informationen nedan, beroende på vilken typ av anslutning du har, och välj sedan **[!UICONTROL Connect]**.

För **S3-anslutningar** måste du ange ditt ID för åtkomstnyckel och hemlig åtkomstnyckel.

För **SFTP med lösenordsanslutningar** måste du ange domän, port, användarnamn och lösenord.

För **SFTP med SSH-nyckelanslutningar** måste du ange domän, port, användarnamn och SSH-nyckel.

## Steg 2 - Välj vilka schemafält som ska användas som målattribut i de exporterade filerna {#destination-attributes}

I det här steget väljer du vilka fält som ska exporteras till e-postmarknadsföringsmål.

![Målattribut](/help/rtcdp/destinations/assets/destination-attributes.png)

### Identitet {#identity}

Vi rekommenderar att du väljer en unik identifierare från ditt [unionsschema](https://www.adobe.io/apis/experienceplatform/home/profile-identity-segmentation/profile-identity-segmentation-services.html#!api-specification/markdown/narrative/technical_overview/unified_profile_architectural_overview/unified_profile_architectural_overview.md). Det här är fältet som dina användares identiteter är avskärmade från. Oftast är det här fältet e-postadressen, men det kan också vara ett lojalitetsprogram-ID eller ett telefonnummer. I tabellen nedan finns de vanligaste unika identifierarna och deras XDM-fält i ett enhetligt schema.

| Unik identifierare | XDM-fält i Unified Schema |
---------|----------
| E-postadress | `personalEmail.address` |
| Telefon | `mobilePhone.number` |
| Förmånsprogram-ID | `Customer-defined XDM field` |

### Andra målattribut

Välj vilka andra fält du vill exportera till e-postmålet i fältet Schema. Några rekommenderade alternativ är:

| Schema | XDM-fält |
---------|----------
| Förnamn | `person.name.firstName` |
| Efternamn | `person.name.lastName` |
| Telefon | `mobilePhone.number` |
| Adress, ort | `homeAddress.city` |
| Adresstillstånd | `homeAddress.stateProvince` |
| Adress Postnummer | `homeAddress.postalCode` |
| Födelsedag | `person.birthDayAndMonth` |

## Steg 3 - Importera data från lagringsplatsen till målet

Läs de enskilda artiklarna om destinationsorten för e-postmarknadsföring om du vill lära dig hur du importerar data från din lagringsplats till destinationer:

* [Adobe Campaign](/help/rtcdp/destinations/adobe-campaign-destination.md#import-data-into-campaign)
* [Salesforce Marketing Cloud](/help/rtcdp/destinations/salesforce-marketing-cloud-destination.md#import-data-into-salesforce)
* [Oracle Eloqua](/help/rtcdp/destinations/oracle-eloqua-destination.md#import-data-into-eloqua)
* [Oracle Responsys](/help/rtcdp/destinations/oracle-responsys-destination.md#import-data-into-responsys)

## Aktivera segment för e-postmarknadsföringsmål

Instruktioner om hur du aktiverar segment för e-postmarknadsföringsmål finns i [Aktivera data till mål](/help/rtcdp/destinations/activate-destinations.md).