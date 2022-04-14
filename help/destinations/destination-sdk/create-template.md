---
description: Som en del av Destinationen SDK har Adobe utvecklarverktyg som hjälper dig att konfigurera och testa destinationen. Den här sidan beskriver hur du skapar och testar en meddelandeomformningsmall.
title: Skapa och testa en meddelandeomformningsmall
exl-id: 15e7f436-4d33-4172-bd14-ad8dfbd5e4a8
source-git-commit: 97ffaa2a53dbbf5a7be5f002e63be4ed3339f565
workflow-type: tm+mt
source-wordcount: '960'
ht-degree: 0%

---

# Create and test a message transformation template {#create-template}

## Översikt {#overview}

Som en del av Destinationen SDK har Adobe utvecklarverktyg som hjälper dig att konfigurera och testa destinationen. This page describes how to create and test a message transformation template. For information on how to test your destination, read [Test your destination configuration](./test-destination.md).

Till **skapa och testa en meddelandeomvandlingsmall** mellan målschemat i Adobe Experience Platform och meddelandeformatet som stöds av ditt mål, använd *Mallredigeringsverktyg* beskrivs närmare nedan.  Läs mer om dataomvandlingen mellan käll- och målschemat i [meddelandeformatdokument](./message-format.md#using-templating).

Nedan visas hur du skapar och testar en meddelandeomformningsmall som passar in i [arbetsflöde för målkonfiguration](./configure-destination-instructions.md) i Destination SDK:

![Bild av var steget Skapa mall passar in i arbetsflödet för målkonfiguration](./assets/create-template-step.png)

## Varför du måste skapa och testa en meddelandeomformningsmall {#why-create-message-transformation-template}

One of the first steps in creating your destination in Destination SDK is to think about how the data format for segment membership, identities, and profile attributes is transformed when exported from Adobe Experience Platform to your destination. Hitta information om omvandlingen mellan Adobe XDM-schemat och målschemat i [meddelandeformatdokument](./message-format.md#using-templating).

För att omvandlingen ska lyckas måste du skapa en omformningsmall som liknar den i det här exemplet: [Skapa en mall som skickar segment, identiteter och profilattribut](./message-format.md#segments-identities-attributes).

Adobe har ett mallverktyg som gör att du kan skapa och testa meddelandemallen som omformar data från Adobe XDM-formatet till det format som stöds av målet. Verktyget har två API-slutpunkter som du kan använda:
* Use the *sample template API* to get a sample template.
* Använd *rendera mall-API* för att återge exempelmallen så att du kan jämföra resultatet med målets förväntade dataformat. När du har jämfört exporterade data med det dataformat som förväntas av målet kan du redigera mallen. This way, the exported data you generate matches the data format expected by your destination.

## Steps to complete before creating the template {#prerequisites}

Innan du är redo att skapa mallen måste du slutföra stegen nedan:

1. [Skapa en målserverkonfiguration](./destination-server-api.md). Mallen som du skapar skiljer sig åt, baserat på det värde som du anger för `maxUsersPerRequest` parameter.
   * Use `maxUsersPerRequest=1` if you want an API call to your destination to include a single profile, along with its segment qualifications, identities, and profile attributes.
   * Use `maxUsersPerRequest` with a value greater than one if you want an API call to your destination to include multiple profiles, along with their segment qualifications, identities, and profile attributes.
2. [Create a destination configuration](./destination-configuration-api.md#create) and add the ID of the destination server configuration in `destinationDelivery.destinationServerId`.
3. [Get the ID of the destination configuration](./destination-configuration-api.md#retrieve-list) that you just created, so you can use it in the template creation tool.
4. Förstå [vilka funktioner och filter du kan använda](./supported-functions.md) i meddelandeomformningsmallen.

## Använda exempelmallens API och återge mall-API för att skapa en mall för ditt mål {#iterative-process}

>[!TIP]
>
>Innan du skapar och redigerar din meddelandeomformningsmall kan du börja med att anropa [rendera mall-API-slutpunkt](./render-template-api.md#render-exported-data) med en enkel mall som exporterar dina Raw-profiler utan att använda några omformningar. Syntaxen för den enkla mallen är: <br> `"template": "{% for profile in input.profiles %}{{profile|raw}}{% endfor %}}"`

The process to get and test the template is iterative. Repeat the steps below until the exported profiles match your destination&#39;s expected data format.

1. Första, [hämta en exempelmall](./create-template.md#sample-template-api).
2. Använd exempelmallen som utgångspunkt för att skapa ett eget utkast.
3. Call the [render template API endpoint](./create-template.md#render-template-api) with your own template. Adobe genererar exempelprofiler baserat på ditt schema och returnerar resultatet eller eventuella fel som påträffats.
4. Jämför exporterade data med det dataformat som du förväntar dig av målet. Redigera mallen om det behövs.
5. Upprepa den här processen tills de exporterade profilerna matchar målets förväntade dataformat.

## Get a sample template using the Sample template API {#sample-template-api}

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

If the destination ID you provide corresponds to a destination configuration with [best effort aggregation](./destination-configuration.md#best-effort-aggregation) and `maxUsersPerRequest=1` in the aggregation policy, the request returns a sample template similar to this one:

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

If the destination ID you provide corresponds to a destination server template with [configurable aggregation](./destination-configuration.md#configurable-aggregation) or [best effort aggregation](./destination-configuration.md#best-effort-aggregation) with `maxUsersPerRequest` greater than one, the request returns a sample template similar to this one:

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

## Character-escape your template {#character-escape-template}

Innan du använder mallen för att återge profiler som matchar målets förväntade format, måste du undvika mallen som i skärminspelningen nedan.

![Video that shows how to character-escape a template using an online character escaping tool](./assets/escape-characters.gif)

Du kan använda ett onlineverktyg för teckenigenkänning. The demo above uses the [JSON Escape formatter](https://jsonformatter.org/json-escape).

## Återge mall-API {#render-template-api}

After creating a message transformation template using the [sample template API](./create-template.md#sample-template-api), you can [render the template](./render-template-api.md) to generate exported data based on it. På så sätt kan du verifiera om de profiler som Adobe Experience Platform skulle exportera till ditt mål matchar målets förväntade format.

Refer to the API reference for examples of calls that you can make:

* [Återge en mall utan profiler som skickats i brödtexten](./render-template-api.md#multiple-profiles-no-body)
* [Återge en mall med profiler som skickats i brödtexten](./render-template-api.md#multiple-profiles-with-body)

Redigera mallen och anropa återgivningsmallens API-slutpunkt tills de exporterade profilerna matchar målets förväntade dataformat.

## Lägg till mallen för escape-konverteringar i målserverkonfigurationen

Once you are satisfied with your message transformation template, add it to your [destination server configuration](./server-and-template-configuration.md), in `httpTemplate.requestBody.value`.
