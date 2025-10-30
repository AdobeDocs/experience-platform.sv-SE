---
title: IP-adressen Tillåtslista för API för direktuppspelningsinmatning
description: Lär dig hur du säkrar åtkomsten till API:t för direktuppspelningsinmatning genom att endast tillåta angivna IP-adresser genom att tillåtslista. I den här guiden beskrivs hur du konfigurerar, aktiverar och hanterar IP-adressbaserade begränsningar för API-säkerhet.
hide: true
hidefromtoc: true
badge: beta
source-git-commit: f1d851afae5ad271e3c7d9d887f614058a262874
workflow-type: tm+mt
source-wordcount: '453'
ht-degree: 0%

---

# IP-adressen tillåtslista för API för direktuppspelningsinmatning

>[!AVAILABILITY]
>
>Stöd för IP-adresshämtning med API för direktuppspelning finns i betaversionen och din organisation har kanske inte åtkomst till det än. Funktionen och dokumentationen kan komma att ändras.

Du kan nu tillåtslista IP-adresser för API:t för direktuppspelningsinmatning. Använd den här funktionen om du vill skydda dina inmatningsslutpunkter genom att begränsa åtkomsten till endast de IP-adresser som du anger.

## Hur IP-adressen tillåtslista fungerar

Funktionen IP-tillåtelselistning fungerar enligt följande:

1. **Skicka in IP-adresser:** Du anger en lista över betrodda IP-adresser mappade till dina sandlådor.
2. **Konfiguration:** Adobe konfigurerar tillåtelselista på organisations- och sandlådenivå för din organisation.
3. **Tvingande:** Inkommande begäranden utvärderas mot det angivna tillåtelselista:
   * Om IP-adressen matchar din tillåtelselista behandlas begäran normalt.
   * Om IP-adressen inte finns på tillåtelselista blockeras begäran och ett HTTP 403-fel tas emot utan någon svarstext.

## Viktiga överväganden

* Funktionen för att tillåtslista IP-adresser gäller bara för [API:t för direktuppspelningsinmatning](https://developer.adobe.com/experience-platform-apis/references/streaming-ingestion/) (`dcs.adobedc.net`) och gäller **inte** för `server.adobedc.net` eller `edge.adobedc.net`.
* Nya sandlådor är öppna som standard tills tillåtelselistning är aktiverat.
* Om du tar bort en sandlåda från tillåtelselista öppnas den på nytt på Internet.
* Du måste underhålla den fullständiga listan över mappningar från sandbox till IP-adress på din sida och alltid skicka den fullständiga listan i det formulär som tillåtslista IP-adressen. Inkrementella uppdateringar stöds inte.

## Aktivera tillåtelselistning av IP-adress

Följ stegen nedan om du vill aktivera IP-adresstillåtslista för din organisation:

1. Hämta och fyll i formuläret [IP-adress som tillåtslista ](../images/assets/ip_allowlisting_aep.xlsx.zip).
2. Öppna en supportanmälan och arkivera ämnet som **AEP DCS &amp; Streaming Ingtake - IP Tillåtelselistning request**. Bifoga det ifyllda formuläret till den här biljetten.
3. När du har skickat in din anmälan vidarebefordrar Adobe kundtjänst din förfrågan till konstruktören.
4. Teknikerna möjliggör tillåtelselistning och bekräftar installationen.
5. Sedan validerar du åtkomsten och bekräftar med hjälp av supportbiljetten.

| Organisation | Namn på sandlåda | Tillåtna IP-adresser |
| --- | --- | --- |
| KOM | Prod | 203.0.113.42, 198.51.100.25, 192.0.2.10 |
| KOM | Dev | 203.0.113.43, 198.51.100.26, 192.0.2.11 |
| LUMA | Prod | 203.0.113.46, 198.51.100.29, 192.0.2.14 |

## Vanliga frågor och svar

Här nedan finns svar på vanliga frågor om IP-adresshämtningar som tillåtslista för API:t Streaming Ingestion.

### Vilka API:er omfattas?

Endast API-slutpunkterna `dcs.adobedc.net` för direktuppspelning.

## Vad händer om min förfrågan kommer från en IP-adress som inte finns med i listan?

Den blockeras med ett HTTP 403-fel.

### Skyddas nya sandlådor automatiskt?

Nej. De är öppna tills du anger IP-adressmappningar via det tillåtslista formuläret.

### Kan jag bara skicka uppdaterade IP-adresser när tillåtelselista ändras?

Nej. Du måste alltid skicka den fullständiga listan över mappningar av sandlådor och IP-adresser. Partiella (stegvisa) uppdateringar accepteras inte.