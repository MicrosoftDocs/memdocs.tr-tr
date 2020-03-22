---
title: Microsoft Intune-Azure 'da Android kurumsal e-posta ayarları | Microsoft Docs
description: Exchange sunucularını kullanan cihaz yapılandırması e-posta profilleri oluşturun ve Azure Active Directory öznitelikleri alın. SSL veya SMIME 'yi etkinleştirin, sertifikalar veya Kullanıcı adı/parola ile kullanıcıların kimliğini doğrulayın ve Microsoft Intune kullanarak Android iş profili cihazlarındaki e-posta ve zamanlamaları eşitler.
keywords: ''
author: MandiOhlinger
ms.author: mandia
manager: dougeby
ms.date: 03/19/2020
ms.topic: reference
ms.service: microsoft-intune
ms.subservice: configuration
ms.localizationpriority: medium
ms.technology: ''
ms.suite: ems
search.appverid: MET150
ms.reviewer: maholdaa
ms.custom: seodec18
ms.collection: M365-identity-device-management
ms.openlocfilehash: ab544d285e49fd3914a8e9867c35ad9ed97f5fe8
ms.sourcegitcommit: 017b93345d8d8de962debfe3db5fc1bda7719079
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/21/2020
ms.locfileid: "80087024"
---
# <a name="android-enterprise-device-settings-to-configure-email-authentication-and-synchronization-in-intune"></a>Intune 'da e-posta, kimlik doğrulama ve eşitlemeyi yapılandırmak için Android kurumsal cihaz ayarları

Bu makalede, Android kurumsal cihazlarda denetleyebilmeniz için farklı e-posta ayarları listelenir ve açıklanmaktadır. Mobil cihaz Yönetimi (MDM) çözümünüzün bir parçası olarak, bu ayarları ve e-postaları şifrelemek için SSL kullanmak, bir e-posta sunucusu yapılandırmak için kullanın.

Bir Intune Yöneticisi olarak, iş profilinde Android kurumsal cihazlara e-posta ayarları oluşturabilir ve atayabilirsiniz.

Intune 'da e-posta profilleri hakkında daha fazla bilgi için bkz. [e-posta ayarlarını yapılandırma](email-settings-configure.md)

## <a name="before-you-begin"></a>Başlamadan önce

Bir [cihaz yapılandırma profili](email-settings-configure.md) oluşturun (iş profilini seçin) veya bir [uygulama yapılandırma ilkesi](../apps/app-configuration-policies-use-android.md)oluşturun.

## <a name="android-enterprise"></a>Android Kurumsal

- **E-posta uygulaması**: **Gmail** veya **dokuz iş**seçin.
- **E-posta sunucusu**: Exchange sunucunuzun konak adını girin. Örneğin, şunu girin: `outlook.office365.com`.
- **AAD'den kullanıcı adı özniteliği**: Bu ad, Intune'un Azure Active Directory'den (Azure AD) aldığı özniteliktir. Intune, bu profil tarafından kullanılan kullanıcı adını dinamik olarak oluşturur. Seçenekleriniz şunlardır:

  - **Kullanıcı asıl adı**: `user1` veya `user1@contoso.com`gibi adı alır.
  - **Kullanıcı adı**: yalnızca `user1`gibi adı alır.

- **AAD 'Den e-posta adresi özniteliği**: Bu ad, Intune 'un Azure AD 'den aldığı e-posta özniteliğidir. Intune, bu profil tarafından kullanılan e-posta adresini dinamik olarak oluşturur. Seçenekleriniz şunlardır:
  - **Kullanıcı asıl adı**: e-posta adresi olarak `user1@contoso.com` veya `user1`gibi tam asıl adı kullanır.
  - **BIRINCIL SMTP adresi**: Exchange 'de oturum açmak için `user1@contoso.com`gıbı birincil SMTP adresini kullanır.

- **Kimlik doğrulama yöntemi**: e-posta profili tarafından kullanılan kimlik doğrulama yöntemi olarak **Kullanıcı adı ve parola** ya da **Sertifikalar** seçin.
  - **Sertifika**’yı seçerseniz, Exchange bağlantısının kimliğini doğrulamak için daha önce oluşturduğunuz istemci SCEP veya PKCS sertifika profilini seçin.
- **SSL**: e-posta gönderirken, e-posta alırken ve Exchange Server ile iletişim kurarken GÜVENLI yuva KATMANı (SSL) iletişimini kullanmak için **Etkinleştir** ' i seçin.
- **Eşitlenmesi yapılacak e-posta miktarı**: e-posta eşitlemesini istediğiniz süreyi seçin. Veya tüm kullanılabilir e-postaları eşleştirmek için **sınırsız** ' yı seçin.
- **Eşitlenecek içerik türü** (yalnızca dokuz çalışma): cihazlarda hangi verileri eşitlemek istediğinizi seçin. Seçenekleriniz şunlardır:
  - **Kişiler**: son kullanıcıların kişileri cihazlarıyla eşitlemesine izin vermek için **Etkinleştir** ' i seçin.
  - **Takvim**: son kullanıcıların takvimi cihazlarıyla eşitlemesine izin vermek için **Etkinleştir** ' i seçin.
  - **Görevler**: son kullanıcıların tüm görevleri cihazlarıyla eşitlemesine izin vermek için **Etkinleştir** ' i seçin.

## <a name="next-steps"></a>Sonraki adımlar

[Profili atama](device-profile-assign.md) ve [durumunu izleme](device-profile-monitor.md).

[Android Samsung KNOX](email-settings-android.md), [IOS/ıpados](email-settings-ios.md), [Windows 10 ve üzeri](email-settings-windows-10.md)ve [Windows Phone 8,1](email-settings-windows-phone-8-1.md) cihazları için e-posta profilleri de oluşturabilirsiniz.
