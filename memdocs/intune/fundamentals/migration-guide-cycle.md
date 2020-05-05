---
title: Tipik bir Intune geçiş döngüsü nasıl gerçekleşir
titleSuffix: Microsoft Intune
description: Bu makalede, Microsoft Intune geçiş döngüsünün nasıl işlediği açıklanmakta ve bu döngüleri nasıl idare edebileceğinize dair örnekler verilmektedir.
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
ms.assetid: 3688b724-9521-4210-bf4d-bcf47d8d4ca0
ms.reviewer: dagerrit
ms.suite: ems
search.appverid: MET150
ms.collection: M365-identity-device-management
ms.openlocfilehash: cdef53672c46fe4e49a5d21a22e585654c504f03
ms.sourcegitcommit: 1442a4717ca362d38101785851cd45b2687b64e5
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 04/23/2020
ms.locfileid: "82075957"
---
# <a name="typical-migration-cycle"></a>Tipik geçiş döngüsü

Bir kuruluşun, BT departmanında kullanıcılarının bir alt kümesini hedefleyerek küçük bir pilot ile Intune geçişini başlatması yaygındır. Ayrıca, kuruluşunuz, geçiş zaman çerçevesini belirlemede yardımcı olmak üzere değişiklik, Kullanıcı sayısı, karmaşıklık, gereksinimler, konum ve iş riski gibi faktörlerin bu tür faktörleri tartışmasına gerek duyar.

Hedef gruplarınızın nasıl zamanlanabileceği hakkında bir örnek aşağıda verilmiştir:

  | **Geçiş hedeflenen gruplar** | **Dönem 1** | **Dönem 2** | **Dönem 3** | **Dönem 4** | **...**
|:---:|:---:|:---:|:---:|:---:|:---:|
| Sınırlı Pilot BT kuruluşu (50 kullanıcı) | Planı Duyurma | Kayıt talimatı verme | Son tarih verme | Koşullu erişimi zorlama |  |                                                        
| Genişletilmiş Pilot BT kuruluşu (200 kullanıcı) |  | Planı Duyurma | Kayıt talimatı verme | Son tarih verme | Koşullu erişimi zorlama |
| Geçiş aşaması 1 Teknik bilgiye sahip kullanıcılar (2000) |  |  | Planı Duyurma | Kayıt talimatı verme | Son tarih verme |
| Geçiş aşaması 2 Doğu ABD |  |  |  | Planı Duyurma | Kayıt talimatı verme |
| Tüm Bölgeler |  |  |  |  | Planı Duyurma |

## <a name="customer-migration-case-study"></a>Müşteri geçişi örnek olay incelemesi

### <a name="adatum-corporation"></a>Adatum Corporation

[Adatum Corporation’ın bir üçüncü taraf MDM sağlayıcısından Intune'a geçiş sürecini](https://gallery.technet.microsoft.com/Intune-migration-guide-893a95e3?redir=0) inceleyin.

## <a name="monitoring-migration"></a>Geçiş izleme

Intune, geçişi izleyebilmenizi sağlayan çeşitli yollar sunar:

* Intune kullanıcı grubu görünümleri

* Yerleşik raporlar kümesi

* Konsol içi uyarılar

Her aşamadan sonra kaç kullanıcının cihazlarını kaydettiğini izleyerek şunları yapabilirsiniz:

- İletişim planınızın verimliliğini değerlendirmek.

- Koşullu erişim zorlama etkisini tahmin edin.


## <a name="post-migration"></a>Geçiş sonrası

Intune'a geçtikten sonra önceki MDM sağlayıcısını devre dışı bırakın ve hizmet aboneliğinizi bitirin. Ayrıca, MDM sağlayıcısının yönergelerini izleyerek gereksiz altyapı gereksinimlerini kaldırın.
