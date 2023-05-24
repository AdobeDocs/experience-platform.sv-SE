---
title: Stöd för SRI (Subresource Integrity)
description: Läs om hur underresursintegritet (SRI) stöds i Adobe Experience Platform.
exl-id: bd8bc3f7-9a85-44e2-ae07-f0664179b51c
source-git-commit: a8b0282004dd57096dfc63a9adb82ad70d37495d
workflow-type: tm+mt
source-wordcount: '601'
ht-degree: 0%

---

# Stöd för delresursintegritet (SRI)

>[!NOTE]
>
>Adobe Experience Platform Launch har omklassificerats som en serie datainsamlingstekniker i Adobe Experience Platform. Som ett resultat av detta har flera terminologiska förändringar införts i produktdokumentationen. Se följande [dokument](../../term-updates.md) för en konsoliderad hänvisning till terminologiska förändringar.

Det här dokumentet beskriver hur underresursintegritet (SRI) stöds i Adobe Experience Platform.

Moderna webbplatser skapas genom att man refererar till bilder, innehåll och skript från olika platser på webben. Med SRI kan en webbläsare verifiera att innehållet i en begärd fil inte har ändrats oväntat.

När de används är de kompatibla med varandra, men SRI skiljer sig från en CSP (Content Security Policy), som ser till att endast filer från betrodda källor tillåts på webbplatsen. SRI går ett steg längre genom att säkerställa att innehållet i dessa filer matchar dina förväntningar.

>[!NOTE]
>
>Mer detaljerad information om SRI finns i [MDN-webbdokument](https://developer.mozilla.org/en-US/docs/Web/Security/Subresource_Integrity).

SRI-valideringsprocessen kan sammanfattas enligt följande:

1. Du genererar en kryptografisk hash av resursen som du vill validera.
1. På webbplatsen placeras hashen i `integrity` -attributet för det HTML-element som läser in filen.
1. När webbläsaren ser `integrity` -attribut begär webbläsaren resursen och skapar oberoende av varandra en egen version av den kryptografiska hashen.
1. Webbläsaren jämför `integrity` hash med den som den genererade. Om de matchar är resursen tillåten. Om de inte matchar blockeras resursen.

## Begränsningar i tagghanteringssystem

Som ett TMS-system (tag management system) innehåller taggar i Adobe Experience Platform ett kompilerat JavaScript-bibliotek som du laddar in på sidorna med ett enda `<script>` element (inbäddningskod). Den dynamiska funktionaliteten i TMS uppnås genom att innehållet i skriptet byts ut dynamiskt utan att du behöver ändra något.

Men när skriptinnehållet ändras, så gör även den kryptografiska hashen för det innehållet. Därför är det enda sättet att få SRI att fungera med en TMS att uppdatera inbäddningskoden samtidigt som du publicerar en ny version. För många motverkar detta det primära syftet med att använda ett TMS från början.

Nästa bästa säkerhetsalternativ för taggar är att implementera en skyddsprofil för innehåll. Mer information finns i handboken på [CSP och taggar](./content-security-policy.md).

## Integrera SRI i byggdistributionen

Om du fortfarande vill använda SRI för dina biblioteksbyggen måste du använda självbetjäning. Om du använder värdtjänster som hanteras av Adobe finns det inget sätt att använda SRI utan att ha tid där det nya bygginnehållet inte matchar `integrity` -attributet för inbäddningskoden.

Automatiseringen av uppdateringsprocessen för inbäddningskoden varierar i komplexitet beroende på webbplatsens struktur, men de allmänna stegen kan sammanfattas enligt följande:

1. Hämta produktionsbiblioteket, antingen via SFTP eller genom att hämta arkivet från användargränssnittet.
1. Generera den kryptografiska hashen för huvudbygget.
1. Kontrollera att inbäddningskoden `integrity` attributet uppdateras till den nya hash-koden och att det refererade bygget uppdateras som en del av samma distribution.

>[!IMPORTANT]
>
>Detta tillvägagångssätt täcker endast huvudbygget. Den innehåller inte några av de mindre filer som kan finnas.

## Nästa steg

Det här dokumentet täcker begränsningarna med att använda SRI med taggar och de steg som krävs för att integrera det i din biblioteksbygge - trots dessa begränsningar. Om du inte redan har läst guiden rekommenderar vi att du läser den [CSP och taggar](./content-security-policy.md) för ett alternativt säkerhetsalternativ.
