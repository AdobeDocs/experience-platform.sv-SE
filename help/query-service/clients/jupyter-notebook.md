---
title: Anslut Jupyter-anteckningsbok till frågetjänst
description: Lär dig hur du ansluter Jupyter-anteckningsbok med Adobe Experience Platform Query Service.
source-git-commit: f910deca43ac49d3a3452b8dbafda20ffdf3bf48
workflow-type: tm+mt
source-wordcount: '610'
ht-degree: 0%

---

# Anslut [!DNL Jupyter Notebook] till frågetjänst

Det här dokumentet innehåller de steg som krävs för att ansluta [!DNL Jupyter Notebook] med Adobe Experience Platform Query Service.

## Komma igång

Den här guiden kräver att du redan har åtkomst till [!DNL Jupyter Notebook] och känner till gränssnittet. För nedladdning [!DNL Jupyter Notebook] Mer information finns i [officiell [!DNL Jupyter Notebook] dokumentation](https://jupyter.org/).

Hämta nödvändiga autentiseringsuppgifter för anslutning [!DNL Jupyter Notebook] till Experience Platform måste du ha tillgång till [!UICONTROL Queries] i plattformsgränssnittet. Kontakta din organisations administratör om du inte har tillgång till [!UICONTROL Queries] arbetsyta.

>[!TIP]
>
>[!DNL Anaconda Navigator] är ett grafiskt användargränssnitt som gör det enklare att installera och starta vanliga [!DNL Python] program som [!DNL Jupyter Notebook]. Det hjälper även till att hantera paket, miljöer och kanaler utan att använda kommandoradskommandon.
>Du kan [installera den version av programmet som du föredrar](https://docs.anaconda.com/anaconda/install/) från sin webbplats.
>Följ den guidade installationsprocessen. På startskärmen för Anaconda Navigator väljer du **[!DNL Jupyter Notebook]** i listan över program som stöds för att starta programmet.
>![The [!DNL Anaconda Navigator] hemskärm med [!DNL Jupyter Notebook] markerad.](../images/clients/jupyter-notebook/anaconda-navigator-home.png)
>Mer information finns i deras [officiell dokumentation](https://docs.anaconda.com/anaconda/navigator/).

## Starta [!DNL Jupyter Notebook]

När du har öppnat en ny [!DNL Jupyter Notebook] webbprogram väljer du **[!DNL New]** listruta följt av **[!DNL Python 3]** för att skapa en ny anteckningsbok. The [!DNL Notebook] redigeraren visas.

![The [!DNL Jupiter Notebook] Fliken Arkiv med [!DNL New dropdown] och [!DNL Python] 3 markerade.](../images/clients/jupyter-notebook/new-notebook.png)

På första raden i [!DNL Notebook] anger du följande värde: `pip install psycopg2-binary` och markera **[!DNL Run]** i kommandofältet. Ett meddelande om att åtgärden lyckades visas under inmatningsraden.

>[!IMPORTANT]
>
>Som en del av den här processen för att skapa en anslutning måste du välja **[!DNL Run]** för att köra varje kodrad.

![The [!DNL Notebook] Användargränssnitt med kommandot Installera bibliotek markerat.](../images/clients/jupyter-notebook/install-library.png)

Importera sedan en [!DNL PostgreSQL] databasadapter för [!DNL Python]. Ange värdet: `import psycopg2`och markera **[!DNL Run]**. Det finns inget meddelande om att processen lyckades. Om det inte finns något felmeddelande fortsätter du till nästa steg.

![The [!DNL Notebook] Gränssnitt med drivrutinskoden för importdatabasen markerad.](../images/clients/jupyter-notebook/import-dbdriver.png)

Du måste nu ange dina Adobe Experience Platform-uppgifter genom att ange värdet: `conn = psycopg2.connect("{YOUR_CREDENTIALS}")`. Dina anslutningsreferenser finns i [!UICONTROL Queries] -avsnittet, under [!UICONTROL Credentials] -fliken i plattformsgränssnittet. Läs dokumentationen om hur du [hitta organisationens autentiseringsuppgifter](../ui/credentials.md) för detaljerade anvisningar.

Vi rekommenderar att du använder inloggningsuppgifter som inte upphör att gälla när du använder tredjepartsklienter för att spara arbetet med att ange dina uppgifter upprepade gånger. I dokumentationen finns instruktioner om [hur du genererar och använder inloggningsuppgifter som inte förfaller](../ui/credentials.md#non-expiring-credentials).

>[!IMPORTANT]
>
>När du kopierar inloggningsuppgifter från plattformsanvändargränssnittet ska du kontrollera att det inte finns någon ytterligare formatering av inloggningsuppgifterna. De ska alla ligga på en rad, med ett enda mellanrum mellan egenskaperna och värdena. Autentiseringsuppgifterna omges av citattecken och **not** kommaavgränsade.

![The [!DNL Notebook] Gränssnitt med anslutningsautentiseringsuppgifterna markerade.](../images/clients/jupyter-notebook/provide-credentials.png)

Dina [!DNL Jupyter Notebook] -instansen är nu ansluten till frågetjänsten.

## Exempelfrågekörning

Nu när du är ansluten [!DNL Jupyter Notebook] för att fråga tjänsten kan du utföra frågor på dina datauppsättningar med [!DNL Notebook] indata. I följande exempel används en enkel fråga för att demonstrera processen.

Ange följande värden:

```console
cur = conn.cursor()
cur.execute('''{YOUR_QUERY_HERE}''')
data = [r for r in cur]
```

Anropa sedan parametern (`data` i exemplet ovan) om du vill visa frågeresultatet i ett oformaterat svar.

![The [!DNL Notebook] Gränssnitt med kommandon som returnerar och visar SQL-resultat i anteckningsboken.](../images/clients/jupyter-notebook/example-query.png)

Använd följande kommandon om du vill formatera resultatet på ett mer läsbart sätt:

- `colnames = [desc[0] for desc in cur.description]`
- `import pandas as pd`
- `import numpy as np`

Dessa kommandon genererar inget meddelande om att åtgärden lyckades. Om det inte finns något felmeddelande kan du sedan använda en funktion för att skriva ut resultatet av SQL-frågan i ett tabellformat.

![De kommandon som krävs för att formatera SQL-resultaten.](../images/clients/jupyter-notebook/format-results-commands.png)

Ange och kör `df.head()` -funktion för att se sökresultaten i tabellform.

![Tabellresultat av SQL-frågan i [!DNL Jupyter Notebook].](../images/clients/jupyter-notebook/format-results-output.png)

## Nästa steg

Nu när du har anslutit till frågetjänsten kan du använda [!DNL Jupyter Notebook] för att skriva frågor. Mer information om hur du skriver och kör frågor finns i [köra frågeguide](../best-practices/writing-queries.md).
