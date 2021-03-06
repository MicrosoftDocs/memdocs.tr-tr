---
title: Android cihazını Microsoft Intune App ve Entrust Datacard kaydetme
description: Bir Android cihazı kaydedin ve Entrust Datacard ile türetilmiş kimlik bilgisi kimlik doğrulamasını ayarlayın.
keywords: ''
author: lenewsad
ms.author: lanewsad
manager: dougeby
ms.date: 04/17/2020
ms.topic: end-user-help
ms.prod: ''
ms.service: microsoft-intune
ms.subservice: end-user
ms.technology: ''
ms.assetid: ''
searchScope:
- User help
ROBOTS: ''
ms.reviewer: jeyang
ms.suite: ems
ms.custom: intune-enduser
ms.collection: M365-identity-device-management
ms.openlocfilehash: f59d3c0d06e9b12acab3292ba0c977b181e7c07e
ms.sourcegitcommit: 48ec5cdc5898625319aed2893a5aafa402d297fc
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 06/08/2020
ms.locfileid: "84531800"
---
# <a name="set-up-android-device-with-company-portal-and-entrust-datacard"></a>Şirket Portalı ve Entrust Datacard ile Android cihazı ayarlama

Kuruluşunuzun e-postasına, dosyalarına ve uygulamalarına güvenli, mobil erişim kazanmak için cihazınızı Microsoft Intune uygulamasına kaydedin. Cihazınız kaydedildikten sonra, *yönetilen*hale gelir. Kuruluşunuz, Intune gibi bir mobil cihaz yönetimi (MDM) sağlayıcısı aracılığıyla cihaza ilkeler ve uygulamalar atayabilir.

Kayıt sırasında, bir türetilmiş kimlik bilgisini cihazınıza de yüklersiniz. Kuruluşunuz, kaynaklara erişirken veya e-postaları imzalama ve şifreleme için türetilmiş kimlik bilgilerini bir kimlik doğrulama yöntemi olarak kullanmanızı gerektirebilir.

Şunları yapmak için bir akıllı kart kullanıyorsanız, büyük olasılıkla türetilmiş bir kimlik bilgisi ayarlamanız gerekir:

* Okul veya iş uygulamalarında oturum açma, Wi-Fi ve sanal özel ağlar (VPN)
* Okul veya iş e-postalarını S/MIME sertifikaları kullanarak imzalama ve şifreleme

Bu makalede şunları yapacaksınız:

* Intune uygulamasıyla bir mobil Android cihaz kaydetme
* Kuruluşunuzun türetilmiş kimlik bilgisi sağlayıcısından türetilmiş bir kimlik bilgisi yükleyerek akıllı kartınızı ayarlayın [Entrust Datacard](https://www.entrustdatacard.com/)

## <a name="what-are-derived-credentials"></a>Türetilmiş kimlik bilgileri nelerdir?

Türetilmiş kimlik bilgileri, akıllı kart kimlik bilgilerinizle derlenen ve cihazınızda yüklü olan bir sertifikadır. Bu, iş kaynaklarına uzaktan erişim izni verir, ancak yetkisiz kullanıcıların hassas bilgilere erişmesini önler.

Türetilmiş kimlik bilgileri şu şekilde kullanılır:

* Okul veya iş uygulamalarında, Wi-Fi ve VPN 'de oturum açan öğrencilerin ve çalışanların kimliklerini doğrulama
* Okul veya iş e-postalarını S/MIME sertifikaları ile imzalama ve şifreleme

Türetilmiş kimlik bilgileri, özel yayın (SP) 800-157 kapsamında türetilmiş kişisel kimlik doğrulama (PıV) kimlik bilgileri için ulusal standartlar ve Teknoloji Enstitüsü (NıST) kuralları uygulamasıdır.

## <a name="prerequisites"></a>Ön koşullar

 Kaydı tamamlayabilmeniz için, şunları yapmanız gerekir:

* Okulunuz veya iş tarafından sağlanmış akıllı kartınız
* Akıllı kartınızla oturum açabileceğiniz bir bilgisayar veya bilgi noktası erişimi
* Android 7,0 veya üzerini çalıştıran yeni veya fabrika ayarlarına sahip bir cihaz
* Cihazınızda yüklü Microsoft Intune uygulaması

## <a name="enroll-device"></a>Cihaz kaydetme  

1. Yeni veya fabrika ayarlarına sıfırlama cihazınızı açın.  
2. **Hoş Geldiniz** ekranında dili seçin. QR kodu veya NFC ile kayıt yapmanız istenirse, yöntemiyle eşleşen aşağıdaki adımları izleyin.  
     * NFC: kuruluşunuzun ağına bağlanmak için bir programcı cihazında NFC ile desteklenen cihazınıza dokunun. Ekrandaki istemleri izleyin. Chrome 'un hizmet koşulları ekranına ulaştığınızda, 5. adıma geçin.  

     * QR kodu: [QR kod kaydı](#qr-code-enrollment)'Ndaki adımları doldurun.  

     Başka bir yöntem kullanmanız istenirse adım 3 ' e geçin.    

3. Wi-Fi ' e bağlanın ve **İleri**' ye dokunun. Kayıt yönteminiz ile eşleşen adımı izleyin. 

    * Belirteç: Google oturum açma ekranına geldiğinizde, [belirteç kaydı](#token-enrollment)'ndaki adımları doldurun.  
    * Google sıfırı Touch: Wi-Fi ' a Bağlandıktan sonra cihazınız kuruluşunuz tarafından tanınacaktır. 4. adıma geçin ve kurulum tamamlanana kadar ekrandaki istemleri izleyin.    
 
       ![Google of Touch kullanıyorsanız gördüğünüz Google terimleri ekranının örnek görüntüsü, & devam et ' i vurgulama düğmesi.](./media/google-zero-touch-intune-app-01.png)   
   
4. Google 'ın şartlarını gözden geçirin. Sonra **& devam et**' e dokunun.  

      ![Google terms ekranının örnek görüntüsü, kabul & devam et düğmesine vurgu.](./media/fully-managed-intune-app-04.png)   

5. Chrome 'un hizmet koşullarını gözden geçirin. Sonra **& devam et**' e dokunun.  

   ![Chrome hizmet koşulları ekranının örnek görüntüsü, & devam et düğmesine vurgu.](./media/fully-managed-intune-app-06.png)   

6. Oturum açma ekranında, **oturum açma seçenekleri** ' ne tıklayın ve ardından **başka bir cihazdan oturum açın**. 

7. Ekrandaki kodu yazın.  

8. Akıllı kart etkin cihazınıza geçin ve ekranınızda gösterilen web adresine gidin. 

9. Daha önce yazdığınız kodu girin.

   > [!div class="mx-imgBorder"]
   > ![Şirket Portalı Web sitesinin ekran görüntüsü "kod girin" istemi.](./media/enter-code-intercede.png)

10. Oturum açmak için akıllı kartınızı ekleyin.  

11. Oturum açma ekranında iş veya okul hesabınızı seçin. Ardından mobil cihazınıza geri dönün. 

12. Kuruluşunuzun gereksinimlerine bağlı olarak, ekran kilitleme veya şifreleme gibi ayarları güncelleştirmeniz istenebilir. Bu istemler görürseniz **Ayarla** ' ya dokunun ve ekrandaki yönergeleri izleyin.  

       ![İş telefonunuzu ayarlama ekranınızın örnek görüntüsü, küme oluştur düğmesi.](./media/fully-managed-intune-app-10.png)   

13. Cihazınıza iş uygulamaları yüklemek için, **yükler**' e dokunun. Yükleme tamamlandıktan sonra **İleri**' ye dokunun.  

       ![İş telefonunuzu ayarlama ekranınızın örnek görüntüsü, Install düðmesini vurgulaması.](./media/fully-managed-intune-app-11.png)    

14. Microsoft Intune uygulamasını açmak için **Başlat** ' a dokunun. 

    ![İş telefonunuzu ayarlama ekranınızın örnek görüntüsü, Başlat düğmesini vurguladır.](./media/fully-managed-intune-app-17.png)   
 
15. Mobil cihazınızda Intune uygulamasına dönün ve kayıt tamamlanana kadar ekrandaki yönergeleri izleyin. 

    ![Erişim ayarlama, cihaz ekranınızı kaydetme, bitti düğmesi gibi örnek görüntü.](./media/fully-managed-intune-app-19.png)   

16. Cihazınızı ayarlamayı bitirmeden bu makaledeki [akıllı kartınızı ayarlama](enroll-android-device-entrust-datacard.md#set-up-smart-card) bölümüne ilerleyin.  

### <a name="qr-code-enrollment"></a>QR kod kaydı  
Bu bölümde, şirketinizin sağladığı QR kodunuzu taracaksınız.  İşiniz bittiğinde cihaz kayıt adımlarına geri yönlendiriyoruz.     
  
1. **Karşılama** EKRANıNDA, QR kodu kurulumu 'nu başlatmak için ekrana beş kez dokunun.  

   ![Cihaz kurulumu hoş geldiniz ekranının örnek görüntüsü, ekrana dokunarak görüntülenecek yönergeleri vurgular.](./media/qr-code-intune-app-01.png)  

2. Wi-Fi ' a bağlanmak için ekrandaki yönergeleri izleyin.  
3. Cihazınızın bir QR kodu tarayıcısı yoksa, kurulum ekranları bir tarayıcı yüklendiği için ilerlemeyi gösterir. Yüklemenin tamamlanmasını bekleyin.  
4. İstendiğinde, kuruluşunuzun size verdiği kayıt profili QR kodunu tarayın.  
5. [Cihaza kaydet](#enroll-device)'e dönün, kuruluma devam etmek için 4. adımı izleyin.  

### <a name="token-enrollment"></a>Belirteç kaydı  
Bu bölümde, şirketinizin sunduğu belirteci girersiniz. İşiniz bittiğinde cihaz kayıt adımlarına geri yönlendiriyoruz.  

1. Google oturum açma ekranında, **e-posta veya telefon** kutusuna **AFW # kurulum**yazın. Sonra **İleri**' ye dokunun. 

   ![Google oturum açma ekranının örnek görüntüsü, "AFW # kurulum" ın alana yazılmış olduğunu gösterir.](./media/token-intune-app-01.png)   

2. **Android cihaz ilkesi** uygulaması için **yüklemeyi** seçin. Yükleme işlemine devam edin. Cihazınıza bağlı olarak, ek koşulları gözden geçirmeniz ve kabul etmeniz gerekebilir.    

3. **Bu cihazı kaydet** ekranında **İleri**' yi seçin.  

4. **Kodu girin**' i seçin.  

5. **Tarama veya kod girme** ekranında, kuruluşunuzun size verdiği kodu yazın.  Ardından **İleri**'ye tıklayın.  

   ![Taramanın örnek görüntüsü veya kod girme, Ileri vurgu düğmesi.](./media/token-intune-app-04.png)  

6. [Cihaza kaydet](#enroll-device)'e dönün, kuruluma devam etmek için 4. adımı izleyin.

## <a name="set-up-smart-card"></a>Akıllı kart ayarlama  

1. Kayıt tamamlandıktan sonra, Intune uygulaması akıllı kartınızı ayarlamanıza yönelik bildirim gönderir. Bildirime dokunun. Bildirim alamazsanız, e-postanızı kontrol edin.

   > [!div class="mx-imgBorder"]
   > ![Cihaz giriş ekranında Şirket Portalı anında iletme bildiriminin örnek ekran görüntüsü.](./media/action-required-in-app-android.png)

2. **Akıllı kart ayarla** ekranında:

   1. Kuruluşunuzun kurulum yönergelerinin bağlantısına dokunun. Kuruluşunuz ek yönergeler sağlamıyorsa, bu makaleye gönderilir.

   2. **Başlat**' a dokunun. 

   > [!div class="mx-imgBorder"]
   > ![Şirket Portalı mobil akıllı kart erişimini ayarlama ekranının örnek ekran görüntüsü.](./media/smart-card-open-entrust-android.png)

3. Akıllı kart etkin cihazınıza geçiş yapın ve ıdentityguard 'ı açın.

4. Akıllı kimlik bilgisi oturum açma alanını bulun ve oturum aç düğmesini seçin.

5. Bir sertifika seçmeniz istendiğinde, akıllı kart kimlik bilgilerinizi seçin. Sonra **Tamam**’ı seçin.

6. Akıllı kart PIN 'inizi girin.

7. Eylem listesinden seçim yapmanız istenir. Türetilmiş bir mobil akıllı kimlik bilgileri için kaydolmanızı sağlayan birini seçin. Bağlantı veya düğme, **türetilmiş bir mobil akıllı kart kimlik bilgisi için kaydolmak istiyorum gibi görünebilir.**

8. Başarılı bir şekilde indirdiğiniz ve akıllı kimlik bilgileri etkinleştirilmiş uygulamayı yüklediğinizden emin olmalısınız. Sonra bir sonraki ekrana geçin.

9. Türetilmiş akıllı kart kimlik bilgileriniz hakkında bilgi girin:

    1. Kimlik adı için, *türetilmiş kimlik bilgileri*gibi bir ad girin.  
    2. Açılan menüde, **Entrust ıdentityguard mobil akıllı kimlik bilgileri**' ni seçin.

    3. Sonraki ekrana devam edin. Bir QR kodunu, altında sayısal parolaya sahip olacak şekilde görürsünüz.

10. Android cihazınıza geri dönün. Intune uygulaması > **QR kodu al** ekranında, **İleri**' ye dokunun.

    > [!div class="mx-imgBorder"]
    > ![Şirket Portalı QR kodu alma ekranının örnek ekran görüntüsü.](./media/get-qr-code-entrust-android.png)

11. Intune uygulamasının kameranızı kullanmasına izin vermeniz istenirse, **Izin ver**' e dokunun.

12. Akıllı kart özellikli cihazınızda bulunan QR kodunun görüntüsünü tarayın.

13. **Parola gerekli** EKRANıNDA, QR kodu altında görüntülenen parolayı girin.

    > [!div class="mx-imgBorder"]
    > ![Şirket Portalı "parola gerekli" ekranının örnek ekran görüntüsü.](./media/password-required-entrust-android.png)  

14. Intune uygulaması, iş veya okul kaynaklarına erişmek için gereken sertifikaları indirip yüklemeye başlar. İnternet bağlantınıza bağlı olarak, bu işlem biraz zaman alabilir. Bu süre boyunca uygulamayı kapatmayın.

    > [!div class="mx-imgBorder"]
    > ![Şirket Portalı "sertifika Indirme ve yükleme" ekranının örnek ekran görüntüsü](./media/install-certificates-entrust-android.png)

15. Tüm sertifikalar işlendikten sonra, Intune uygulamasının cihazınızı ayarlamayı tamamlamasını bekleyin. **Her şey ayarlamış** olduğunuzu gördüğünüzde kurulumun tamamlandığını bilirsiniz! etkileşime geçebilirsiniz.

    > [!div class="mx-imgBorder"]
    > !["Tüm hazırsınız" ekranın örnek ekran görüntüsü](./media/all-set-android.png)

## <a name="next-steps"></a>Sonraki adımlar

Kayıt tamamlandıktan sonra e-posta, Wi-Fi ve kuruluşunuzun kullanabildiği tüm uygulamalar gibi iş kaynaklarına erişebilirsiniz. Intune uygulamasında uygulama alma, arama, yükleme ve kaldırma hakkında daha fazla bilgi için bkz.:

* [Cihazınızdaki yönetilen uygulamaları kullanma](use-managed-apps-on-your-device-android.md)  
* [Şirket Portalı Web sitesinden uygulamaları yönetme](manage-apps-cpweb.md)  

Bu bilgiler yardımcı olmadı mı? Şirketinizin destek bölümüne başvurun. Kişi bilgileri için [Şirket Portalı Web sitesine](https://go.microsoft.com/fwlink/?linkid=2010980) bakın.