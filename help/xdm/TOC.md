---
audience: user
user-guide-title: Experience Data Model (XDM) - systemhjälp
breadcrumb-title: XDM-guide (Experience Data Model)
user-guide-description: Använd XDM-klasser (Experience Data Model) och schemafältgrupper för att standardisera upplevelsedata.
feature: Scheman
source-git-commit: bd312024a1a3fb6da840a38d6e9d19fcbd6eab5a
workflow-type: tm+mt
source-wordcount: '310'
ht-degree: 7%

---


# Experience Data Model (XDM) System {#xdm}

* [XDM - systemöversikt](home.md)
* Scheman {#schema}
   * [Grunderna för schemakomposition](schema/composition.md)
   * [Bästa tillvägagångssätt för datamodellering](schema/best-practices.md)
   * [Begränsningar för XDM-fälttyp](schema/field-constraints.md)
   * [Namnavstånd i XDM](./schema/namespaces.md)
   * [XDM-fältordlista](schema/field-dictionary.md)
   * Branschdatamodeller {#industries}
      * [Översikt](./schema/industries/overview.md)
      * [Detaljhandel](./schema/industries/retail.md)
      * [Finansiella tjänster](./schema/industries/financial.md)
      * [Resor och turism](./schema/industries/travel-hospitality.md)
* Klasser {#classes}
   * [Individuell XDM-profil](./classes/individual-profile.md)
   * [XDM ExperienceEvent](./classes/experienceevent.md)
   * [Segmentdefinition](./classes/segment-definition.md)
* Schemafältgrupper {#field-groups}
   * Profilfältgrupper {#profile}
      * [Demografiska detaljer](./field-groups/profile/demographic-details.md)
      * [IAB TCF 2.0-samtycke](./field-groups/profile/iab.md)
      * [IdentityMap](./field-groups/profile/identitymap.md)
      * [Förmånsinformation](./field-groups/profile/loyalty-details.md)
      * [Kontaktinformation, privat](./field-groups/profile/personal-contact-details.md)
      * [Innehåll och inställningar](./field-groups/profile/consents.md)
      * [Information om segmentmedlemskap](./field-groups/profile/segmentation.md)
      * [Kontaktinformation, arbete](./field-groups/profile/work-contact-details.md)
   * Händelsefältgrupper {#event}
      * [Information om kampanjmarknadsföring](./field-groups/event/campaign-marketing-details.md)
      * [Kanalinformation](./field-groups/event/channel-details.md)
      * [Handelsinformation](./field-groups/event/commerce-details.md)
      * [Information om slutanvändar-ID](./field-groups/event/enduserids.md)
      * [Miljöinformation](./field-groups/event/environment-details.md)
      * [IAB TCF 2.0-samtycke](./field-groups/event/iab.md)
      * [Webbinformation](./field-groups/event/web-details.md)
   * [Uppdateringar av fältgruppnamn](./field-groups/name-updates.md)
* Datatyper {#data-types}
   * [Program](./data-types/application.md)
   * [Beacon](./data-types/beacon.md)
   * [Webbläsarinformation](./data-types/browser-details.md)
   * [Handel](./data-types/commerce.md)
   * [Samtyckessträng](./data-types/consent-string.md)
   * [Innehåll och inställningar](./data-types/consents.md)
   * [Enhet](./data-types/device.md)
   * [E-postadress](./data-types/email-address.md)
   * [Miljö](./data-types/environment.md)
   * [Experience channel](./data-types/experience-channel.md)
   * [Allmänt fält för samtycke](./data-types/consent-field.md)
   * [Allmänt inställningsfält för marknadsföring](./data-types/marketing-field.md)
   * [Allmänt fält för marknadsföringsinställningar med prenumerationer](./data-types/marketing-field-subscriptions.md)
   * [Allmänt inställningsfält för personalisering](./data-types/personalization-field.md)
   * [Geo](./data-types/geo.md)
   * [Geo Circle](./data-types/geo-circle.md)
   * [Geo-koordinater](./data-types/geo-coordinates.md)
   * [Info om geo-interaktion](./data-types/geo-interaction-details.md)
   * [Geo Shape](./data-types/geo-shape.md)
   * [Identitet](./data-types/identity.md)
   * [Marknadsföring](./data-types/marketing.md)
   * [Mät](./data-types/measure.md)
   * [Order](./data-types/order.md)
   * [Betalningsartikel](./data-types/payment-item.md)
   * [Person](./data-types/person.md)
   * [Personnamn](./data-types/person-name.md)
   * [Telefonnummer](./data-types/phone-number.md)
   * [Montera kontext](./data-types/place-context.md)
   * [POI-information](./data-types/poi-details.md)
   * [POI-interaktion](./data-types/poi-interaction.md)
   * [Postadress](./data-types/postal-address.md)
   * [Produktlisteartikel](./data-types/product-list-item.md)
   * [Sökning](./data-types/search.md)
   * [Prenumeration](./data-types/subscription.md)
   * [Webbinformation](./data-types/web-information.md)
   * [Interaktion via webben](./data-types/web-interaction.md)
   * [Information om webbsidor](./data-types/webpage-details.md)
* [!UICONTROL Schemas] UI {#ui}
   * [Översikt](./ui/overview.md)
   * [Utforska XDM-resurser](./ui/explore.md)
   * Skapa och redigera resurser {#resources}
      * [Scheman](./ui/resources/schemas.md)
      * [Klasser](./ui/resources/classes.md)
      * [Fältgrupper](./ui/resources/field-groups.md)
      * [Datatyper](./ui/resources/data-types.md)
   * Definiera fält {#fields}
      * [Översikt](./ui/fields/overview.md)
      * [Obligatoriska fält](./ui/fields/required.md)
      * [Objektfält](./ui/fields/object.md)
      * [Matrisfält](./ui/fields/array.md)
      * [Uppräkningsfält](./ui/fields/enum.md)
      * [Identitetsfält](./ui/fields/identity.md)
      * [Relationsfält](./ui/fields/relationship.md)
   * [Generera XDM-exempeldata](./ui/sample.md)
   * [Exportera XDM-scheman](./ui/export.md)
* API för schemaregister {#api}
   * [Översikt](api/overview.md)
   * [Komma igång](api/getting-started.md)
   * [Scheman](api/schemas.md)
   * [Beteenden](api/behaviors.md)
   * [Klasser](api/classes.md)
   * [Fältgrupper för schema](api/field-groups.md)
   * [Datatyper](api/data-types.md)
   * [Beskrivningar](api/descriptors.md)
   * [Unions](api/unions.md)
   * [Exportera/importera](api/export-import.md)
   * [Exempeldata](api/sample-data.md)
   * [Granskningslogg](api/audit-log.md)
   * [Ad hoc-scheman](api/ad-hoc.md)
   * [Blandningar (borttagna)](api/mixins.md)
   * [Bilaga](api/appendix.md)
* Självstudiekurser {#tutorials}
   * [Skapa ett schema (UI)](tutorials/create-schema-ui.md)
   * [Skapa ett schema (API)](tutorials/create-schema-api.md)
   * [Definiera en relation mellan två scheman (UI)](tutorials/relationship-ui.md)
   * [Definiera en relation mellan två scheman (API)](tutorials/relationship-api.md)
   * [Skapa ett ad hoc-schema (API)](tutorials/ad-hoc.md)
* [Felsökningsguide](troubleshooting-guide.md)
* [API-referens](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/schema-registry.yaml)
* [Versionsinformation för plattform](https://www.adobe.com/go/platform-release-notes-en)