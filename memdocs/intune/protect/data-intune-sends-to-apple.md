---
title: Intune’un Apple’a gönderdiği veriler
titleSuffix: Microsoft Intune
description: Intune’un Apple’a gönderdiği veri listesi.
keywords: ''
author: ErikjeMS
ms.author: erikje
manager: dougeby
ms.date: 02/26/2018
ms.topic: conceptual
ms.service: microsoft-intune
ms.subservice: protect
ms.localizationpriority: high
ms.technology: ''
ms.assetid: b204a956-18ec-11e8-accf-0ed5f89f718b
ms.reviewer: ''
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: da9ab5fe5a8716e3af0ae02122f51d06e6e55e6f
ms.sourcegitcommit: 3d895be2844bda2177c2c85dc2f09612a1be5490
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/13/2020
ms.locfileid: "79329454"
---
# <a name="data-intune-sends-to-apple"></a>Intune’un Apple’a gönderdiği veriler

[!INCLUDE [azure_portal](../includes/azure_portal.md)]

Bir cihazda aşağıdaki Apple hizmetlerinden herhangi biri etkinleştirildiğinde Microsoft Intune, Apple ile bir bağlantı kurar ve Apple ile kullanıcı ve cihaz bilgilerini paylaşır: 

- [Apple Aygıt Kayıt Programı (DEP)](../enrollment/device-enrollment-program-enroll-ios.md)
- [Apple MDM Anında İletme sertifikası (APNS)](../enrollment/apple-mdm-push-certificate-get.md)
- [Apple School Manager (ASM)](https://docs.microsoft.com/schooldatasync/apple-school-manager-integration-with-intune-for-education-and-school-data-sync)
- [Apple Volume Purchase Program (VPP)](../apps/vpp-apps-ios.md)

Microsoft Intune’un bir bağlantı kurabilmesi için, önce Apple hizmetlerinin her biri için bir Apple hesabı oluşturmalısınız.

Aşağıdaki tabloda Microsoft Intune'un bir cihazdan etkinleştirilmiş Apple hizmetlerine gönderdiği veriler listelenir. 

| Hizmet | Apple’a gönderilen veriler | Kullanım alanı: |
|---|---| ---|
| [APNS](https://developer.apple.com/library/content/documentation/Miscellaneous/Reference/MobileDeviceManagementProtocolRef/3-MDM_Protocol/MDM_Protocol.html#//apple_ref/doc/uid/TP40017387-CH3-SW2) | Belirteç, PushMagic | Sunucu cihazı kabul ederse cihaz, anında iletme bildirimi cihaz belirtecini sunucuya sağlar. Sunucu, cihaza anında iletme mesajı göndermek için bu belirteci kullanmalıdır. Bu iade etme iletisi ayrıca bir PushMagic dizesi içerir. Sunucu bu dizeyi hatırlamalı ve cihaza gönderdiği tüm anında iletme mesajlarına eklemelidir. |
| [ASM/DEP](https://developer.apple.com/library/content/documentation/Miscellaneous/Reference/MobileDeviceManagementProtocolRef/3-MDM_Protocol/MDM_Protocol.html#//apple_ref/doc/uid/TP40017387-CH3-SW2) | Sunucu belirteci | Apple hizmetinde kimlik doğrulaması için kullanılan anında iletme bildirimi cihaz belirteci. |
| ASM/DEP | server_name | MDM sunucusu için tanımlanabilir bir ad. |
| ASM/DEP | server_uuid | Sistem tarafından oluşturulan sunucu tanımlayıcısı. |
| ASM/DEP | admin_id | Kullanılmakta olan geçerli belirteçleri oluşturan kişinin Apple kimliği. |
| ASM/DEP | org_name | Kuruluş adı. |
| ASM/DEP | org_email | Kuruluşun e-posta adresi. |
| ASM/DEP | org_phone | Kuruluşun telefonu. |
| ASM/DEP | org_address | Kuruluşun adresi. |
| ASM/DEP | org_id | DEP müşteri kimliği. Bu anahtar sadece protokol sürümü 3 ve sonrası için kullanılabilir. |
| ASM/DEP | serial_number | Cihazın seri numarası (dize). |
| ASM/DEP | {1&gt;model&lt;1} | Model adı (dize). |
| ASM/DEP | açıklama | Cihazın açıklaması (dize). |
| ASM/DEP | asset_tag | Cihazın varlık etiketi (dize). |
| ASM/DEP | profile_status | Profili yükleme durumu. Olası değerler: **Boş**, **atandı**, **gönderildi** veya **kaldırıldı**. |
| ASM/DEP | profile_uuid | Atanan profilin benzersiz kimliği. |
| ASM/DEP | device_assigned_by | Cihazı atayan kişinin e-postası. |
| ASM/DEP | os | Cihazın işletim sistemi: iOS/ıpados, OSX veya tvOS. Bu anahtar, X-Server-Protokol-Sürüm 2 ve sonrası için geçerlidir. |
| ASM/DEP | device_family | Cihazın Apple ürün ailesi: iPad, iPhone, iPod, Mac veya AppleTV. Bu anahtar, X-Server-Protokol-Sürüm 2 ve sonrası için geçerlidir. |
| ASM/DEP | profile_name | Dize. Profil için okunabilir bir ad. |
| ASM/DEP | support_phone_number | İsteğe bağlı. Dize. Kuruluş için bir destek telefon numarası. |
| ASM/DEP | support_email_address | İsteğe bağlı. Dize. Kuruluş için bir destek e-posta adresi. Bu anahtar, X-Server-Protokol-Sürüm 2 ve sonrası için geçerlidir. |
| ASM/DEP | bölüm | İsteğe bağlı. Dize. Kullanıcı tanımlı departman veya konum adı. |
| ASM/DEP | devices | Cihaz seri numaralarını içeren bir dize dizisi. (Boş olabilir.) |
| VPP | Intune UserId guid | Intune tarafından oluşturulan GUID. |
| VPP | Managed AppleId UPN | Apple ile VPP belirteç bağlantısını yapılandırırken Yönetici tarafından belirtilen AppleID (Apple Kimliği). |
| VPP | Seri Numarası | Yönetilen cihazın seri numarası. |

Microsoft Intune ile Apple hizmetlerini kullanmayı bırakmak ve verileri silmek için hem Microsoft Intune Apple belirtecini devre dışı bırakmanız hem de Apple hesabınızı silmeniz gerekir. Hesap yönetimini nasıl gerçekleştireceğinizi görmek için Apple hesabına bakın.


