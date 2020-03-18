---
title: Android kullanıcılarınız uygulamalarını nasıl alır
description: Android uygulamalarını son kullanıcılara sağlama yöntemleri
keywords: ''
author: lenewsad
ms.author: lanewsad
manager: dougeby
ms.date: 03/12/2020
ms.topic: conceptual
ms.service: microsoft-intune
ms.subservice: fundamentals
ms.localizationpriority: high
ms.technology: ''
ms.assetid: f33d1684-b1b5-44f7-9aac-c6d5186a5d7c
ms.reviewer: aanavath
ms.suite: ems
search.appverid: MET150
ms.custom: intune-classic
ms.collection: M365-identity-device-management
ms.openlocfilehash: e1d18a423242300b6c2b66c01c59404cef42ebd9
ms.sourcegitcommit: b5a9ce31de743879d2a6306cea76be3a093976bb
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/14/2020
ms.locfileid: "79372560"
---
# <a name="how-your-android-users-get-their-apps"></a>Android kullanıcılarınız uygulamalarını nasıl alır  

Bu makale, Android cihaz yöneticinizin son kullanıcılarının Microsoft Intune aracılığıyla dağıttığınız uygulamaları nasıl ve nereden alabileceğini anlamanıza yardımcı olur. Bilgiler cihaz türüne göre değişebilir (yerel Android cihazlar veya Samsung Knox Standard cihazlar).

## <a name="native-non-samsung-knox-standard-android-devices"></a>Yerel (Samsung Knox Standard harici) Android cihazlar   

| Uygulama türü | İş kolu (LOB) uygulamaları | Play Store uygulamaları  |
| ------------- |-------------| -----|
| Kullanılabilir uygulamalar      | Kullanıcılar Şirket Portalı’nda **yükle**’ye dokunur. Bir bildirim görüntülenir ve kullanıcılar buna dokunarak yüklemeyi başlatır. Yükleme başarılı olduktan sonra, bildirim görüntüden kaldırılır. | Kullanıcılar Şirket Portalı uygulamaya dokunur ve Play Store bir uygulama sayfasına alınmıştır. Bu, yüklemeyi başlattıkları yerdir.|
| Gerekli uygulamalar      | **Android 9,0 ve önceki sürümleri çalıştıran cihazlarda**, kullanıcılara bir uygulama indirmesi gerektiğini belirten bir bildirim gösterilir. Kullanıcılar indirme ve yüklemeyi başlatmak için bildirime dokunur. Yükleme başarılı olduktan sonra, bildirim görüntüden kaldırılır. **Android 10 ve üzeri çalıştıran cihazlarda**, kullanıcılara bir uygulama indirmesi gerektiğini belirten bir bildirim gösterilir. Kullanıcılar indirmeyi başlatmak için bildirime dokunduktan sonra uygulamanın yüklenmesini başlatacak bir bildirim alır. Yükleme başarılı olduktan sonra, bildirim görüntüden kaldırılır.| Kullanıcılara, bir uygulama yüklemeleri gerektiğini belirten bir bildirim gösterilir. Kullanıcılar bildirime dokunur ve Play Store bir uygulama sayfasına alınır. Bu, yüklemeyi başlattıkları yerdir. Yükleme başarılı olduktan sonra, bildirim görüntüden kaldırılır. |

Son kullanıcılarınızın [LOB uygulamalarını](../apps/lob-apps-android.md)yüklemek için bilinmeyen kaynaklardan yükleme yapmasına izin vermeniz gerekir. Bu ayar normalde iki farklı yerde bulunur:

* **Android 7.1.2 ve altı sürümler**: **Ayarlar** > **Güvenlik** > **Bilinmeyen kaynaklar**
* **Android 8.0 ve üzeri sürümler**: **Ayarlar** > **Uygulamalar ve bildirimler** > **Özel uygulama erişimi** > **Bilinmeyen uygulama yükleme** > **Şirket Portalı** > **Bu kaynağa izin ver**

Bu durumda Şirket Portalı uygulaması, son kullanıcıya bilgi verip onu doğrudan uygun ayara yönlendirecektir. 

## <a name="samsung-knox-standard-android-devices"></a>Samsung Knox Standard Android cihazlar

| Uygulama türü | İş kolu (LOB) uygulamaları | Play Store uygulamaları  |
| ------------- |-------------| -----|
| Kullanılabilir uygulamalar      | Kullanıcılar Şirket Portalı’nda **yükle**’ye dokunur. Uygulama, başka kullanıcı müdahalesi olmadan yüklenir. | Kullanıcılar Şirket Portalı uygulamaya dokunur ve Play Store bir uygulama sayfasına alınır. Bu, yüklemeyi başlattıkları yerdir.|
| Gerekli uygulamalar      | **Android 9,0 ve önceki sürümleri çalıştıran cihazlarda**, uygulama herhangi bir kullanıcı müdahalesi olmadan yüklenir. **Android 10 ve üzeri çalıştıran cihazlarda**, kullanıcılara bir uygulama indirmesi gerektiğini belirten bir bildirim gösterilir. Kullanıcılar yüklemeyi başlatmak için bildirime dokunur. Yükleme başarılı olduktan sonra, bildirim görüntüden kaldırılır. | Kullanıcılara, bir uygulama yüklemeleri gerektiğini belirten bir bildirim gösterilir. Kullanıcılar bildirime dokunur ve Play Store bir uygulama sayfasına alınır. Bu, yüklemeyi başlattıkları yerdir. Yükleme başarılı olduktan sonra, bildirim görüntüden kaldırılır. |

Uygulamalar, aşağıda açıklandığı gibi yönetilebilir veya yönetilmeyebilir. Uygulamaları yönetilen uygulama yapma işlemi, tüm Android cihaz türlerinde aynıdır.

**Yönetilen uygulamalar** -bu uygulamalar ilkeler aracılığıyla yönetilir. Intune tarafından "sarmalanmış" veya Intune uygulama SDK 'Sı ile oluşturulmuştur. Bu uygulamalar Intune tarafından yönetilebilir ve uygulama ilkeleri uygulanabilir.

**Yönetilmeyen uygulamalar** -bu uygulamalar ilkeler aracılığıyla yönetilmez. Intune tarafından sarmalanmamış veya Intune uygulama SDK 'Sı dahil değildir. Uygulama ilkeleri bu uygulamalara uygulanamaz.

## <a name="zebra-devices-with-zebra-mobility-extensions"></a>Zeköşeli Mobility uzantılarına sahip zeköşeli cihazlar

Intune, Cihaz Yöneticisi tarafından yönetilen Zeköşeli cihazlara uygulamaları sessizce yüklemek için Zeköşeli Mobility uzantıları (MX) araç takımını kullanır. Bu özellik, Zeköşeli cihazlarda Kullanıcı müdahalesi olmadan uygulama dağıtmanıza ve güncelleştirmenize olanak tanır. Cihazınızdaki MX sürümü 4,2 veya daha eski bir sürümse, uygulamalar sessizce yüklenmez. Daha fazla bilgi için bkz. Zeköşeli Web sitesinde [tam MX özelliği matrisi](http://techdocs.zebra.com/mx/compatibility/) .

Zeköşeli cihazlara dağıtılan LOB uygulamalarının, cihazdaki ortak bir konumdan yüklenmesi gerekir. . Apk uygulama paketine, cihazdaki ortak depolamaya da erişimi olan diğer uygulama ve hizmetlerle erişilebilir. Genellikle bu erişim, uygulamanın indirilmesi tamamlanırken ve yükleme başlangıcında küçük bir pencere olur. Bu pencere bir zamanlama saldırısına izin verebilir. Örneğin, bu pencere sırasında bir. APK paketi değiştirilebilir. Intune,. apk 'nin Genel depolamada harcadığı süreyi en aza indirir ve imzasız uygulamaların yüklenmesine izin vermez. Güvenlik riskini en aza indirmenize yardımcı olmak için karşıya yüklediğiniz. apk dosyalarının hassas bilgiler içermediğinden emin olun.

## <a name="see-also"></a>Ayrıca bkz.

[Microsoft Intune’la uygulama ekleme](../apps/apps-add.md)

[İOS/ıpados kullanıcılarınızın uygulamalarını nasıl alır](end-user-apps-ios.md)

[Windows kullanıcılarınız uygulamalarını nasıl alır](end-user-apps-windows.md)
