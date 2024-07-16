---
title: Stöd för SRI (Subresource Integrity)
description: Läs om hur underresursintegritet (SRI) stöds i Adobe Experience Platform.
exl-id: bd8bc3f7-9a85-44e2-ae07-f0664179b51c
source-git-commit: a8b0282004dd57096dfc63a9adb82ad70d37495d
workflow-type: tm+mt
source-wordcount: '594'
ht-degree: 0%

---

# Stöd för delresursintegritet (SRI)

>[!NOTE]
>
>Adobe Experience Platform Launch har omklassificerats som en serie datainsamlingstekniker i Adobe Experience Platform. Som ett resultat av detta har flera terminologiska förändringar införts i produktdokumentationen. I följande [dokument](../../term-updates.md) finns en konsoliderad referens till de ändrade terminologin.

Det här dokumentet beskriver hur underresursintegritet (SRI) stöds i Adobe Experience Platform.

Moderna webbplatser skapas genom att man refererar till bilder, innehåll och skript från olika platser på webben. Med SRI kan en webbläsare verifiera att innehållet i en begärd fil inte har ändrats oväntat.

När de används är de kompatibla med varandra, men SRI skiljer sig från en CSP (Content Security Policy), som ser till att endast filer från betrodda källor tillåts på webbplatsen. SRI går ett steg längre genom att säkerställa att innehållet i dessa filer matchar dina förväntningar.

>[!NOTE]
>
>Mer detaljerad information om SRI finns i [MDN-webbdokumenten](https://developer.mozilla.org/en-US/docs/Web/Security/Subresource_Integrity).

SRI-valideringsprocessen kan sammanfattas på följande sätt:

1. Du genererar en kryptografisk hash av resursen som du vill validera.
1. På webbplatsen placeras hashen i attributet `integrity` för det HTML-element som läser in filen.
1. När webbläsaren ser attributet `integrity` begär webbläsaren resursen och skapar en egen version av den kryptografiska hashen oberoende av varandra.
1. Webbläsaren jämför hashen `integrity` med den som den genererade. Om de matchar är resursen tillåten. Om de inte matchar blockeras resursen.

## Begränsningar i tagghanteringssystem

Som ett tagghanteringssystem (TMS) innehåller taggar i Adobe Experience Platform en kompilerad JavaScript-biblioteksversion som du läser in på dina sidor med ett enda `<script>`-element (inbäddningskod). Den dynamiska funktionaliteten i TMS uppnås genom att innehållet i skriptet byts ut dynamiskt utan att du behöver ändra något.

Men när skriptinnehållet ändras, så gör även den kryptografiska hashen för det innehållet. Därför är det enda sättet att få SRI att fungera med en TMS att uppdatera inbäddningskoden samtidigt som du publicerar en ny version. För många motverkar detta det primära syftet med att använda ett TMS från början.

Nästa bästa säkerhetsalternativ för taggar är att implementera en skyddsprofil för innehåll. Mer information finns i handboken om [CSP och taggar](./content-security-policy.md).

## Integrera SRI i byggdistributionen

Om du fortfarande vill använda SRI för dina biblioteksbyggen måste du använda självbetjäning. Om du använder värdtjänster som hanteras med Adobe finns det inget sätt att använda SRI utan att ha en viss tid där det nya bygginnehållet inte matchar attributet `integrity` för inbäddningskoden.

Automatiseringen av uppdateringsprocessen för inbäddningskoden varierar i komplexitet beroende på webbplatsens struktur, men de allmänna stegen kan sammanfattas enligt följande:

1. Hämta produktionsbiblioteket, antingen via SFTP-leverans eller genom att hämta arkivet från användargränssnittet.
1. Generera den kryptografiska hashen för huvudbygget.
1. Kontrollera att inbäddningskodens `integrity`-attribut uppdateras till den nya hash-koden och att den refererade versionen uppdateras som en del av samma distribution.

>[!IMPORTANT]
>
>Detta tillvägagångssätt täcker endast huvudbygget. Den innehåller inte några av de mindre filer som kan finnas.

## Nästa steg

Det här dokumentet täcker begränsningarna med att använda SRI med taggar och de steg som krävs för att integrera det i din biblioteksbygge - trots dessa begränsningar. Om du inte redan har det rekommenderar vi att du läser guiden för [CSP och taggar](./content-security-policy.md) för ett alternativt säkerhetsalternativ.
