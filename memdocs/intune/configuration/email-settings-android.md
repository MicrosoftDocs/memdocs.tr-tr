---
title: Microsoft Intune-Azure 'da Android e-posta ayarları | Microsoft Docs
description: Bir cihaz Exchange sunucularının kullandığı yapılandırma e-posta profilleri oluşturma ve Azure Active Directory öznitelikleri alınamıyor. SSL veya SMIME 'yi etkinleştirin, sertifikalar veya Kullanıcı adı/parola ile kullanıcıların kimliğini doğrulayın ve Microsoft Intune kullanarak Android Samsung KNOX cihazlarda e-posta ve zamanlamaları eşitler.
keywords: ''
author: MandiOhlinger
ms.author: mandia
manager: dougeby
ms.date: 02/18/2020
ms.topic: reference
ms.service: microsoft-intune
ms.subservice: configuration
ms.localizationpriority: medium
ms.technology: ''
ms.suite: ems
search.appverid: MET150
ms.custom: seodec18
ms.collection: M365-identity-device-management
ms.openlocfilehash: 31310accbaded1e048cb3c5b574557ffcef0335c
ms.sourcegitcommit: 3d895be2844bda2177c2c85dc2f09612a1be5490
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/13/2020
ms.locfileid: "79333062"
---
# <a name="android-device-settings-to-configure-email-authentication-and-synchronization-in-intune"></a>Intune 'da e-posta, kimlik doğrulama ve eşitlemeyi yapılandırmak için Android cihaz ayarları

Bu makalede, Intune 'da Android Samsung KNOX cihazlarında denetim için kullanabileceğiniz farklı e-posta ayarları listelenir ve açıklanmaktadır. Mobil cihaz Yönetimi (MDM) çözümünüzün bir parçası olarak, bu ayarları ve e-postaları şifrelemek için SSL kullanmak, bir e-posta sunucusu yapılandırmak için kullanın.

Bir Intune Yöneticisi olarak, Android Samsung KNOX Standard cihazlarına e-posta ayarları oluşturabilir ve atayabilirsiniz.

Intune 'da e-posta profilleri hakkında daha fazla bilgi için bkz. [e-posta ayarlarını yapılandırma](email-settings-configure.md)

## <a name="before-you-begin"></a>Başlamadan önce

[Bir cihaz yapılandırma profili oluşturun](email-settings-configure.md#create-a-device-profile).

## <a name="android-samsung-knox"></a>Android (Samsung Knox)

- **E-posta sunucusu**: Exchange sunucunuzun konak adını girin. Örneğin, şunu girin: `outlook.office365.com`.
- **Hesap adı**: E-posta hesabı için görünen adı girin. Bu ad, cihazlarda kullanıcılara gösterilir.
- **AAD'den kullanıcı adı özniteliği**: Bu ad, Intune'un Azure Active Directory'den (Azure AD) aldığı özniteliktir. Intune, bu profil tarafından kullanılan kullanıcı adını dinamik olarak oluşturur. Seçenekleriniz şunlardır:
  - **Kullanıcı Asıl Adı**: Adı alır; örneğin `user1` veya `user1@contoso.com`
  - **Kullanıcı adı**: Yalnızca adı alır; örneğin `user1`
  - **sAM Hesap Adı**: Etki alanı gerektirir; örneğin `domain\user1`. sAM hesabı adı yalnızca Android cihazlarıyla birlikte kullanılır.

    Şunları da girin:  
    - **Kullanıcı etki alanı adı kaynağı**: **AAD** (Azure Active Directory) veya **Özel**’i seçin.

      Öznitelikleri **AAD**’den almayı seçerseniz şunları girin:
      - **AAD’den kullanıcı etki alanı adı**: Kullanıcının **Tam etki alanı adı** veya **NetBIOS adı** özniteliğini alma arasında seçim yapın

      **Özel** öznitelikler kullanmayı seçerseniz şunları girin:
      - **Kullanılacak özel etki alanı adı**: Intune’un etki alanı adı olarak kullanacağı bir değer seçin; örneğin `contoso.com` veya `contoso`

- **AAD 'Den e-posta adresi özniteliği**: Bu ad, Intune 'un Azure AD 'den aldığı e-posta özniteliğidir. Intune, bu profil tarafından kullanılan e-posta adresini dinamik olarak oluşturur. Seçenekleriniz şunlardır:
  - **Kullanıcı asıl adı**: e-posta adresi olarak `user1@contoso.com` veya `user1`gibi tam asıl adı kullanır.
  - **BIRINCIL SMTP adresi**: Exchange 'de oturum açmak için `user1@contoso.com`gıbı birincil SMTP adresini kullanır.

- **Kimlik doğrulama yöntemi**: E-posta profili tarafından kullanılan kimlik doğrulama yöntemi olarak **Kullanıcı Adı ve Parola**’yı veya **Sertifikalar**’ı seçin.
  - **Sertifika**’yı seçerseniz, Exchange bağlantısının kimliğini doğrulamak için daha önce oluşturduğunuz istemci SCEP veya PKCS sertifika profilini seçin.

### <a name="security-settings"></a>Güvenlik ayarları

- **SSL**: E-posta gönderirken, e-posta alırken ve Exchange sunucusuyla iletişim kurarken Güvenli Yuva Katmanı (SSL) iletişimini kullanın.
- **S/MIME**: Giden e-postaları S/MIME şifrelemesi kullanarak gönderin.
  - **Sertifika**’yı seçerseniz, Exchange bağlantısının kimliğini doğrulamak için daha önce oluşturduğunuz istemci SCEP veya PKCS sertifika profilini seçin.

### <a name="synchronization-settings"></a>Eşitleme ayarları

- **Eşitlenecek e-posta miktarı**: Eşitlemek istediğiniz e-postalar için gün sayısını seçin veya **Sınırsız**’ı seçerek kullanılabilir tüm e-postaları eşitleyin.
- **Eşitleme zamanlaması**: Cihazların Exchange sunucusundan veri eşitleyeceği zamanlamayı seçin. Ayrıca, verileri geldiğinde eşitleyen **İletiler geldiğinde** seçeneğini veya eşitlemenin cihaz kullanıcısı tarafından başlatılmasını gerektiren **El ile** seçeneğini belirleyebilirsiniz.

### <a name="content-sync-settings"></a>İçerik eşitleme ayarları

- **Eşitlenecek içerik türü**: cihazlarda eşitlemek istediğiniz içerik türlerini seçin. **Yapılandırılmadı** , bu ayarı devre dışı bırakır. **Yapılandırılmadı**olarak ayarlandığında, bir son kullanıcı cihazda eşitlemeyi etkinleştiriyorsa, ilke yeniden zorlandığında cihaz Intune ile eşitlendikten sonra eşitleme yeniden devre dışı bırakılır. 

  Aşağıdaki içeriği eşitleyebilirsiniz:  
  - **Kişiler**: son kullanıcıların kişileri cihazlarıyla eşitlemesine izin vermek için **Etkinleştir** ' i seçin.
  - **Takvim**: son kullanıcıların takvimi cihazlarıyla eşitlemesine izin vermek için **Etkinleştir** ' i seçin.
  - **Görevler**: son kullanıcıların tüm görevleri cihazlarıyla eşitlemesine izin vermek için **Etkinleştir** ' i seçin.

## <a name="next-steps"></a>Sonraki adımlar

[Profili atama](device-profile-assign.md) ve [durumunu izleme](device-profile-monitor.md).

[Android kurumsal iş profili](email-settings-android-enterprise.md), [IOS/ıpados](email-settings-ios.md), [Windows 10 ve üzeri](email-settings-windows-10.md)ve [8,1 Windows Phone](email-settings-windows-phone-8-1.md)için e-posta profilleri de oluşturabilirsiniz.
