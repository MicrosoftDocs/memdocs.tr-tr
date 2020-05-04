---
title: Microsoft Intune tarafından yönetilen cihazlar için kayıt seçenekleri
titleSuffix: ''
description: Yöneticilerin Microsoft Intune tarafından yönetilen cihazlar için ayarlayabilecekleri kayıt seçeneklerinin bir listesi.
keywords: ''
author: ErikjeMS
ms.author: erikje
manager: dougeby
ms.date: 10/31/2017
ms.topic: conceptual
ms.service: microsoft-intune
ms.subservice: enrollment
ms.localizationpriority: high
ms.technology: ''
ms.assetid: cf4ad6d4-423f-4826-ab8d-6eb7a7cfb559
search.appverid: MET150
ms.custom: get-started
ms.collection: M365-identity-device-management
ms.openlocfilehash: 3a769b1f1a0f11a4dd98c2f38e313012a7e2590b
ms.sourcegitcommit: 7f17d6eb9dd41b031a6af4148863d2ffc4f49551
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 04/21/2020
ms.locfileid: "79332862"
---
# <a name="enrollment-options-for-devices-managed-by-intune"></a>Intune tarafından yönetilen cihazlar için kayıt seçenekleri

Bir Intune yöneticisi olarak kullanıcılara yardımcı olmak ve Intune yeteneklerini etkinleştirmek için cihaz kaydını yapılandırabilirsiniz.  Intune, aşağıdaki kayıt seçeneklerini sunar:

## <a name="terms-and-conditions"></a>hüküm ve koşullar

Cihazlarını kaydetmek ve uygulama ve e-posta gibi şirket kaynaklarına erişmek üzere Şirket Portalı’nı kullanabilmeleri için önce şirketin hüküm ve koşullarını kabul etmelerini zorunlu tutabilirsiniz. Hüküm ve koşulların yapılandırması isteğe bağlıdır. [Hüküm ve koşullar](terms-and-conditions-create.md) hakkında daha fazla bilgi edinin.

## <a name="enrollment-restrictions"></a>Kayıt kısıtlamaları

Cihaz kaydını şunlara göre kısıtlayabilirsiniz:
- Cihaz platformu
- Kişi başına düşen cihaz sayısı
- Kişisel cihazları engelleme

[Kayıt kısıtlamaları](enrollment-restrictions-set.md) hakkında daha fazla bilgi edinin.

## <a name="enable-apple-device-enrollment"></a>Apple cihaz kaydını etkinleştirme

İOS/ıpados ve macOS cihaz kaydı için MDM anında iletme sertifikası gereklidir. [MDM anında iletme sertifikaları](apple-mdm-push-certificate-get.md) hakkında daha fazla bilgi edinin.

## <a name="corporate-identifiers"></a>Kurumsal tanımlayıcılar

Şirkete ait cihazları belirlemek için uluslararası mobil cihaz tanımlayıcısı (IMEI) numaralarını ve seri numaraları listeleyebilirsiniz. [Kurumsal tanımlayıcılar](corporate-identifiers-add.md) hakkında daha fazla bilgi edinin.
## <a name="multi-factor-authentication"></a>Multi-factor authentication

Kullanıcıların bir cihaz kaydederken telefon, PIN veya biyometrik veri gibi ilave doğrulama yöntemleri kullanmasını gerekli kılabilirsiniz. [Çok faktörlü kimlik doğrulaması](multi-factor-authentication.md) hakkında daha fazla bilgi edinin.

## <a name="device-enrollment-manager"></a>Cihaz kaydı yöneticisi
Kullanıcıları, cihaz kayıt yöneticileri yapabilirsiniz.  DEM kullanıcıları, çok sayıda mobil cihazı tek bir kullanıcı hesabıyla yönetebilir. Cihaz kayıt yöneticisi (DEM) hesabı, 1.000’e kadar cihazı kaydedebilir. [Cihaz kayıt yöneticileri](device-enrollment-manager-enroll.md) hakkında daha fazla bilgi edinin.

## <a name="device-categories"></a>Cihaz kategorileri

Tanımladığınız cihaz kategorilerine dayanarak cihazları gruplara otomatik olarak ekleyebilirsiniz. Cihazları gruplar halinde düzenlemek, bu cihazları yönetmenizi kolaylaştırır. [Cihaz kategorileri](device-group-mapping.md) hakkında daha fazla bilgi edinin.
