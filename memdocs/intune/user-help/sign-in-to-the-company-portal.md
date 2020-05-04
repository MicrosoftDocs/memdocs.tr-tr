---
title: Şirket Portalı uygulamasında oturum açma | Microsoft Docs
description: Birden çok platformdaki Şirket Portalı uygulamasında oturum açmayı öğrenin.
keywords: ''
author: lenewsad
ms.author: lanewsad
manager: dougeby
ms.date: 12/31/2019
ms.topic: article
ms.prod: ''
ms.service: microsoft-intune
ms.subservice: end-user
ms.technology: ''
ms.assetid: cfd214bc-f072-4808-af2e-a3cbf7af9bca
searchScope:
- User help
ROBOTS: ''
ms.reviewer: esmich
ms.suite: ems
ms.custom: intune-enduser
ms.collection: ''
ms.openlocfilehash: 4088185da2c01cfa7fd343203f7452d2796c4466
ms.sourcegitcommit: 7f17d6eb9dd41b031a6af4148863d2ffc4f49551
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 04/21/2020
ms.locfileid: "79324322"
---
# <a name="sign-in-to-company-portal"></a>Şirket Portalı oturum açın  

Şirket Portalı uygulamasında oturum açmak için üç yol vardır:

* İş e-posta adresiniz ve parolanızla oturum açın.  
* Sertifika tabanlı kimlik doğrulamasıyla oturum açın.  
* Başka bir cihazdan oturum açın.    


## <a name="sign-in-with-your-email-address-and-password"></a>E-posta adresiniz ve parolanızla oturum açın
Aşağıdaki adımlarda iOS için Şirket Portalı ekran görüntüleri gösterilmektedir.  

1. Uygulamayı cihazınızda açın ve **oturum aç**' a dokunun.  

   ![Şirket Portalı oturum açma sayfasının örnek ekran görüntüsü.](./media/intune-ios-cp-signin-1908.png)


2. **İş veya okul hesabınızı** girin ve **İleri**’ye dokunun.

   ![Kullanıcı aynı ekranda hem e-posta adresini hem de parolasını girmek yerine yalnızca kendi e-posta adresini girer.](./media/cp_ios_aad_signin_after_1804_002.png)

3. Parolanızı girin ve **Oturum Aç**’a dokunun.

   ![E-posta adresi kabul edildikten sonra kullanıcıdan parolası istenir.](./media/cp_ios_aad_signin_after_1804_003.png)

4. Uygulama, kimlik bilgilerinizi doğrulayacaktır. İşiniz bittiğinde kuruluşunuzun kaynaklarına erişebilir ve kullanılabilir uygulamaları yükleyebilirsiniz.  

   ![Kimlik doğrulama işleminden sonra Şirket Portalı uygulama oturum açar, bir yükleme çubuğu gösterir.](./media/cp_ios_aad_signin_after_1804_004.png)

## <a name="sign-in-with-certificate-based-authentication"></a>Sertifika tabanlı kimlik doğrulamasıyla oturum açın
Bu oturum açma seçeneğini yalnızca kuruluşunuz sertifika tabanlı kimlik doğrulamasına izin veriyorsa ve kullanabileceğiniz bir sertifikanız varsa görürsünüz.  

1. Cihazınızda Şirket Portalı uygulamasını açın.  

2. **İş veya okul hesabınızı** girin.  

3. **Sertifika ile oturum açma** bağlantısına dokunun.  

4. Sertifikayı kullanmak için **Devam**’a dokunun.  

## <a name="sign-in-from-another-device"></a>Başka bir cihazdan oturum açma

Şirketiniz, bilgisayarlarınıza erişmek için akıllı kartlar kullanıyorsa, başka bir cihazdan oturum açarak kimlik doğrulamanız gerekebilir.  

1. Cihazınızda Şirket Portalı uygulamasını açın. İş kaynaklarınıza erişmek için kullanacağınız cihaz olduğundan emin olun.       

1. **Başka bir cihazdan oturum aç '** ı seçin.  

   ![Şirket Portalı oturum açma sayfası kullanıcıdan e-posta adresini ister.  "Ileri" düğmesini ve "başka bir cihazdan oturum aç" bağlantısını gösterir. Ayrıca bir “Hesabınıza erişemiyor musunuz?” bağlantısı da vardır. Aşağıdaki bir bağlantı Microsoft Gizlilik ve Tanımlama bilgilerine yönlendirir.](./media/cp_ios_aad_signin_after_1804_005.png)

2. Şirket Portalı’nda oturum açmak için benzersiz, tek seferlik bir kod alacaksınız. Kodu kopyalayın.

   ![İş bilgisayarınızdan benzersiz bir geçiş kodu ile https://microsoft.com/devicelogin sayfasına gidip oturum açmak için bu kodu kullanmaya ilişkin yönergeler sağlanır.](./media/cp_ios_aad_signin_after_1804_006.png)

3. Diğer cihazınızda (kimlik doğrulamak için kullandığınız) tarayıcınızı açın ve adresine gidin [https://microsoft.com/devicelogin](https://microsoft.com/devicelogin). Kodu girin veya yapıştırın.  

   ![Kullanıcının Şirket Portalı uygulamasındaki tarayıcı yerine iş bilgisayarındaki tarayıcısının bir resmi. Görüntülenen "Cihaz oturum açma" sayfası kullanıcıdan Şirket Portalı uygulamasından aldığı kodu girmesini ister.](../fundamentals/media/whats-new-app-ui/cp_ios_aad_signin_from_another_device_after_1704_004.png)

4. Şirket Portalı iş cihazınızda oturum açmasını sağlamak için __devam__ ' ı seçin.   

   ![Kullanıcı kendi benzersiz kodunu alana girmiştir ve "Cihaz oturum açma" sitesi Intune Şirket Portalı’nın oturum açmak üzere yetkilendirilecek doğru uygulama olup olmadığının doğrulanmasını istemiştir.](../fundamentals/media/whats-new-app-ui/cp_ios_aad_signin_from_another_device_after_1704_005.png) 

5. Kod doğrulandığında pencereyi kapatabilirsiniz.  

   ![Bir onay sayfası, kullanıcının kendi cihazında Şirket Portalı uygulamasında oturum açtığını ve bu sayfanın artık kapatılabileceğini belirtir.](../fundamentals/media/whats-new-app-ui/cp_ios_aad_signin_from_another_device_after_1704_006.png)

6. Şirket Portalı uygulama, iş cihazınızda oturumunuzu kapatır.  

   ![Kimlik doğrulama işleminden sonra Şirket Portalı, ilerlemeyi gösteren bir çubuk ile oturum açar.](./media/cp_ios_aad_signin_after_1804_007.png)

Bu bilgiler yardımcı olmadı mı? Şirketinizin destek bölümüne başvurun. Kişi bilgileri için [Şirket Portalı Web sitesine](https://go.microsoft.com/fwlink/?linkid=2010980) bakın.  
