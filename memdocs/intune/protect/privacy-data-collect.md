---
title: Intune’da veri toplama
titleSuffix: Microsoft Intune
description: Intune’da kişisel verilerin nasıl toplandığını öğrenin.
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
ms.assetid: d1171740-936d-46a5-af37-f418bd6fa63e
ms.reviewer: angerobe
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: e986a6dcb598a11a0f2906d6d7be8e2e1abb6aba
ms.sourcegitcommit: 3d895be2844bda2177c2c85dc2f09612a1be5490
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/13/2020
ms.locfileid: "79329122"
---
# <a name="data-collection-in-intune"></a>Intune’da veri toplama

Kullanıcılar Intune kullanarak şirkete ait veya kişisel cihazlarını kaydettiklerinde, Intune bazı kişisel verileri toplar ve paylaşır. Intune, kişisel verileri aşağıdaki kaynaklardan toplar:

- Yöneticinin Azure portalında Intune kullanımı.
- Son kullanıcı cihazları (Intune yönetimine kaydolduklarında ve Intune kullanımı sırasında).
- Üçüncü taraf hizmetlerdeki müşteri hesapları (yöneticinin yönergelerine göre).
- Tanılama, performans ve kullanım bilgileri.

Intune bu kaynaklardan bilgileri şu üç kategori altında toplar: [tanımlanan](#identified-data), [takma ad kullanılan](#pseudonymized-data) ve [toplam](#aggregated-data).

> [!NOTE]
> Her nedenden dolayı hizmetimizin tarafından toplanan herhangi bir veriyi üçüncü taraflardan satmayacağız.

## <a name="identified-data"></a>Tanımlanan veriler

Intune tarafından toplanan kişisel verilerin çoğu tanımlanan verilerdir. Bu tür veriler bir kullanıcı, cihaz veya uygulamaya bağlıdır ve yönetimin yapısı gereği gereklidir. Tanımlanan veriler, bir kullanıcının cihaz ve uygulamalarını yönetmek ve Intune hizmetini sağlamak için kullanılır.

Intune tarafından toplanan tanımlanan veriler şunları içerebilir ancak bu kadarla sınırlı değildir: 

- Kullanıcı bilgileri
  - Sahip adı/kullanıcı görünen adı (kullanıcının Azure’da kayıtlı ve theAzureUserID olarak tanımlanan adı)
  - Kullanıcı Asıl Adı veya e-posta adresi
  - Üçüncü taraf kullanıcı tanımlamaları (AppleID gibi)
- Donanım envanteri bilgileri
  - Cihaz adı
  - Üretici
  - İşletim sistemi
  - Seri numarası
  - IMEI numarası
  - IP adresi
  - Wi-Fi MacAddress
  - ICCID
  - Telefon numarası
- Aşağıdaki etkinliklere ilişkin veriler dahil olmak üzere denetim günlüğü bilgileri
  - Yönet
  - Oluştur
  - Güncelleştirme (düzenleme)
  - Sil
  - Ata
  - Uzak görevler
- Destek bilgileri
  - İletişim bilgileri (ad, telefon numarası, e-posta adresi)
  - Microsoft’un destek, ürün ve/veya müşteri deneyimi ekibi üyeleriyle e-posta yoluyla yapılan tartışmalar
- Erişim denetimi bilgileri (Intune, bu verileri [Rol Tabanlı Erişim Denetimi](../fundamentals/role-based-access-control.md) gibi özellikler yoluyla yönetim rolleri ve işlevlerine erişimi yönetmek için kullanır.)
  - Statik doğrulayıcılar (müşterinin parolası)
  - Sertifikalar için gizlilik anahtarları 
- Yönetici ve hesap bilgileri
  - Yönetici kullanıcının adı ve soyadı
  - Yönetici kullanıcı adı
  - UPN (e-posta)
  - Telefon numarası
  - Hesap sahibinin e-posta adresi
  - Tüm müşteri BT yöneticilerinin Active Directory kimliği
  - Müşteriyi faturalandırma için ödeme verileri
  - Abonelik anahtarı
- Uygulama envanteri, örneğin
  - uygulama adı
  - sürüm
  - uygulama kimliği
  - boyut
  - yükleme konumu
  - Uygulama envanteri verileri, yalnızca Yönetici tarafından şirkete ait cihaz olarak işaretlendiğinde veya uyumlu uygulama özelliği açık olduğunda toplanır.  
- Müşteri 3. taraf kiracı kimlikleri, örneğin Apple Kimliği. 

## <a name="pseudonymized-data"></a>Takma ad kullanılan veriler

Takma ad kullanılan veriler, bir benzersiz tanımlayıcı ile ilişkilidir. Bu tanımlayıcı genellikle sistem tarafından oluşturulan ve kendi başına bir bireyi tanımlayamayan ancak kuruluş hizmetlerini kullanıcılara teslim etmek için kullanılan bir numaradır. 

Intune tarafından toplanan takma ad kullanılan veriler şunları içerebilir ancak bu kadarla sınırlı değildir: 

- Bir kullanıcı ve/veya cihaza bağlı tanılama, performans ve kullanım verileri
  - Bir özelliğin kullanılma sayısı
  - Özelliğe sağlanan komutlar
  - Bir hizmetin yanıt süresi
  - Yüklemeler ve diğer işlemlerin başarı oranları
  - Intune Şirket Portalı uygulama hataları
  - Kullanıcı ve cihaz tanımlayıcıları
  - Başvuru, bağıntı ve yönetime yönelik tanımlayıcılar 
- Bir cihaz veya kullanıcıya bağlı olmayan cihaz verileri (bu veriler bir cihaz veya kullanıcıya bağlıysa Intune bunlara tanımlanan verilere olduğu gibi davranır)
  - Intune cihaz kimliği
  - Azure Active Directory cihaz kimliği
  - Intune cihaz yönetimi kimliği
  - Kiracı kimliği
  - Hesap kimliği
  - EAS cihaz kimliği
  - Platforma özgü kimlikler
  - İOS için AppleID/ıpados cihazları
  - Mac cihazlar için Mac Adresi
  - Windows cihazlar için Windows kimliği
- Yönetilen uygulama bilgileri
  - Yönetilen uygulama kimliği
  - Yönetilen uygulama cihaz etiketi
  - Intune cihaz yönetimi kimliği
  - Azure Active Directory cihaz kimliği
  - Şifreleme anahtarları

## <a name="aggregated-data"></a>Toplam veriler

Toplam veriler, Intune hizmetini sağlamak ve geliştirmek için kullanılır. 

Intune tarafından toplanan toplam veriler şunları içerebilir ancak bu kadarla sınırlı değildir: 

- Tüm Intune kiracılarındaki yönetici kullanım verileri (örneğin Yönetici konsoluyla etkileşimdeyken seçilen yönetici denetimleri)
- Kiracı hesap bilgileri (bu verilere Intune dikey penceresinden ulaşılabilir)
  - Kayıtlı cihaz veya kullanıcı sayısı
  - Tanımlı cihaz platformu sayısı  
  - Yüklü cihaz sayısı
  - installedDeviceCount: Uygulamanın yüklü olduğu cihaz sayısı.
  - notApplicableDeviceCount: Uygulamanın kullanılamadığı cihaz sayısı.
  - notInstalledDeviceCount: Uygulamanın kullanılabildiği ancak yüklü olmadığı cihaz sayısı.
  - Pendingınstalldevicecount: uygulamanın geçerli olduğu ve yüklemenin beklediği cihaz sayısı.

## <a name="next-steps"></a>Sonraki adımlar

Intune’un verileri nasıl [depolayıp işlediği](privacy-data-store-process.md) ve [paylaştığı](privacy-data-secure-share.md) hakkında daha fazla bilgi edinin. 
