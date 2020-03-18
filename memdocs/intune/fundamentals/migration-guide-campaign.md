---
title: Intune geçiş kampanyası başlatma
titleSuffix: Microsoft Intune
description: Bu makalede, bir Microsoft Intune geçiş işlemi başlatma hakkında yol gösterilmektedir.
keywords: ''
author: dougeby
ms.author: dougeby
manager: dougeby
ms.date: 01/02/2018
ms.topic: conceptual
ms.service: microsoft-intune
ms.subservice: fundamentals
ms.localizationpriority: high
ms.technology: ''
ms.assetid: f781b029-50f2-46ee-8ff7-03b4a6719e80
ms.reviewer: dagerrit
ms.suite: ems
search.appverid: MET150
ms.collection: M365-identity-device-management
ms.openlocfilehash: 11959de1d03c7aa9cd29de2b4069c6d7bc133f79
ms.sourcegitcommit: 3d895be2844bda2177c2c85dc2f09612a1be5490
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/13/2020
ms.locfileid: "79331282"
---
# <a name="phase-2-migration-campaign"></a>2\. Aşama: Geçiş işlemi

Kuruluşunuzun gereksinimlerinize en uygun geçiş yaklaşımını seçin ve uygulama taktiklerini özel gereksinimlerinize göre ayarlayın. Bu rehberin geri kalanında kullanıcılarınızın cihazlarını Intune’a kaydetme amacına ulaşmanız için gereken araçlar sağlanacaktır.

## <a name="keys-to-a-successful-migration"></a>Başarılı bir geçişin önemli noktaları

Bir üçüncü taraf MDM sağlayıcısından Intune’a geçişin olmazsa olmazları şöyledir:

- Açık bir iletişim ile yardım yoluyla son kullanıcı kesinti süreleri ve memnuniyetsizliği en aza indirgenir.

- Belirli ve somut geçiş yönergeleriniz olduğundan emin olun.

- Intune’a kayıt öncesinde tüm yönetilen cihazların mevcut MDM sağlayıcısındaki kayıtları silinmelidir.

- Son kullanıcılara cihazlarının kaydını nasıl kaldıracakları konusunda mevcut MDM sağlayıcınızdan yönergeler sağlayın.

- Aşamalı bir yaklaşım kullanın. Küçük bir pilot kullanıcı grubu kullanın ve tam ölçekli dağıtıma ulaşana kadar aşamalı olarak daha fazla kullanıcı grubu ekleyin.

- Her döngünün yardım masası yükünü ve kayıt başarısını izleyin. Her grup için başarı ölçütlerinin bir sonrakine geçmeden önce değerlendirilmesini sağlamak için zaman çizelgesinde süre bırakın. Pilot dağıtımınız aşağıdakileri doğrulamalıdır:

  - Kayıt başarı ve başarısızlık hızları beklentiler dahilindedir.

  - Kullanıcı üretkenliği:

    - VPN, Wi-Fi, e-posta ve sertifikalar gibi şirket kaynakları çalışır durumdadır.

    - Sağlanan uygulamalara erişilebilir.

  - Veri güvenliği:

    - Uyumluluk raporlaması yapılıyor.

    - Mobil uygulama korumaları uygulanıyor.

Geçişin ilk aşamasını tamamladıktan sonra, gelecek aşama için [geçiş döngüsünü](migration-guide-cycle.md) yineleyin.

- Tüm kullanıcılar Intune’a geçirilene kadar aşamalı döngüleri yineleyin.

- Yardım masası ekibinin, geçiş süreci boyunca son kullanıcıları desteklemeye hazır olduğundan emin olun. Destek çağrısı iş yükünü tahmin edebilene kadar gönüllü bir geçiş çalıştırın.

- Yardım masası, kalan kullanıcı sayısıyla başa çıkabilecek duruma gelene kadar kayıt için bir son tarih belirlemeyin

> [!IMPORTANT]
> Exchange veya SharePoint Online gibi kaynaklara erişim denetimleri uygulamak için hem Intune hem de mevcut üçüncü taraf MDM çözümünüzü yapılandırmayın. Ayrıca, cihazların aynı anda yalnızca bir çözüme kayıtlı olması gerekir.

## <a name="next-steps"></a>Sonraki adımlar

[İletişim planınızı](migration-guide-communication-plan.md) oluşturun.
