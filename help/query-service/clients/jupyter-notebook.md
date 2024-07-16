---
title: Anslut Jupyter-anteckningsbok till frågetjänst
description: Lär dig hur du ansluter Jupyter-anteckningsbok med Adobe Experience Platform Query Service.
exl-id: 358eab67-538f-4ada-931f-783b92db4a1c
source-git-commit: 1af89160cbf5b689396921869fec6c30a5bcfff0
workflow-type: tm+mt
source-wordcount: '559'
ht-degree: 0%

---

# Anslut [!DNL Jupyter Notebook] till frågetjänsten

Det här dokumentet innehåller de steg som krävs för att ansluta [!DNL Jupyter Notebook] till Adobe Experience Platform Query Service.

## Komma igång

Den här guiden kräver att du redan har åtkomst till [!DNL Jupyter Notebook] och känner till dess gränssnitt. Om du vill hämta [!DNL Jupyter Notebook] eller om du vill ha mer information läser du [officiell [!DNL Jupyter Notebook] dokumentation](https://jupyter.org/).

Om du vill få de nödvändiga autentiseringsuppgifterna för att ansluta [!DNL Jupyter Notebook] till Experience Platform måste du ha tillgång till arbetsytan [!UICONTROL Queries] i plattformsgränssnittet. Kontakta din organisationsadministratör om du inte har tillgång till arbetsytan [!UICONTROL Queries].

>[!TIP]
>
>[!DNL Anaconda Navigator] är ett grafiskt användargränssnitt (GUI) som gör det enklare att installera och starta vanliga [!DNL Python]-program som [!DNL Jupyter Notebook]. Det underlättar också hanteringen av paket, miljöer och kanaler utan kommandoradskommandon.
>Följ den guidade installationsprocessen på deras webbplats för att [installera den version av programmet](https://docs.anaconda.com/anaconda/install/) som du föredrar.
>Välj **[!DNL Jupyter Notebook]** i listan över program som stöds för att starta programmet på startskärmen för Anaconda Navigator.
>Mer information finns i den [officiella Anaconda-dokumentationen](https://docs.anaconda.com/anaconda/navigator/).

Den officiella Jupyter-dokumentationen innehåller anvisningar om hur du [kör anteckningsboken från kommandoradsgränssnittet](https://docs.jupyter.org/en/latest/running.html#how-do-i-open-a-specific-notebook) (CLI).

## Starta [!DNL Jupyter Notebook]

När du har öppnat ett nytt [!DNL Jupyter Notebook]-webbprogram väljer du listrutan **[!DNL New]** i gränssnittet, följt av **[!DNL Python 3]**, för att skapa en ny anteckningsbok. [!DNL Notebook]-redigeraren visas.

Ange följande värde på den första raden i [!DNL Notebook]-redigeraren: `pip install psycopg2-binary` och välj **[!DNL Run]** i kommandofältet. Ett meddelande om att åtgärden lyckades visas under inmatningsraden.

>[!IMPORTANT]
>
>Som en del av den här processen för att skapa en anslutning måste du välja **[!DNL Run]** för att köra varje kodrad.

Importera sedan ett [!DNL PostgreSQL]-databaskort för [!DNL Python]. Ange värdet: `import psycopg2` och välj **[!DNL Run]**. Det finns inget meddelande om att processen lyckades. Om det inte finns något felmeddelande fortsätter du till nästa steg.

Du måste nu ange dina Adobe Experience Platform-autentiseringsuppgifter genom att ange värdet: `conn = psycopg2.connect("{YOUR_CREDENTIALS}")`. Dina anslutningsautentiseringsuppgifter finns i avsnittet [!UICONTROL Queries] på fliken [!UICONTROL Credentials] i användargränssnittet för plattformen. Mer information finns i dokumentationen om hur du [hittar dina organisationsuppgifter](../ui/credentials.md).

Vi rekommenderar att du använder inloggningsuppgifter som inte upphör att gälla när du använder tredjepartsklienter för att spara arbetet med att ange dina uppgifter upprepade gånger. I dokumentationen finns instruktioner om [hur du genererar och använder autentiseringsuppgifter som inte upphör att gälla](../ui/credentials.md#non-expiring-credentials).

>[!IMPORTANT]
>
>När du kopierar inloggningsuppgifter från plattformsgränssnittet behövs ingen ytterligare formatering av inloggningsuppgifterna. De kan anges på en rad med ett enda mellanrum mellan egenskaperna och värdena. Autentiseringsuppgifterna omges av citattecken och **inte** kommaavgränsade.

```python
conn = psycopg2.connect('''sslmode=require host=<YOUR_HOST_CREDENTIAL> port=80 dbname=prod:all user=<YOUR_ORGANIZATION_ID> password=<YOUR_PASSWORD>''')"
```

[!DNL Jupyter Notebook]-instansen är nu ansluten till frågetjänsten.

## Exempelfrågekörning

Nu när du har anslutit [!DNL Jupyter Notebook] till frågetjänsten kan du utföra frågor på dina datauppsättningar med dina [!DNL Notebook]-indata. I följande exempel används en enkel fråga för att demonstrera processen.

Ange följande värden:

```python
cur = conn.cursor()
cur.execute('''<YOUR_QUERY_HERE>''')
data = [r for r in cur]
```

Anropa sedan parametern (`data` i exemplet ovan) för att visa frågeresultaten i ett oformaterat svar.

Använd följande kommandon om du vill formatera resultatet på ett mer läsbart sätt:

- `colnames = [desc[0] for desc in cur.description]`
- `import pandas as pd`
- `import numpy as np`
- `df = pd.DataFrame(samples,columns=colnames)`
- `df.fillna(0,inplace=True)`

Dessa kommandon genererar inget meddelande om att åtgärden lyckades. Om det inte finns något felmeddelande kan du sedan använda en funktion för att skriva ut resultatet av SQL-frågan i ett tabellformat.

Ange och kör funktionen `df.head()` för att se resultatet av en tabellfråga.

## Nästa steg

Nu när du har anslutit till frågetjänsten kan du använda [!DNL Jupyter Notebook] för att skriva frågor. Mer information om hur du skriver och kör frågor finns i [guiden ](../best-practices/writing-queries.md) som kör frågor.
