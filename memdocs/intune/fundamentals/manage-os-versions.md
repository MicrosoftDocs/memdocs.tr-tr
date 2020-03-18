---
title: Microsoft Intune ile işletim sistemi sürümlerini yönetme
titleSuffix: Microsoft Intune
description: Microsoft Intune ile platformlar arasında işletme sistemlerini nasıl yöneteceğinizi öğrenin.
keywords: ''
author: brenduns
ms.author: brenduns
manager: dougeby
ms.date: 01/02/2019
ms.topic: conceptual
ms.service: microsoft-intune
ms.subservice: fundamentals
ms.localizationpriority: high
ms.assetid: 361ef17b-1ee0-4879-b7b1-d678b0787f5a
search.appverid: MET150
ms.collection: M365-identity-device-management
ms.openlocfilehash: c25a40d288b643c289c05322e3e2d4677afb0b60
ms.sourcegitcommit: 3d895be2844bda2177c2c85dc2f09612a1be5490
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/13/2020
ms.locfileid: "79332450"
---
# <a name="manage-operating-system-versions-with-intune"></a>Intune ile işletim sistemi sürümlerini yönetme
Modern mobil ve masaüstü platformlarda önemli güncelleştirmeler, düzeltme ekleri ve yeni sürümler sık sık yayınlanır. Windows üzerinde güncelleştirmeleri ve düzeltme eklerini tamamen yönetmek için denetimlerinizi vardır, ancak iOS/ıpados ve Android gibi diğer platformlar, son kullanıcılarınızın işleme katılmasını gerektirir.  Microsoft Intune, farklı platformlarda işletim sistemi sürümü yönetiminizi yapılandırmak için farklı işlevlere sahiptir.

Intune, şu yaygın senaryolarda size yardımcı olabilir: 
- Son kullanıcı cihazlarınızda hangi işletim sistemi sürümlerinin olduğunu belirleme
- Yeni bir işletim sistemi sürümünü doğrularken kuruluş verilerine erişimi denetleme
- Son kullanıcıların, kuruluş tarafından onaylanmış son işletim sistemi sürümüne yükseltmelerini teşvik etme/gerekli kılma
- Yeni bir işletim sistemi sürümünün tüm kuruluşa sunulmasını yönetme
  
## <a name="operating-system-version-control-using-intune-mobile-device-management-mdm-enrollment-restrictions"></a>Intune mobil cihaz yönetimi (MDM) kayıt kısıtlamaları ile işletim sistemi sürüm denetimi
Intune MDM kayıt kısıtlamaları, cihazların kaydına izin vermeden önce istemci cihaz gereksinimlerini belirlemenize olanak tanır. Amaç, son kullanıcılarınızın kuruluş kaynaklarına erişim kazanmadan önce yalnızca uyumlu cihazları kaydetmesini gerektirmektir. Cihaz gereksinimleri, desteklenen platformlar için izin verilen en düşük ve en yüksek işletim sistemi sürümlerini içerir.

![Platform yapılandırma kısıtlamaları dikey penceresi](./media/manage-os-versions/os-version-platform-configurations.png)

### <a name="in-practice"></a>Uygulama

Kuruluşlar, aşağıdaki ayarları kullanarak kuruluş kaynaklarına erişimi denetlemek için cihaz türü kısıtlamalarını kullanır:

1. Kuruluşunuzda son kullanıcıların geçerli ve desteklenen platformları kullanmasını sağlamak için en düşük işletim sistemi sürümünü kullanın.
2. En yüksek işletim sistemini belirtmeyin (sınırsız) veya yeni işletim sistemi sürümlerinin dahili olarak sınanmasına izin vermek için en son doğrulanmış sürüme ayarlayın.

Ayrıntılar için bkz. [Cihaz türü kısıtlamaları ayarlama](../enrollment/enrollment-restrictions-set.md#create-a-device-type-restriction).

## <a name="operating-system-version-reporting-and-compliance-with-intune-mdm-device-compliance-policies"></a>İşletim sistemi sürüm raporlama ve Intune MDM cihaz uyumluluk ilkeleriyle uyumluluk

Intune MDM cihaz uyumluluk ilkeleri size aşağıdaki araçları sağlar:

- Uyumluluk kurallarını belirtme
- Raporlama ile uyumluluk durumunu görüntüleme
- Cihaz karantina ve koşullu erişim aracılığıyla uyumsuzluk üzerinde işlem yapın

Kayıt kısıtlamalarına benzer şekilde cihaz uyumluluk ilkeleri de en düşük ve en yüksek işletim sistemi sürümlerini içerir. İlkeler ayrıca, kullanıcılarınızın cihazlarını uyumlu hale getirmeleri için mehil süresi sağlamak amacıyla bir uyumluluk zaman çizelgesi içerir. Cihaz uyumluluk ilkeleri, kayıtlı son kullanıcı cihazlarınızı kuruluş ilkesiyle uyumlu tutar.

![Cihaz uyumluluğu - uyumsuz cihazlar için eylemler](./media/manage-os-versions/os-version-actions-noncompliance.png)

### <a name="in-practice"></a>Uygulama
Kuruluşlar, cihaz uyumluluk ilkelerini kayıt kısıtlamaları ile aynı senaryolar için kullanır. Bu ilkeler kullanıcıların kuruluşunuzdaki geçerli, doğrulanmış işletim sistemlerini kullanmalarını sağlar. Son Kullanıcı cihazlarının uyumsuz olduğu durumlarda, son kullanıcılar kuruluşunuz için desteklenen işletim sistemi aralığı içinde olana kadar, koşullu erişim aracılığıyla kurumsal kaynaklara erişim engellenebilir. Son kullanıcılar, uyumlu olmadıklarına dair bir ileti alır ve erişimi yeniden kazanmak için gerekli adımlar onlara sağlanır.   

Ayrıntılar için bkz. [Cihaz uyumluluğuna başlama](../protect/device-compliance-get-started.md).
 
## <a name="operating-system-version-controls-using-intune-app-protection-policies"></a>Intune uygulama koruma ilkelerini kullanarak işletim sistemi sürüm denetimleri    
Intune uygulama koruma ilkeleri ve mobil uygulama yönetimi (MAM) erişim ayarları, uygulama katmanında en düşük işletim sistemi düzeyini belirtmenize imkan verir. Böylece son kullanıcılarınızın işletim sistemlerini belirtilen bir en düşük sürüme güncelleştirmelerini teşvik edebilir veya gerekli kılabilirsiniz.
 
İki farklı seçeneğiniz vardır: 
- **Uyarı** -uyar, son kullanıcıya, belirtilen sürümün altında işletim sistemi sürümü olan bir cihazda uygulama koruma ILKESI veya mam erişim ayarları içeren bir uygulama açtıklarında yükseltme olmaları gerektiğini bildirir. Uygulama ve kuruluş verileri için erişime izin verilir.
  Android güncelleştirme Uyarısı iletişim kutusunun ![görüntüsü](./media/manage-os-versions/os-version-update-warning.png) 

- **Block** Block, son kullanıcıya, belirtilen sürümün altında işletim sistemi sürümü olan bir cihazda uygulama koruma ILKESI veya mam erişim ayarları içeren bir uygulama açtıklarında yükseltmeleri gerektiğini bildirir. Uygulama ve kuruluş verileri için erişime izin verilmez.
  Uygulama erişimi engellendi iletişim kutusunun ![görüntüsü](./media/manage-os-versions/os-version-access-blocked.png)

### <a name="in-practice"></a>Uygulama
Günümüzde kuruluşlar, uygulama koruma ilkesi ayarlarını uygulamalar açıldığında veya devam ettirildiğinde, uygulamaları güncel tutmaları konusunda son kullanıcıları eğitmek amacıyla kullanır. Örnek yapılandırma: Son kullanıcıların sürümleri güncel sürümün bir altı olduğunda uyarılır ve güncel sürümün iki altı olduğunda engellenir.
 
Ayrıntılar için bkz. [Uygulama koruma ilkeleri oluşturma ve atama](../apps/app-protection-policies.md).

## <a name="managing-a-new-operating-system-version-rollout"></a>Yeni bir işletim sistemi sürümü dağıtımını yönetme
Belirlediğiniz zaman çizelgesi içinde kuruluşunuzu yeni bir işletim sistemi sürümüne geçirmenize yardımcı olması için bu makaledeki Intune işlevlerini kullanabilirsiniz. Aşağıdaki adımlar, kullanıcılarınızı yedi gün içinde işletim sistemi v1’den işletim sistemi v2’ye taşımanız için örnek bir dağıtım modeli sağlar.
- **Adım 1**: Cihaz kaydı için işletim sistemi v2’yi en düşük sürüm olarak gerektirmek amacıyla kayıt kısıtlamalarını kullanın. Böylece kayıt zamanında yeni son kullanıcı cihazlarının uyumlu olması sağlanır.
- **Adım 2a**: Kullanıcılar uygulamayı açtığında veya devam ettirdiğinde işletim sistemi v2’nin gerekli olduğu konusunda uyarı almaları için Intune uygulama koruma ilkelerini kullanın.
- **Adım 2b:** . Cihazın uyumlu olması için işletim sistemi v2’yi en düşük sürüm olarak belirtmek amacıyla cihaz uyumluluk ilkelerini kullanın. Uyumsuzluk durumunda yedi günlük bir mehil süresi sağlamak ve kullanıcılara zaman çizelgeniz ile gereksinimlerinize dair bir e-posta bildirimi göndermek için **Eylemler**’i kullanın.
  - Bu ilkeler, uygulama koruma ilkesi etkin uygulamalar açıldığında mevcut cihazların Intune Şirket Portalı yoluyla güncelleştirilmesi gerektiği konusunda son kullanıcıları bilgilendirir.
  - Uyumsuz cihazlara sahip kullanıcıları belirlemek için bir uyumluluk raporu çalıştırabilirsiniz. 
- **Adım 3a**: Cihaz, işletim sistemi v2 kullanmıyorsa bir uygulama açıldığında veya devam ettirildiğinde kullanıcıları engellemek için Intune uygulama koruma ilkelerini kullanın.
- **Adım 3b**: Cihazın uyumlu olması için işletim sistemi v2’yi en düşük sürüm olarak belirtmek amacıyla cihaz uyumluluk ilkelerini kullanın.
  - Bu ilkeler, kuruluş verilerine erişimi sürdürmeleri için cihazların güncelleştirilmesini gerektirir. Korunan hizmetler, cihaz koşullu erişimiyle kullanıldığında engellenir. Açıldıklarında veya kuruluş verilerine eriştiklerinde uygulama koruma ilkesi etkin uygulamalar engellenir.

## <a name="next-steps"></a>Sonraki adımlar

Kuruluşunuzda işletim sistemi sürümlerini yönetmek için aşağıdaki kaynakları kullanın:

- [Cihaz türü kısıtlamalarını ayarlama](../enrollment/enrollment-restrictions-set.md#create-a-device-type-restriction)
- [Cihaz uyumluluğuna başlama](../protect/device-compliance-get-started.md)
- [Uygulama koruma ilkeleri oluşturma ve atama](../apps/app-protection-policies.md)
