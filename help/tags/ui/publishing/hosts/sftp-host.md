---
title: SFTP-värdar
description: Lär dig hur du konfigurerar taggar i Adobe Experience Platform för att leverera biblioteksbyggen till en säker, självvärd SFTP-server.
exl-id: 3c1dc43b-291c-4df4-94f7-a03b25dbb44c
source-git-commit: 8ded2aed32dffa4f0923fedac7baf798e68a9ec9
workflow-type: tm+mt
source-wordcount: '801'
ht-degree: 0%

---

# SFTP-värdar

>[!NOTE]
>
>Adobe Experience Platform Launch har omklassificerats som en serie datainsamlingstekniker i Adobe Experience Platform. Som ett resultat av detta har flera terminologiska förändringar införts i produktdokumentationen. Se följande [dokument](../../../term-updates.md) för en konsoliderad hänvisning till terminologiska förändringar.

Med Adobe Experience Platform kan du leverera kodbiblioteksbyggen till en säker SFTP-server som du har som värd, vilket ger dig större kontroll över hur byggnaderna lagras och hanteras. Den här guiden beskriver hur du konfigurerar en SFTP-värd för en taggegenskap i användargränssnittet för Experience Platform eller datainsamlingen.

>[!NOTE]
>
>Du kan också välja att använda en värd som hanteras av Adobe i stället. Se guiden [Värdar som hanteras av Adobe](./managed-by-adobe-host.md) för mer information.
>
>Information om fördelarna och begränsningarna med självvärdande bibliotek finns i [webbhotellguide](./self-hosting-libraries.md).

## Konfigurera en åtkomstnyckel för servern {#access-key}

Plattformen ansluter till din SFTP-plats med hjälp av en krypterad nyckel. Det finns några steg för att konfigurera detta korrekt:

### Skapa ett nyckelpar för offentlig/privat nyckel

Du måste ha ett nyckelpar för offentlig/privat nyckel installerat på SFTP-servern. Du kan generera nycklarna på servern eller generera dem någon annanstans och installera dem på servern. Läs GitHub-dokumentationen om [hur du genererar SSH-nycklar](https://help.github.com/articles/generating-a-new-ssh-key-and-adding-it-to-the-ssh-agent/#generating-a-new-ssh-key) för mer information.

### Kryptera nycklarna

Den privata nyckeln används för att kryptera den offentliga nyckeln. Du måste ange din privata nyckel när du skapar SFTP-värden. Se avsnittet om [kryptera värden](../../../api/guides/encrypting-values.md) i Reactor API guide för instruktioner om kryptering av publika nycklar. Använd produktionsmiljöns GPG-nyckel om du inte vet att du behöver en viss. Slutligen kan du kryptera din privata nyckel från vilken dator som helst, så du behöver inte installera GPG på servern för att slutföra det här steget.

### IP-adresser för Tillåtelselista-plattformen

Du kan behöva godkänna en uppsättning IP-adresser som ska användas i företagets brandvägg för att plattformen ska kunna nå din SFTP-server och ansluta till den. Dessa IP-adresser är:

* `184.72.239.68`
* `23.20.85.113`
* `54.226.193.184`

>[!NOTE]
>
>Strukturen för taggbyggen har ändrats med tiden. De använder symboliska länkar (symboler) internt för att bibehålla bakåtkompatibilitet så att tidigare inbäddningskoder fortsätter att fungera med den senaste byggstrukturen. SFTP-servern måste ha stöd för användning av länkar för att fungera som ett giltigt mål för taggbyggen.

Mer detaljerad information finns i följande artikel på [konfigurera SFTP-servrar så att de kan leverera](https://medium.com/launch-by-adobe/configuring-an-sftp-server-for-use-with-adobe-launch-bc626027e5a6).

## Skapa en SFTP-värd {#create}

Välj **[!UICONTROL Hosts]** i den vänstra navigeringen, följt av **[!UICONTROL Add Host]**.

![Bild som visar knappen Lägg till värd som markeras i användargränssnittet](../../../images/ui/publishing/sftp-hosts/add-host-button.png)

Dialogrutan Värdskapande visas. Ange ett namn för värden och under **[!UICONTROL Type]**, markera **[!UICONTROL SFTP]**.

![Bild som visar det SFTP-värdalternativ som väljs](../../../images/ui/publishing/sftp-hosts/select-sftp.png)

### Konfigurera SFTP-värden {#configure}

Dialogrutan utökas och innehåller ytterligare konfigurationsalternativ för SFTP-värden. Dessa förklaras nedan.

![Bild som visar nödvändig information för en SFTP-värdanslutning](../../../images/ui/publishing/sftp-hosts/host-details.png)

| Konfigurationsfält | Beskrivning |
| --- | --- |
| [!UICONTROL Don't Use Symlinks] | Som standard använder alla SFTP-värdar symboliska länkar (symboler) till referensbiblioteket [byggen](../builds.md) som sparas på servern. Alla servrar har dock inte stöd för symboler. När det här alternativet är markerat använder värden en kopieringsåtgärd för att uppdatera byggmaterialet direkt i stället för att använda symboler. |
| [!UICONTROL SFTP Server URL] | URL-bassökvägen för servern. |
| [!UICONTROL Path] | Sökvägen som ska läggas till i basserverns URL för den här värden. |
| [!UICONTROL Port] | Porten måste vara något av följande:<ul><li>`21`</li><li>`22`</li><li>`80`</li><li>`200-299`</li><li>`443`</li><li>`2000-2999`</li><li>`4343`</li><li>`8080`</li><li>`8888`</li></ul>Av säkerhetsskäl bör Adobe begränsa antalet portar som kan användas för utgående trafik. De valda portarna är vanligtvis tillåtna via brandväggar och innehåller vissa intervall för flexibilitet. |
| [!UICONTROL Username] | Användarnamnet som ska användas vid åtkomst till servern. |
| [!UICONTROL Encrypted Private Key] | Den krypterade privata nyckeln som du skapade i en [föregående steg](#access-key). |

Välj **[!UICONTROL Save]** för att skapa värden med den valda konfigurationen.

![Bild som visar den SFTP-värd som sparas](../../../images/ui/publishing/sftp-hosts/save-host.png)

När du väljer **[!UICONTROL Save]**, testas anslutningen och möjligheten att leverera filerna till SFTP-servern. Plattformen skapar en mapp, skriver en fil i den mappen, kontrollerar att filen finns där och rensar sedan efter sig själv. Om användarkontot på din SFTP-server (det som är kopplat till det säkra certifikat som du har angett för plattformen) inte har de behörigheter som krävs för att utföra den här åtgärden, får värden statusen&quot;Misslyckad&quot;.

## Nästa steg

I den här guiden beskrivs hur du konfigurerar en SFTP-server som är värd för sig själv för användning i taggar. När värden har upprättats kan du koppla den till en eller flera av dina [miljöer](../environments.md) för publicering av taggbibliotek. Mer information om hur du aktiverar taggfunktioner på webben och i mobila enheter finns i [publicera översikt](../overview.md).
