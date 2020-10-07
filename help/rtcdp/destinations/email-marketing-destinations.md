---
keywords: email;Email;e-mail;email destinations
title: Destinationer för e-postmarknadsföring
seo-title: Destinationer för e-postmarknadsföring
type: Tutorial
description: Med ESP (Email Service Providers) kan ni hantera era e-postmarknadsföringsaktiviteter, t.ex. för att skicka e-postkampanjer.
seo-description: Med ESP (Email Service Providers) kan ni hantera era e-postmarknadsföringsaktiviteter, t.ex. för att skicka e-postkampanjer.
translation-type: tm+mt
source-git-commit: 8c94d3631296c1c3cc97501ccf1a3ed995ec3cab
workflow-type: tm+mt
source-wordcount: '773'
ht-degree: 0%

---


# E-postmarknadsföringsmål {#email-marketing-destinations}

Med ESP (Email Service Providers) kan du hantera dina e-postmarknadsföringsaktiviteter, som att skicka e-postkampanjer med reklam. Adobe kunddataplattform i realtid integreras med ESP:er genom att ni kan aktivera segment för e-postmarknadsföringsmål.

För att skicka segment till e-postmarknadsföringsmål för era kampanjer måste CDP i realtid i Adobe först ansluta till destinationen.

Att ansluta till e-postmarknadsföringsmål är en process i tre steg. Varje steg beskrivs längre ned på den här sidan.

Anslut till antingen Amazon S3 eller SFTP i det anslutande målflödet som beskrivs i avsnittet nedan. CDP exporterar dina segment som `.csv` eller `.txt` filer i realtid och levererar dem till den plats du önskar. Schemalägg dataimporten på er e-postmarknadsföringsplattform från den lagringsplats som är aktiverad i CDP i realtid. Processen för att importera data varierar för varje partner. Mer information finns i de enskilda destinationsartiklarna.

## Steg 1 - Konfigurera mål {#connect-destination}

1. I **[!UICONTROL Connections]** > **[!UICONTROL Destinations]** väljer du det mål för e-postmarknadsföring som du vill ansluta till och sedan **[!UICONTROL Configure]**.

   ![Anslut till mål](/help/rtcdp/destinations/assets/connect-email-marketing.png)

2. Om du tidigare har konfigurerat en anslutning till ditt e-postmarknadsföringsmål markerar du den befintliga anslutningen i **[!UICONTROL Authentication]** steget **[!UICONTROL Existing Account]** . Du kan också välja **[!UICONTROL New Account]** att skapa en ny anslutning till ditt mål för e-postmarknadsföring. I väljaren kan du välja mellan Amazon S3, SFTP med lösenord eller SFTP med SSH-nyckel. **[!UICONTROL Connection type]** Fyll i informationen nedan, beroende på vilken typ av anslutning du har, och välj sedan **[!UICONTROL Connect]**.

   För **S3-anslutningar** måste du ange ditt Amazon Access Key ID och Secret Access Key.

   För **SFTP med lösenordsanslutningar** måste du ange domän, port, användarnamn och lösenord för SFTP-servern.

   För **SFTP med SSH-nyckelanslutningar** måste du ange domän, port, användarnamn och SSH-nyckel för SFTP-servern.

3. I **[!UICONTROL Setup]** steget anger du ett [!UICONTROL Name] och ett [!UICONTROL Description] för det nya målet samt [!UICONTROL File format] för de exporterade filerna. <br>
Om du valde Amazon S3 som lagringsalternativ i föregående steg, sätter du in [!UICONTROL Bucket name] och [!UICONTROL Folder path] i molnlagringsmålet där filerna ska levereras. För alternativet SFTP-lagring anger du den plats [!UICONTROL Folder path] där filerna ska levereras. <br>
I det här steget kan du även välja vilket som helst [!UICONTROL Marketing use case] som ska gälla för det här målet. Fall av marknadsanvändning anger avsikten för vilken data ska exporteras till destinationen. Du kan välja bland Adobe-definierade användningsfall för marknadsföring eller skapa ett eget marknadsföringsexempel. Mer information om användningsfall för marknadsföring finns på sidan [Datastyrning i CDP](/help/rtcdp/privacy/data-governance-overview.md#destinations) i realtid. Mer information om de enskilda Adobe-definierade användningsfallen för marknadsföring finns i översikten över [dataanvändningspolicyn](/help/data-governance/policies/overview.md#core-actions). <br>
   ![Steget för e-postkonfiguration](/help/rtcdp/destinations/assets/email-setup-step.png)

## Steg 2 - Välj vilka segmentmedlemmar som ska inkluderas i målexporten {#select-segments}

På **[!UICONTROL Select Segments]** sidan väljer du vilka segment som ska skickas till målet. Mer information om fälten finns i avsnitten nedan.

![Markera segment](/help/rtcdp/destinations/assets/email-select-segments.png)

## Steg 3 - Konfigurera filnamn

Mer information om redigeringsalternativen för filnamn finns i [konfigurationssteget](/help/rtcdp/destinations/activate-destinations.md#configure) i självstudiekursen om aktiveringsmål.

## Steg 4 - Välj attribut - Välj vilka schemafält som ska användas som målattribut i de exporterade filerna {#destination-attributes}

I det här steget väljer du vilka fält som ska exporteras till e-postmarknadsföringsmål.

![Målattribut](/help/rtcdp/destinations/assets/recommended-attributes.png)

Mer information om det här steget finns i [steget Välj attribut](/help/rtcdp/destinations/activate-destinations.md#select-attributes) i självstudiekursen Aktivera mål.

### Identity {#identity}

Vi rekommenderar att du väljer en unik identifierare från ditt [unionsschema](../../profile/home.md#profile-fragments-and-union-schemas). Det här är fältet som dina användares identiteter är avskärmade från. Oftast är det här fältet e-postadressen, men det kan också vara ett lojalitetsprogram-ID eller ett telefonnummer. I tabellen nedan finns de vanligaste unika identifierarna och deras XDM-fält i schemat.

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
| Segmentmedlemskap | `segmentMembership.status` |

## Steg 5 - Importera data från lagringsplatsen till målet

Läs de enskilda artiklarna om destinationsorten för e-postmarknadsföring om du vill lära dig hur du importerar data från din lagringsplats till destinationer:

* [Adobe Campaign](/help/rtcdp/destinations/adobe-campaign-destination.md#import-data-into-campaign)
* [Salesforce Marketing Cloud](/help/rtcdp/destinations/salesforce-marketing-cloud-destination.md#import-data-into-salesforce)
* [Oracle Eloqua](/help/rtcdp/destinations/oracle-eloqua-destination.md#import-data-into-eloqua)
* [Oracle Responsys](/help/rtcdp/destinations/oracle-responsys-destination.md#import-data-into-responsys)

## Aktivera segment för e-postmarknadsföringsmål

Instruktioner om hur du aktiverar segment för e-postmarknadsföringsmål finns i [Aktivera data till mål](/help/rtcdp/destinations/activate-destinations.md).

## Ytterligare resurser

* [Aktivera data till mål](/help/rtcdp/destinations/activate-destinations.md)
* [Skapa e-postmarknadsföringsmål och aktivera data med API:t för Flow Service](https://docs.adobe.com/content/help/en/experience-platform/tutorials/destinations/email-marketing-api.html)