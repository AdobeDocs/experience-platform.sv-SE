---
keywords: e-post;E-post;e-post;e-postadresser
title: Översikt över destinationer för e-postmarknadsföring
type: Tutorial
description: Med ESP (Email Service Providers) kan ni hantera era e-postmarknadsföringsaktiviteter, t.ex. för att skicka e-postkampanjer.
translation-type: tm+mt
source-git-commit: 6655714d4b57d9c414cd40529bcee48c7bcd862d
workflow-type: tm+mt
source-wordcount: '776'
ht-degree: 0%

---


# Översikt över mål för e-postmarknadsföring {#email-marketing-destinations}

Med ESP (Email Service Providers) kan du hantera dina e-postmarknadsföringsaktiviteter, som att skicka e-postkampanjer med reklam. Adobe Experience Platform kan integreras med ESP:er genom att ni kan aktivera segment för e-postmarknadsföring.

För att kunna skicka segment till e-postmarknadsföringsmål för era kampanjer måste Platform först ansluta till destinationen.

Att ansluta till e-postmarknadsföringsmål är en process i tre steg. Varje steg beskrivs längre ned på den här sidan.

Anslut till antingen Amazon S3 eller SFTP i det anslutande målflödet som beskrivs i avsnittet nedan. Plattformen exporterar dina segment som `.csv` eller `.txt`-filer och levererar dem till den plats du föredrar. Schemalägg dataimporten på din e-postmarknadsföringsplattform från den lagringsplats som är aktiverad i Platform. Processen för att importera data varierar för varje partner. Mer information finns i de enskilda destinationsartiklarna.

## Konfigurera mål {#connect-destination}

I **[!UICONTROL Connections]** > **[!UICONTROL Destinations]** väljer du det e-postmarknadsföringsmål som du vill ansluta till och sedan **[!UICONTROL Configure]**.

![Anslut till mål](../../assets/catalog/email-marketing/overview/connect-email-marketing.png)

Om du tidigare har konfigurerat en anslutning till ditt mål för e-postmarknadsföring väljer du **[!UICONTROL Existing Account]** i **[!UICONTROL Authentication]**-steget och väljer din befintliga anslutning. Du kan också välja **[!UICONTROL New Account]** för att konfigurera en ny anslutning till ditt mål för e-postmarknadsföring. I **[!UICONTROL Connection type]**-väljaren kan du välja mellan Amazon S3, SFTP med lösenord eller SFTP med SSH-nyckel. Fyll i informationen nedan, beroende på din anslutningstyp, och välj sedan **[!UICONTROL Connect]**.

- För **S3-anslutningar** måste du ange ditt Amazon Access Key ID och Secret Access Key.
- För **SFTP med Lösenord**-anslutningar måste du ange domän, port, användarnamn och lösenord för SFTP-servern.
- För **SFTP med SSH-nyckel**-anslutningar måste du ange domän, port, användarnamn och SSH-nyckel för SFTP-servern.

Du kan också bifoga den RSA-formaterade offentliga nyckeln för att lägga till kryptering till dina exporterade filer under **[!UICONTROL Key]**-avsnittet. Observera att den här offentliga nyckeln **måste** skrivas som en Base64-kodad sträng.

I steget **[!UICONTROL Setup]** anger du ett namn och en beskrivning för det nya målet samt filformatet för de exporterade filerna.

Om du valde Amazon S3 som lagringsalternativ i föregående steg anger du namnet på hakparentesen och mappsökvägen i molnlagringsmålet där filerna ska levereras. För alternativet SFTP-lagring anger du den mappsökväg där filerna ska levereras.

I det här steget kan du även välja alla användningsfall för marknadsföring som ska gälla för den här destinationen. Fall av marknadsanvändning anger avsikten för vilken data ska exporteras till destinationen. Du kan välja bland Adobe-definierade användningsfall för marknadsföring eller skapa ett eget marknadsföringsexempel. Mer information om användningsfall för marknadsföring finns i [Översikt över dataanvändningsprinciper](../../../data-governance/policies/overview.md).

![Steget för e-postkonfiguration](../../assets/catalog/email-marketing/overview/email-setup-step.png)

## Välj vilka segmentmedlemmar som ska inkluderas i målexporter {#select-segments}

På sidan **[!UICONTROL Select Segments]** väljer du vilka segment som ska skickas till målet. Mer information om fälten finns i avsnitten nedan.

![Markera segment](../../assets/common/email-select-segments.png)

## Konfigurera filnamn

Mer information om redigeringsalternativen för segmentschema och filnamn finns i [Konfigurera](../../ui/activate-destinations.md#configure)-steget i självstudiekursen om aktiveringsmål.

## Välj attribut - Välj vilka schemafält som ska användas som målattribut i de exporterade filerna {#destination-attributes}

I det här steget väljer du vilka fält som ska exporteras till e-postmarknadsföringsmål samt markerar vilka fält som är obligatoriska.

![Målattribut](../../assets/catalog/email-marketing/overview/recommended-attributes.png)

Mer information om det här steget finns i [Select attributes](../../ui/activate-destinations.md#select-attributes)-steget i självstudiekursen om aktivering av mål.

### Identitet {#identity}

Vi rekommenderar att du väljer en unik identifierare i ditt [unionsschema](../../../profile/home.md#profile-fragments-and-union-schemas). Det här är fältet som dina användares identiteter är avskärmade från. Oftast är det här fältet e-postadressen, men det kan också vara ett lojalitetsprogram-ID eller ett telefonnummer. I tabellen nedan finns de vanligaste unika identifierarna och deras XDM-fält i schemat.

| Unik identifierare | XDM-fält i Unified Schema |
----------------- | ---------------------------
| E-postadress | `personalEmail.address` |
| Telefon | `mobilePhone.number` |
| Förmånsprogram-ID | `Customer-defined XDM field` |

### Andra målattribut

Välj vilka andra fält du vill exportera till e-postmålet i fältet Schema. Några rekommenderade alternativ är:

| Schema | XDM-fält |
------ | ---------
| Förnamn | `person.name.firstName` |
| Efternamn | `person.name.lastName` |
| Telefon | `mobilePhone.number` |
| Adress, ort | `homeAddress.city` |
| Adresstillstånd | `homeAddress.stateProvince` |
| Adress Postnummer | `homeAddress.postalCode` |
| Födelsedag | `person.birthDayAndMonth` |
| Segmentmedlemskap | `segmentMembership.status` |

## Importera data från lagringsplatsen till målet

Läs de enskilda artiklarna om destinationsorten för e-postmarknadsföring om du vill lära dig hur du importerar data från din lagringsplats till destinationer:

- [Adobe Campaign](./adobe-campaign.md#import-data-into-campaign)
- [Oracle Eloqua](./oracle-eloqua.md#import-data-into-eloqua)
- [Oracle Responsys](./oracle-responsys.md#import-data-into-responsys)
- [Salesforce Marketing Cloud](./salesforce-marketing-cloud.md#import-data-into-salesforce)

## Aktivera segment för e-postmarknadsföringsmål

Instruktioner om hur du aktiverar segment för e-postmarknadsföringsmål finns i [Aktivera data till mål](../../ui/activate-destinations.md).

## Ytterligare resurser

- [Aktivera data till mål](../../ui/activate-destinations.md)
- [Skapa e-postmarknadsföringsmål och aktivera data med API:t för Flow Service](../../api/email-marketing.md)