---
title: Microsoft Intune - Azure’da SCEP ve PKCS sertifikalarını kaldırma | Microsoft Docs
titleSuffix: ''
description: Yöneticiler, Microsoft Intune’dan sertifika kaldırmak için silme veya devre dışı bırakma eylemlerini kullanabilirler. Bir cihaz kaydının silinmesi veya bir uyumluluk ilkesinin kaldırılması gibi, sertifikaların otomatik olarak kaldırıldığı bazı senaryolar da vardır. Intune lisansının kaybolması veya kaldırılması gibi, sertifikaların otomatik olarak cihazda kaldığı bazı senaryolar da vardır. Android, Android Enterprise, iOS/ıpados, macOS ve Windows cihazlarının farklı yollarına bakın.
keywords: ''
author: brenduns
ms.author: brenduns
manager: dougeby
ms.date: 03/19/2020
ms.topic: how-to
ms.service: microsoft-intune
ms.subservice: protect
ms.localizationpriority: high
ms.technology: ''
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.reviewer: lacranda
ms.openlocfilehash: 90f75420eeb19bf78f41190fa45ae5133e7746d9
ms.sourcegitcommit: 302556d3b03f1a4eb9a5a9ce6138b8119d901575
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 05/27/2020
ms.locfileid: "83990038"
---
# <a name="remove-scep-and-pkcs-certificates-in-microsoft-intune"></a>Microsoft Intune’da SCEP ve PKCS sertifikalarını kaldırma

Microsoft Intune, cihazlara sertifika eklemek için Basit Sertifika Kayıt Protokolü (SCEP) ve ortak anahtar şifreleme standartları (PKCS) sertifika profillerini kullanabilirsiniz.

Bu sertifikalar [, cihazı sildiğinizde veya](../remote-actions/devices-wipe.md#wipe) [devre dışı](../remote-actions/devices-wipe.md#retire) bırakıldığında kaldırılabilir. Ayrıca, sertifikaların otomatik olarak kaldırıldığı senaryolar ve sertifikaların cihazda kalacağı senaryolar da vardır. Bu makalede bazı yaygın senaryolar ve bu senaryoların PKCS ve SCEP sertifikaları üzerindeki etkisi listelenmiştir.

> [!NOTE]
> Şirket içi Active Directory veya Azure Active Directory (Azure AD) ' den çıkarılan bir kullanıcının sertifikalarını kaldırmak ve iptal etmek için şu adımları sırasıyla izleyin:
>
> 1. Kullanıcının cihazını temizleyin veya devre dışı bırakın.
> 2. Kullanıcıyı şirket içi Active Directory veya Azure AD 'den kaldırın.

## <a name="manually-deleted-certificates"></a>El ile silinen sertifikalar

Bir sertifikayı el ile silme, SCEP veya PKCS sertifika profilleri tarafından sağlanan platformlar ve Sertifikalar arasında uygulanan bir senaryodur. Örneğin, bir Kullanıcı bir sertifika ilkesi tarafından hedeflenirse bir cihazdan bir sertifikayı silebilir.

Bu senaryoda, sertifika silindikten sonra cihaz, Intune ile bir dahaki sefer denetlediğinde, beklenen sertifika eksik olduğu için aygıtın uyumsuz olduğu tespit edilir. Intune daha sonra cihazı uyumluluğa geri yüklemek için yeni bir sertifika yayınlar. Sertifikayı geri yüklemek için başka bir eylem gerekmez.

## <a name="windows-devices"></a>Windows cihazları

### <a name="scep-certificates"></a>SCEP sertifikaları

Bir SCEP sertifikası şu durumlarda iptal edilir *ve* kaldırılır:

- Bir kullanıcı kaydı geri alır.
- Yönetici [silme](../remote-actions/devices-wipe.md#wipe) eylemini çalıştırır.
- Yönetici [devre dışı bırakma](../remote-actions/devices-wipe.md#retire) eylemini çalıştırır.
- Cihaz bir Azure AD grubundan kaldırılır.
- Bir sertifika profili grup atamasından kaldırılır.

Bir SCEP sertifikası şu durumlarda iptal edilir:

- Bir yönetici, SCEP profilini değiştirir veya güncelleştirir.

Şu durumlarda bir kök sertifika kaldırılır:

- Bir kullanıcı kaydı geri alır.
- Yönetici [silme](../remote-actions/devices-wipe.md#wipe) eylemini çalıştırır.
- Yönetici [devre dışı bırakma](../remote-actions/devices-wipe.md#retire) eylemini çalıştırır.

SCEP sertifikaları cihazda *kalır* (sertifikalar iptal edilmez veya kaldırılmaz):

- Bir Kullanıcı Intune lisansını kaybeder.
- Bir yönetici, Intune lisansını çizer.
- Yönetici, kullanıcıyı veya grubu Azure AD 'den kaldırır.

### <a name="pkcs-certificates"></a>PKCS sertifikaları

Bir PKCS sertifikası şu durumlarda iptal edilir *ve* kaldırılır:

- Bir kullanıcı kaydı geri alır.
- Yönetici [silme](../remote-actions/devices-wipe.md#wipe) eylemini çalıştırır.
- Yönetici [devre dışı bırakma](../remote-actions/devices-wipe.md#retire) eylemini çalıştırır.

Şu durumlarda bir kök sertifika kaldırılır:

- Bir kullanıcı kaydı geri alır.
- Yönetici [silme](../remote-actions/devices-wipe.md#wipe) eylemini çalıştırır.
- Yönetici [devre dışı bırakma](../remote-actions/devices-wipe.md#retire) eylemini çalıştırır.

PKCS sertifikaları cihazda *kalır* (sertifikalar iptal edilmez veya kaldırılmaz):

- Bir Kullanıcı Intune lisansını kaybeder.
- Bir yönetici, Intune lisansını çizer.
- Yönetici, kullanıcıyı veya grubu Azure AD 'den kaldırır.
- Bir yönetici, PKCS profilini değiştirir veya güncelleştirir.
- Bir sertifika profili grup atamasından kaldırılır.

## <a name="ios-devices"></a>iOS cihazları

### <a name="scep-certificates"></a>SCEP sertifikaları

Bir SCEP sertifikası şu durumlarda iptal edilir *ve* kaldırılır:

- Bir kullanıcı kaydı geri alır.
- Yönetici [silme](../remote-actions/devices-wipe.md#wipe) eylemini çalıştırır.
- Yönetici [devre dışı bırakma](../remote-actions/devices-wipe.md#retire) eylemini çalıştırır.
- Cihaz Azure AD grubundan kaldırılır.
- Bir sertifika profili grup atamasından kaldırılır.

Bir SCEP sertifikası şu durumlarda iptal edilir:

- Bir yönetici, SCEP profilini değiştirir veya güncelleştirir.

Şu durumlarda bir kök sertifika kaldırılır:

- Bir kullanıcı kaydı geri alır.
- Yönetici [silme](../remote-actions/devices-wipe.md#wipe) eylemini çalıştırır.
- Yönetici [devre dışı bırakma](../remote-actions/devices-wipe.md#retire) eylemini çalıştırır.

SCEP sertifikaları cihazda *kalır* (sertifikalar iptal edilmez veya kaldırılmaz):

- Bir Kullanıcı Intune lisansını kaybeder.
- Bir yönetici, Intune lisansını çizer.
- Yönetici, kullanıcıyı veya grubu Azure AD 'den kaldırır.

### <a name="pkcs-certificates"></a>PKCS sertifikaları

Bir PKCS sertifikası şu durumlarda iptal edilir *ve* kaldırılır:

- Bir kullanıcı kaydı geri alır.
- Yönetici [silme](../remote-actions/devices-wipe.md#wipe) eylemini çalıştırır.
- Yönetici [devre dışı bırakma](../remote-actions/devices-wipe.md#retire) eylemini çalıştırır.

Bir PKCS sertifikası şu durumlarda kaldırılır:

- Bir sertifika profili grup atamasından kaldırılır.

Şu durumlarda bir kök sertifika kaldırılır:

- Bir kullanıcı kaydı geri alır.
- Yönetici [silme](../remote-actions/devices-wipe.md#wipe) eylemini çalıştırır.
- Yönetici [devre dışı bırakma](../remote-actions/devices-wipe.md#retire) eylemini çalıştırır.

PKCS sertifikaları cihazda *kalır* (sertifikalar iptal edilmez veya kaldırılmaz):

- Bir Kullanıcı Intune lisansını kaybeder.
- Bir yönetici, Intune lisansını çizer.
- Yönetici, kullanıcıyı veya grubu Azure AD 'den kaldırır.
- Bir yönetici, PKCS profilini değiştirir veya güncelleştirir.

## <a name="android-knox-devices"></a>Android KNOX cihazları

### <a name="scep-certificates"></a>SCEP sertifikaları

Bir SCEP sertifikası şu durumlarda iptal edilir *ve* kaldırılır:

- Bir kullanıcı kaydı geri alır.
- Yönetici [silme](../remote-actions/devices-wipe.md#wipe) eylemini çalıştırır.

Bir SCEP sertifikası şu durumlarda iptal edilir:

- Yönetici [devre dışı bırakma](../remote-actions/devices-wipe.md#retire) eylemini çalıştırır.
- Cihaz bir Azure AD grubundan kaldırılır.
- Bir sertifika profili grup atamasından kaldırılır.
- Yönetici, kullanıcıyı veya grubu Azure AD 'den kaldırır.
- Bir yönetici, SCEP profilini değiştirir veya güncelleştirir.

Şu durumlarda bir kök sertifika kaldırılır:

- Bir kullanıcı kaydı geri alır.
- Yönetici [silme](../remote-actions/devices-wipe.md#wipe) eylemini çalıştırır.
- Yönetici [devre dışı bırakma](../remote-actions/devices-wipe.md#retire) eylemini çalıştırır.

SCEP sertifikaları cihazda *kalır* (sertifikalar iptal edilmez veya kaldırılmaz):

- Bir Kullanıcı Intune lisansını kaybeder.
- Bir yönetici, Intune lisansını çizer.
- Yönetici, kullanıcıyı veya grubu Azure AD 'den kaldırır.

### <a name="pkcs-certificates"></a>PKCS sertifikaları

Bir PKCS sertifikası şu durumlarda iptal edilir *ve* kaldırılır:

- Bir kullanıcı kaydı geri alır.
- Yönetici [silme](../remote-actions/devices-wipe.md#wipe) eylemini çalıştırır.
- Yönetici [devre dışı bırakma](../remote-actions/devices-wipe.md#retire) eylemini çalıştırır.

Şu durumlarda bir kök sertifika kaldırılır:

- Bir kullanıcı kaydı geri alır.
- Yönetici [silme](../remote-actions/devices-wipe.md#wipe) eylemini çalıştırır.
- Yönetici [devre dışı bırakma](../remote-actions/devices-wipe.md#retire) eylemini çalıştırır.

PKCS sertifikaları cihazda *kalır* (sertifikalar iptal edilmez veya kaldırılmaz):

- Bir Kullanıcı Intune lisansını kaybeder.
- Bir yönetici, Intune lisansını çizer.
- Yönetici, kullanıcıyı veya grubu Azure AD 'den kaldırır.
- Bir yönetici, PKCS profilini değiştirir veya güncelleştirir.
- Bir sertifika profili grup atamasından kaldırılır.


> [!NOTE]
> Android for Work cihazları önceki senaryolar için doğrulanmaz.
> Android eski cihazlar (Samsung olmayan, iş dışı tüm profil cihazları) sertifika kaldırma için etkinleştirilmemiştir.

## <a name="macos-certificates"></a>macOS sertifikaları

### <a name="scep-certificates"></a>SCEP sertifikaları

Bir SCEP sertifikası şu durumlarda iptal edilir *ve* kaldırılır:

- Bir kullanıcı kaydı geri alır.
- Yönetici [devre dışı bırakma](../remote-actions/devices-wipe.md#retire) eylemini çalıştırır.
- Cihaz bir Azure AD grubundan kaldırılır.
- Bir sertifika profili grup atamasından kaldırılır.

Bir SCEP sertifikası şu durumlarda iptal edilir:

- Bir yönetici, SCEP profilini değiştirir veya güncelleştirir.

SCEP sertifikaları cihazda *kalır* (sertifikalar iptal edilmez veya kaldırılmaz):

- Bir Kullanıcı Intune lisansını kaybeder.
- Bir yönetici, Intune lisansını çizer.
- Yönetici, kullanıcıyı veya grubu Azure AD 'den kaldırır.

> [!NOTE]
> macOS cihazlarda fabrika sıfırlaması yapmak için [silme](../remote-actions/devices-wipe.md#wipe) eyleminin kullanımı desteklenmez.

### <a name="pkcs-certificates"></a>PKCS sertifikaları

Bir PKCS sertifikası şu durumlarda iptal edilir *ve* kaldırılır:

- Bir kullanıcı kaydı geri alır.
- Yönetici [devre dışı bırakma](../remote-actions/devices-wipe.md#retire) eylemini çalıştırır.

Şu durumlarda bir kök sertifika kaldırılır:

- Bir kullanıcı kaydı geri alır.
- Yönetici [devre dışı bırakma](../remote-actions/devices-wipe.md#retire) eylemini çalıştırır.

PKCS sertifikaları cihazda kalır (sertifikalar iptal edilmez veya kaldırılmaz):

- Bir Kullanıcı Intune lisansını kaybeder.
- Bir yönetici, Intune lisansını çizer.
- Bir sertifika profili grup atamasından kaldırılır. (Profil kaldırılır.)
- Yönetici, kullanıcıyı veya grubu Azure AD 'den kaldırır.
- Bir yönetici, PKCS profilini değiştirir veya güncelleştirir.

## <a name="next-steps"></a>Sonraki adımlar

[Kimlik doğrulama için sertifika kullanma](certificates-configure.md)