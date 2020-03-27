---
title: Microsoft Intune-Azure 'da değişiklik ve olayları denetleme | Microsoft Docs
description: Microsoft Intune etkinliklerinin kaydedildiği denetim günlüklerini gözden geçirmeyi öğrenin.
keywords: ''
ms.author: dougeby
author: dougeby
manager: dougeby
ms.date: 03/18/2019
ms.topic: troubleshooting
ms.service: microsoft-intune
ms.subservice: fundamentals
ms.localizationpriority: medium
ms.technology: ''
ms.assetid: 6ee841cc-5694-4ba1-8f66-1d58edec30a4
search.appverid: MET150
ms.collection: M365-identity-device-management
ms.openlocfilehash: 5b271c05f71cdd166533d837e46c1396bf66c06c
ms.sourcegitcommit: e2567b5beaf6c5bf45a2d493b8ac05d996774cac
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/27/2020
ms.locfileid: "80326723"
---
# <a name="use-audit-logs-to-track-and-monitor-events-in-microsoft-intune"></a>Microsoft Intune olayları izlemek ve izlemek için Denetim günlüklerini kullanma

Denetim günlükleri, Microsoft Intune değişiklik üreten etkinliklerin bir kaydını içerir. Yöneticilerin çoğu Intune iş yükleri için gözden geçirebileceği denetim olayları oluşturma, güncelleştirme (düzenleme), silme, atama ve uzak eylemleri. Varsayılan olarak, tüm müşteriler için denetim etkindir. Devre dışı bırakılamaz.

> [!NOTE]
> Denetim olayları, Aralık 2017 özelliği sürümünde kaydetmeye başladı. Önceki olaylar kullanılamıyor.

## <a name="who-can-access-the-data"></a>Verilere kimler erişebilir?

Aşağıdaki izinlere sahip kullanıcılar denetim günlüklerini gözden geçirebilir:

- Genel Yönetici
- Intune Hizmet Yöneticisi
- **Denetim verileri** - **Okuma** izinlerine sahip bir Intune rolüne atanmış olan yöneticiler

## <a name="audit-logs-for-intune-workloads"></a>Intune iş yükleri için denetim günlükleri

İzleme grubundaki denetim günlüklerini her Intune iş yükü için gözden geçirebilirsiniz:

1. [Microsoft Endpoint Manager Yönetim merkezinde](https://go.microsoft.com/fwlink/?linkid=2109431)oturum açın.
2. **Denetim günlükleri** > **Kiracı Yönetimi** ' ni seçin.
3. Sonuçları filtrelemek için, **filtre** ' yi seçin ve aşağıdaki seçenekleri kullanarak sonuçları daraltın.
    - **Kategori**: **Uyumluluk**, **cihaz**ve **rol**.
    - **Etkinlik**: burada listelenen seçenekler **Kategori**altında seçilen seçenekle kısıtlıdır.
    - **Tarih aralığı**: önceki ay, hafta veya güne ait günlükleri seçebilirsiniz.
4. **Uygula**'yı seçin.
4. Etkinlik ayrıntılarını görmek için listeden bir öğe seçin.

## <a name="route-logs-to-azure-monitor"></a>Günlükleri Azure Izleyici 'ye yönlendirin

Denetim günlükleri ve işletimsel Günlükler de Azure Izleyici 'ye yönlendirilebilir. **Denetim günlükleri**' nde, **veri ayarlarını dışarı aktar**' ı seçin:

![Intune 'da veri ayarlarını dışarı aktar ' i seçerek günlük verilerini Azure izleyici 'ye aktarın](./media/monitor-audit-logs/audit-logs-export-data-settings.png)

> [!NOTE]
> Bu özellik hakkında daha fazla bilgi edinmek ve bunu kullanmak üzere önkoşulları gözden geçirmek için bkz. [depolama, Olay Hub 'ları veya Log Analytics 'e günlük verileri gönderme](review-logs-using-azure-monitor.md).

> [!NOTE]
> **Başlatan (aktör)** , görevi kimin çalıştırdığını ve nerede Çalıştırıldığın bilgilerini içerir. Örneğin, etkinliği Azure portal Intune 'da çalıştırırsanız, **uygulama** **Microsoft Intune Portal uzantısını** her zaman listeler ve **uygulama kimliği** her zaman aynı GUID 'yi kullanır.
>
> **Hedef (ler)** bölümünde birden çok hedef ve değiştirilen özellikler listelenir.  

## <a name="use-graph-api-to-retrieve-audit-events"></a>Denetim olaylarını almak için Graph API kullanma

Grafik API 'SI kullanımıyla ilgili ayrıntılar için, bir yıllık denetim olayları almak üzere bkz. [list auditEvents](https://docs.microsoft.com/graph/api/intune-auditing-auditevent-list?view=graph-rest-1.0).

## <a name="next-steps"></a>Sonraki adımlar

[Depolama, Olay Hub 'ları veya Log Analytics 'e günlük verilerini gönderin](review-logs-using-azure-monitor.md).

[İstemci uygulama koruma günlüklerini gözden geçirin](../apps/app-protection-policy-settings-log.md).