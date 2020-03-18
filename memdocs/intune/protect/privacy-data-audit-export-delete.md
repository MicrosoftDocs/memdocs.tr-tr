---
title: Kişisel verileri denetleme, dışarı aktarma veya silme
titleSuffix: Microsoft Intune
description: Kişisel verileri denetleme, dışarı aktarma veya silme hakkında bilgi edinin.
keywords: ''
author: ErikjeMS
ms.author: erikje
manager: dougeby
ms.date: 05/18/2018
ms.topic: conceptual
ms.service: microsoft-intune
ms.subservice: protect
ms.localizationpriority: high
ms.technology: ''
ms.assetid: 96990be0-eb1e-43a4-a0e4-09c7dbdc2bf4
ms.reviewer: kerimh
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: db3146bbaae3362e97c8c076823b58dbcd57c4af
ms.sourcegitcommit: 3d895be2844bda2177c2c85dc2f09612a1be5490
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/13/2020
ms.locfileid: "79325322"
---
# <a name="audit-export-or-delete-personal-data-in-intune"></a>Intune’da kişisel verileri denetleme, dışarı aktarma veya silme

Intune yöneticileri, denetim günlükleriyle ilgili kişisel verileri etkinlik izlemek için kullanabilir. Yöneticiler ayrıca kişisel verileri dışarı aktarabilir ve silebilir.

[!INCLUDE [GDPR-related guidance](../includes/gdpr-intro-sentence.md)]

## <a name="audit-personal-data"></a>Kişisel verileri denetleme

Denetim günlükleri, kiracı yöneticilerine Microsoft Intune’da değişiklik yaratan etkinliklerin kaydını sağlar. Denetim günlükleri, birçok yönetim etkinliği için mevcuttur ve genellikle eylem oluşturur, güncelleştirir (düzenler), siler ve atar. Denetim olayları oluşturan kaldırma görevleri de gözden geçirilebilir. Bu denetim günlükleri, cihazları Intune’da kayıtlı olan kullanıcıların kişisel verilerini içerebilir.  

Intune, güvenlik nedeniyle kullanıcı ve cihaz eylemleri için denetim günlüklerini bir yıllık bir süre boyunca tutabilir. Bu günlükler, bir yıllık saklama döneminden sonra otomatik olarak silinir.

Denetim günlüklerini gözden geçirmek için bkz. [Intune etkinlikleri için denetim günlükleri](../fundamentals/monitor-audit-logs.md). 

Yöneticiler denetim günlüklerini silemez.

Bu denetim olayları, bir yıl boyunca saklanır. Kiracı yöneticileri, [bu destek isteği formunu](https://privacy.microsoft.com/en-US/privacy-questions?) kullanarak denetim günlüklerini isteyebilir.

## <a name="export-personal-data"></a>Kişisel verileri dışarı aktarma

Yöneticiler; hesaplar, hizmet verileri ve ilişkili günlükler dahil olmak üzere son kullanıcı kişisel verilerini Veri Sahibi Hakları istekleri doğrultusunda dışarı aktarabilir. Kişisel verileri gizli tutmak için geçerli bir yasal sebebiniz varsa veri sahibine bu verilerin bir kopyasını sağlayıp sağlamamak size ve kuruluşunuza kalmıştır. Verileri sağlamaya karar verirseniz asıl belgenin bir kopyasını, uygun şekilde redakte edilmiş halini veya paylaşmaya uygun gördüğünüz kısımların ekran görüntüsünü veri sahibiyle paylaşabilirsiniz.

Bir kullanıcının kişisel verilerini dışarı aktarmak için şunları kullanabilirsiniz: 
- Cihazlar listesini dışarı aktarmak için Intune MDM Cihaz dikey penceresi. Cihaz verilerini doğrudan da kopyalayabilirsiniz.
- [Export-IntuneData.ps1 betiği](https://aka.ms/intunedataexport).

## <a name="delete-end-user-personal-data"></a>Son kullanıcı kişisel verilerini silme

Kişisel verileri Intune yönetiminden kaldırmanın üç yolu vardır:
- Cihazı Azure Active Directory’den silmek
- Cihazı fabrika ayarlarına sıfırlamak
- Kullanıcının kendisini kaldırması

### <a name="delete-a-user-from-intune"></a>Intune’dan kullanıcı silmek

Bir son kullanıcının kişisel verilerini Intune’dan silmek için yöneticinin [kullanıcıyı Azure Active Directory’den (AAD) silmesi](https://docs.microsoft.com/azure/active-directory/fundamentals/add-users-azure-active-directory#delete-a-user) gerekir. Kullanıcı AAD’den silindiğinde (kalıcı olarak silindiğinde) Intune, AAD’den silme sinyalini alır ve kullanıcının kişisel verilerinin tamamını otomatik olarak Intune hizmetinden temizlemeye başlar. Kaldırma eylemini takip eden 30 gün içerisinde kullanıcı bilgileri Intune hizmetinden silinir.

### <a name="reset-device-to-factory-settings"></a>Cihazı fabrika ayarlarına sıfırlama
Fabrika ayarlarına sıfırlama, tüm şirkete ait ve kişisel veri ve ayarlar yerine orijinal fabrika ayarlarını geri yükler. Bu, cihazı yeni bir çalışana vermek için kullanışlıdır. Kullanıcı dosyaları, kullanıcının yüklediği uygulamalar ve varsayılan olmayan ayarlar kaldırılır ve bu veriler kaldırma eylemini izleyen 30 gün içerisinde Intune hizmetinden silinir.

### <a name="user-self-removal-from-intune-management"></a>Kullanıcının kendisini Intune yönetiminden kaldırması
Kullanıcılar, yönetici yardımı olmadan kendi [Android, Apple veya Windows](https://docs.microsoft.com/user-help/unenroll-your-device-from-intune-android) cihazlarını Intune’dan kaldırabilir.   

### <a name="retire"></a>Devre Dışı Bırak
**Kullanımdan kaldırma** eylemi; şirket uygulamaları, Intune'un yönettiği uygulamalara ilişkin veriler, ilke ayarları ve Intune yoluyla sağlanan e-posta profilleri gibi Intune tarafından sağlanan verileri kaldırır. Bu eylem, kullanıcının kişisel verilerini cihazda bırakır.

### <a name="delete-a-tenant-from-microsoft-intune"></a>Microsoft Intune’dan kiracı silme

Bir Intune kiracısı Intune hesabını iptal ederse, Intune hesabının kapatılmasını izleyen 180 gün içerisinde tüm kiracı verileri silinir. AAD kiracısı diğer Microsoft kuruluş abonelikleri (Azure, Office 365) ile ilişkiliyse yalnızca Intune Müşteri Verileri silinir. AAD kiracı kaynağı, diğer abonelikler tarafından kullanılmak üzere saklanır. AAD kiracısıyla ilişkili tek abonelik Intune hesabıysa Intune Müşteri Verilerinin yanında kiracı ve tüm kaynaklar da silinir.

## <a name="next-steps"></a>Sonraki adımlar

Intune’da kişisel verileri [denetleme, dışarı aktarma ve silme](privacy-data-audit-export-delete.md) hakkında bilgi edinin.
