---
title: (Alfa) [!DNL LiveRamp SFTP] anslutning
description: Lär dig använda LiveRamp-kontakten för att ta in målgrupper från Adobe Real-time Customer Data Platform till LiveRamp Connect.
hidefromtoc: true
hide: true
exl-id: b8ce7ec2-7af9-4d26-b12f-d38c85ba488a
source-git-commit: 8c9d736c8d2c45909a2915f0f1d845a7ba4d876d
workflow-type: tm+mt
source-wordcount: '1743'
ht-degree: 0%

---

# (Alfa) [!DNL LiveRamp - SFTP] anslutning {#liveramp-destination}

Använd LiveRamp-anslutningen för att ta in målgrupper från Adobe Real-time Customer Data Platform till [!DNL LiveRamp Connect].

>[!IMPORTANT]
>
><p>Målanslutningen är för närvarande i alfavärdet och är endast tillgänglig för ett begränsat antal kunder. Funktionen och dokumentationen kan komma att ändras.</p>
&gt;<p>Slutversionen av den här målanslutningen kan kräva kundmigrering.</p>

## Användningsfall {#use-cases}

För att du bättre ska förstå hur och när du ska använda [!DNL LiveRamp SFTP] mål, här är ett exempel på användning som Adobe Experience Platform-kunder kan lösa genom att använda den här destinationen.

Som marknadsförare vill jag skicka målgrupper från Adobe Experience Platform till inbyggda identiteter i [!DNL LiveRamp Connect] så att jag kan inrikta mig på användare på [!DNL CTV] plattformar, använda [!DNL Ramp ID] identifierare.

## Förutsättningar {#prerequisites}

The [!DNL LiveRamp - SFTP] anslutningsexporterar filer med [LiveRamp&#39;s SFTP](https://docs.liveramp.com/connect/en/upload-a-file-via-liveramp-s-sftp.html) lagring.

Innan du skickar data från Experience Platform till [!DNL LiveRamp SFTP]behöver du [!DNL LiveRamp] autentiseringsuppgifter. Kontakta [!DNL LiveRamp] för att få dina uppgifter, om du inte redan har dem.

## Identiteter som stöds {#supported-identities}

LiveRamp SFTP stöder aktivering av identiteter som PII-baserade identifierare, kända identifierare och anpassade ID:n som beskrivs i [LiveRamp-dokumentation](https://docs.liveramp.com/connect/en/identity-and-identifier-terms-and-concepts.html#known-identifiers).

I [mappningssteg](#map) av aktiveringsarbetsflödet måste du definiera målmappningarna som anpassade attribut.

## Målgrupper som stöds {#supported-audiences}

I det här avsnittet beskrivs alla målgrupper som du kan exportera till det här målet.

Alla destinationer stöder aktivering av målgrupper som genererats via Experience Platform [Segmenteringstjänst](../../../segmentation/home.md).

Dessutom stöder denna destination även aktivering av de målgrupper som beskrivs i tabellen nedan.

| Målgruppstyp | Beskrivning |
---------|----------|
| Anpassade överföringar | Målgrupper [importerad](../../../segmentation/ui/overview.md#importing-an-audience) till Experience Platform från CSV-filer. |

{style="table-layout:auto"}

## Exportera typ och frekvens {#export-type-frequency}

Se tabellen nedan för information om exporttyp och frekvens för destinationen.

| Objekt | Typ | Anteckningar |
---------|----------|---------|
| Exporttyp | **[!UICONTROL Audience export]** | Du exporterar alla medlemmar i en målgrupp med identifierarna (namn, telefonnummer eller andra) som används i [!DNL LiveRamp SFTP] mål. |
| Exportfrekvens | **[!UICONTROL Daily batch]** | När profiler uppdateras i Experience Platform baserat på målgruppsutvärdering uppdateras profilerna (identiteterna) en gång om dagen nedströms målplattformen. Läs mer om [gruppfilsbaserade mål](/help/destinations/destination-types.md#file-based). |

{style="table-layout:auto"}

## Anslut till målet {#connect}

>[!IMPORTANT]
> 
>Om du vill ansluta till målet behöver du **[!UICONTROL Manage Destinations]** [åtkomstkontrollbehörighet](/help/access-control/home.md#permissions). Läs [åtkomstkontroll - översikt](/help/access-control/ui/overview.md) eller kontakta produktadministratören för att få de behörigheter som krävs.

Om du vill ansluta till det här målet följer du stegen som beskrivs i [självstudiekurs om destinationskonfiguration](../../ui/connect-destination.md). I arbetsflödet för att konfigurera mål fyller du i fälten som listas i de två avsnitten nedan.

### Autentisera till mål {#authenticate}

Om du vill autentisera mot målet fyller du i de obligatoriska fälten och väljer **[!UICONTROL Connect to destination]**.

**SFTP-autentisering med lösenord** {#sftp-password}

![Exempelbild som visar hur du autentiserar till målet med hjälp av SFTP med lösenord](../../assets/catalog/advertising/liveramp/liveramp-sftp-password.png)

* **[!UICONTROL Username]**: Användarnamnet för [!DNL LiveRamp SFTP] lagringsplats.
* **[!UICONTROL Password]**: Lösenordet för [!DNL LiveRamp SFTP] lagringsplats.
* **[!UICONTROL PGP/GPG encryption key]**: Du kan också bifoga den RSA-formaterade offentliga nyckeln för att lägga till kryptering till de exporterade filerna. Visa ett exempel på en korrekt formaterad krypteringsnyckel i bilden nedan. Om du anger en krypteringsnyckel måste du även ange en **[!UICONTROL Encryption subkey ID]** i [målinformation](#destination-details) -avsnitt.

  ![Bild som visar ett exempel på en korrekt formaterad PGP-nyckel i användargränssnittet](../../assets/catalog/advertising/liveramp/pgp-key.png)

**SFTP med autentisering med SSH-nyckel** {#sftp-ssh}

![Exempelbild som visar hur man autentiserar till målet med SSH-nyckeln](../../assets/catalog/advertising/liveramp/liveramp-sftp-ssh.png)

* **[!UICONTROL Username]**: Användarnamnet för [!DNL LiveRamp SFTP] lagringsplats.
* **[!UICONTROL SSH Key]**: Privat [!DNL SSH] som används för att logga in på [!DNL LiveRamp SFTP] lagringsplats. Den privata nyckeln måste vara formaterad som en [!DNL Base64]-encoded string och får inte vara lösenordsskyddad.

   * Koppla samman [!DNL SSH] tangent till [!DNL LiveRamp SFTP] server måste du skicka in en biljett via [!DNL LiveRamp]vår tekniska supportportal och ange din offentliga nyckel. Mer information finns i [LiveRamp-dokumentation](https://docs.liveramp.com/connect/en/upload-a-file-via-liveramp-s-sftp.html#upload-with-an-sftp-client).

* **[!UICONTROL PGP/GPG encryption key]**: Du kan också bifoga den RSA-formaterade offentliga nyckeln för att lägga till kryptering till de exporterade filerna. Om du anger en krypteringsnyckel måste du även ange en **[!UICONTROL Encryption subkey ID]** i [målinformation](#destination-details) -avsnitt. Visa ett exempel på en korrekt formaterad krypteringsnyckel i bilden nedan.

  ![Bild som visar ett exempel på en korrekt formaterad PGP-nyckel i användargränssnittet](../../assets/catalog/advertising/liveramp/pgp-key.png)

### Fyll i målinformation {#destination-details}

>[!CONTEXTUALHELP]
>id="platform_destinations_liveramp_subkey"
>title="ID för krypteringsundernyckel"
>abstract="Det undernyckel-ID som används för kryptering, baserat på den offentliga krypteringsnyckeln för LiveRamp. Det här fältet är obligatoriskt om du har angett en krypteringsnyckel i autentiseringssteget."
>additional-url="https://docs.liveramp.com/connect/en/encrypting-files-for-uploading.html#downloading-the-current-encryption-key" text="Lär dig hur du hämtar undernyckel-ID:t"

Om du vill konfigurera information för målet fyller du i de obligatoriska och valfria fälten nedan. En asterisk bredvid ett fält i användargränssnittet anger att fältet är obligatoriskt.

![Skärmbild av användargränssnittet för plattformen som visar hur du fyller i information för ditt mål](../../assets/catalog/advertising/liveramp/liveramp-connection-details.png)

* **[!UICONTROL Name]**: Ett namn som du känner igen det här målet med i framtiden.
* **[!UICONTROL Description]**: En beskrivning som hjälper dig att identifiera det här målet i framtiden.
* **[!UICONTROL Folder path]**: Sökvägen till [!DNL LiveRamp] `uploads` undermapp som ska vara värd för de exporterade filerna. The `uploads` läggs automatiskt till i mappsökvägen.
   * Om du till exempel vill exportera filerna till `uploads/my_export_folder`, skriva in `my_export_folder` i **[!UICONTROL Folder path]** fält.
* **[!UICONTROL Compression format]**: Välj den komprimeringstyp som Experience Platform ska använda för de exporterade filerna. Tillgängliga alternativ är **[!UICONTROL GZIP]** eller **[!UICONTROL None]**.
* **[!UICONTROL Encryption subkey ID]**: Den undernyckel som används för kryptering, baserat på [!DNL LiveRamp] offentlig krypteringsnyckel. Det här fältet är obligatoriskt om du har angett en krypteringsnyckel i [autentisering](#authenticate) steg. Se [!DNL LiveRamp] [krypteringsdokumentation](https://docs.liveramp.com/connect/en/encrypting-files-for-uploading.html#downloading-the-current-encryption-key) om du vill lära dig hur du hämtar undernyckel-ID:t.

### Aktivera aviseringar {#enable-alerts}

Du kan aktivera varningar för att få meddelanden om dataflödets status till ditt mål. Välj en avisering i listan om du vill prenumerera och få meddelanden om status för ditt dataflöde. Mer information om varningar finns i guiden [prenumerera på destinationsvarningar med hjälp av användargränssnittet](../../ui/alerts.md).

När du är klar med informationen för målanslutningen väljer du **[!UICONTROL Next]**.

## Aktivera målgrupper till det här målet {#activate}

>[!IMPORTANT]
> 
>Om du vill aktivera data måste du ha **[!UICONTROL Manage Destinations]**, **[!UICONTROL Activate Destinations]**, **[!UICONTROL View Profiles]** och **[!UICONTROL View Segments]** [behörigheter för åtkomstkontroll](/help/access-control/home.md#permissions). Läs [åtkomstkontroll - översikt](/help/access-control/ui/overview.md) eller kontakta produktadministratören för att få de behörigheter som krävs.

Läs [Aktivera målgruppsdata för att batchprofilera exportmål](/help/destinations/ui/activate-batch-profile-destinations.md) för instruktioner om hur du aktiverar målgrupper till det här målet.

### Schemaläggning {#scheduling}

I [!UICONTROL Scheduling] skapar du ett exportschema för varje målgrupp med inställningarna nedan.

>[!IMPORTANT]
>
>Alla målgrupper som aktiveras för detta mål måste konfigureras med exakt samma schema, vilket visas nedan.

* **[!UICONTROL File export options]**: [!UICONTROL Export full files]. [Inkrementell filexport](../../ui/activate-batch-profile-destinations.md#export-incremental-files) stöds för närvarande inte för [!DNL LiveRamp] mål.
* **[!UICONTROL Frequency]**: [!UICONTROL Daily]
* Ställ in exporttiden på **[!UICONTROL After segment evaluation]**. Schemalagd målgruppsexport och [export av filer på begäran](../../ui/export-file-now.md) stöds för närvarande inte för [!DNL LiveRamp] mål.
* **[!UICONTROL Date]**: Välj start- och sluttider för exporten.

![Skärmbild av användargränssnittet för plattformen som visar steg för målgruppsplanering.](../../assets/catalog/advertising/liveramp/liveramp-segment-scheduling.png)

Det går inte att konfigurera det exporterade filnamnet för tillfället. Alla filer som exporteras till [!DNL LiveRamp SFTP] destinationen namnges automatiskt baserat på följande mall:

`%ORGANIZATION_NAME%_%DESTINATION%_%DESTINATION_INSTANCE_ID%_%DATETIME%`

![Skärmbild för användargränssnittet för plattformen som visar den exporterade filnamnsmallen.](../../assets/catalog/advertising/liveramp/liveramp-file-name.png)

Exempel: namnet på en exporterad fil för en organisation med namnet [!DNL Luma] skulle kunna se ut ungefär så här:

```json
Luma_LiveRamp_52137231-4a99-442d-804c-39a09ddd005d_20230330_153857.csv
```

### Mappa attribut och identiteter {#map}

I **[!UICONTROL Mapping]** kan du välja vilka attribut och identiteter du vill exportera för dina profiler.

>[!IMPORTANT]
>
>Detta mål stöder aktivering av ett källidentitetsnamnutrymme per aktiveringsflöde. Om du behöver exportera flera ID-namnutrymmen, som `Email` och `Phone`måste du [skapa ett separat aktiveringsflöde](../../ui/activate-batch-profile-destinations.md) för varje identitet.

I **[!UICONTROL Mapping]** steg, **[!UICONTROL Target field]** mappningen definierar namnet på kolumnrubriken i den exporterade CSV-filen. Du kan ändra CSV-kolumnrubrikerna i den exporterade filen till valfritt eget namn genom att ange ett eget namn för **[!UICONTROL Target field]**.

1. I **[!UICONTROL Mapping]** steg, välja **[!UICONTROL Add new mapping]**. En ny mappningsrad visas på skärmen.

   ![Skärmbilden för användargränssnittet i Experience Platform visar skärmen Mapping.](../../assets/catalog/advertising/liveramp/liveramp-add-new-mapping.png)

2. I **[!UICONTROL Select source field]** väljer du **[!UICONTROL Select attributes]** och välj det XDM-attribut som du vill mappa, eller välj **[!UICONTROL Select identity namespace]** och välj en identitet som ska kopplas till ditt mål.

   ![Skärmbilden för användargränssnittet i Experience Platform visar skärmen för källmappning.](../../assets/catalog/advertising/liveramp/liveramp-source-mapping.png)

3. I **[!UICONTROL Select target field]** anger du det attributnamn som du vill mappa det markerade källfältet till. Attributnamnet som definieras här återspeglas i den exporterade CSV-filen som en kolumnrubrik.

   ![Skärmbilden för användargränssnittet i Experience Platform visar målmappningsskärmen.](../../assets/catalog/advertising/liveramp/liveramp-target-mapping.png)

   Du kan också ange attributnamnet genom att skriva det direkt i **[!UICONTROL Target field]**.

   ![Skärmbilden för användargränssnittet i Experience Platform visar målmappningsskärmen.](../../assets/catalog/advertising/liveramp/liveramp-target-field.png)

När du har lagt till alla mappningar du vill använda väljer du **[!UICONTROL Next]** och slutföra aktiveringsarbetsflödet.

## Exporterade data/Validera dataexport {#exported-data}

Dina data exporteras till [!DNL LiveRamp SFTP] lagringsplats som du konfigurerade som CSV-filer.

Vid export av filer till [!DNL LiveRamp SFTP] mål, Platform genererar en CSV-fil för varje [princip-ID för sammanslagning](../../../profile/merge-policies/overview.md).

Låt oss titta på följande målgrupper:

* Målgrupp A (sammanfogningsprincip 1)
* Målgrupp B (sammanfogningspolicy 2)
* Målgrupp C (sammanfogningspolicy 1)
* Målgrupp D (sammanfogningspolicy 1)

Plattformen exporterar två CSV-filer till [!DNL LiveRamp SFTP]:

* En CSV-fil som innehåller målgrupperna A, C och D.
* En CSV-fil som innehåller målgrupp B.

Exporterade CSV-filer innehåller profiler med de valda attributen och motsvarande målgruppsstatus, i separata kolumner, med attributnamnet, och `audience_namespace:audience_ID` par som kolumnrubriker, vilket visas i exemplet nedan:

`ATTRIBUTE_NAME, AUDIENCE_NAMESPACE_1:AUDIENCE_ID_1, AUDIENCE_NAMESPACE_2:AUDIENCE_ID_2,..., AUDIENCE_NAMESPACE_X:AUDIENCE_ID_X`

Profilerna som ingår i de exporterade filerna kan matcha ett av följande kvalificeringstillstånd för målgruppen:

* `Active`: Profilen är för närvarande kvalificerad för målgruppen.
* `Expired`: Profilen är inte längre kvalificerad för målgruppen, men har tidigare kvalificerats.
* `""`(tom sträng): Profilen har aldrig kvalificerats för målgruppen.

Till exempel en exporterad CSV-fil med en `email` attribut, två målgrupper som kommer från Experience Platform [Segmenteringstjänst](../../../segmentation/home.md)och en [importerad](../../../segmentation/ui/overview.md#importing-an-audience) extern publik, skulle kunna se ut så här:

```csv
email,ups:aa2e3d98-974b-4f8b-9507-59f65b6442df,ups:45d4e762-6e57-4f2f-a3e0-2d1893bcdd7f,CustomerAudienceUpload:7729e537-4e42-418e-be3b-dce5e47aaa1e
abc117@testemailabc.com,active,,
abc111@testemailabc.com,,,active
abc102@testemailabc.com,,,active
abc116@testemailabc.com,active,,
abc107@testemailabc.com,active,expired,active
abc101@testemailabc.com,active,active,
```

I exemplet ovan är `ups:aa2e3d98-974b-4f8b-9507-59f65b6442df` och `ups:45d4e762-6e57-4f2f-a3e0-2d1893bcdd7f` beskriver målgrupper som härrör från segmenteringstjänsten, medan `CustomerAudienceUpload:7729e537-4e42-418e-be3b-dce5e47aaa1e` beskriver en publik som importerats till Platform som [anpassad överföring](../../../segmentation/ui/overview.md#importing-an-audience).

Eftersom Platform genererar en CSV-fil för varje [princip-ID för sammanslagning](../../../profile/merge-policies/overview.md)genererar det också en separat dataflödeskörning för varje ID för sammanfogningsprincip.

Det innebär att **[!UICONTROL Identities activated]** och **[!UICONTROL Profiles received]** mätvärden i [dataflödeskörningar](../../../dataflows/ui/monitor-destinations.md#dataflow-runs-for-batch-destinations) sidan sammanställs för varje grupp av målgrupper som använder samma sammanfogningsprincip, i stället för att visas för varje målgrupp.

Som en följd av att dataflöden genereras för en grupp målgrupper som använder samma sammanfogningsprincip visas inte målgruppsnamnen i [kontrollpanel](../../../dataflows/ui/monitor-destinations.md#dataflow-runs-for-batch-destinations).

![Skärmbild för användargränssnittet i Experience Platform som visar aktiverade identiteter.](../../assets/catalog/advertising/liveramp/liveramp-metrics.png)

## Överför exporterade data till LiveRamp {#upload-to-liveramp}

När dina data har exporterats till [!DNL LiveRamp - SFTP] måste du överföra data till [!DNL LiveRamp] plattform.

Mer information om hur du överför filer från [!DNL LiveRamp - SFTP] lagring till [!DNL LiveRamp] kan du läsa följande dokumentation: [Att tänka på vid överföring av den första filen till en publik](https://docs.liveramp.com/connect/en/considerations-when-uploading-the-first-file-to-an-audience.html#considerations-when-uploading-the-first-file-to-an-audience).

## Dataanvändning och styrning {#data-usage-governance}

Alla [!DNL Adobe Experience Platform] destinationerna är kompatibla med dataanvändningsprinciper när data hanteras. Detaljerad information om hur [!DNL Adobe Experience Platform] använder datastyrning, läs [Datastyrning - översikt](/help/data-governance/home.md).

## Ytterligare resurser {#additional-resources}

Mer information om hur du konfigurerar din LiveRamp SFTP-lagring finns i [officiell dokumentation](https://docs.liveramp.com/connect/en/upload-a-file-via-liveramp-s-sftp.html).
