---
title: Intune ile Pradeo tümleştirmesini ayarlama
titleSuffix: Intune on Azure
description: Intune ile Pradeo bağlayıcısı tümleştirmesi
keywords: ''
author: brenduns
ms.author: brenduns
manager: dougeby
ms.date: 10/21/2019
ms.topic: conceptual
ms.service: microsoft-intune
ms.subservice: protect
ms.localizationpriority: high
ms.technology: ''
ms.assetid: 82872ba6-80f8-4cc9-adf4-0ccd8ff26dd2
search.appverid: MET150
ms.collection: M365-identity-device-management
ms.openlocfilehash: 10cda4126f709ddd0cb5cda40b36067bd078a3f0
ms.sourcegitcommit: 1442a4717ca362d38101785851cd45b2687b64e5
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 04/23/2020
ms.locfileid: "82079595"
---
# <a name="integrate-pradeo-mobile-threat-defense-with-intune"></a>Pradeo Mobile Threat Defense 'i Intune ile tümleştirme

Pradeo Mobile Threat Defense çözümünü Intune ile tümleştirmek için aşağıdaki adımları tamamlayın.

> [!NOTE]  
> Bu mobil tehdit savunma satıcısı, kayıtlı olmayan cihazlar için desteklenmez.

## <a name="before-you-begin"></a>Başlamadan önce

> [!NOTE]
> Aşağıdaki adımların [Pradeo Security konsolunda](https://pradeo-security.com/) tamamlanması gerekir.

Pradeo’yu Intune ile tümleştirme sürecini başlatmadan önce aşağıdakilere sahip olduğunuzdan emin olun:

- Microsoft Intune aboneliği

- Şu izinleri vermek için Azure Active Directory yönetici kimlik bilgileri:

  - Oturum açma ve kullanıcı profilini okuma

  - Dizine oturum açmış kullanıcı olarak erişin

  - Dizin verilerini oku

  - Intune’a cihaz bilgilerini gönderme

- Pradeo Security konsoluna erişmek için gereken yönetici kimlik bilgileri.

### <a name="pradeo-app-authorization"></a>Pradeo uygulama yetkilendirmesi

Pradeo uygulama yetkilendirme işlemi şu şekildedir:

- Pradeo hizmetine Intune’a cihaz durumuyla ilgili bilgi iletme izni verin.

- Pradeo, cihazın veritabanını doldurmak için Azure AD kayıt grubu üyeliğiyle eşitlenir.

- Pradeo yönetim konsolunun Azure AD Çoklu Oturum Açma (SSO) kullanmasına izin verin.

- Pradeo uygulamasının Azure AD SSO kullanarak oturum açmasına izin verin.

## <a name="to-set-up-pradeo-integration"></a>Pradeo tümleştirmesini ayarlamak için

1. [Pradeo Security konsolu](https://www.pradeo-security.com)’na gidin ve kimlik bilgilerinizle oturum açın.

2. Menüden **Yönetim - Enterprise Mobility Yönetimi**’ni seçin.

3. **Intune logosunu** seçin.

4. **EMM (Enterprise Mobility Yönetimi - Intune)** penceresindeki **1. Adım** altında bulunan **Pradeo Bağlayıcısı** düğmesini seçin. 

    ![Pradeo EMM Intune penceresinin ekran görüntüsü](./media/pradeo-mtd-connector-integration/pradeo_setup.png)

5. Microsoft Intune bağlantı penceresinde Intune kimlik bilgilerinizi girin.

5. Pradeo web sayfası yeniden açılacaktır. **2. Adım** altında **Pradeo Cihaz Durumu** düğmesini seçin.

7. Pradeo-Intune Bağlayıcısı penceresinde **Kabul Et**’i seçin. 

8. Pradeo cihaz API bağlayıcısı penceresinde **Kabul Et**’i seçin.

9. Pradeo web sayfası yeniden açılacaktır. **3. Adım** altında **Microsoft’a Bağlan** düğmesini seçin. 

10. Microsoft Intune kimlik doğrulaması penceresinde Intune kimlik bilgilerinizi girin.

11. **Başarılı Tümleştirme** iletisi göründüğünde tümleştirme tamamlanmıştır.

## <a name="next-steps"></a>Sonraki adımlar

- [Kayıtlı cihazlar için Pradeo uygulamalarını ayarlama](mtd-apps-ios-app-configuration-policy-add-assign.md)
