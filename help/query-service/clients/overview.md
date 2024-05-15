---
keywords: Experience Platform;hem;populära ämnen;Query Service;Query Service;connect;connect to query service;aqua data studio;Aqua Data Studio;Looker;Looker;Postico;postico;Power BI bi;psql;rstudio;PSQL;RStudio;Tableau;tab leau;
solution: Experience Platform
title: Koppla klienter till frågetjänsten
description: Det här dokumentet förklarar hur du ansluter till Query Service från ett antal klientprogram och hur du verifierar dessa anslutningar.
exl-id: 2ba20179-5adb-4259-a120-231a40e78054
source-git-commit: 26f0725f0f239707bd719ed46929648f8d557155
workflow-type: tm+mt
source-wordcount: '269'
ht-degree: 0%

---

# Koppla klienter till [!DNL Query Service]

I det här avsnittet beskrivs hur du ansluter till [!DNL Query Service] från en mängd olika klientprogram och hur du verifierar dessa anslutningar. [!DNL Query Service] använder [!DNL PostgreSQL] så instruktionerna i det här avsnittet förklarar hur du använder [!DNL PostgreSQL] verktyg och drivrutiner för att ansluta och skriva frågor.

>[!IMPORTANT]
>
>TLS/SSL-certifikaten i produktionsmiljöer för API:t för frågetjänsten Interactive Postgres uppdaterades onsdagen den 24 januari 2024.<br>Även om detta är ett årligt krav har rotcertifikatet i kedjan även ändrats eftersom Adobe TLS/SSL-certifikatprovidern har uppdaterat sin certifikathierarki. Detta kan påverka vissa Postgres-klienter om deras lista över certifikatutfärdare saknar rotcertifikatet. En PSQL CLI-klient kan till exempel behöva lägga till rotcertifikaten i en explicit fil `~/postgresql/root.crt`, annars kan det leda till ett fel. Till exempel: `psql: error: SSL error: certificate verify failed`. Se [officiell PostgreSQL-dokumentation](https://www.postgresql.org/docs/current/libpq-ssl.html#LIBQ-SSL-CERTIFICATES) om du vill ha mer information om problemet.<br>Rotcertifikatet som ska läggas till kan hämtas från [https://cacerts.digicert.com/DigiCertGlobalRootG2.crt.pem](https://cacerts.digicert.com/DigiCertGlobalRootG2.crt.pem).

Instruktioner finns för följande klienter:

- [[!DNL Aqua Data Studio]](./aqua-data-studio.md)
- [[!DNL DbVisualizer]](./dbvisulaizer.md)
- [[!DNL Looker]](./looker.md)
- [[!DNL Postico (Mac)]](./postico.md)
- [[!DNL Power BI (PC)]](./power-bi.md)
- [[!DNL PSQL]](./psql.md)
- [[!DNL RStudio]](./rstudio.md)
- [[!DNL Tableau]](./tableau.md)

>[!IMPORTANT]
>
>Som Power BI- och Tableau-användare kan du ansluta Customer Journey Analytics till dina BI-verktyg från fliken med autentiseringsuppgifter för frågetjänsten. Instruktioner om hur du gör det finns i dokumentationen för inloggningsuppgifterna [koppla dina BI-verktyg till Customer Journey Analytics](../ui/credentials.md#connect-to-customer-journey-analytics).
