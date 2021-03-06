---
title: Microsoft Intune - Azure’daki Windows 8.1 uyumluluk ilkeleri | Microsoft Docs
description: Microsoft Intune Windows 8.1 için uyumluluk ayarlarken kullanabileceğiniz tüm ayarların listesini görüntüleyin. İşletim sistemi alt ve üst sınırı uyumluluğunu denetleyin, parola kısıtlamalarını ve uzunluğunu belirleyin, veri depolama alanında şifrelemeyi etkinleştirin ve çok daha fazlasını yapın.
keywords: ''
author: brenduns
ms.author: brenduns
manager: dougeby
ms.date: 08/14/2020
ms.topic: reference
ms.service: microsoft-intune
ms.subservice: protect
ms.localizationpriority: medium
ms.technology: ''
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: 9b423d289e81c48479adcaa7a594974b23a9476c
ms.sourcegitcommit: cb12dd341792c0379bebe9fd5f844600638c668a
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/15/2020
ms.locfileid: "88252716"
---
# <a name="windows-81-settings-to-mark-devices-as-compliant-or-not-compliant-using-intune"></a>Intune'u kullanarak cihazları uyumlu veya uyumlu değil şeklinde işaretlemek için kullanabileceğiniz Windows 8.1 ayarları

[!INCLUDE [windows-phone-81-windows-10-mobile-support](../includes/windows-phone-81-windows-10-mobile-support.md)]
Bu makalede Intune'daki Windows 8.1 cihazları için yapılandırabileceğiniz farklı uyumluluk ayarları listelenmekte ve anlatılmaktadır. Bu ayarları mobil cihaz yönetimi (MDM) çözümünüzün bir parçası olarak kullanarak basit parola kullanılmasını engelleyebilir, işletim sistemi için alt ve üst sınır belirleyebilir ve çok daha fazlasını yapabilirsiniz.

Bu özellik şu platformlarda geçerlidir:

- Windows 8.1 ve üzeri

Intune yöneticisi olarak bu uyumluluk ayarlarını kullanarak kuruluşunuzun kaynaklarının korunmasına yardımcı olabilirsiniz. Uyumluluk ilkeleri ve işlevleri hakkında daha fazla bilgi için bkz. [Cihaz uyumluluğunu kullanmaya başlama](device-compliance-get-started.md).

## <a name="before-you-begin"></a>Başlamadan önce

[Bir uyumluluk Ilkesi oluşturun](create-compliance-policy.md#create-the-policy). **Platform**için **Windows 8.1 ve üstünü**seçin.

## <a name="device-properties"></a>Cihaz Özellikleri

### <a name="operating-system-version"></a>İşletim Sistemi Sürümü

**Windows 8.1 ve üzeri**
- **En düşük işletim sistemi sürümü**:  
  İzin verilen en düşük sürümü girin. Bir cihaz en düşük işletim sistemi sürümü gereksinimini karşılamadığında uyumsuz olarak bildirilir. Yükseltme hakkında bilgi içeren bir bağlantı gösterilir. Cihaz kullanıcısı cihazlarını yükseltmeyi seçebilir ve ardından şirket kaynaklarına erişim alabilir.

- **En yüksek işletim sistemi sürümü**:  
  İzin verilen en yüksek sürümü girin. Bir cihaz, kurala girilen sürümden daha sonraki bir işletim sistemi sürümünü kullanırken, kuruluş kaynaklarına erişim engellenir. Cihaz kullanıcısına BT yöneticisine başvurması istenir. Cihaz, işletim sistemi sürümüne izin vermek için bir kural olana kadar kuruluş kaynaklarına erişemez.

Windows 8.1 bilgisayarları **3** sürümünü döndürür. Windows için işletim sistemi sürüm kuralı Windows 8.1’e ayarlanırsa, cihaz Windows 8.1’e sahip olsa bile uyumsuz olarak bildirilir.

## <a name="system-security"></a>Sistem Güvenliği

### <a name="password"></a>Parola

- **Mobil cihazların kilidini açmak için parola gerektir**:  
  - **Yapılandırılmadı** (*varsayılan*)-Bu ayar uyumluluk veya uyumsuzluk için değerlendirilmez.
  - **Gerektir** -kullanıcıların cihazına erişebilmeleri için önce bir parola girmesi gerekir.

- **Basit parolalar**:  
  - **Yapılandırılmadı** (*varsayılan*)-kullanıcılar, **1234** veya **1111**gibi basit parolalar oluşturabilir.
  - **Engelle** -kullanıcılar, **1234** veya **1111**gibi basit parolalar oluşturamaz.  

- **Minimum parola uzunluğu**:  
  Parolanın sahip olması gereken minimum rakam veya karakter sayısını girin.

  Windows çalıştıran ve bir Microsoft hesabı ile erişilen cihazlarda, aşağıdaki koşullardan biri karşılandığında uyumluluk ilkesi doğru şekilde değerlendirilemiyor:  
  - Minimum parola uzunluğu sekiz karakterden fazla
  - En az karakter kümesi sayısı ikiden büyük

- **Parola türü**:  
  Parolanın yalnızca **Sayısal** karakterlerden mi yoksa sayı ve diğer karakterlerin karışımından (**Alfasayısal**) mı oluşması gerektiğini seçin.

  *Alfasayısal*olarak ayarlandığında, aşağıdaki ayar kullanılabilir.  

  - **Paroladaki alfasayısal olmayan karakter sayısı**:  
    *Parola türü* **alfasayısal**olarak ayarlandığında, parolanın içermesi gereken karakter kümesi sayısı alt sınırını belirtin. Seçenekler **0** ile **4** küme arasındadır ve varsayılan değer **1**' dir.
    
    Dört karakter kümesi şunlardır:
    - Küçük harfler
    - Büyük harfler
    - Simgeleri
    - Sayılar

    Daha yüksek bir sayı ayarlanırsa kullanıcının daha karmaşık bir parola oluşturması gerekir. Microsoft hesabı ile erişilen cihazlarda, aşağıdaki koşullardan biri karşılandığında uyumluluk ilkesi doğru şekilde değerlendirilemiyor:

    - Minimum parola uzunluğu sekiz karakterden fazla
    - En az karakter kümesi sayısı ikiden büyük

- **Parola istenmeden önce geçmesi gereken, işlem yapılmayan dakika sayısı**:  
  Kullanıcı parolasını yeniden girmeden önce boşta geçen süreyi girin.

- **Parola kullanım süresi (gün)**:  
  Parolanın süresi dolmadan önce geçecek gün sayısını seçin ve kullanıcıların yeni bir tane oluşturması gerekir.

- **Yeniden kullanılması önlenecek önceki parola sayısı**:  
  Daha önce kullanılan kaç parolanın kullanılamayacağını belirtir.

### <a name="encryption"></a>Şifreleme

- **Cihazda veri depolamanın şifrelenmesi**:  
  - **Yapılandırılmadı** (*varsayılan*)
  - **Gerektir** -kullanım, cihazlarınızda veri depolamayı şifrelemek için *gerektir* .


<!-- not on phone   
- **Require encryption on mobile device**: **Require** the device to be encrypted to connect to data storage resources.
--> 

## <a name="next-steps"></a>Sonraki adımlar

- [Uyumlu olmayan cihazlara uygulanacak eylemleri ekleyin](actions-for-noncompliance.md) ve [ilkeleri filtrelemek için kapsam etiketlerini kullanın](../fundamentals/scope-tags.md).
- [Uyumluluk ilkelerinizi izleyin](compliance-policy-monitor.md).
- Bkz. [Windows 10 ve üzeri cihazlar için uyumluluk ilkesi ayarları](compliance-policy-create-windows.md).