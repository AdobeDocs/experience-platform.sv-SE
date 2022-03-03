---
title: Policy Class
description: This document provides an overview of the Policy class in Experience Data Model (XDM).
source-git-commit: c0437b8f9d93c46dbec991a33a893a5b9e0cdf2c
workflow-type: tm+mt
source-wordcount: '220'
ht-degree: 0%

---

# [!UICONTROL Policy]

[!UICONTROL Policy]

![](../images/classes/policy.png)

| Property | Data type | Beskrivning |
| --- | --- | --- |
| `assignedBeneficiary` | [[!UICONTROL Person]](../data-types/person.md) | Captures the beneficiary (or beneficiaries) assigned to the policy. |
| `benefitAmount` | [[!UICONTROL Currency]](../data-types/currency.md) | The amount to be paid as per the policy terms. |
| `location` | [[!UICONTROL Postal address]](../data-types/postal-address.md) | The location in which the insurance policy is issued. |
| `owner` | [!UICONTROL Object] | Captures the policy holder&#39;s profile information. |
| `owner.faxPhone` | [[!UICONTROL Phone number]](../data-types/phone-number.md) | The owner&#39;s fax phone number. |
| `owner.homeAddress` | [[!UICONTROL Postal address]](../data-types/postal-address.md) | The owner&#39;s home address. |
| `owner.homePhone` | [[!UICONTROL Phone number]](../data-types/phone-number.md) | The owner&#39;s home phone number. |
| `owner.mobilePhone` | [[!UICONTROL Phone number]](../data-types/phone-number.md) | The owner&#39;s mobile phone number. |
| `owner.personalEmail` | [[!UICONTROL Email address]](../data-types/email-address.md) | The owner&#39;s personal email address. |
| `ID` | [!UICONTROL String] | An identifier for the insurance policy. |
| `_id` | [!UICONTROL String] | A unique, system-generated string identifier for the record. This field is used to track the uniqueness of an individual record, prevent duplication of data, and to look up that record in downstream services.<br><br> However, you can still opt to supply your own unique ID values if you wish. |
| `endDate` | [!UICONTROL DateTime] | The date when the insurance policy coverage ends (or ended). |
| `hasAssignedBeneficiary` | [!UICONTROL Boolean] | Indicates whether the policy has a beneficiary assigned. |
| `name` | [!UICONTROL String] | The name of the insurance policy. |
| `startDate` | [!UICONTROL DateTime] | The date when the insurance policy coverage starts (or started). |
| `type` | [!UICONTROL String] | The type of insurance policy, such as home, automobile, renter, or boat. |

{style=&quot;table-layout:auto&quot;}
