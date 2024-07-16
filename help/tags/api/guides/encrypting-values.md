---
title: Krypteringsvärden
description: Lär dig hur du krypterar känsliga värden när du använder Reactor API.
exl-id: d89e7f43-3bdb-40a5-a302-bad6fd1f4596
source-git-commit: a8b0282004dd57096dfc63a9adb82ad70d37495d
workflow-type: tm+mt
source-wordcount: '366'
ht-degree: 0%

---

# Krypteringsvärden

När du använder taggar i Adobe Experience Platform kräver vissa arbetsflöden att du anger känsliga värden (till exempel en privat nyckel när du levererar bibliotek till miljöer via värdar). Dessa fullmakters känsliga karaktär gör det nödvändigt
säker överföring och lagring.

I det här dokumentet beskrivs hur du krypterar känsliga värden med [GnuPG-kryptering](https://www.gnupg.org/gph/en/manual/x110.html) (kallas även GPG) så att bara taggsystemet kan läsa dem.

## Hämta den offentliga GPG-nyckeln och kontrollsumman

Efter [nedladdning](https://gnupg.org/download/) och installation av den senaste versionen av GPG måste du hämta den offentliga GPG-nyckeln för taggproduktionsmiljön:

* [GPG-nyckel](https://github.com/adobe/reactor-developer-docs/blob/master/files/launch%40adobe.com_pub.gpg)
* [Kontrollsumma](https://github.com/adobe/reactor-developer-docs/blob/master/files/launch%40adobe.com_pub.gpg.sum)

## Importera nyckeln till nyckelkedjan

När du har sparat nyckeln på datorn är nästa steg att lägga till den i GPG-nyckelkedjan.

**Syntax**

```shell
gpg --import {KEY_NAME}
```

| Parameter | Beskrivning |
| --- | --- |
| `{KEY_NAME}` | Namnet på filen med den offentliga nyckeln. |

{style="table-layout:auto"}

**Exempel**

```shell
gpg --import launch@adobe.com_pub.gpg
```

## Kryptera värden

När du har lagt till nyckeln i nyckelkedjan kan du börja kryptera värden med flaggan `--encrypt`. Följande skript visar hur det här kommandot fungerar:

```shell
echo -n 'Example value' | gpg --armor --encrypt -r "Tags Data Encryption <launch@adobe.com>"
```

Det här kommandot kan delas upp enligt följande:

* Indata har angetts för kommandot `gpg`.
* `--armor` skapar ASCII-utdata i stället för binära. Detta gör det enklare att överföra värdet via JSON.
* `--encrypt` instruerar GPG att kryptera data.
* `-r` anger mottagaren för data. Endast mottagaren (den som har den privata nyckeln som motsvarar den offentliga nyckeln) får dekryptera data. Mottagarnamnet för den önskade nyckeln kan hittas genom att undersöka utdata för `gpg --list-keys`.

Ovanstående kommando använder den offentliga nyckeln för `Tags Data Encryption <launch@adobe.com>` för att kryptera värdet `Example value` i ASCII-upphöjt format.

Kommandots utdata skulle likna följande:

```shell
-----BEGIN PGP MESSAGE-----

hQIMAxJHCI6fydT/ARAAwQ0Y0k7eSAbd0T9seoaWX75G70O2gxAF20KY5FWiZ9/m
/RkgJwhJusZyEdazC/CmAdfXi9bsVxQT0i06ErUxXfQF0VtweRlcyRBsxzLz6Hr+
BpYGnq+cCCzGAT73Gg1CM4UWmaPKLLyWKGkXtDBAqVBRAIQT/8JhnkbyWIohHkWV
I/Uf7NrPXuaSmrqZ1SZQgwjIM3qNMR02qtqg59dncKoCQBji8Oeb8lqRLskRT0Jq
gVgbJYwSe2n6KpJkELJ6QtF9lCRl1+yU4mvM4jBHgkM1+vb1WmbFRIR40dDpg85N
0J9hVj4bg//eLRDfAdEC9kgq9Atph0WqJ5EpehdS7yVO9lO8mpbpqZ4BCGjTi/VS
isEPr6eZ2mxRbk8f9Z4csRZnkErY8ep5+cqC5CZVdmguWvC9PKzXqEsPFd0PSYk3
Qp3UIW2/JMf16E5CKmntm+gKdl6kggZOOvNQuyJYa9yNbzySPerHXsknTOxV+QP/
WXwrAL52g5+gpMib7Ve/KBz5/OViDhDqkmHzlGad73W74d+CYjf0AnuXuWRRlUMT
s8ORw1eplInldhXk2mgkGPZS/gWDs3zpKUu4GSO9AaeWldynLG/Bgh78XhumQ58h
ekGD+p3PyyvxjfS5G/wf9HQZ085+mnjpKFa7fuFBQPbg4WpBadhWrhobthC+hN3S
SAE9yWU11Y3xpoxqg4y7iYZ6rnX+qP2oUNYxC2/hdhsFbbZtUh4s51qaoLbe0iWB
OUoIPf4KxTaboHZOEy32ZBng5heVrn4i9w==
=jrfE
-----END PGP MESSAGE-----
```

Dessa utdata kan endast dekrypteras av system som har den privata nyckeln som
motsvarar den offentliga nyckeln `Tags Data Encryption <launch@adobe.com>`.

Detta utdatavärde är det värde som ska anges i en när data skickas till Reactor API. Systemet lagrar krypterade utdata och dekrypterar dem tillfälligt efter behov. Systemet dekrypterar till exempel värdautentiseringsuppgifterna tillräckligt länge för att initiera en anslutning till servern och tar sedan omedelbart bort alla spår av det dekrypterade värdet.

>[!NOTE]
>
>Formatet på det pökta, krypterade värdet är viktigt. Se till att radbrytningarna flödar korrekt i värdet som anges i begäran.
