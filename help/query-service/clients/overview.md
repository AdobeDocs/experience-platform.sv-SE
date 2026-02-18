---
keywords: Experience Platform;home;populära topics;Query service;query service;connect;connect to query service;aqua data studio;Aqua Data Studio;Looker;Looker;Postico;postico;Power BI;power bi;psql;rstudio;PSQL;RStudio;Tableau;tableau;
solution: Experience Platform
title: Koppla klienter till frågetjänsten
description: Det här dokumentet förklarar hur du ansluter till Query Service från ett antal klientprogram och hur du verifierar dessa anslutningar.
exl-id: 2ba20179-5adb-4259-a120-231a40e78054
source-git-commit: 5e5a196074e844826579102fa6b36102c6481096
workflow-type: tm+mt
source-wordcount: '281'
ht-degree: 0%

---

# Anslut klienter till frågetjänsten

I det här avsnittet beskrivs hur du ansluter till frågetjänsten från en mängd olika klientprogram och hur du verifierar dessa anslutningar. Frågetjänsten använder protokollet PostgreSQL, så instruktionerna i det här avsnittet beskriver hur du använder PostgreSQL-verktyg och -drivrutiner för att ansluta till och skriva frågor.

>[!IMPORTANT]
>
>TLS/SSL-certifikaten i produktionsmiljöer för API:t för frågetjänsten Interactive Postgres uppdaterades onsdagen den 24 januari 2024.<br>Även om detta är ett årligt krav har rotcertifikatet i kedjan också ändrats eftersom Adobe TLS/SSL-certifikatleverantör har uppdaterat sin certifikathierarki. Detta kan påverka vissa Postgres-klienter om deras lista över certifikatutfärdare saknar rotcertifikatet. En PSQL CLI-klient kan till exempel behöva lägga till rotcertifikaten i en explicit fil `~/postgresql/root.crt`, annars kan det leda till ett fel, till exempel `psql: error: SSL error: certificate verify failed`. Mer information om det här problemet finns i den [officiella PostgreSQL-dokumentationen](https://www.postgresql.org/docs/current/libpq-ssl.html#LIBQ-SSL-CERTIFICATES).<br>Rotcertifikatet som ska läggas till kan hämtas från [https://cacerts.digicert.com/DigiCertGlobalRootG2.crt.pem](https://cacerts.digicert.com/DigiCertGlobalRootG2.crt.pem).

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
>Som Power BI- och Tableau-användare kan du ansluta Customer Journey Analytics till dina BI-verktyg med hjälp av autentiseringsuppgifterna på fliken för frågetjänstens autentiseringsuppgifter. Instruktioner om hur du [ansluter dina BI-verktyg till Customer Journey Analytics](../ui/credentials.md#connect-to-customer-journey-analytics) finns i dokumentationen för autentiseringsuppgifter.
