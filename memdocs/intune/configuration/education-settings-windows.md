---
title: Microsoft Intune-Azure 'da Windows 10 eğitim ayarları | Microsoft Docs
description: Windows 10 cihazları için tüm eğitim ayarlarının listesini görüntüleyin. Bu ayarları, test alma uygulaması ile bir cihaz yapılandırma profilinde kullanın, kullanıcıların veya öğrencilerin oturum açmasını, test sırasında ekranı nasıl izleyeceğinizi ve Intune 'da daha fazlasını yapın.
keywords: ''
author: lenewsad
ms.author: lanewsad
manager: dougeby
ms.date: 07/03/2019
ms.topic: reference
ms.service: microsoft-intune
ms.subservice: configuration
ms.localizationpriority: medium
ms.technology: ''
ms.assetid: 6f4de4bd-3dde-4a8d-8e22-46c5d06c3eea
ms.reviewer: kakyker
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: 2c6648f66c585dac5b8913fdb13adfcb98cbf927
ms.sourcegitcommit: 0c7e6b9b47788930dca543d86a95348da4b0d902
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/26/2020
ms.locfileid: "88912704"
---
# <a name="configure-the-take-a-test-app-on-windows-10-devices-using-intune"></a>Intune kullanarak Windows 10 cihazlarda bir test alma uygulaması yapılandırma

Bir test al uygulaması, dersin Windows 10 cihazlarında çevrimiçi testleri güvenli bir şekilde yönetmenizi sağlar. Test al uygulamasını ayarlamak için, Intune 'da bir cihaz yapılandırma profili oluşturmanız ve güvenli değerlendirme ayarlarını yapılandırmanız gerekir. Bu makalede, test alma uygulaması için bulacağınız ayarlar açıklanmaktadır. 

Profili yapılandırdıktan sonra öğrencilerinize atayıp dağıtın. 

[Intune 'da bir test uygulaması alma](education-settings-configure.md) bu özellik hakkında daha fazla bilgi sağlar.

## <a name="before-you-begin"></a>Başlamadan önce

[Bir cihaz yapılandırma profili oluşturun](education-settings-configure.md#create-a-device-profile).

## <a name="take-a-test-settings"></a>Test ayarları yapın

- **Hesap türü**: kullanıcıların testte oturum açmasını seçin. Seçenekleriniz şunlardır:
  - Azure AD hesabı
  - Etki alanı hesabı
  - Yerel hesap
  - Yerel Konuk hesabı: yalnızca Windows 10, sürüm 1903 ve üzeri sürümleri çalıştıran cihazlarda kullanılabilir.
- **Hesap Kullanıcı adı**: bir test alma uygulamasıyla kullanılan hesabın kullanıcı adını girin. Hesapları aşağıdaki biçimde girebilirsiniz:
  - `user@contoso.com`
  - `domain\username`
  - `user@contoso.com`
  - `computerName\username`
- **Hesap adı**: bir yerel Konuk hesap türü ayarlamak Için, test alma uygulaması ile kullanılan hesabın adını girin. Hesap adı, oturum açma ekranında bir kutucuk olarak görüntülenir. Öğrenciler, testi başlatmak için kutucuğa tıklayın.  
- **Değerlendirme URL 'si**: kullanıcıların geçirmesine istediğiniz testin URL 'sini girin. URL 'YI alma hakkında daha fazla bilgi için [test alma belgelerine](/education/windows/take-tests-in-windows-10)bakın.
- **Yazıcı bağlantısı**: **gerekli** yalnızca bir yazıcıya bağlı cihazlardan test alma uygulaması erişimine izin verir. Bu ayar ayrıca uygulamanın Yazdır düğmesini test çiciler için kullanılabilir hale getirir. **Yapılandırılmadı** (varsayılan) olarak ayarlandığında, Intune bu ayarı değiştirmez veya güncelleştirmez. Varsayılan olarak, işletim sistemi öğrencilerin bir yazıcıya bağlı olmayan cihazlardan uygulamaya erişmesine izin verebilir.  
- **Ekran izleme**: **izin ver** , kullanıcılar bir test alırken ekran etkinliğini izler. **Yapılandırılmadı** (varsayılan) olarak ayarlandığında, Intune bu ayarı değiştirmez veya güncelleştirmez. Varsayılan olarak işletim sistemi, sınama sırasında ekranı izlemeden engel olabilir.
- **Metin önerileri**: **izin ver** ' i seçin, böylece test takiciler metin önerilerini görüntüleyebilir. **Yapılandırılmadı** (varsayılan) olarak ayarlandığında, Intune bu ayarı değiştirmez veya güncelleştirmez. Varsayılan olarak, işletim sistemi, kullanıcılar bir test sunarken metin önerilerini engelleyebilir.

## <a name="next-steps"></a>Sonraki adımlar

[Profili atayın](device-profile-assign.md)ve [durumunu izleyin](device-profile-monitor.md).

[Test alma uygulaması](education-settings-configure.md)hakkında daha fazla bilgi edinin.