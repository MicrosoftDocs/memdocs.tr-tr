---
title: Android Cihaz Yöneticisi kaydı Microsoft Intune
titleSuffix: ''
description: Cihaz yönetici kaydını kullanarak Android cihazlarını Intune 'a kaydetme.
keywords: ''
author: ErikjeMS
ms.author: erikje
manager: dougeby
ms.date: 07/23/2019
ms.topic: conceptual
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
ms.openlocfilehash: 1afbd444f46d14bb272410da54d43c5a5f8207d0
ms.sourcegitcommit: e2567b5beaf6c5bf45a2d493b8ac05d996774cac
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/27/2020
ms.locfileid: "80327320"
---
# <a name="android-device-administrator-enrollment"></a>Android cihaz yöneticisi kaydı

Android Cihaz Yöneticisi (bazen "eski" Android yönetimi ve Android 2,2 ile kullanıma sunulan) Android cihazlarını yönetmenin bir yoludur. Ancak, geliştirilmiş yönetim işlevselliği artık [Android Enterprise](https://www.android.com/enterprise/management/) (Android 5,0 ile yayımlanmıştır) ile kullanılabilir. Modern, daha zengin ve daha güvenli cihaz yönetimine geçiş çabasında, Google yeni Android sürümlerindeki Cihaz Yöneticisi desteğini düşürdüğünde.

Bu nedenle, bu tür azaltılmış işlevselliği önlemek için aşağıda açıklanan Cihaz Yöneticisi işlemini kullanarak yeni cihazların kaydedilmesini öneririz.

Aynı nedenlerden dolayı, cihazların Android 10 ' a güncelleyecekse Cihaz Yöneticisi yönetiminden da cihazları geçirmeniz önerilir. 

Android cihaz yöneticisi desteği için Intune desteği hakkında daha fazla bilgi için [Bildirimler bölümüne](../fundamentals/whats-new.md#decreasing-support-for-android-device-administrator)bakın.

Kullanıcıların, Android cihazlarını Cihaz Yöneticisi yönetimine kaydetmesine hala karar verirseniz, sonraki bölüme geçin.  

Google 'ın Android kurumsal özellikleri hakkında daha fazla bilgi için şu makalelere bakın:
- [Google 'ın cihaz yöneticisinden Android kuruluşa geçiş kılavuzu](http://static.googleusercontent.com/media/android.com/en/enterprise/static/2016/pdfs/enterprise/Android-Enterprise-Migration-Bluebook_2019.pdf)
- [Google 'ın Cihaz Yöneticisi API 'sini kullanımdan kaldırma planına yönelik belgeleri](https://developers.google.com/android/work/device-admin-deprecation)

## <a name="set-up-device-administrator-enrollment"></a>Cihaz yönetici kaydını ayarlama

1. Mobil cihazların yönetimine hazırlık olarak, **Microsoft Intune**’a mobil cihaz yönetimi (MDM) yetkilisi ayarlamanız gerekir. Yönergeler için bkz. [MDM yetkilisini ayarlama](../fundamentals/mdm-authority-set.md). Bu öğeyi yalnızca mobil cihaz yönetimi için Intune’u ilk defa kurduğunuzda ayarlayabilirsiniz.
2. [Microsoft Endpoint Manager Yönetim Merkezi](https://go.microsoft.com/fwlink/?linkid=2109431) ' nde oturum açın ve **cihaz yönetim > ayrıcalıklarına sahip kişisel ve şirkete ait cihazlarda** > **cihazları** ** > ** ** >  > cihazları** **yönetmek için Cihaz Yöneticisi 'ni kullanın**.
3. [Kullanıcılarınıza cihazlarını nasıl kaydedeceklerini anlatın](../user-help/enroll-device-android-company-portal.md).  

Bir kullanıcı kaydolduktan sonra [uyumluluk ilkeleri atama](../protect/compliance-policy-create-android.md), [uygulamaları yönetme](../apps/app-management.md) ve daha fazlası dahil olmak üzere kullanıcının cihazlarını Intune’da yönetmeye başlayabilirsiniz.

Diğer kullanıcı görevleri hakkında daha fazla bilgi için şu makalelere bakın:
- [Microsoft Intune’da son kullanıcı deneyimi hakkında kaynaklar](../fundamentals/end-user-educate.md)
- [Android cihazınızı Intune ile kullanma](https://docs.microsoft.com/mem/intune/user-help/why-enroll-android-device)


## <a name="block-device-administrator-enrollment"></a>Cihaz Yöneticisi kaydını engelle
Android Cihaz Yöneticisi cihazlarını engellemek veya yalnızca kişisel Android Cihaz Yöneticisi cihazlarının kaydını engellemek için bkz. [cihaz türü kısıtlamalarını ayarlama](enrollment-restrictions-set.md).


## <a name="next-steps"></a>Sonraki adımlar
- [Uyumluluk ilkeleri atama](../protect/compliance-policy-create-android.md)
- [Uygulamaları yönetme](../apps/app-management.md)
