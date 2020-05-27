---
title: İOS veya ıpados cihazını Intune Şirket Portalı ve DıŞA purebred ile kaydetme
description: İOS veya ıpados cihazını kaydetmeyi ve DıŞA yönelik kimlik doğrulaması ile birlikte bulunan kimlik doğrulamasını nasıl ayarlayacağınızı öğrenin.
keywords: ''
author: lenewsad
ms.author: lanewsad
manager: dougeby
ms.date: 10/31/2019
ms.topic: end-user-help
ms.prod: ''
ms.service: microsoft-intune
ms.subservice: end-user
ms.technology: ''
ms.assetid: ''
searchScope:
- User help
ROBOTS: ''
ms.reviewer: tisilver
ms.suite: ems
ms.custom: intune-enduser
ms.collection: ''
ms.openlocfilehash: 50330bbdc61eeeada022c44f4d1f2f68b31f19a4
ms.sourcegitcommit: a77ba49424803fddcaf23326f1befbc004e48ac9
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 05/27/2020
ms.locfileid: "83881549"
---
# <a name="set-up-ios-or-ipados-device-with-company-portal-and-disa-purebred"></a>İOS veya ıpados cihazını Şirket Portalı ve DıŞA purebred ile ayarlama  

Kuruluşunuzun e-postasına, dosyalarına ve uygulamalarına güvenli, mobil erişim kazanmak için cihazınızı Intune Şirket Portalı uygulamasına kaydedin. Cihazınız kaydedildikten sonra, *yönetilen*hale gelir. Kuruluşunuz, Intune gibi bir mobil cihaz yönetimi (MDM) sağlayıcısı aracılığıyla cihaza ilkeler ve uygulamalar atayabilir.  

Kayıt sırasında, bir türetilmiş kimlik bilgisini cihazınıza de yüklersiniz. Kuruluşunuz, kaynaklara erişirken veya e-postaları imzalama ve şifreleme için türetilmiş kimlik bilgilerini bir kimlik doğrulama yöntemi olarak kullanmanızı gerektirebilir. 

Şunları yapmak için bir akıllı kart kullanıyorsanız, büyük olasılıkla türetilmiş bir kimlik bilgisi ayarlamanız gerekir:

* Okul veya iş uygulamalarında oturum açma, Wi-Fi ve sanal özel ağlar (VPN)
* Okul veya iş e-postalarını S/MIME sertifikaları kullanarak imzalama ve şifreleme  

Bu makalede şunları yapacaksınız:  

   * Intune Şirket Portalı ile bir mobil iOS veya ıpados cihazı kaydedin.  
   * Kuruluşunuzun türetilmiş kimlik bilgisi sağlayıcısından, DıŞA purebred: https:/cyber.mil/pki-pke/purebred/türetilmiş bir kimlik bilgisi alın \/ .  

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
* Mobil cihazınız
* Cihazınızda yüklü iOS ve Idos Intune Şirket Portalı uygulaması   

Ayrıca, kurulum sırasında purebred Aracısı veya temsilcisiyle iletişim kurmanız gerekecektir.      

## <a name="enroll-device"></a>Cihaz kaydetme  
1. Mobil cihazınızda iOS için Şirket Portalı App/ıpados ' i açın ve iş hesabınızla oturum açın.  

2. Ekrandaki kodu yazın.  

    ![Ekran ileti ve kodu ile Şirket Portalı uygulamasının örnek görüntüsü.](./media/copy-code-intercede.png)  
3. Akıllı kart etkin cihazınıza geçin ve adresine gidin https://microsoft.com/devicelogin . 
4. Daha önce yazdığınız kodu girin.  

    ![Şirket Portalı Web sitesinin örnek ekran görüntüsü "kodu gir" istemi.](./media/enter-code-intercede.png)   

5. Oturum açmak için akıllı kartınızı ekleyin.  
6. Mobil cihazınızda Şirket Portalı uygulamasına dönün ve cihazınızı kaydetmek için ekrandaki yönergeleri izleyin.  
7. Kayıt tamamlandıktan sonra, Şirket Portalı akıllı kartınızı ayarlama konusunda sizi uyarır. Bildirime dokunun. Bildirim alamazsanız, e-postanızı kontrol edin.   

    ![Cihaz giriş ekranında Şirket Portalı anında iletme bildiriminin örnek ekran görüntüsü.](./media/action-required-in-app-intercede.png)  
8. **Mobil akıllı kart erişim ekranında kurulum** :  
    a. Kuruluşunuzun kurulum yönergelerinin bağlantısına dokunun. Kuruluşunuz ek yönergeler sağlamıyorsa, bu makaleye gönderilir.  
    b. Purebred uygulamasını açmak için **Aç** ' a tıklayın.  

    ![Şirket Portalı mobil akıllı kart erişimini ayarlama ekranının örnek ekran görüntüsü.](./media/smart-card-open-disa-purebred.png)  
9. Purebred kayıt uygulamasını açmak Şirket Portalı izin vermeniz istendiğinde **Aç**' ı seçin.   

    ![Rekkred uygulamasını açmak için Şirket Portalı isteminin örnek ekran görüntüsü.](./media/open-app-prompt-disa-purbred.png)  
10. Uygulama çalışırken, purebred kayıt yapılandırma profilini yapılandırmak ve indirmek için kuruluşunuzun purebred aracısıyla birlikte çalışın.   
11. Ayarlar uygulaması > **genel**  >  **profiller cihaz yönetimi**  >  **yüklemesi profili** & ' ne gidin ve **yükler**' e dokunun.  
12. Cihaz geçiş kodunuzu girin.  
13. Profili yükler. Yüklemeyi başlatmak için birden çok kez **yükleme** ' ye dokunmanız gerekebilir. 
14. Purebred kayıt uygulamasına geri dönün. Devam etmek için purebred aracısının yönergelerini izleyin.  
 
15. Yapılandırma profilini indirdikten sonra, ayarlar uygulaması > **genel**  >  **profiller cihaz yönetimi**  >  **yükleme profili** & ' ne gidin ve **Yükle**' ye dokunun.   
16.  Cihaz geçiş kodunuzu girin.
17. Profili yükler. Yüklemeyi başlatmak için birden çok kez **yükleme** ' ye dokunmanız gerekebilir. 
18. Yükleme tamamlandıktan sonra Şirket Portalı uygulamasına geri dönün.  
19.  **Mobil akıllı kart erişimi kurulumu** ekranında, **devam**' a dokunun.  

20. **Sertifikaları Içeri aktar** ekranında, dışarı aktarılan türetilmiş kimlik bilgisini alıp içeri aktarırsınız.  

    a. **Devam**' a dokunun.   

    ![Sertifikaları Içeri aktarma Şirket Portalı ayarlama ekranının örnek ekran görüntüsü.](./media/import-certificate-disa-purebred.png)  
    b. İCloud sürücü **gezinme**  >  **konumlarına** gidin ve **diğer konumlar**' a dokunun.  

    ![İCloud sürücüsünün örnek ekran görüntüsü, daha fazla konum seçeneğine gözatıp menü vurgulaması.](./media/icloud-drive-more-locations.png)  
    c. **Purebred anahtar zincirini**etkinleştirmek için anahtara dokunun.  

    ![İCloud sürücüsünün örnek ekran görüntüsü, purebred anahtar zinciri anahtarının etkin olduğunu vurgulama görünümü.](./media/icloud-drive-enable-purebred-keychain.png)   

    d. **Purebred kimlik bilgisi paketi**' ne dokunun.  

    ![Seçilebilir purebred kimlik bilgisi paketi seçeneği içeren bir iOS ekranının örnek ekran görüntüsü.](./media/purebred-credential-package.png)  
    f. Sertifika listesi görüntülenir. Bir tane seçin ve ardından **anahtarı Içeri aktar**' a dokunun.  

    ![Seçilebilir sertifikaların listesinin örnek ekran görüntüsü, önceden seçilmiş bir.](./media/import-purebred-keychain.png) 
21. Şirket Portalı uygulamasına dönün ve Şirket Portalı cihazınızın kurulumunu tamamlamasını bekleyin.   

## <a name="next-steps"></a>Sonraki adımlar  
Kayıt tamamlandıktan sonra e-posta, Wi-Fi ve kuruluşunuzun kullanabildiği tüm uygulamalar gibi iş kaynaklarına erişebilirsiniz. Şirket Portalı uygulamaları alma, arama, yükleme ve kaldırma hakkında daha fazla bilgi için bkz.:

* [Şirket Portalı Web sitesinden uygulamaları yönetme](manage-apps-cpweb.md)  
* [Cihazınızdaki yönetilen uygulamaları kullanma](use-managed-apps-on-your-device-ios.md)  

Bu bilgiler yardımcı olmadı mı? Şirketinizin destek bölümüne başvurun. Kişi bilgileri için [Şirket Portalı Web sitesine](https://go.microsoft.com/fwlink/?linkid=2010980) bakın.
