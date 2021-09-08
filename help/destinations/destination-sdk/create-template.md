---
description: Som en del av mål-SDK har Adobe utvecklarverktyg som hjälper dig att konfigurera och testa målet. Den här sidan beskriver hur du skapar och testar en meddelandeomformningsmall.
title: Skapa och testa en meddelandeomformningsmall
source-git-commit: cf6c6adf128ec867cd67af609a40b04d2c632bf9
workflow-type: tm+mt
source-wordcount: '895'
ht-degree: 0%

---

# Skapa och testa en meddelandeomformningsmall {#create-template}

## Översikt {#overview}

Som en del av mål-SDK har Adobe utvecklarverktyg som hjälper dig att konfigurera och testa målet. Den här sidan beskriver hur du skapar och testar en meddelandeomformningsmall. Mer information om hur du testar målet finns i [Testa målkonfigurationen](./test-destination.md).

Om du vill **skapa och testa en meddelandeomformningsmall** mellan målschemat i Adobe Experience Platform och det meddelandeformat som stöds av ditt mål använder du *mallutvecklingsverktyget* som beskrivs nedan.  Läs mer om dataomvandlingen mellan käll- och målschemat i [meddelandeformatdokumentet](./message-format.md#using-templating).

Nedan visas hur du skapar och testar en meddelandeomformningsmall passar in i [arbetsflödet för målkonfiguration](./configure-destination-instructions.md) i mål-SDK:

![Bild av var steget Skapa mall passar in i arbetsflödet för målkonfiguration](./assets/create-template-step.png)

## Varför du måste skapa och testa en meddelandeomformningsmall {#why-create-message-transformation-template}

Ett av de första stegen i att skapa destinationen i mål-SDK är att tänka på hur dataformatet för segmentmedlemskap, identiteter och profilattribut ändras när de exporteras från Adobe Experience Platform till destinationen. Hitta information om omvandlingen mellan Adobe XDM-schemat och målschemat i [meddelandeformatdokumentet](./message-format.md#using-templating).

För att omvandlingen ska lyckas måste du skapa en omformningsmall som liknar den i det här exemplet: [Skapa en mall som skickar segment, identiteter och profilattribut](./message-format.md#segments-identities-attributes).

Adobe har ett mallverktyg som gör att du kan skapa och testa meddelandemallen som omformar data från Adobe XDM-formatet till det format som stöds av målet. Verktyget har två API-slutpunkter som du kan använda:
* Använd *exempelmallens API* för att hämta en exempelmall.
* Använd *återgivningsmallens API* för att återge exempelmallen så att du kan jämföra resultatet med målets förväntade dataformat. När du har jämfört exporterade data med det dataformat som förväntas av målet kan du redigera mallen. På så sätt matchar de exporterade data som du genererar det dataformat som förväntas av målet.

## Använda exempelmallens API och återge mall-API för att skapa en mall för ditt mål {#iterative-process}

Processen att hämta och testa mallen är iterativ. Upprepa stegen nedan tills de exporterade profilerna matchar målets förväntade dataformat.

1. [Hämta först en exempelmall](./create-template.md#sample-template-api).
2. Använd exempelmallen som utgångspunkt för att skapa ett eget utkast.
3. Anropa [API-slutpunkten för återgivningsmallen](./create-template.md#render-template-api) med din egen mall. Adobe genererar exempelprofiler baserat på ditt schema och returnerar resultatet eller eventuella fel som påträffats.
4. Jämför exporterade data med det dataformat som du förväntar dig av målet. Redigera mallen om det behövs.
5. Upprepa den här processen tills de exporterade profilerna matchar målets förväntade dataformat.

## Steg som ska slutföras innan mallen skapas {#prerequisites}

Innan du är redo att skapa mallen måste du slutföra stegen nedan:

1. [Skapa en målserverkonfiguration](./destination-server-api.md). Mallen som du ska generera skiljer sig åt, baserat på det värde som du anger för parametern `maxUsersPerRequest`.
   * Använd `maxUsersPerRequest=1` om du vill att ett API-anrop till målet ska innehålla en enda profil, tillsammans med dess segmentkvalifikationer, identiteter och profilattribut.
   * Använd `maxUsersPerRequest` med ett större värde än ett om du vill att ett API-anrop till målet ska innehålla flera profiler, tillsammans med deras segmentkvalifikationer, identiteter och profilattribut.
2. [Skapa en ](./destination-configuration-api.md#create) målkonfiguration och lägg till ID:t för målserverkonfigurationen i  `destinationDelivery.destinationServerId`.
3. [Hämta ID:t för den ](./destination-configuration-api.md#retrieve-list) målkonfiguration som du nyss skapade, så att du kan använda det i mallverktyget.

## Hämta en exempelmall med exempelmallens API {#sample-template-api}

>[!NOTE]
>
>Fullständig API-referensdokumentation finns i [Hämta API-åtgärder för exempelmallar](./sample-template-api.md).

Lägg till ett mål-ID till anropet, så som visas nedan, så returnerar svaret ett mallexempel som motsvarar mål-ID:t.

```shell
curl --location --request GET 'https://platform.adobe.io/data/core/activation/authoring/testing/template/sample/5114d758-ce71-43ba-b53e-e2a91d67b67f' \
--header 'Content-Type: application/json' \
--header 'Accept: application/json' \
--header 'x-api-key: {API_KEY}' \
--header 'Authorization: Bearer {ACCESS_TOKEN}' \
--header 'x-gw-ims-org-id: {IMS_ORG}' \
--header 'x-sandbox-name: {SANDBOX_NAME}' \
```

Om det mål-ID som du anger motsvarar en målservermall med `maxUsersPerRequest=1` returnerar begäran en exempelmall som liknar den här:

```python
{#- THIS is an example template for a single profile -#}
{#- A '-' at the beginning or end of a tag removes all whitespace on that side of the tag. -#}
{
    "identities": [
    {%- for idMapEntry in input.profile.identityMap -%}
    {%- set namespace = idMapEntry.key -%}
        {%- for identity in idMapEntry.value %}
        {
            "type": "{{ namespace }}",
            "id": "{{ identity.id }}"
        }{%- if not loop.last -%},{%- endif -%}
        {%- endfor -%}{%- if not loop.last -%},{%- endif -%}
    {% endfor %}
    ],
    "AdobeExperiencePlatformSegments": {
        "add": [
        {%- for segment in input.profile.segmentMembership.ups | added %}
            "{{ segment.key }}"{%- if not loop.last -%},{%- endif -%}
        {% endfor %}
        ],
        "remove": [
        {#- Alternative syntax for filtering segments by status: -#}
        {% for segment in removedSegments(input.profile.segmentMembership.ups) %}
            "{{ segment.key }}"{%- if not loop.last -%},{%- endif -%}
        {% endfor %}
        ]
    }
}
```

Om det mål-ID som du anger motsvarar en målservermall med `maxUsersPerRequest` större än en, returnerar begäran en exempelmall som liknar den här:

```python
{#- THIS is an example template for multiple profiles -#}
{#- A '-' at the beginning or end of a tag removes all whitespace on that side of the tag. -#}
{
    "profiles": [
    {%- for profile in input.profiles %}
        {
            "identities": [
            {%- for idMapEntry in profile.identityMap -%}
            {%- set namespace = idMapEntry.key -%}
                {%- for identity in idMapEntry.value %}
                {
                    "type": "{{ namespace }}",
                    "id": "{{ identity.id }}"
                }{%- if not loop.last -%},{%- endif -%}
                {%- endfor -%}{%- if not loop.last -%},{%- endif -%}
            {% endfor %}
            ],
            "AdobeExperiencePlatformSegments": {
                "add": [
                {%- for segment in profile.segmentMembership.ups | added %}
                    "{{ segment.key }}"{%- if not loop.last -%},{%- endif -%}
                {% endfor %}
                ],
                "remove": [
                {#- Alternative syntax for filtering segments by status: -#}
                {% for segment in removedSegments(profile.segmentMembership.ups) %}
                    "{{ segment.key }}"{%- if not loop.last -%},{%- endif -%}
                {% endfor %}
                ]
            }
        }{%- if not loop.last -%},{%- endif -%}
    {% endfor %}
    ]
}
```

## Tecken-undgå din mall {#character-escape-template}

Innan du använder mallen för att återge profiler som matchar målets förväntade format, måste du undvika mallen som i skärminspelningen nedan.

![Video som visar hur du kan kringgå en mall med hjälp av ett onlineverktyg för teckenigenkänning](./assets/escape-characters.gif)

Du kan använda ett onlineverktyg för teckenigenkänning. I demonstrationen ovan används formateraren [JSON Escape](https://jsonformatter.org/json-escape).

## Återge mall-API {#render-template-api}

När du har skapat en meddelandeomformningsmall med [exempelmallens API](./create-template.md#sample-template-api) kan du [återge mallen](./render-template-api.md) och generera exporterade data baserat på den. På så sätt kan du verifiera om de profiler som Adobe Experience Platform skulle exportera till ditt mål matchar målets förväntade format.

Se API-referensen för exempel på anrop som du kan göra:

* [Återge en mall utan profiler som skickats i brödtexten](./render-template-api.md#multiple-profiles-no-body)
* [Återge en mall med profiler som skickats i brödtexten](./render-template-api.md#multiple-profiles-with-body)

Redigera mallen och anropa återgivningsmallens API-slutpunkt tills de exporterade profilerna matchar målets förväntade dataformat.

## Lägg till mallen för escape-konverteringar i målserverkonfigurationen

När du är nöjd med mallen för meddelandeomformning lägger du till den i din [målserverkonfiguration](./server-and-template-configuration.md) i `httpTemplate.requestBody.value`.