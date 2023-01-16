---
title: Anslut Jupyter-anteckningsbok till frågetjänst
description: Lär dig hur du ansluter Jupyter-anteckningsbok med Adobe Experience Platform Query Service.
exl-id: 358eab67-538f-4ada-931f-783b92db4a1c
source-git-commit: 1af89160cbf5b689396921869fec6c30a5bcfff0
workflow-type: tm+mt
source-wordcount: '571'
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
>Följ den guidade installationsprocessen på deras webbplats för att [installera den version av programmet som du föredrar](https://docs.anaconda.com/anaconda/install/).
>På startskärmen för Anaconda Navigator väljer du **[!DNL Jupyter Notebook]** i listan över program som stöds för att starta programmet.
>Mer information finns i [officiell dokumentation för Anaconda](https://docs.anaconda.com/anaconda/navigator/).

I den officiella Jupyter-dokumentationen finns instruktioner för att [köra anteckningsboken från kommandoradsgränssnittet](https://docs.jupyter.org/en/latest/running.html#how-do-i-open-a-specific-notebook) (CLI).

## Starta [!DNL Jupyter Notebook]

När du har öppnat en ny [!DNL Jupyter Notebook] webbprogram väljer du **[!DNL New]** listruta från användargränssnittet, följt av **[!DNL Python 3]** för att skapa en ny anteckningsbok. The [!DNL Notebook] redigeraren visas.

På första raden i [!DNL Notebook] anger du följande värde: `pip install psycopg2-binary` och markera **[!DNL Run]** i kommandofältet. Ett meddelande om att åtgärden lyckades visas under inmatningsraden.

>[!IMPORTANT]
>
>Som en del av den här processen för att skapa en anslutning måste du välja **[!DNL Run]** för att köra varje kodrad.

Importera sedan en [!DNL PostgreSQL] databasadapter för [!DNL Python]. Ange värdet: `import psycopg2`och markera **[!DNL Run]**. Det finns inget meddelande om att processen lyckades. Om det inte finns något felmeddelande fortsätter du till nästa steg.

Du måste nu ange dina Adobe Experience Platform-uppgifter genom att ange värdet: `conn = psycopg2.connect("{YOUR_CREDENTIALS}")`. Dina anslutningsreferenser finns i [!UICONTROL Queries] -avsnittet, under [!UICONTROL Credentials] -fliken i plattformsgränssnittet. Läs dokumentationen om hur du [hitta organisationens autentiseringsuppgifter](../ui/credentials.md) för detaljerade anvisningar.

Vi rekommenderar att du använder inloggningsuppgifter som inte upphör att gälla när du använder tredjepartsklienter för att spara arbetet med att ange dina uppgifter upprepade gånger. I dokumentationen finns instruktioner om [hur du genererar och använder inloggningsuppgifter som inte förfaller](../ui/credentials.md#non-expiring-credentials).

>[!IMPORTANT]
>
>När du kopierar inloggningsuppgifter från plattformsgränssnittet behövs ingen ytterligare formatering av inloggningsuppgifterna. De kan anges på en rad med ett enda mellanrum mellan egenskaperna och värdena. Autentiseringsuppgifterna omges av citattecken och **not** kommaavgränsade.

```python
conn = psycopg2.connect('''sslmode=require host=<YOUR_HOST_CREDENTIAL> port=80 dbname=prod:all user=<YOUR_ORGANIZATION_ID> password=<YOUR_PASSWORD>''')"
```

Dina [!DNL Jupyter Notebook] -instansen är nu ansluten till frågetjänsten.

## Exempelfrågekörning

Nu när du är ansluten [!DNL Jupyter Notebook] för att fråga tjänsten kan du utföra frågor på dina datauppsättningar med [!DNL Notebook] indata. I följande exempel används en enkel fråga för att demonstrera processen.

Ange följande värden:

```python
cur = conn.cursor()
cur.execute('''<YOUR_QUERY_HERE>''')
data = [r for r in cur]
```

Anropa sedan parametern (`data` i exemplet ovan) om du vill visa frågeresultatet i ett oformaterat svar.

Använd följande kommandon om du vill formatera resultatet på ett mer läsbart sätt:

- `colnames = [desc[0] for desc in cur.description]`
- `import pandas as pd`
- `import numpy as np`
- `df = pd.DataFrame(samples,columns=colnames)`
- `df.fillna(0,inplace=True)`

Dessa kommandon genererar inget meddelande om att åtgärden lyckades. Om det inte finns något felmeddelande kan du sedan använda en funktion för att skriva ut resultatet av SQL-frågan i ett tabellformat.

Ange och kör `df.head()` -funktion för att se sökresultaten i tabellform.

## Nästa steg

Nu när du har anslutit till frågetjänsten kan du använda [!DNL Jupyter Notebook] för att skriva frågor. Mer information om hur du skriver och kör frågor finns i [köra frågeguide](../best-practices/writing-queries.md).
