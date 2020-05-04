---
title: Piyasaya çıkma ve zaman dilimleri için hedeflenen grupları belirleme
titleSuffix: Microsoft Intune
description: Bu makale, Microsoft Intune’a sunulacak gruplara ve bu dağıtımların zaman dilimlerine karar vermenize yardımcı olur.
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
ms.assetid: 3a63f78f-a7e7-4f44-9288-16b28d5d58ca
ms.reviewer: jeffbu, cgerth
ms.suite: ems
search.appverid: MET150
ms.custom: intune-classic
ms.collection: M365-identity-device-management
ms.openlocfilehash: 7aa18316ad1b4473ac70399e1370bfececadbfaf
ms.sourcegitcommit: 7f17d6eb9dd41b031a6af4148863d2ffc4f49551
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 04/21/2020
ms.locfileid: "79330974"
---
# <a name="develop-a-rollout-plan"></a>Dağıtım planı geliştirme

Piyasaya çıkma planınız Intune sunumunuz için hedeflemek istediğiniz kuruluş gruplarını, her grup için piyasaya çıkma zaman dilimini ve kullanacağımız kayıt yaklaşımlarını tanımlar.

## <a name="targeted-groups-and-timeframes"></a>Hedeflenen gruplar ve zaman dilimleri

İlk olarak, Intune sunumu ile hedeflenen grupları ve [kullanım örneği senaryolarınızda](planning-guide-scenarios.md) tanımladığınız grupları gözden geçirin.

İkinci olarak, hedeflenen her grup için zaman dilimini belirleyin. Genellikle bu görev, her grubun piyasaya çıkma zaman dilimini belirlemeye yardımcı olması için Intune dağıtım ekibi ve hedeflenen gruplar arasında iletişim kurulmasını gerektirir. Bu tür bir iletişimde yer alması gereken noktalar şunları içerir:
* Grubun değişiklik açısından bekleniyor
* Kullanıcı ve cihaz sayısı
* Cihaz platformları türleri
* Gereksinimler
* Coğrafi konum
* İş riski

## <a name="rollout-phases"></a>Dağıtım aşamaları
Kuruluşlar genellikle BT bölümündeki küçük bir kullanıcı grubunu hedefleyerek Intune dağıtımını ilk başta pilot olarak denemeyi tercih eder. Ardından pilot, daha kapsamlı bir BT kullanıcıları grubuna genişletilebilir ve diğer kuruluş gruplarından katılım sağlanabilir.

### <a name="pilot"></a>Pilot
Piyasaya çıkmanın ilk aşaması pilot kullanıcılara uygulanmalıdır. Pilot kullanıcılar, yeni bir çözümdeki ilk kullanıcılar olduklarını anlamalıdır. Yapılandırma, belgeleme, bildirimler gibi faktörleri iyileştirmek ve sonraki piyasaya çıkma aşamalarında diğer tüm kullanıcıların kullanımını kolaylaştırmak amacıyla geri bildirim sağlamaya istekli olmaları gerekir. Bu kullanıcılar, yöneticiler veya VIP olmamalıdır.

Pilot aşaması, daha önce toplanan [zorlukları](planning-guide-deployment-goals.md) sınamak ve [gereksinimleri](planning-guide-requirements.md) geliştirmek için iyi bir fırsattır.

[İletişim](planning-guide-communication-plan.md) planınızı, [destek](planning-guide-support-plan.md) planınızı ve [sınama ve doğrulama](planning-guide-test-validation.md) işlemlerinizi herhangi bir sorunu, kullanıcılara olan etkisi henüz azken çözmek için dahil edin.

### <a name="production-rollout"></a>Üretim piyasaya çıkma
Başarılı bir pilot işleminden sonra, kuruluşunuzun gruplarının geri kalanını hedefleyerek tam bir üretim dağıtımı başlatmaya hazırsınız demektir. Farklı piyasaya çıkma grupları ve aşamalarına bazı örnekler şunlardır:

- **Departmanlar** <br/>Her departman bir piyasaya çıkma aşaması olabilir. Tüm departmanı bir seferde hedeflersiniz. Bu piyasaya çıkma türünde, her departmandaki kullanıcılar büyük olasılıkla mobil cihazı aynı şekilde kullanır ve aynı uygulamalara erişir. Kullanıcılar, muhtemelen aynı türde ilkelere sahip olacaktır.

- **Coğrafya** <br/>Bu yaklaşımda, aynı kıta, ülke/bölge veya aynı şirketin Binası gibi belirli bir Coğrafya 'daki tüm kullanıcılara dağıtırsınız. Bu tür aşamalı dağıtım, kullanıcıların belirli konumuna odaklanma olanağı sağlar. Bu, Intune’un aynı anda dağıtıldığı konum sayısının azalmasıyla daha fazla [beyaz eldiven](#user-assisted-enrollment) yaklaşımına olanak tanıyabilir. Farklı departmanların veya kullanım örneklerinin aynı konumda olma olasılığından dolayı farklı kullanım örnekleri aynı anda dağıtılabilir.

- **Platform** <br/>Bu dağıtım türü aynı anda benzer platformları dağıtmaya dayalıdır. Örnek olarak, ilk ay, Android ve Windows tarafından izlenen tüm iOS/ıpados cihazları olabilir. Bu tür aşamalı dağıtımda yardım masasının aynı anda yalnızca tek bir platformu desteklemesi yeterli olacağından, yardım masası desteğini basitleştirmeye yardımcı olur.

Aşağıda hedeflenen grupları ve zaman çizelgelerini içeren bir Intune dağıtım planına örnek verilmiştir:

| **Dağıtım aşaması** | **Temmuz** | **Ağustos** | **Eylül** | **Ekim** |
|:---:|:---:|:---:|:---:|:---:|
| Sınırlı Pilot | BT (50 kullanıcı) |  |  |  |                                                         
| Genişletilmiş Pilot | BT (200 kullanıcı), BT Yöneticileri (10 kullanıcı) |  |  |  |                                                         
| Üretim dağıtım aşaması 1 |  | Satış ve Pazarlama (2000 kullanıcı) |  |  |
| Üretim dağıtım aşaması 2 |  |  | Perakende (1000 kullanıcı) |  |
| Üretim dağıtım aşaması 3 |  |  |  | İK (50 kullanıcı), Finans (40 kullanıcı), Yöneticiler (30 kullanıcı) |

Kuruluşunuzun dağıtım aşamalarını girmek için [Yukarıdaki tablonun bir şablonunu indirebilirsiniz](https://gallery.technet.microsoft.com/Intune-deployment-planning-fae156c2?redir=0) .
## <a name="match-rollout-groups-to-enrollment-approaches"></a>Kayıt yaklaşımlarının piyasaya çıkma gruplarına eşlenmesi

Artık Intune piyasaya çıkma için hedeflenen grupları ve zaman dilimlerini belirlediğinize göre, bir sonraki adım her grup için en uygun Intune kaydı yaklaşımını seçmektir. Aşağıdakileri içeren farklı kayıt yaklaşımları kullanabilirsiniz:
* Kullanıcı self servis
* Kullanıcı yardımlı kayıt
* BT teknik fuarı

### <a name="user-self-service"></a>Kullanıcı self servis

Bu durumda, kullanıcı genellikle BT departmanı tarafından sağlanan kayıt yönergelerini izleyerek kendi cihazını kaydetmekten sorumludur. Kuruluşlarda en yaygın olarak kullanılan yaklaşım budur ve ölçeklenebilirliği kullanıcı yardımlı kayıttan daha fazladır.

### <a name="user-assisted-enrollment"></a>Kullanıcı yardımlı kayıt

Bu, "beyaz eldiven" yaklaşımı olarak bilinir. Bir BT ekip üyesi kullanıcıya kayıt sürecinde yüz yüze veya Skype üzerinden yardımcı olur. Bu yaklaşım genellikle yönetim ekibi ve kayıt sürecinde daha fazla yardıma ihtiyaç duyan diğer gruplarda kullanılır.

### <a name="it-tech-fair"></a>BT teknik fuarı

Intune kullanıcı kaydı için başka bir seçenek de BT teknik fuarı düzenlemektir. Bu etkinlikte, BT grubu, kullanıcıların Intune kaydı hakkında bilgi alabileceği, sorular sorabileceği ve kayıt sürecine ilişkin yardım alabileceği bir Intune kayıt yardım standı kurar. Bu seçenek, özellikle Intune piyasaya çıkmasının ilk aşamalarında hem BT grubu hem de kullanıcı için yararlı olabilir.

Kayıt yaklaşımlarını eklemek için yukarıdaki Intune dağıtım planının güncelleştirilmiş bir örneği aşağıda verilmiştir:

| **Dağıtım aşaması** | **Temmuz** | **Ağustos** | **Eylül** | **Ekim** |
|:---:|:---:|:---:|:---:|:---:|
| Sınırlı Pilot |  |  |  |  |
| Self servis | BT |  |  |  |
| Genişletilmiş Pilot |  |  |  |  |
| Self servis | BT |  |  |  |
| Beyaz eldiven | BT Yöneticileri |  |  |  |
| Üretim dağıtım aşaması 1 |  | Satış, Pazarlama |  |  |
| Self servis |  | Satış ve Pazarlama |  |  |
| Üretim dağıtım aşaması 2 |  |  | Perakende |  |
| Self servis |  |  | Perakende |  |
| Üretim dağıtım aşaması 3 |  |  |  | Yöneticiler, ık, finans |
| Self servis |  |  |  | İK, Finans |
| Beyaz eldiven |  |  |  | Yöneticiler |

## <a name="next-steps"></a>Sonraki adımlar

Sonraki bölümde [bir Intune dağıtımı iletişim planı geliştirme](planning-guide-communication-plan.md) hakkında yönergeler sağlanır.
