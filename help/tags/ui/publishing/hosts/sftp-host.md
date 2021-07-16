---
title: SFTP-värdar
description: Lär dig hur du konfigurerar taggar i Adobe Experience Platform för att leverera biblioteksbyggen till en säker, självvärd SFTP-server.
source-git-commit: 39d9468e5d512c75c9d540fa5d2bcba4967e2881
workflow-type: tm+mt
source-wordcount: '522'
ht-degree: 1%

---

# SFTP-värdar

>[!NOTE]
>
>Adobe Experience Platform Launch omdöms till en serie datainsamlingstekniker i Experience Platform. Som ett resultat av detta har flera terminologiska förändringar införts i produktdokumentationen. Se följande [dokument](../../../term-updates.md) för en konsoliderad referens till terminologiska ändringar.

Om du inte vill att Adobe ska hantera dina värdbibliotek är det andra alternativet att låta Adobe Experience Platform leverera byggen till en säker SFTP-server som du är värd för.

Plattformen ansluter till din SFTP-plats med hjälp av en krypterad nyckel. Det finns några steg för att konfigurera detta korrekt:

1. Du måste ha ett nyckelpar för offentlig/privat nyckel installerat på SFTP-servern. Du kan generera nycklarna på servern eller generera dem någon annanstans och installera dem på servern. Mer information finns i GitHub-dokumentationen om [hur du skapar SSH-nycklar](https://help.github.com/articles/generating-a-new-ssh-key-and-adding-it-to-the-ssh-agent/#generating-a-new-ssh-key).
1. Den privata nyckeln används för att kryptera den offentliga GPG-nyckeln. Du måste ange din privata nyckel när du skapar SFTP-värden. I avsnittet [Kryptera värden](https://developer.adobelaunch.com/api/guides/encrypting_values/) i dokumentationen för Reactor API finns instruktioner om hur du krypterar offentliga GPG-nycklar. Använd produktionsmiljöns GPG-nyckel om du inte vet att du behöver en viss. Slutligen kan du kryptera din privata nyckel från vilken dator som helst, så du behöver inte installera GPG på servern för att slutföra det här steget.
1. Du kan behöva godkänna IP-adresserna som används med företagets brandvägg för att plattformen ska kunna nå din SFTP-server och ansluta till den. Dessa IP-adresser är:
   * `184.72.239.68`
   * `23.20.85.113`
   * `54.226.193.184`

>[!NOTE]
>
>Strukturen för taggbyggen har ändrats med tiden. De använder symboliska länkar (symboler) internt för att bibehålla bakåtkompatibilitet så att tidigare inbäddningskoder fortsätter att fungera med den senaste byggstrukturen. SFTP-servern måste ha stöd för användning av länkar för att fungera som ett giltigt mål för taggbyggen.

Mer detaljerad information finns i följande mediaartikel om [hur du konfigurerar SFTP-servrar för att leverera en bygge](https://medium.com/launch-by-adobe/configuring-an-sftp-server-for-use-with-adobe-launch-bc626027e5a6).

## Skapa en SFTP-värd

1. Öppna fliken [!UICONTROL Hosts].
1. Skapa den nya värden.
1. Ge värden ett namn.
1. Välj **[!UICONTROL SFTP]** som värdtyp.
1. Ange värden, sökväg, port, användarnamn och krypterad privat nyckel.

   Porten måste vara något av följande:

   * 21
   * 22
   * 80
   * 200-299
   * 443
   * 2000-2999
   * 4343
   * 8080
   * 8888

   >[!NOTE]
   >
   >Som en god säkerhetsrutin begränsar Adobe antalet portar som kan användas för utgående trafik. De valda portarna är vanligtvis tillåtna via brandväggar, plus vissa intervall för flexibilitet.

1. Välj **[!UICONTROL Save]**.

När du väljer **[!UICONTROL Save]** testas anslutningen och möjligheten att leverera filerna till SFTP-servern. Plattformen skapar en mapp, skriver en fil i den mappen, kontrollerar att filen finns där och rensar efter sig själv. Om användarkontot på din SFTP-server (det som är kopplat till det säkra certifikat som du har angett för plattformen) inte har de behörigheter som krävs för att utföra den här åtgärden, får värden statusen&quot;Misslyckad&quot;.
