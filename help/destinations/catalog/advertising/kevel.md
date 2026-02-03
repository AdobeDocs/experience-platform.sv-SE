---
title: Kevel Connection
description: Använd Kevel streaming-målet för att aktivera målgrupper direkt i Kevels API:er för UserDB och segmenthantering och ge stöd för målgruppsanpassning i realtid vid beslut.
last-substantial-update: 2026-01-27T00:00:00Z
source-git-commit: 04d01b2deafb1b8f1b0c256f31475bb75989a2c4
workflow-type: tm+mt
source-wordcount: '1037'
ht-degree: 1%

---


# [!DNL Kevel]-anslutning {#kevel}

## Översikt {#overview}

[[!DNL Kevel]](https://www.kevel.com/) innehåller den AI-aktiverade tekniken och expertvägledningen som hjälper innovativa handelsledare att starta, skala och lyckas inom detaljhandelsmedia. Retail Media Cloud för [!DNL Kevel] har funktioner för riktade, hänförliga och anpassningsbara annonseringsformat för annonsering på plats och utanför webbplatsen.

Strömningsmålet [!DNL Kevel] för Adobe Experience Platform gör det möjligt för kunder att aktivera Adobe-målgrupper direkt i [!DNL Kevel]s API:er för UserDB och segmenthantering för att ge stöd för målanpassning i realtid vid annonsbeslut.

>[!IMPORTANT]
> 
>Om du har frågor eller vill begära en uppdatering om [!DNL Kevel]-målet eller dess dokumentation skickar du ett e-postmeddelande till [!DNL Kevel]-teamet på [support@kevel.com](mailto:support@kevel.com).

## Användningsfall {#use-cases}

Ni kan aktivera avancerade förstahandsbeteendemålgrupper i alla era medieupplevelser för detaljhandeln för att leverera mer relevanta annonser och bättre resultat. I Experience Platform bygger du upp värdefulla, intent-baserade målgrupper, till exempel ofta förekommande kategorikunder eller användare med senaste produktintresse, och synkroniserar dessa medlemskap till [!DNL Kevel] i realtid. [!DNL Kevel] gör omedelbart dessa segment tillgängliga för annonsbeslut, vilket möjliggör exakt målinriktning för sponsrade produkter och andra format i söknings-, bläddrings- och appupplevelser. Så fort man är berättigad kan man agera utifrån dessa signaler för att få mer relevanta intryck, bättre målinriktning samt bättre mätning och ROAS.

## Förhandskrav {#prerequisites}

För att förbereda dig för att använda målet [!DNL Kevel] måste följande krav vara uppfyllda:

- Du måste ha en aktiv **[!DNL Kevel]-nätverks**- och API-åtkomst.
- Du behöver en **[!DNL Kevel]API-nyckel** med behörighet att skapa segment och uppdatera UserDB-poster.
- Du måste konfigurera identitetsnamnutrymmen i Experience Platform som mappar till de identiteter som din webbplats eller app skickar under [!DNL Kevel] annonsbegäranden (till exempel ECID, GAID, IDFA, lojalitets-ID).
- Adobe-kunder bör endast mappa identiteter som används vid realtidsannonsbegäranden, eftersom varje identitet resulterar i en UserDB-post.

## Identiteter som stöds {#supported-identities}

Målet [!DNL Kevel] stöder aktivering för alla identiteter som programmet kan använda när det skickar annonsförfrågningar till [!DNL Kevel]. Du kan mappa upp till tre identitetsnamnutrymmen för att generera motsvarande UserDB-poster.

[!DNL Kevel] stöder följande Experience Platform-identitetsnamnutrymmen:

| Namnutrymme för identitet | Beskrivning | Normal användning |
|--------------------|---------------------------------|----------------------------------------------------------------|
| **ECID** | EXPERIENCE CLOUD ID | Används för personalisering på plats och Adobe-övergripande identifiering. |
| **GAID** | GOOGLE ADVERTISING ID | Används för Android app-/enhetstrafik. |
| **IDFA** | APPLE ADVERTISING ID | Används för iOS app-/enhetstrafik (med förbehåll för ATT DU samtycker). |
| **EXTERNAL_ID** | Externt ID (anpassad identifierare) | Skickar egna eller backend-genererade ID:n. |

{style="table-layout:auto"}

### Stöd för anpassade identitetsnamnutrymmen

[!DNL Kevel]-målet **accepterar också anpassade namnutrymmen**, enligt definitionen i din Experience Platform-implementering.

Detta innebär:

- Du kan mappa **kundspecifika identitetsnamnutrymmen** (till exempel: `loyalty_id`, `gigya_id` eller en anpassad identitet som du har definierat i identitetstjänsten).
- Dessa namnutrymmen kan tilldelas till `kevel_user_key1`, `kevel_user_key2` eller `kevel_user_key3` på samma sätt som globala namnutrymmen.
- [!DNL Kevel] genererar **en UserDB-post per instans av varje mappad identitet**, vilket möjliggör matchning i realtid vid annonsbeslut för varje identifierare som systemen skickar.

### Beteende för identitetsmappning

- Du kan mappa **upp till tre** Experience Platform-identitetsnamnutrymmen till [!DNL Kevel] tre identitetsplatser.
- För varje aktiverad profil tar [!DNL Kevel] emot **en UserDB-post per instans av varje mappad identitet**.
- Kunder bör bara mappa identiteter som de faktiskt skickar in annonsbegäranden till [!DNL Kevel] för att undvika onödig lagring i UserDB.

![Mappningsexempel för Kevel-mål](/help/destinations/assets/catalog/advertising/kevel-destination-mappings.png)

## Målgrupper {#supported-audiences}

| Målgruppsursprung | Stöds | Beskrivning |
|-----------------------|-----------|---------------------------------------------------------- |
| Segmenteringstjänst | Ja | Adobe Profilmålgrupper utvärderade med segmenteringsmotorn. |
| Anpassade överföringar | Nej | Stöds inte just nu. |

{style="table-layout:auto"}

## Exportera typ och frekvens {#export-type-frequency}

| Objekt | Typ | Anteckningar |
|------|------|-------|
| Exporttyp | **Segmentexport** | [!DNL Kevel] får en uppdatering när en profil kvalificerar sig för eller avslutar en målgrupp. |
| Exportfrekvens | **Direktuppspelning** | Uppdateringar skickas i realtid med Destination SDK ramverk för direktuppspelning. |

{style="table-layout:auto"}

## Anslut till målet {#connect}

Följ standardarbetsflödet för Experience Platform [anslut ett mål](../../ui/connect-destination.md).

>[!IMPORTANT]
> 
>Du måste ha behörigheterna **Visa mål** och **Hantera mål**.

### Autentisera till mål {#authenticate}

Ange följande fält när du ansluter till [!DNL Kevel]:

- **Bearer-token** - din [!DNL Kevel] API-nyckel.

![Autentiseringsalternativ för Kevel-mål](/help/destinations/assets/catalog/advertising/kevel-destination-authentication.png)

### Fyll i målinformation {#destination-details}

Efter autentiseringen konfigurerar du:

- **Namn** - En etikett som identifierar den här målinstansen.
- **Beskrivning** - Valfri text som beskriver målinstansen.
- **[!DNL Kevel]Nätverks-ID** - nätverksidentifieraren [!DNL Kevel].

![Målinformation för Kevel-mål](/help/destinations/assets/catalog/advertising/kevel-destination-details.png)

## Aktivera segment till den här destinationen {#activate}

Om du vill skicka målgrupper till [!DNL Kevel] följer du arbetsflödet i\
[Aktivera profiler och segment för att direktuppspela segmentets exportmål](/help/destinations/ui/activate-segment-streaming-destinations.md).

### Inaktivera målgrupper {#deactivate}

När en målgrupp inaktiveras eller tas bort från målet [!DNL Kevel] i Experience Platform slutar Experience Platform att skicka fler profilkvalificeringsuppdateringar för den målgruppen. Alla befintliga segment som skapats i [!DNL Kevel] är fortfarande tillgängliga och tas inte bort automatiskt.

Om [!DNL Kevel]-segmentet används för närvarande i en aktiv kampanj förhindrar [!DNL Kevel] borttagning för att undvika avbrott i direktleveransen. I så fall ger inaktiveringen i Experience Platform följande resultat:

- Experience Platform dataflödesstopp
- Segmentet [!DNL Kevel] finns fortfarande och kan vara kopplat till kampanjer tills det tas bort manuellt eller kampanjen uppdateras

Om du vill sluta målinrikta i [!DNL Kevel] måste du se till att segmentet tas bort från alla aktiva kampanjer i [!DNL Kevel]s kampanjhanteringssystem.

### Mappa attribut och identiteter {#map}

[!DNL Kevel] kräver:

- **Identitetsnamnutrymmen** - Upp till tre identitetsnamnutrymmen har mappats till [!DNL Kevel] identitetsplatser.
- **Segmentmedlemskap** - Ingen manuell mappning krävs. Experience Platform skickar automatiskt segmentmedlemsidentifierare och alias.

Under aktiveringen markerar du de identitetsnamnutrymmen som du har konfigurerat för [!DNL Kevel]. Varje identitet genererar ett eget uppdateringsanrop för UserDB.

## Exporterade data/Validera dataexport {#exported-data}

När en profil kvalificerar sig för eller avslutar en målgrupp skickar Experience Platform en direktuppspelningsuppdatering till [!DNL Kevel].

### Exempelnyttolast mottagen av [!DNL Kevel] UserDB

```json
PUT /udb/{networkId}/segments?userKey=ECID-12345
{
  "segments": [1723, 3344, 9988]
}
```

| Parameter | Beskrivning |
|-----------|-------------|
| **userKey** | Härledd från den mappade Adobe-identiteten. |
| **segment** | Uppsättningen med [!DNL Kevel] segment-ID:n som motsvarar de Adobe-målgrupper som profilen för närvarande används för. |

{style="table-layout:auto"}

### Exempel på Experience Platform-profil som används vid export {#sample-profile}

När målgrupper aktiveras till målet [!DNL Kevel] skickar Experience Platform profilfragment som innehåller både **segmentkvalifikationer** och **identiteter som mappats av kunden** till identitetsplatserna för [!DNL Kevel].

Nedan visas ett exempel på en exporterad profil som visar:

- Flera identitetsnamnutrymmen har mappats till `kevel_user_key1`, `kevel_user_key2` och `kevel_user_key3`
- Ett enda aktiverat segment i namnutrymmet `ups`

```json
{
  "segmentMembership": {
    "ups": {
      "9d161bbb-c785-474a-965b-7d7bc2adf879": {
        "status": "realized",
        "lastQualificationTime": "2025-12-10T21:43:38.541076Z"
      }
    }
  },
  "identityMap": {
    "kevel_user_key1": [
      {
        "id": "ECID-fN1zo"
      },
      {
        "id": "ECID-9Xr2p"
      }
    ],
    "kevel_user_key2": [
      {
        "id": "GAID-4oic4"
      }
    ],
    "kevel_user_key3": [
      {
        "id": "IDFA-nB5fU"
      }
    ]
  }
}
```

#### Så här tolkar [!DNL Kevel] den här profilen

Med målkonfigurationen [!DNL Kevel] genererar varje mappad identitet en distinkt UserDB-post, vilket innebär att [!DNL Kevel] får:

- En uppdatering för `ECID-fN1zo`
- En uppdatering för `ECID-9Xr2p`
- En uppdatering för `GAID-4oic4`
- En uppdatering för `IDFA-nB5fU`

Detta gör att samma person kan identifieras vid annonstillfället med hjälp av någon av deras tillgängliga identiteter, där varje identitet har en identisk uppsättning segmentmedlemskap.

## Dataanvändning och styrning {#data-usage-governance}

Alla [!DNL Adobe Experience Platform]-mål är kompatibla med dataanvändningsprinciper när data hanteras. Mer information om hur [!DNL Adobe Experience Platform] använder datastyrning finns i [Översikt över datastyrning](/help/data-governance/home.md).

## Ytterligare resurser {#additional-resources}

- [[!DNL Kevel] UserDB-referens](https://dev.kevel.com/reference/userdb)
- [[!DNL Kevel] Målgruppssegmentering](https://dev.kevel.com/docs/segment-targeting)
