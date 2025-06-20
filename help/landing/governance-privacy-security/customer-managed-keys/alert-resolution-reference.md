---
title: Referens för CMK-varningsmatchning
description: Identifiera, felsök och åtgärda vanliga varningar som utlöses av felkonfigurationer av kundhanterad nyckel (CMK) i Adobe Experience Platform. Använd den här vägledningen när du vill följa tydliga steg-för-steg-instruktioner och återställa säker nyckelåtkomst.
source-git-commit: 0d9cc046956dd380bb8816f0d8bf497bbad6140b
workflow-type: tm+mt
source-wordcount: '918'
ht-degree: 0%

---

# Referens för CMK-aviseringsupplösning

Använd den här vägledningen när du vill felsöka och lösa varningar som utlöses av felkonfigurerade CMK-inställningar (Customer Managed Key) i Adobe Experience Platform. Det hjälper systemadministratörer och implementeringsspecialister att identifiera orsaker och använda lösningar för att återställa säker åtkomst.

## Aviseringskategorier {#categories}

I följande avsnitt beskrivs vilka typer av varningar som kan utlösas av problem med kundhanterad nyckel (CMK) i Adobe Experience Platform:

- [Nyckelåtkomst inaktiverad](#key-access-disabled)
- [Nyckelåtkomstfel](#key-access-failure)
- [Aviseringsmeddelande](#alert-notification)

## Nyckelåtkomst inaktiverad {#key-access-disabled}

Den här varningen indikerar att Adobe Experience Platform inte kan komma åt den konfigurerade CMK-filen eftersom nyckeln inaktiveras eller inte kan nås av relaterade nyckelkonfigurationsproblem.

>[!IMPORTANT]
>
>I det här fallet behandlar Adobe CMK åtkomstfelet som en avsiktlig borttagning och rensar alla data som är kopplade till organisationen, baserat på din SLA.

### När det inträffar

Den här varningen utlöses när krypteringsnyckeln i Azure Key Vault är i inaktiverat tillstånd, borttagen eller felkonfigurerad på ett sätt som förhindrar åtkomst under plattformsåtgärder.

### Möjliga orsaker

Följande är vanliga orsaker till att den här varningen kan inträffa:

- Nyckeln inaktiverades manuellt.
- Nyckelåtgärder (wrapKey/unwrapKey) har tagits bort.
- Nyckelaktiveringsdatumet anges i framtiden.
- Nyckelns förfallodatum har redan inträffat.
- Nyckeln har tagits bort.
- MultiTenant App-behörigheterna har tagits bort eller ändrats.
- MultiTenant App har tagits bort.
- Egenskaperna för MultiTenant App har ändrats.
- Nyckelvalvet har tagits bort eller är inte längre tillgängligt.

### Upplösning

+++Om tangenten är inaktiverad

1. Navigera till det [Azure Key Vault](https://portal.azure.com/) som innehåller CMK.
2. Välj den tangent som är associerad med Adobe Experience Platform.
3. Kontrollera att nyckelns status är inställd på **Aktiverad**.
4. Om nyckeln är inaktiverad aktiverar du den via Azure-portalen eller CLI-kommandot `az keyvault key enable`.

>[!NOTE]
>
>Anpassa det här kommandot för din Azure-miljö.

+++

+++Om tangentåtgärder har ändrats

1. Lägg till behörigheterna `wrapKey` och `unwrapKey` till nyckeln igen.

>[!NOTE]
>
>Alla nyckelns inställningar, inklusive aktiverings- och förfallodatum, måste vara giltiga för att nyckeln ska fungera.

+++

+++Om aktiverings- eller förfallodatumet är felkonfigurerat

1. Ställ in aktiveringsdatumet till föregående eller nuvarande.
2. Ange ett framtida förfallodatum.

+++

+++Om tangenten har tagits bort

1. Kontrollera att mjuk borttagning är aktiverat i Azure Key Vault.
2. Navigera till Hantera borttagna nycklar i Azure-portalen eller CLI.
3. Välj den borttagna nyckeln i listan med objekt som har tagits bort på skärmen.
4. Klicka på **Återställ** om du vill återställa nyckeln.

+++

+++Om MultiTenant App-behörigheterna har tagits bort eller ändrats

1. Återställ rätt behörigheter för MultiTenant App.
2. Kontrollera att följande behörighet har beviljats: `Key Vault Crypto Service Encryption User`

+++

+++Om MultiTenant-appen har tagits bort

Det här är en stor förändring. Du måste kontakta Adobe för att återställa eller återskapa MultiTenant App.

+++

+++Om inställningarna för MultiTenant App ändrades

1. Återställ ändringarna av egenskaperna som är kopplade till MultiTenant App.

+++

+++Om nyckelvalvet har tagits bort

1. Bekräfta att mjuk borttagning är aktiverat i Azure.
2. Navigera till Hantera borttagna valv i portalen eller CLI.
3. Återställ det borttagna valvet inom kvarhållningsperioden (7-90 dagar).
4. Om rensningsskyddet är inaktiverat kan du fortfarande återställa valvet.

>[!NOTE]
>
>Om skyddet för mjuk borttagning eller tömning inte är korrekt konfigurerat kanske nyckeln eller valvet inte kan återställas.

+++

## Nyckelåtkomstfel {#key-access-failure}

Denna varning indikerar att Adobe Experience Platform inte kunde komma åt CMK på grund av nekad åtkomst på nätverksnivå eller konfigurationsbaserat.

>[!IMPORTANT]
>
>Detta behandlas som ett fel som kan återställas. Data har **inte** rensats under SLA i det här fallet.

### När det inträffar

Den här varningen utlöses vanligtvis när Key Vault-brandväggen inte är konfigurerad för att tillåta Adobe CMK-åtkomst eller när identitetsbaserad åtkomst misslyckas.

### Möjliga orsaker

- Brandväggen för nyckelvalv blockerar Adobe statiska IP (`20.88.123.53`)
- Nyckeln finns inte längre på den förväntade platsen
- Behörigheter för Adobe MultiTenant App saknas
- Nyckelvalvet har tagits bort eller felkonfigurerats
- Objekt-ID för MultiTenant App har ändrats

### Upplösning

+++Om nyckelvalvet eller nyckeln inte längre finns

1. Kontrollera att nyckelvalvet och krypteringsnyckeln fortfarande finns.
2. Om nyckeln togs bort följer du återställningsstegen för mjuk borttagning under &quot;Nyckelåtkomst inaktiverad&quot;.

+++

+++Om MultiTenant App-behörigheter saknas eller ändras

1. Bekräfta att Adobe MultiTenant App har följande behörigheter:
   - `get`, `wrapKey` och `unwrapKey` på nyckeln.
2. Kontrollera att objekt-ID:t för MultiTenant App är korrekt. Om den har ändrats kan du återanvända behörigheter.

+++

+++Om brandväggen blockerar Adobe

1. Granska brandväggsregler i Azure Key Vault.
2. Kontrollera att de tillåter åtkomst från Adobe statiska IP: `20.88.123.53`.

>[!NOTE]
>
>Även med rätt behörigheter förhindrar en blockerad IP-adress nyckelåtkomst.

+++

## Aviseringsmeddelande {#alert-notification}

Den här varningen fungerar som ett allmänt meddelande för CMK-konfiguration eller åtkomstavvikelser som inte matchar en känd feltyp.

>[!NOTE]
>
>Den här varningen kan bero på ett internt fel, en ny felkonfiguration eller ett oväntat tillstånd.

### När det inträffar

Den här varningen visas när Adobe CMK upptäcker ett okänt, ostöds eller nytt problem under åtkomst eller övervakning av nycklar.

### Möjliga orsaker

- Oväntade brandväggs-/nätverksförhållanden
- Nyckel- eller valändringar som inte täcks av fördefinierade larmtyper
- Interna nätverksstörningar i Adobe
- Felkonfiguration Adobe har inte setts tidigare

### Upplösning

+++Om orsaken är okänd eller tvetydig

1. Granska varningsmeddelandet för kontextdetaljer.
2. Kontrollera brandväggs-, valv- och nyckelinställningarna för de senaste ändringarna.
3. Om det inte finns någon tydlig orsak kontaktar du Adobe support för vägledning.
4. Övervaka loggar och systembeteende för att identifiera mönster.

+++

## Nästa steg

Mer information om hur aviseringar utlöses och hur du konfigurerar IP-tillåtelselistning för [!DNL Azure] CMK finns i guiden [Konfigurera aviseringar och IP-tillåtelselista för Azure CMK](./azure/alerts-and-ip-access.md).
