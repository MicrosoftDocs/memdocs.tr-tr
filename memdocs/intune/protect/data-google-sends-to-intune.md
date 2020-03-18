---
title: Google’ın Intune’a gönderdiği veriler
titleSuffix: Microsoft Intune
description: Google’ın Intune’a gönderdiği verilerin listesi.
keywords: ''
author: ErikjeMS
ms.author: erikje
manager: dougeby
ms.date: 04/18/2018
ms.topic: conceptual
ms.service: microsoft-intune
ms.subservice: protect
ms.localizationpriority: high
ms.technology: ''
ms.assetid: c379c8db-788a-454e-9098-665ea3bc7b56
ms.reviewer: ''
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: f218ffd5d11e800588000e8b24aa81a7554b7051
ms.sourcegitcommit: 3d895be2844bda2177c2c85dc2f09612a1be5490
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/13/2020
ms.locfileid: "79329466"
---
# <a name="data-google-sends-to-intune"></a>Google’ın Intune’a gönderdiği veriler

[!INCLUDE [azure_portal](../includes/azure_portal.md)]

Bir cihazda Android kurumsal cihaz yönetimi etkinleştirildiğinde Microsoft Intune, Google ve kullanıcıyla bir bağlantı kurar ve cihaz bilgileri, Intune ve Google arasında paylaşılır. Microsoft Intune’un bağlantı kurabilmesi için önce bir Google hesabı oluşturmanız gerekir.

Aşağıdaki tabloda, bir cihazda cihaz yönetimi etkinleştirildiğinde Google’ın Intune’a gönderdiği veriler listelenmiştir:


| Google’ın Intune’a gönderdiği veriler | Ayrıntılar | Kullanım alanı: | Örnek |
|:---:|:---:|:---:|:---:|
| Kurumsal veriler | Müşterinin Google’daki kuruluş tanımlayıcıları. | Intune ve Google arasında müşteri bilgileriyle ilgili bağlantı kurar. | **enterpriseId** örnek: LC04eik8a6.<br>**Ad**. Android kurumsal yapılandırılırken girilen Yönetici adı. Örnek: Joe Smith.<br>**Yönetici e-postası**. Android kurumsal yapılandırılırken kullanılan YourAdmin@gmail.com. |
| Uygulama verileri | Yönetilen Play Store uygulamaları için veriler. | Uygulamayı kullanılabilir veya gerekli olarak kullanıcılara veya cihazlara hedefler. | **Uygulama Adı** örnek: Contoso Ambar Envanteri Uygulaması.<br>**Uygulamayı temsil eden Benzersiz Tanımlayıcı** örnek: app:com.Contoso.Warehouse.InventoryTracking |
| Hizmet hesabı | Belirli müşteri çağrılarında kullanılacak benzersiz dahili Google hizmet hesabı. | Müşteri adına Google’a çağrı yapmak için kullanılır (uygulama, cihaz vb. görüntülemek için) | **Ad** örnek: InternalAccount@InternalService.com.<br>**Anahtarlar** örnek: ServiceAccountPassword |


Microsoft Intune ile Android kurumsal cihaz yönetimini kullanmayı bırakmak ve verileri silmek için hem Microsoft Intune Android kurumsal cihaz yönetimini devre dışı bırakmanız hem de Google hesabınızı silmeniz gerekir. Hesap yönetimini nasıl gerçekleştireceğinizi görmek için Google hesabına bakın.


