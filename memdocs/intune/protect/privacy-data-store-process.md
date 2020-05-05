---
title: Intune’da veri depolama ve işleme
titleSuffix: Microsoft Intune
description: Intune’da kişisel verilerin nasıl depolanıp işlendiğini öğrenin.
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
ms.assetid: edb07842-6a16-482e-8c1d-541a29e169a8
ms.reviewer: angerobe
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: 9bb40b21d9a257586bbd38d24b2e9b6b0a9f8ce3
ms.sourcegitcommit: 1442a4717ca362d38101785851cd45b2687b64e5
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 04/23/2020
ms.locfileid: "82079544"
---
# <a name="data-storage-and-processing-in-intune"></a>Intune’da veri depolama ve işleme

Intune [verileri topladıktan](privacy-data-collect.md) sonra, verilerin depolanması ve işlenmesi aşağıda ayrıntılı olarak açıklanmıştır.

## <a name="storing-personal-data"></a>Kişisel verileri depolama

Toplanan ve telemetri olmayan tüm veriler, Intune hizmetinde işlenir ve aşağıdaki depolama konumlarından bir veya birkaçında depolanır: 

- SQLAzure 
- Güvenilir Koleksiyonlar (Service Fabric)  
- Azure Storage 

İzleme için anahtar olan telemetri (hizmet günlükleri, performans günlükleri, hatalar vb.) Microsoft 'un telemetri veri depolarına gönderilir.

### <a name="storage-locations"></a>Depolama konumları

Microsoft, Intune hizmetlerini dünya çapında birçok bölgede sunmakta ve yönetmektedir. Intune, yönetici tarafından Müşteri Verileri için yapılan depolama konumu seçimlerine saygı duyar.

Daha fazla bilgi için bkz. [verilerinizin nerede bulunduğu](https://www.microsoft.com/trust-center/privacy/data-location) yer.

### <a name="personal-data-retention"></a>Kişisel verilerin saklanması

Genel olarak, kişisel veriler, Kullanıcı Intune yönetiminden kaldırıldıktan sonra 30 gün boyunca Intune tarafından korunur.

Intune kullanımının bir parçası olarak toplanan telemetri verileri en fazla 30 gün boyunca tutulur.

Denetim günlükleri ise bir sene boyunca saklanabilir.

## <a name="processing-personal-data"></a>Kişisel verilerin işlenmesi

Intune, kişisel verileri ISO sertifikalı sistemlerle işler. Daha fazla bilgi için bkz. [Hizmet Güveni Portalı](https://www.microsoft.com/en-us/TrustCenter/stp).

### <a name="profiling-and-marketing"></a>Profil oluşturma ve pazarlama

Microsoft Intune, hizmet sağlama işleminin parçası olarak toplanan hiçbir kişisel veriyi profil oluşturma veya pazarlama amacıyla kullanmaz. 

### <a name="restrict-processing-of-personal-data"></a>Kişisel verilerin işlenmesini kısıtlama

Bir kullanıcının kişisel verilerinin işlenmesini kısıtlamak için, kullanıcılar hesabını şu şekilde silebilirsiniz:
1. Kullanıcının aşağıdakiler dahil olmak üzere kişisel verilerinin elektronik kopyasını dışarı aktararak
    - accounts
    - hizmet verileri
    - ilişkili günlükler
2. Kullanıcının hesabı ve Intune 'dan ilişkili veriler siliniyor.

## <a name="next-steps"></a>Sonraki adımlar

Intune’un verileri nasıl [güvenlik altına aldığı ve paylaştığı](privacy-data-secure-share.md) hakkında daha fazla bilgi edinin. 
