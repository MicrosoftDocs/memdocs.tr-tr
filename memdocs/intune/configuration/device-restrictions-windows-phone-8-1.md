---
title: Windows Phone 8.1 için Microsoft Intune cihaz kısıtlama ayarları
titleSuffix: ''
description: Windows Phone 8.1 çalıştıran cihazlarda cihaz ayarlarını ve işlevselliğini denetlemek için kullanabileceğiniz Intune ayarlarını öğrenin.
keywords: ''
author: MandiOhlinger
ms.author: mandia
manager: dougeby
ms.date: 3/6/2018
ms.topic: reference
ms.service: microsoft-intune
ms.subservice: configuration
ms.localizationpriority: medium
ms.technology: ''
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: 3696ebf52ee093befc3b6eadc6d1a5041d5929e9
ms.sourcegitcommit: 3d895be2844bda2177c2c85dc2f09612a1be5490
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/13/2020
ms.locfileid: "79333130"
---
# <a name="microsoft-intune-windows-phone-81-device-restriction-settings"></a>Microsoft Intune Windows Phone 8.1 cihaz kısıtlama ayarları



Bu makalede, Windows Phone 8.1 çalıştıran cihazlar için yapılandırabileceğiniz Microsoft Intune cihaz kısıtlama ayarları gösterilir.


## <a name="general"></a>Genel

- **Kamera** - Cihazın kamerasını etkinleştirir veya engeller.
- **Kopyala ve yapıştır** - Cihazda kopyalama ve yapıştırma işlevlerini etkinleştirir veya engeller.
- **Çıkarılabilir depolama** - Cihazın SD kartları gibi çıkarılabilir depolama birimleri kullanmasına olanak tanır.
- **Coğrafi konum** - Cihazın konum bilgilerini kullanmasına olanak tanır.
- **Microsoft hesabı** - Kullanıcının cihaza bir Microsoft hesabı bağlamasını etkinleştirin veya engelleyin.
- **Ekran yakalama** - Kullanıcının ekran içeriğini resim dosyası olarak yakalamasına olanak tanır.
- **Tanılama verisi gönderme** - Cihazın Microsoft’a tanılama bilgileri göndermesini etkinleştirir.
- **Özel e-posta hesapları eşitleme** - Cihazın Microsoft olmayan e-posta hesaplarına bağlanmasına olanak tanır.

## <a name="password"></a>Parola

- **Parola** - Son kullanıcının cihaza erişmek için parola girmesini zorunlu tutun.
  - **Gerekli parola türü** - Gerekli parola türünü belirtir (alfasayısal veya yalnızca sayısal gibi).
  - **En az parola uzunluğu** - Parolada bulunması gereken karakter sayısı alt sınırını belirtir.
  - **Basit parolalar** - ‘0000’ ve ‘1234’ gibi basit parolaların kullanılabileceğini belirtir.
  - **Cihaz silinmeden önceki oturum açma hatası sayısı** - Cihaz temizlenmeden önce kullanıcının kaç kez hatalı parola girilebileceğini belirtir.
  - **Ekran kilitlenmeden önce geçmesi gereken, işlem yapılmayan dakika sayısı** - Ekran otomatik olarak kilitlenmeden önce cihazın boşta bekleyeceği süreyi belirtir.
  - **Parola geçerlilik süresi (gün)** - Cihaz parolasının değiştirilmesi gerekmeden önce geçmesi gereken gün sayısını belirtir.
  - **Önceki parolaların yeniden kullanılmasını engelle** - Önceden kullanılmış olan kaç parolanın anımsanacağını belirtir.
- **Şifreleme** - Desteklenen mobil cihazlarda verilerin şifrelenmesini zorunlu tutar.

## <a name="app-store"></a>Uygulama Mağazası

- **Uygulama mağazası** - Kullanıcıların cihazdan uygulama mağazasına bağlanmasına olanak tanır.

## <a name="restricted-apps"></a>Kısıtlı uygulamalar

Kısıtlı uygulamalar listesinde, aşağıdaki listelerden birini yapılandırabilirsiniz:

**Engellenen uygulamalar** listesi - Intune tarafından yönetilmeyen, kullanıcıların yüklemesine ve çalıştırmasına izin verilmeyen uygulamaları listeleyin.
**İzin verilen uygulamalar** listesi - Kullanıcıların yüklemesine izin verilen uygulamaları listeleyin. Intune tarafından yönetilen uygulamalara otomatik olarak izin verilir.

Listeyi yapılandırmak için **Ekle**’ye tıklayın, sonra da tercih ettiğiniz bir ad (isteğe bağlı olarak uygulama yayımcısı) ve uygulamanın uygulama mağazasındaki URL'sini belirtin.

### <a name="how-to-specify-the-url-to-an-app-in-the-store"></a>Mağazadaki uygulamanın URL’sini belirtme

İzin verilen veya engellenen uygulamalar listesinde bir uygulama URL'si belirtmek için aşağıdaki biçimi kullanın:

[Windows Phone Mağazası](https://www.microsoft.com/store/apps/windows-phone) sayfasında, kullanmak istediğiniz uygulamayı arayın.

Uygulamanın sayfasını açın ve URL'yi panoya kopyalayın. Artık bunu izin verilen veya engellenen uygulamalar listesinde URL olarak kullanabilirsiniz.

Örnek: Mağazada Skype uygulamasını arayın. Kullandığınız URL `http://www.windowsphone.com/store/app/skype/c3f8e570-68b3-4d6a-bdbb-c0a3f4360a51` olacaktır.



### <a name="additional-options"></a>Ek seçenekler

Ayrıca, **Içeri aktar** ' a tıklayarak listeyi <*uygulama URL 'si*>, uygulama*adı*> < uygulama*yayımcısı*< veya aynı biçimde kısıtlanmış uygulamalar listesinin Içeriğini içeren bir CSV dosyası oluşturmak için **dışarı aktar** ' a tıklayabilirsiniz.


## <a name="browser"></a>Tarayıcı

- **Web tarayıcısı** - Cihazlarda yerleşik web tarayıcısını etkinleştirir veya engeller.

## <a name="cellular-and-connectivity"></a>Hücresel ve Bağlantı

- **Wi-Fi** - Cihazda Wi-Fi işlevselliğini etkinleştirir veya devre dışı bırakır.
- **Wi-Fi paylaşımı** - Cihazda Wi-Fi paylaşımının kullanımını etkinleştirir.
- **Wi-Fi etkin noktalarına otomatik bağlanma** - Cihazın ücretsiz Wi-Fi etkin noktalarına otomatik olarak bağlanmasına ve tüm kullanım koşullarını otomatik olarak kabul etmesine olanak tanır.
- **Wi-Fi etkin nokta raporlama** - Kullanıcının yakındaki bağlantıların keşfetmesine yardımcı olmak için Wi-Fi bağlantıları hakkında bilgi gönderir.
- **NFC** - Bu özelliği destekleyen cihazlarda yakın alan iletişimini kullanan işlemleri etkinleştirir veya devre dışı bırakır.
- **Bluetooth** - Cihazda Bluetooth işlevselliğini etkinleştirir veya devre dışı bırakır.
