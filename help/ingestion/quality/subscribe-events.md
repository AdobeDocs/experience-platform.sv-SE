---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Prenumerera på dataöverföringshändelser
topic: overview
translation-type: tm+mt
source-git-commit: 4817162fe2b7cbf4ae4c1ed325db2af31da5b5d3

---


# Meddelanden om dataöverföring

Processen att samla in data i Adobe Experience Platform består av flera steg. När du har identifierat datafiler som behöver importeras till plattformen, börjar inmatningsprocessen och varje steg sker i följd tills data antingen har importerats eller misslyckats. Inmatningsprocessen kan initieras med [Adobe Experience Platforms API](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/ingest-api.yaml) för datainmatning eller med användargränssnittet för Experience Platform.

Data som läses in på Platform måste gå igenom flera steg för att nå sin destination, Data Lake eller i realtidskundprofilens datalager. Varje steg innebär att bearbeta data, validera data och sedan lagra data innan de skickas vidare till nästa steg. Beroende på mängden data som hämtas kan detta bli en tidskrävande process och det finns alltid en risk att processen misslyckas på grund av validerings-, semantik- eller bearbetningsfel. Om ett fel uppstår måste dataproblemen åtgärdas och sedan måste hela importen startas om med de korrigerade datafilerna.

Experience Platform gör det möjligt att prenumerera på en uppsättning händelser som publiceras i varje steg i processen, vilket gör det lättare att övervaka processen och meddela dig om statusen för inkapslade data och eventuella fel.

## Tillgängliga statusmeddelandehändelser

Nedan visas en lista över tillgängliga statusmeddelanden för dataöverföring som du kan prenumerera på.

>[!NOTE] Det finns bara ett händelseämne för alla meddelanden om dataöverföring. Händelsekoden kan användas för att skilja mellan olika statusvärden.

| Plattformstjänst | Status | Händelsebeskrivning | Händelsekod |
| ---------------- | ------ | ----------------- | ---------- |
| Datalager | framgång | Inmatning - batchen har slutförts | ing_load_success |
| Datalager | fel | Inmatning - batchen misslyckades | ing_load_error |
| Kundprofil i realtid | framgång | Profiltjänst - datainläsningsbatch lyckades | ps_load_success |
| Kundprofil i realtid | fel | Profiltjänst - Datainläsningsbatchen misslyckades | ps_load_error |
| Identitetsdiagram | framgång | Identitetsdiagram - datainläsningsbatchen har slutförts | ig_load_success |
| Identitetsdiagram | fel | Identitetsdiagram - datainläsningsbatchen misslyckades | ig_load_error |

## Meddelandenyttolastschema

Datainmatningsmeddelandets händelseschema är ett XDM-schema (Experience Data Model) som innehåller fält och värden som ger information om statusen för de data som hämtas. Besök den offentliga XDM GitHub-repon för att se det senaste [meddelandeschemat](https://github.com/adobe/xdm/blob/master/schemas/common/notifications/ingestion.schema.json).

## Prenumerera på statusmeddelanden för datainmatning

Genom [Adobe I/O Events](https://www.adobe.io/apis/experienceplatform/events.html)kan du prenumerera på flera olika typer av meddelanden via webbhooks. Om du vill veta mer om webbhooks och hur du prenumererar på Adobe I/O Events med hjälp av webbhooks kan du läsa [introduktionen till Adobe I/O Events-webbhooks](https://www.adobe.io/apis/experienceplatform/events/docs.html#!adobedocs/adobeio-events/master/intro/webhook_docs_intro.md) .

### Skapa en ny integrering med Adobe I/O Console

Logga in på [Adobe I/O Console](https://console.adobe.io/home) och klicka på fliken *Integreringar* eller klicka på **Skapa integrering** under Snabbstart. När skärmen *Integrering* visas klickar du på **Ny integrering** för att skapa en ny integrering.

![Skapa ny integrering](../images/quality/subscribe-events/create_integration_start.png)

Skärmen *Skapa ny integrering* visas. Välj **Ta emot händelser** i realtid och klicka sedan på **Fortsätt**.

![Ta emot händelser nära realtid](../images/quality/subscribe-events/create_integration_receive_events.png)

Nästa skärm innehåller alternativ för att skapa integreringar med olika händelser, produkter och tjänster som är tillgängliga för din organisation baserat på dina prenumerationer, berättiganden och behörigheter. För den här integreringen väljer du **plattformsmeddelanden** under Experience Platform och klickar sedan på **Fortsätt**.

![Välj händelseprovider](../images/quality/subscribe-events/create_integration_select_provider.png)

Formuläret *Integreringsinformation* visas. Du måste ange ett namn och en beskrivning för integreringen samt certifikat för offentlig nyckel.

Om du inte har något offentligt certifikat kan du generera ett i terminalen med följande kommando:

```shell
openssl req -x509 -sha256 -nodes -days 365 -newkey rsa:2048 -keyout private.key -out certificate_pub
```

När du har skapat ett certifikat drar och släpper du filen i rutan **Publika nycklar för certifikat** eller klickar på **Välj en fil** för att bläddra i din filkatalog och välja certifikatet direkt.

När du har lagt till ditt certifikat visas alternativet *Händelseregistrering* . Klicka på **Lägg till händelseregistrering**.

![integreringsinformation](../images/quality/subscribe-events/create_integration_details.png)

Dialogrutan *Händelseregistreringsinformation* utökas så att ytterligare kontroller visas. Här kan du välja önskad händelsetyp och registrera din webkrok. Ange ett namn för händelseregistreringen, webkroks-URL *(valfritt)* samt en kort beskrivning. Välj slutligen de händelsetyper som du vill prenumerera på (meddelande om dataöverföring) och klicka sedan på **Spara**.

![Välj händelser](../images/quality/subscribe-events/create_integration_select_event.png)

## Nästa steg

När du har skapat en I/O-integrering kan du visa alla mottagna meddelanden för den integreringen. Mer information om hur du spårar händelser finns i [hjälpguiden för Adobe I/O Events](https://www.adobe.io/apis/experienceplatform/events/docs.html#!adobedocs/adobeio-events/master/support/tracing.md) .
