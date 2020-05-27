---
title: Android Kurumsal iş profili cihazlarını Intune’a kaydetme
titleSuffix: Microsoft Intune
description: Android Kurumsal iş profili cihazlarını Intune’a nasıl kaydedeceğinizi öğrenin.
keywords: ''
author: ErikjeMS
ms.author: erikje
manager: dougeby
ms.date: 5/13/2019
ms.topic: how-to
ms.service: microsoft-intune
ms.subservice: enrollment
ms.localizationpriority: high
ms.technology: ''
ms.assetid: ''
ms.reviewer: chmaguir
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: c3da384efb87e5510e64954ed7b1badfb98f6583
ms.sourcegitcommit: 302556d3b03f1a4eb9a5a9ce6138b8119d901575
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 05/27/2020
ms.locfileid: "83987516"
---
# <a name="set-up-enrollment-of-android-enterprise-work-profile-devices"></a>Android Kurumsal iş profili cihazların kaydını ayarlama

[!INCLUDE [azure_portal](../includes/azure_portal.md)]

Intune, iş ve kişisel bilgilerin ayrı olduğundan emin olmak için Android kurumsal iş profili cihazlarına uygulama ve ayarlar dağıtmanıza yardımcı olur. Android Enterprise hakkında ayrıntılı bilgi için bkz. [Android Enterprise Requirements](https://support.google.com/work/android/answer/6174145?hl=en&ref_topic=6151012).

Android Kurumsal iş profili yönetimini ayarlamak için aşağıdaki adımları izleyin:

1. [Intune kiracı Hesabınızı Android Kurumsal hesabınıza bağlayın](connect-intune-android-enterprise.md).
2. Android Kurumsal iş profili kayıt ayarlarını belirtin. Android Kurumsal iş profilleri, [yalnızca belirli Android cihazlarda desteklenmektedir](https://support.google.com/work/android/answer/6174145?hl=en&ref_topic=6151012%20style=%22target=new_window%22). Android kurumsal iş profillerini destekleyen herhangi bir cihaz, Android Cihaz Yöneticisi yönetimini de destekler. Intune, Android Kurumsal iş profilini destekleyen cihazların [Kayıt Kısıtlamaları](enrollment-restrictions-set.md) içerisinde nasıl yönetileceğini belirtmenize olanak sağlar.
    - **Engelle**: Android kurumsal iş profillerini destekleyen cihazlar dahil tüm Android cihazlar, Android Cihaz Yöneticisi kaydı da engellenmediği sürece Android Cihaz Yöneticisi cihazları olarak kaydedilir. 
    - **Izin ver (varsayılan olarak ayarlanır)**: Android kurumsal iş profillerini destekleyen tüm cihazlar Android kurumsal iş profili cihazları olarak kaydedilir. Android kurumsal iş profillerini desteklemeyen Android cihazlar, Android Cihaz Yöneticisi kaydı engellenmediği sürece bir Android Cihaz Yöneticisi cihazı olarak kaydedilir. 
> [!NOTE]
> Varsayılan **Izin ver** olarak ayarlanan yeni kiracılar Için 2019 Temmuz itibariyle geçerlidir. Tüm önceki kiracılar, kayıt kısıtlamalarında hiçbir değişiklik yapmadan deneyimlerdir ve kayıt kısıtlamalarında ayarlamış oldukları her türlü ilkeyi görür. Kayıt kısıtlamaları değişikliği olmayan önceki kiracılar için, **blok** hala Android kurumsal iş profilleri için varsayılan değer olacaktır.

3. [Kullanıcılarınıza cihazlarını nasıl kaydedeceklerini anlatın](../user-help/enroll-device-android-work-profile.md).  

Android kurumsal iş profillerini kullanarak cihazları kaydetmek istiyorsanız, ancak bu cihazlar zaten Android cihaz yöneticisiyle kaydedildiyse, bu cihazların kaydı ve ardından yeniden kaydedilmesi gerekir.
> [!NOTE]
> Yönetici olarak, bunu **devre dışı bırak** işlevini kullanarak uzaktan gerçekleştirebilirsiniz. Bu işlev, **tüm cihazlar** dikey penceresinden cihaz seçildikten sonra Eylemler menüsünde bulunabilir.

Android Kurumsal iş profili cihazlarını bir [Cihaz Kayıt Yöneticisi](device-enrollment-manager-enroll.md) hesabı kullanarak kaydediyorsanız, hesap başına en fazla 10 cihaz kaydedebilirsiniz.

Daha fazla bilgi için bkz. [Intune’un Google’a gönderdiği veriler](../protect/data-intune-sends-to-google.md).

## <a name="next-steps-for-android-enterprise-work-profiles"></a>Android Kurumsal iş profilleri için sonraki adımlar
- [Android Kurumsal iş profili uygulamalarını dağıtma](../apps/apps-add-android-for-work.md)
- [Android Kurumsal iş profili yapılandırma ilkeleri ekleme](../configuration/device-profiles.md)

## <a name="see-also"></a>Ayrıca bkz.

[Microsoft Intune Android kurumsal cihazlarını yapılandırma ve sorunlarını giderme](https://support.microsoft.com/help/4476974)
