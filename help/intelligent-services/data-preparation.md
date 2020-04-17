---
keywords: Experience Platform;home;intelligent services;popular topics
solution: Experience Platform
title: Förbered data för användning i intelligenta tjänster
topic: Intelligent Services
translation-type: tm+mt
source-git-commit: 1d827d1637da05d3d2afc338f48911bb23039949

---


# Förbered data för användning i intelligenta tjänster

För att Intelligent Services ska kunna hitta insikter från era marknadsföringshändelsedata måste data anrikas semantiskt och underhållas i en standardstruktur. Intelligenta tjänster utnyttjar XDM-scheman (Experience Data Model) för att uppnå detta. Alla datauppsättningar som används i Intelligent Services måste överensstämma med XDM-schemat **Consumer Experience Events (CEE)** .

Det här dokumentet innehåller allmän vägledning om hur du mappar data om marknadsföringshändelser från flera kanaler till det här schemat, och ger information om viktiga fält i schemat för att hjälpa dig att avgöra hur data effektivt kan mappas till dess struktur.

## CEE-schemat

Consumer ExperienceEvent-schemat beskriver en individs beteende när det gäller digitala marknadsföringshändelser (webb eller mobil) samt online- eller offlinehandel. Det här schemat måste användas för intelligenta tjänster på grund av semantiskt väl definierade fält (kolumner), så att okända namn som annars skulle göra data mindre tydliga undviks.

Precis som alla XDM-scheman är CEE-blandningen utökningsbar. Med andra ord kan ytterligare fält läggas till i CEE-mixen, och olika varianter kan vid behov inkluderas i flera scheman.

Ett fullständigt exempel på blandningen finns i den [offentliga XDM-databasen](https://github.com/adobe/xdm/blob/797cf4930d5a80799a095256302675b1362c9a15/docs/reference/context/experienceevent-consumer.schema.md)och bör användas som referens för de nyckelfält som beskrivs i avsnittet nedan.

### Nyckelfält

Tabellen nedan visar de viktigaste fälten i CEE-mixen, som bör användas för att Intelligent Services ska kunna generera användbara insikter, inklusive beskrivningar och länkar till referensdokumentation för ytterligare exempel.

| XDM-fält | Beskrivning | Referens |
| --- | --- | --- |
| `xdm:channel` | Marknadsföringskanalen för ExperienceEvent. Fältet innehåller information om kanaltyp, medietyp och platstyp. **Detta fält _måste_anges för att Attribution AI ska fungera med dina data**. Se [tabellen nedan](#example-channels) för några exempelmappningar. | [Experience channel schema](https://github.com/adobe/xdm/blob/797cf4930d5a80799a095256302675b1362c9a15/docs/reference/channels/channel.schema.md) |
| `xdm:productListItems` | En array med artiklar som representerar produkter som valts ut av en kund, inklusive produkt-SKU, namn, pris och kvantitet. | [Schema för handelsinformation](https://github.com/adobe/xdm/blob/797cf4930d5a80799a095256302675b1362c9a15/docs/reference/context/experienceevent-commerce.schema.md) |
| `xdm:commerce` | Innehåller handelsspecifik information om ExperienceEvent, inklusive inköpsordernummer och betalningsinformation. | [Schema för handelsinformation](https://github.com/adobe/xdm/blob/797cf4930d5a80799a095256302675b1362c9a15/docs/reference/context/experienceevent-commerce.schema.md) |
| `xdm:web` | Representerar webbinformation som relaterar till ExperienceEvent, t.ex. interaktionen, sidinformation och referenten. | [Schema för webbinformation om ExperienceEvent](https://github.com/adobe/xdm/blob/797cf4930d5a80799a095256302675b1362c9a15/docs/reference/context/experienceevent-web.schema.md) |

### Exempelkanaler {#example-channels}

Fältet `xdm:channel` representerar den marknadsföringskanal som är relaterad till ExperienceEvent. I följande tabell visas några exempel på marknadsföringskanaler som har mappats till XDM:

| Kanal | `channel.mediaType` | `channel._type` | `channel.mediaAction` |
| --- | --- | --- | --- |
| Betalsökning | BETALT | SÖK | KLICKA |
| Social - marknadsföring | EARNED | SOCIALT | KLICKA |
| Visa | BETALT | VISA | KLICKA |
| E-post | BETALT | E-POST | KLICKA |
| Intern referens | ÄGDA | DIRECT | KLICKA |
| VisaVia | BETALT | VISA | IMPRESSION |
| Omdirigering av QR-kod | ÄGDA | DIRECT | KLICKA |
| SMS-textmeddelande | ÄGDA | SMS | KLICKA |
| Mobil | ÄGDA | MOBILE | KLICKA |

## Mappning och inhämtning av data

När du har fastställt om dina tidsseriedata kan mappas till CEE-schemat kan du påbörja processen med att föra in dina data i Intelligent Services. Kontakta Adobes konsulttjänster för att mappa dina data till schemat och importera dem till tjänsten.

Om du har en Adobe Experience Platform-prenumeration och vill mappa och importera data själv följer du stegen som beskrivs i avsnittet nedan.

### Använda Adobe Experience Platform

>[!NOTE] Stegen nedan kräver en prenumeration på Experience Platform. Om du inte har tillgång till Platform går du vidare till [nästa steg](#next-steps) .

I det här avsnittet beskrivs arbetsflödet för mappning och inmatning av data i Experience Platform för användning i Intelligent Services, inklusive länkar till självstudiekurser för detaljerade steg.

#### Skapa ett CEE-schema och en datauppsättning

När du är redo att börja förbereda dina data för konsumtion är det första steget att skapa ett nytt XDM-schema som använder CEE-mixen. I följande självstudiekurser får du hjälp med att skapa ett nytt schema i gränssnittet eller API:

* [Skapa ett schema i användargränssnittet](../xdm/tutorials/create-schema-ui.md)
* [Skapa ett schema i API:t](../xdm/tutorials/create-schema-api.md)

>[!IMPORTANT] Självstudiekurserna ovan följer ett allmänt arbetsflöde för att skapa ett schema. När du väljer en klass för schemat måste du använda **klassen** XDM ExperienceEvent. När den här klassen har valts kan du lägga till CEE-mixinen i schemat.

När du har lagt till CEE-mixen i schemat kan du lägga till andra mixiner efter behov för ytterligare fält i dina data.

När du har skapat och sparat schemat kan du skapa en ny datauppsättning som baseras på det schemat. I följande självstudiekurser får du hjälp med att skapa en ny datauppsättning i gränssnittet eller API:

* [Skapa en datauppsättning i användargränssnittet](../catalog/datasets/user-guide.md#create) (Följ arbetsflödet för att använda ett befintligt schema)
* [Skapa en datauppsättning i API:t](../catalog/datasets/create.md)

#### Mappa och importera data

När du har skapat ett CEE-schema och en datauppsättning kan du börja mappa dina datatabeller till schemat och importera dessa data till plattformen. I självstudiekursen om hur du [mappar en CSV-fil till ett XDM-schema](../ingestion/tutorials/map-a-csv-file.md) finns mer information om hur du gör detta i användargränssnittet. När en datauppsättning har fyllts i kan samma datauppsättning användas för att importera ytterligare datafiler.

## Nästa steg {#next-steps}

Det här dokumentet innehåller allmän vägledning om hur du förbereder data för användning i Intelligent Services. Kontakta Adobe Consulting Support om du behöver ytterligare rådgivning baserat på ditt användningsfall.

När ni har fyllt i en datauppsättning med era kundupplevelsedata kan ni använda intelligenta tjänster för att generera insikter. Se följande dokument för att komma igång:

* [Översikt över AI-attribut](./attribution-ai/overview.md)
* [Översikt över AI för kunder](./customer-ai/overview.md)
