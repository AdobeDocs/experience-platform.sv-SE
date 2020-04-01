---
keywords: Experience Platform;retail sales recipe;Data Science Workspace;popular topics
solution: Experience Platform
title: Skapa försäljningsschema och datauppsättning för återförsäljning
topic: Tutorial
translation-type: tm+mt
source-git-commit: 91c7b7e285a4745da20ea146f2334510ca11b994

---


# Skapa försäljningsschema och datauppsättning för återförsäljning

I den här självstudiekursen får du de krav och resurser som krävs för alla andra självstudiekurser i Adobe Experience Platform Data Science Workspace. När allt är klart är butiksförsäljningsschemat och datauppsättningarna tillgängliga för dig och medlemmar i din IMS-organisation på Experience Platform.

## Komma igång

Innan du startar den här självstudiekursen måste du ha följande krav:
- Tillgång till Adobe Experience Platform. Om du inte har tillgång till en IMS-organisation i Experience Platform, ska du tala med systemadministratören innan du fortsätter.
- Behörighet att göra Experience Platform API-anrop. Fyll i [Autentisera och få tillgång till API:er](../../tutorials/authentication.md) för Adobe Experience Platform för att få följande värden för att lyckas med den här självstudiekursen:
   - Behörighet: `{ACCESS_TOKEN}`
   - x-api-key: `{API_KEY}`
   - x-gw-ims-org-id: `{IMS_ORG}`
   - Klienthemlighet: `{CLIENT_SECRET}`
   - Klientcertifikat: `{PRIVATE_KEY}`
- Exempeldata och källfiler för [Retail Sales Recipe](../pre-built-recipes/retail-sales.md). Ladda ned de resurser som krävs för den här och andra självstudiekurser för datavetenskap från [Adobes offentliga Git-databas](https://github.com/adobe/experience-platform-dsw-reference/).
- [Python >= 2.7](https://www.python.org/downloads/) och följande Python-förpackningar:
   - [pip](https://pypi.org/project/pip/)
   - [PyYAML](https://pyyaml.org/)
   - [diktor](https://pypi.org/project/dictor/)
   - [JWT](https://pypi.org/project/jwt/)
- En arbetsförståelse för följande koncept som används i den här självstudiekursen:
   - [Experience Data Model (XDM)](../../xdm/home.md)
   - [Grunderna för schemakomposition](../../xdm/schema/field-dictionary.md)

## Skapa schema och datauppsättning för butiksförsäljning

Butiksförsäljningsschemat och datauppsättningarna skapas automatiskt med det angivna Bootstrap-skriptet. Följ stegen nedan i ordning:

### Konfigurera filer

1. I det självstudiekurserna för Experience Platform navigerar du till katalogen `bootstrap`och öppnar `config.yaml` med en lämplig textredigerare.
2. Ange följande värden under `Enterprise` avsnittet:

   ```yaml
   Enterprise:
       api_key: {API_KEY}
       org_id: {IMS_ORG}
       tech_acct: {technical_account_id}
       client_secret: {CLIENT_SECRET}
       priv_key_filename: {PRIVATE_KEY}
   ```

3. Redigera värdena som finns under `Platform` avsnittet, se exemplet nedan:

   ```yaml
   Platform:
       platform_gateway: https://platform.adobe.io
       ims_token: {ACCESS_TOKEN}
       ingest_data: "True"
       build_recipe_artifacts: "False"
       kernel_type: Python
   ```

   - `platform_gateway` : Bassökvägen för API-anrop. Ändra inte det här värdet.
   - `ims_token` : Din `{ACCESS_TOKEN}` far hit.
   - `ingest_data` : I den här självstudiekursen anger du det här värdet som `"True"` för att skapa försäljningsscheman och datauppsättningar för detaljhandeln. Värdet `"False"` skapar bara scheman.
   - `build_recipe_artifacts` : I den här självstudiekursen ställer du in det här värdet så `"False"` att skriptet inte kan generera en Recept-artefakt.
   - `kernel_type` : Körningstypen för Recept-artefakten. Låt det här värdet vara `Python` om `build_recipe_artifacts` är inställt som `"False"`, annars anger du rätt körningstyp.

4. Under `Titles` avsnittet anger du följande information för exempeldata för försäljning (butik), sparar och stänger filen när redigeringarna är klara. Exempel som visas nedan:

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

1. Öppna terminalprogrammet och navigera till resurskatalogen för självstudiekursen för Experience Platform.
2. Ange `bootstrap` katalogen som aktuell arbetssökväg och kör `bootstrap.py` python-skriptet genom att ange följande kommando:

   ```bash
   python bootstrap.py
   ```

   > [!NOTE] Skriptet kan ta flera minuter att slutföra.

## Nästa steg

När bootstrap-skriptet har slutförts kan indata- och utdatamodeller och datamängder för butik visas på Experience Platform. Mer information finns i självstudiekursen [om schemadata för](./preview-schema-data.md)förhandsgranskning.

Du har också lyckats importera exempeldata för butiksförsäljning till Experience Platform med det tillhandahållna bootstrap-skriptet.

Så här fortsätter du att arbeta med inkapslade data:
- [Analysera dina data med Jupyter-anteckningsböcker](../jupyterlab/analyze-your-data.md)
   - Använd Jupyter-anteckningsböcker i Data Science Workspace för att få tillgång till, utforska, visualisera och förstå dina data.
- [Paketera källfiler i en mottagare](./package-source-files-recipe.md)
   - Följ den här självstudiekursen för att lära dig hur du kan ta med din egen modell till arbetsytan för datavetenskap genom att paketera källfiler i en importerbar Recipe-fil.