---
keywords: Experience Platform;recept;data Science Workspace;populära ämnen;recept
solution: Experience Platform
title: Skapa schema och datauppsättning för butiksförsäljning
type: Tutorial
description: I den här självstudiekursen får du de förutsättningar och resurser som krävs för alla andra självstudiekurser i Adobe Experience Platform Data Science Workspace. När du är klar kommer schema och datauppsättningar för detaljhandel att vara tillgängliga för dig och medlemmar i din organisation på Experience Platform.
exl-id: 1b868c8c-7c92-4f99-8486-54fd7aa1af48
source-git-commit: 5d98dc0cbfaf3d17c909464311a33a03ea77f237
workflow-type: tm+mt
source-wordcount: '557'
ht-degree: 0%

---


# Skapa försäljningsschema och datauppsättning för återförsäljning

>[!NOTE]
>
>Data Science Workspace finns inte längre att köpa.
>
>Denna dokumentation är avsedd för befintliga kunder med tidigare tillstånd till Data Science Workspace.

I den här självstudiekursen får du de krav och resurser som krävs för alla andra [!DNL Adobe Experience Platform] [!DNL Data Science Workspace] självstudiekurser. När du är klar är schema och datauppsättningar för detaljhandelsförsäljning tillgängliga för dig och medlemmar i din organisation den [!DNL Experience Platform].

## Komma igång

Innan du startar den här självstudiekursen måste du ha följande krav:
- Åtkomst till [!DNL Adobe Experience Platform]. Om du inte har åtkomst till en organisation i [!DNL Experience Platform], ska du tala med systemadministratören innan du fortsätter.
- Behörighet att göra [!DNL Experience Platform] API-anrop. Slutför självstudiekursen [Autentisera och få tillgång till Adobe Experience Platform API:er](https://www.adobe.com/go/platform-api-authentication-en) för att få tillgång till följande värden för att slutföra den här självstudiekursen:
   - Behörighet: `{ACCESS_TOKEN}`
   - x-api-key: `{API_KEY}`
   - x-gw-ims-org-id: `{ORG_ID}`
   - Klienthemlighet: `{CLIENT_SECRET}`
   - Klientcertifikat: `{PRIVATE_KEY}`
- Exempeldata och källfiler för [Retail Sales Recipe](../pre-built-recipes/retail-sales.md). Hämta resurserna som krävs för den här och andra [!DNL Data Science Workspace] självstudiekurser från den offentliga Git-databasen [Adobe](https://github.com/adobe/experience-platform-dsw-reference/).
- [Python >= 2.7](https://www.python.org/downloads/) och följande [!DNL Python]-paket:
   - [pip](https://pypi.org/project/pip/)
   - [PyYAML](https://pyyaml.org/)
   - [dictor](https://pypi.org/project/dictor/)
   - [JWT](https://pypi.org/project/jwt/)
- En arbetsförståelse för följande koncept som används i den här självstudiekursen:
   - [[!DNL Experience Data Model (XDM)]](../../xdm/home.md)
   - [Grunderna för schemakomposition](../../xdm/schema/field-dictionary.md)

## Skapa schema och datauppsättning för butiksförsäljning

Butiksförsäljningsschemat och datauppsättningarna skapas automatiskt med det angivna Bootstrap-skriptet. Följ stegen nedan i ordning:

### Konfigurera filer

1. I resurspaketet [!DNL Experience Platform] för självstudier navigerar du till katalogen `bootstrap` och öppnar `config.yaml` med en lämplig textredigerare.
2. Ange följande värden under avsnittet `Enterprise`:

   ```yaml
   Enterprise:
       api_key: {API_KEY}
       org_id: {ORG_ID}
       tech_acct: {technical_account_id}
       client_secret: {CLIENT_SECRET}
       priv_key_filename: {PRIVATE_KEY}
   ```

3. Redigera värdena som finns under avsnittet `Platform`, exempel som visas nedan:

   ```yaml
   Platform:
       platform_gateway: https://platform.adobe.io
       ims_token: {ACCESS_TOKEN}
       ingest_data: "True"
       build_recipe_artifacts: "False"
       kernel_type: Python
   ```

   - `platform_gateway`: Bassökvägen för API-anrop. Ändra inte det här värdet.
   - `ims_token`: Din `{ACCESS_TOKEN}` placeras här.
   - `ingest_data`: I den här självstudiekursen anger du det här värdet som `"True"` för att skapa försäljningsscheman och datauppsättningar för detaljhandeln. Värdet `"False"` skapar bara scheman.
   - `build_recipe_artifacts`: I den här självstudiekursen anger du det här värdet som `"False"` för att förhindra att skriptet genererar en mottagarartefakt.
   - `kernel_type`: Körningstypen för mottagarartefakten. Låt det här värdet vara `Python` om `build_recipe_artifacts` har angetts som `"False"`, annars anger du rätt körningstyp.

4. Under avsnittet `Titles` anger du följande information korrekt för exempeldata för försäljning (butik). Spara och stäng filen när redigeringarna är på plats. Exempel som visas nedan:

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

1. Öppna terminalprogrammet och gå till resurskatalogen för självstudiekursen [!DNL Experience Platform].
2. Ange katalogen `bootstrap` som aktuell arbetssökväg och kör skriptet `bootstrap.py` [!DNL Python] genom att ange följande kommando:

   ```bash
   python bootstrap.py
   ```

   >[!NOTE]
   >
   >Skriptet kan ta flera minuter att slutföra.

## Nästa steg

När bootstrap-skriptet har slutförts kan indata- och utdatamodeller och datamängder för butik visas på [!DNL Experience Platform]. Se självstudiekursen [för förhandsgranskning av schemadata](./preview-schema-data.md)
för mer information.

Du har även inläst exempeldata för butiksförsäljning till [!DNL Experience Platform] med det angivna bootstrap-skriptet.

Så här fortsätter du att arbeta med inkapslade data:
- [Analysera dina data med Jupyter Notebooks](../jupyterlab/analyze-your-data.md)
   - Använd Jupyter Notebooks i Data Science Workspace för att få tillgång till, utforska, visualisera och förstå era data.
- [Paketera källfiler i en mottagare](./package-source-files-recipe.md)
   - Följ den här självstudiekursen för att lära dig hur du kan ta med din egen modell till [!DNL Data Science Workspace] genom att paketera källfiler i en importerbar Recipe-fil.
