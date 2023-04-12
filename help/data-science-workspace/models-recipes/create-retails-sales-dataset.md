---
keywords: Experience Platform;butiksrecept;Data Science Workspace;populära ämnen;recept
solution: Experience Platform
title: Skapa schema och datauppsättning för butiksförsäljning
type: Tutorial
description: I den här självstudiekursen får du de krav och resurser som krävs för alla andra självstudiekurser i Adobe Experience Platform Data Science Workspace. När du är klar är schema och datauppsättningar för detaljhandelsförsäljning tillgängliga för dig och medlemmar i din organisation på Experience Platform.
exl-id: 1b868c8c-7c92-4f99-8486-54fd7aa1af48
source-git-commit: 81f48de908b274d836f551bec5693de13c5edaf1
workflow-type: tm+mt
source-wordcount: '551'
ht-degree: 0%

---


# Skapa försäljningsschema och datauppsättning för återförsäljning

I den här självstudiekursen får du de krav och resurser som krävs för alla andra [!DNL Adobe Experience Platform] [!DNL Data Science Workspace] självstudiekurser. När du är klar är schema och datauppsättningar för detaljhandelsförsäljning tillgängliga för dig och medlemmar i din organisation den [!DNL Experience Platform].

## Komma igång

Innan du startar den här självstudiekursen måste du ha följande krav:
- Åtkomst till [!DNL Adobe Experience Platform]. Om du inte har tillgång till en organisation i [!DNL Experience Platform]bör du kontakta systemadministratören innan du fortsätter.
- Behörighet att skapa [!DNL Experience Platform] API-anrop. Slutför [Autentisera och få åtkomst till Adobe Experience Platform API:er](https://www.adobe.com/go/platform-api-authentication-en) självstudiekurs för att få tillgång till följande värden för att slutföra den här självstudiekursen:
   - Behörighet: `{ACCESS_TOKEN}`
   - x-api-key: `{API_KEY}`
   - x-gw-ims-org-id: `{ORG_ID}`
   - Klienthemlighet: `{CLIENT_SECRET}`
   - Klientcertifikat: `{PRIVATE_KEY}`
- Exempeldata och källfiler för [Butiksförs.mottagare](../pre-built-recipes/retail-sales.md). Ladda ned resurser som krävs för detta och andra [!DNL Data Science Workspace] självstudiekurser från [Adobe offentlig Git-databas](https://github.com/adobe/experience-platform-dsw-reference/).
- [Python >= 2.7](https://www.python.org/downloads/) och följande [!DNL Python] paket:
   - [pip](https://pypi.org/project/pip/)
   - [PyYAML](https://pyyaml.org/)
   - [diktor](https://pypi.org/project/dictor/)
   - [JWT](https://pypi.org/project/jwt/)
- En arbetsförståelse för följande koncept som används i den här självstudiekursen:
   - [[!DNL Experience Data Model (XDM)]](../../xdm/home.md)
   - [Grunderna för schemakomposition](../../xdm/schema/field-dictionary.md)

## Skapa schema och datauppsättning för butiksförsäljning

Butiksförsäljningsschemat och datauppsättningarna skapas automatiskt med det angivna Bootstrap-skriptet. Följ stegen nedan i ordning:

### Konfigurera filer

1. Innanför [!DNL Experience Platform] självstudiekursens resurspaket, navigera till katalogen `bootstrap`och öppna `config.yaml` med en lämplig textredigerare.
2. Under `Enterprise` anger du följande värden:

   ```yaml
   Enterprise:
       api_key: {API_KEY}
       org_id: {ORG_ID}
       tech_acct: {technical_account_id}
       client_secret: {CLIENT_SECRET}
       priv_key_filename: {PRIVATE_KEY}
   ```

3. Redigera värdena som finns under `Platform` -avsnittet, exempel som visas nedan:

   ```yaml
   Platform:
       platform_gateway: https://platform.adobe.io
       ims_token: {ACCESS_TOKEN}
       ingest_data: "True"
       build_recipe_artifacts: "False"
       kernel_type: Python
   ```

   - `platform_gateway`: Bassökvägen för API-anrop. Ändra inte det här värdet.
   - `ims_token`: Dina `{ACCESS_TOKEN}` går hit.
   - `ingest_data`: I den här självstudiekursen anger du det här värdet som `"True"` för att skapa försäljningsscheman och datauppsättningar för detaljhandeln. Värdet för `"False"` skapar endast scheman.
   - `build_recipe_artifacts`: I den här självstudiekursen anger du det här värdet som `"False"` för att förhindra att skriptet genererar en Recept-artefakt.
   - `kernel_type`: Körningstypen för Recept-artefakten. Lämna det här värdet som `Python` if `build_recipe_artifacts` anges som `"False"`, annars anger du rätt körningstyp.

4. Under `Titles` ska du ange följande information för exempeldata för butiksförsäljning, spara och stänga filen när redigeringarna är på plats. Exempel som visas nedan:

   ```yaml
   Titles:
       input_class_title: retail_sales_input_class
       input_mixin_title: retail_sales_input_mixin
       input_mixin_definition_title: retail_sales_input_mixin_definition
       input_schema_title: retail_sales_input_schema
       input_dataset_title: retail_sales_input_dataset
       file_replace_tenant_id: DSWRetailSalesForXDM0.9.9.9.json
       file_with_tenant_id: DSWRetailSales_with_tenant_id.json
       is_output_schema_different: "True"
       output_mixin_title: retail_sales_output_mixin
       output_mixin_definition_title: retail_sales_output_mixin_definition
       output_schema_title: retail_sales_output_title
       output_dataset_title: retail_sales_output_dataset
   ```

### Kör bootstrap-skriptet

1. Öppna terminalprogrammet och gå till [!DNL Experience Platform] självstudiekursens resurskatalog.
2. Ange `bootstrap` som aktuell arbetsbana och kör `bootstrap.py` [!DNL Python] genom att ange följande kommando:

   ```bash
   python bootstrap.py
   ```

   >[!NOTE]
   >
   >Skriptet kan ta flera minuter att slutföra.

## Nästa steg

När bootstrap-skriptet har slutförts kan indata- och utdatamodeller och datamängder för butik visas på [!DNL Experience Platform]. Se [självstudiekurs om att förhandsgranska schemadata](./preview-schema-data.md)
för mer information.

Du har även importerat exempeldata för butiksförsäljning till [!DNL Experience Platform] med det medföljande bootstrap-skriptet.

Så här fortsätter du att arbeta med inkapslade data:
- [Analysera dina data med Jupyter Notebooks](../jupyterlab/analyze-your-data.md)
   - Använd Jupyter Notebooks i Data Science Workspace för att få tillgång till, utforska, visualisera och förstå era data.
- [Paketera källfiler i en mottagare](./package-source-files-recipe.md)
   - Följ den här självstudiekursen för att lära dig hur du kan använda din egen modell i [!DNL Data Science Workspace] genom att paketera källfiler i en importerbar Recipe-fil.
