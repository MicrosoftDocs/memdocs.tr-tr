---
title: iOS/ıpados cihaz uyumluluk ayarları Microsoft Intune-Azure | Microsoft Docs
description: Microsoft Intune ' de iOS/ıpados cihazlarınız için uyumluluk ayarlarken kullanabileceğiniz tüm ayarların listesini görüntüleyin. E-postayı zorunlu kılın, jailbreak uygulanmış veya kök erişim izni verilmiş cihazları denetleyin, izin verilene işletim sistemi alt ve üst sınırını ayarlayın, parola uzunluğu ve cihaz boş durma süresi dahil olmak üzere parola kısıtlaması ayarlayın, uygulamaları kısıtlayın ve daha fazlasını yapın.
keywords: ''
author: brenduns
ms.author: brenduns
manager: dougeby
ms.date: 07/20/2020
ms.topic: reference
ms.service: microsoft-intune
ms.subservice: protect
ms.localizationpriority: medium
ms.technology: ''
ms.assetid: 3cfb8222-d05b-49e3-ae6f-36ce1a16c61d
ms.reviewer: samyada
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: e57cd425ca89fa875b89c73a9eba30cecb7516d7
ms.sourcegitcommit: 2e0bc4859f7e27dea20c6cc59d537a31f086c019
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/21/2020
ms.locfileid: "86871925"
---
# <a name="iosipados-settings-to-mark-devices-as-compliant-or-not-compliant-using-intune"></a>Intune kullanarak cihazları uyumlu veya uyumsuz olarak işaretlemek için iOS/ıpados ayarları

Bu makalede, Intune 'da iOS/ıpados cihazlarında yapılandırabileceğiniz farklı uyumluluk ayarları listelenir ve açıklanmaktadır. Mobil cihaz yönetimi (MDM) çözümünüzün bir parçası olarak bu ayarları kullanabilir ve bu sayede e-posta kullanılmasını zorunlu kılabilir, kök erişim izni verilmiş (jailbreak uygulanmış) cihazları uyumlu değil olarak işaretleyebilir, izin verilen tehdit düzeyi belirleyebilir, parolaların kullanım süresini kısıtlayabilir ve çok daha fazlasını yapabilirsiniz.

Bu özellik şu platformlarda geçerlidir:

- iOS
- ıpados

Intune yöneticisi olarak bu uyumluluk ayarlarını kullanarak kuruluşunuzun kaynaklarının korunmasına yardımcı olabilirsiniz. Uyumluluk ilkeleri ve işlevleri hakkında daha fazla bilgi için bkz. [Cihaz uyumluluğunu kullanmaya başlama](device-compliance-get-started.md).

## <a name="before-you-begin"></a>Başlamadan önce

[Bir uyumluluk Ilkesi oluşturun](create-compliance-policy.md#create-the-policy). **Platform**için **IOS/ıpados**' ı seçin.

## <a name="email"></a>E-posta

- **Cihazda e-posta kurulamıyor**  
  - **Yapılandırılmadı** (*varsayılan*)-Bu ayar uyumluluk veya uyumsuzluk için değerlendirilmez.
  - **Gerektir** -yönetilen bir e-posta hesabı gereklidir. Kullanıcının cihazda zaten bir e-posta hesabı varsa, Intune 'un doğru bir şekilde ayarlayabilmesi için e-posta hesabının kaldırılması gerekir. Cihazda bir e-posta hesabı yoksa, kullanıcının yönetilen bir e-posta hesabını yapılandırmak için BT yöneticisiyle iletişim kurabilmesi gerekir.

  Aşağıdaki durumlarda cihaz uyumsuz olarak kabul edilir:  
  - E-posta profili, uyumluluk ilkesi tarafından hedeflenen kullanıcı grubu dışındaki bir kullanıcı grubuna atanmış.
  - Kullanıcı, cihaza dağıtılan Intune e-posta profiliyle eşleşen bir e-posta hesabını cihazda önceden ayarlamış. Intune, kullanıcı tarafından yapılandırılan profilin üzerine yazamaz ve onu yönetemez. Uyumluluk sağlamak için son kullanıcının mevcut e-posta ayarlarını kaldırması gerekir. Ardından, Intune yönetilen e-posta profilini yükleyebilir.  

E-posta profilleri hakkında ayrıntılı bilgi için bkz. [Intune ile e-posta profilleri kullanarak kuruluş e-postasına erişimi yapılandırma](../configuration/email-settings-configure.md).

## <a name="device-health"></a>Cihaz Sistem Durumu

- **Jailbreak uygulanmış cihazlar**  
  *İOS 8,0 ve üzeri için desteklenir*

  - **Yapılandırılmadı** (*varsayılan*)-Bu ayar uyumluluk veya uyumsuzluk için değerlendirilmez.
  - **Block** -root (Jailbreak uygulanmış) cihazlarını uyumsuz olarak işaretle.  

- **Cihazın cihaz tehdit düzeyinde veya altında olmasını gerektir**  
  *İOS 8,0 ve üzeri için desteklenir*

  Risk değerlendirmesini uyumluluk koşulu olarak kullanmak için bu ayarı etkinleştirin. İzin verilen tehdit düzeyini seçin:
  - **Yapılandırılmadı** (*varsayılan*)-Bu ayar uyumluluk veya uyumsuzluk için değerlendirilmez.
  - **Güvenli** -Bu seçenek en güvenli seçenektir ve cihazın herhangi bir tehdit olamayacağı anlamına gelir. Herhangi bir tehdit düzeyi algılanırsa cihaz uyumsuz olarak değerlendirilir.
  - **Düşük** -cihaz, yalnızca düşük düzeyde tehditler varsa uyumlu olarak değerlendirilir. Daha yüksek bir tehdit düzeyi, cihazı uyumlu değil durumuna getirir.
  - **Orta** -cihazda bulunan tehditler düşük veya orta düzeydeyse cihaz uyumlu olarak değerlendirilir. Yüksek düzeyde tehditler algılanırsa cihaz uyumsuz olarak değerlendirilir.
  - **Yüksek** -Bu seçenek, tüm tehdit düzeylerine izin verdiği için en az güvenli seçenektir. Bu çözüm, yalnızca raporlama amacıyla kullanıyorsanız kullanışlı olabilir.

## <a name="device-properties"></a>Cihaz Özellikleri

### <a name="operating-system-version"></a>İşletim Sistemi Sürümü  

- **En düşük işletim sistemi sürümü**  
  *İOS 8,0 ve üzeri için desteklenir*

  Bir cihaz en düşük işletim sistemi sürümü gereksinimini karşılamadığında uyumsuz olarak bildirilir. Yükseltme hakkında bilgi içeren bir bağlantı gösterilir. Son kullanıcı cihazını yükseltmeyi seçebilir. Bundan sonra, kuruluş kaynaklarına erişebilir.

- **En yüksek işletim sistemi sürümü**  
  *İOS 8,0 ve üzeri için desteklenir*

  Cihaz kuralda belirtilenden sonraki bir işletim sistemi sürümünü kullandığında, kuruluş kaynaklarına erişim engellenir. Son kullanıcıdan BT yöneticisine başvurması istenir. İşletim sistemine izin veren bir kural değişikliği oluncaya kadar bu cihaz kuruluş kaynaklarına erişemez.

- **En düşük işletim sistemi derleme sürümü**  
  *İOS 8,0 ve üzeri için desteklenir*

  Apple güvenlik güncelleştirmeleri yayımladığında genellikle işletim sistemi sürümü yerine derleme numarası güncelleştirilir. Bu özelliği kullanarak cihazda izin verilen en düşük işletim sistemi derleme sürümünü girebilirsiniz.

- **En yüksek işletim sistemi derleme sürümü*  
  *İOS 8,0 ve üzeri için desteklenir*

  Apple güvenlik güncelleştirmeleri yayımladığında genellikle işletim sistemi sürümü yerine derleme numarası güncelleştirilir. Bu özelliği kullanarak cihazda izin verilen en yüksek işletim sistemi derleme sürümünü girebilirsiniz.

## <a name="system-security"></a>Sistem Güvenliği

### <a name="password"></a>Parola

> [!NOTE]
> Bir iOS/ıpados cihazına uyumluluk veya yapılandırma ilkesi uygulandıktan sonra, kullanıcılardan 15 dakikada bir geçiş kodu ayarlaması istenir. Geçiş kodu ayarlanana kadar kullanıcılara sürekli bu istem gönderilir. İOS/ıpados cihazı için bir geçiş kodu ayarlandığında, şifreleme işlemi otomatik olarak başlatılır. Geçiş kodu devre dışı bırakılıncaya kadar cihaz şifreli olarak kalır.

- **Mobil cihazların kilidini açmak için bir parola gerektir**  
  - **Yapılandırılmadı** (*varsayılan*)-Bu ayar uyumluluk veya uyumsuzluk için değerlendirilmez.  
  - **Gerektir** -kullanıcıların cihazına erişebilmeleri için önce bir parola girmesi gerekir. parola kullanan iOS/ıpados cihazları şifrelenir.

- **Basit parolalar**  
  *İOS 8,0 ve üzeri için desteklenir*

  - **Yapılandırılmadı** (*varsayılan*)-kullanıcılar, **1234** veya **1111**gibi basit parolalar oluşturabilir.
  - **Engelle** -kullanıcılar, **1234** veya **1111**gibi basit parolalar oluşturamaz.

- **Minimum parola uzunluğu**  
  *İOS 8,0 ve üzeri için desteklenir*

  Parolanın sahip olması gereken minimum rakam veya karakter sayısını girin.

- **Gerekli parola türü**  
  *İOS 8,0 ve üzeri için desteklenir*

  Parolanın yalnızca **Sayısal** karakterlerden mi yoksa sayı ve diğer karakterlerin karışımından (**Alfasayısal**) mı oluşması gerektiğini seçin.

- **Paroladaki alfasayısal olmayan karakter sayısı**  
  Parolada bulunması gereken `&`, `#`, `%`, `!` gibi özel karakterlerin alt sınırını girin.

  Daha yüksek bir sayı ayarlanırsa kullanıcının daha karmaşık bir parola oluşturması gerekir.

- **Parola istenmeden önce ekran kilitlenmesinden sonra geçen en fazla dakika**  
  *İOS 8,0 ve üzeri için desteklenir*

  Kullanıcı cihaza erişmek için bir parola girmeden önce ekranın ne kadar süre sonra kilitlendiğini belirtin. Seçenekler, *Yapılandırılmadı*, *hemen*ve *1 dakikadan* *4 saate*kadar varsayılan değer içerir.

- **Ekran kilitlenmeden önce geçmesi gereken, işlem yapılmayan dakika sayısı**  
  Cihazın ekranını kilitlemeleri için boşta geçen süreyi girin. Seçenekler varsayılan olarak *yapılandırılmamış*, *hemen*ve *1 dakikadan* *15 dakikaya*dahildir.

- **Parola geçerlilik süresi (gün)**  
  *İOS 8,0 ve üzeri için desteklenir*

  Parolanın süresi dolup yeni bir parola oluşturulması gerekmeden önce geçmesi gereken gün sayısını seçin.

- **Yeniden kullanılmasını önleyen önceki parola sayısı**  
  *İOS 8,0 ve üzeri için desteklenir*

  Daha önce kullanılan kaç parolanın kullanılamayacağını belirtir.

### <a name="device-security"></a>Cihaz Güvenliği

- **Kısıtlanmış uygulamalar**  
  Uygulamaların paket kimliklerini ilkeye ekleyerek bunları kısıtlayabilirsiniz. Cihazda bu uygulama yüklüyse cihaz uyumsuz olarak işaretlenir.

  - **Uygulama adı** -paket kimliğini belirlemenize yardımcı olması için Kullanıcı dostu bir ad girin.
  - **Uygulama PAKETI kimliği** -uygulama sağlayıcısı tarafından atanan benzersiz paket kimliğini girin. Paket KIMLIĞINI bulmak için Support.apple.com adresindeki [Yerel iOS ve ıpados uygulamaları Için paket kimlikleri](https://support.apple.com/guide/mdm/native-ios-and-ipados-app-bundle-ids-mdm90f60c1ce/web) bölümüne bakın veya uygulamanın yazılım satıcısına başvurun.

## <a name="next-steps"></a>Sonraki adımlar

- [Uyumlu olmayan cihazlara uygulanacak eylemleri ekleyin](actions-for-noncompliance.md) ve [ilkeleri filtrelemek için kapsam etiketlerini kullanın](../fundamentals/scope-tags.md).
- [Uyumluluk ilkelerinizi izleyin](compliance-policy-monitor.md).
- Bkz. [macOS cihazları için uyumluluk ilkesi ayarları](compliance-policy-create-mac-os.md).
