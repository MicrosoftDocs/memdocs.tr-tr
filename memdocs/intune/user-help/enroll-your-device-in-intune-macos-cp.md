---
title: Mac 'nizi Intune Şirket Portalı kaydetme | Microsoft Docs
description: Şirket Portalı App ile Mac 'i Intune 'a kaydetmeyi öğrenin.
keywords: Mac OS X, macOS, OS X
author: lenewsad
ms.author: lanewsad
manager: dougeby
ms.date: 06/18/2020
ms.topic: end-user-help
ms.prod: ''
ms.service: microsoft-intune
ms.subservice: end-user
ms.technology: ''
ms.assetid: 3bb659cc-9b57-4d19-8631-2c26749fa71c
searchScope:
- User help
ROBOTS: ''
ms.reviewer: kakyker
ms.suite: ems
ms.custom: intune-enduser
ms.collection: ''
ms.openlocfilehash: fe405b66892ec7777d8d1572b2fb6ab6ce1aaa91
ms.sourcegitcommit: 387706b2304451e548d6d9c68f18e4764a466a2b
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 06/19/2020
ms.locfileid: "85094210"
---
# <a name="enroll-your-macos-device-using-the-company-portal-app"></a>Şirket Portalı uygulamasını kullanarak macOS cihazınızı kaydetme  

İş veya okul e-postanıza, dosyalarınıza ve uygulamalarınıza güvenli erişim kazanmak için macOS cihazınızı Intune Şirket Portalı uygulamasına kaydedin.

Kuruluşlar, özel verilere erişebilmek için genellikle cihazınızı kaydetmeniz gerekir. Cihazınız kaydedildikten sonra, *yönetilen*hale gelir. Kuruluşunuz, Intune gibi bir mobil cihaz yönetimi (MDM) sağlayıcısı aracılığıyla cihaza ilkeler ve uygulamalar atayabilir. Cihazınızdaki iş veya okul bilgilerine sürekli erişim sağlamak için cihazınızı kuruluşunuzun ilke ayarlarıyla eşleşecek şekilde ayarlamanız gerekir.  

Bu makalede, macOS için Şirket Portalı uygulamasının, kuruluşunuzun gereksinimlerini karşılayacak şekilde cihazınızı ayarlamak ve sürdürmek üzere nasıl kullanılacağı açıklanır.  


## <a name="what-to-expect-from-the-company-portal-app"></a>Şirket Portalı uygulamasından bekleyebilecekleriniz

İlk kurulum sırasında Şirket Portalı uygulama oturum açmanızı ve kuruluşunuzla kimlik doğrulamasından geçmesini gerektirir. Şirket Portalı, kuruluşunuzun gereksinimlerini karşılamak için yapılandırmanız gereken cihaz ayarlarını size bildirir. Örneğin kuruluşlar genellikle uymanız gereken en düşük veya en yüksek karakterli parola gereksinimleri ayarlar.    

Cihazınızı kaydettikten sonra, Şirket Portalı cihazın kuruluşunuzun gereksinimlerine göre korunduğundan her zaman emin olur. Örneğin, güvenilir olmayan bir kaynaktan uygulama yüklüyorsanız Şirket Portalı sizi uyarır ve kuruluşunuzun kaynaklarına erişimi kısıtlayabilir. Bunun gibi uygulama koruma ilkeleri yaygın bir uygulamadır. Erişimi yeniden kazanmak için büyük olasılıkla uygulamayı kaldırmanız gerekecektir. 

Kayıt sonrasında, kuruluşunuz Multi-Factor Authentication gibi yeni bir güvenlik gereksinimini zorlarsa Şirket Portalı sizi uyarır. Cihazınızla çalışmaya devam edebilmek için bazı değişiklikler yapmaya vaktiniz olur.  

Kayıt hakkında daha fazla bilgi edinmek için bkz. [Şirket Portalı uygulamasını yüklediğimde ve cihazımı kaydettiğimde ne olur?](what-happens-if-you-install-the-Company-Portal-app-and-enroll-your-device-in-intune-macos.md).  

## <a name="get-your-macos-device-managed"></a>MacOS cihazınızın yönetilmesini sağlayın  
MacOS cihazınızı kuruluşunuza kaydetmek için aşağıdaki adımları kullanın. Cihazınızın macOS 10,12 veya sonraki bir sürümü çalıştırması gerekir.   

> [!NOTE]
> Bu süreç boyunca, Şirket Portalı anahtarlığınıza depolanmış gizli bilgilerin kullanılmasına izin vermeniz istenebilir. Bu istemler Apple Security 'nin bir parçasıdır. İstemi aldığınızda, oturum açma Anahtarlık parolanızı yazın ve **her zaman Izin ver**' i seçin. Klavyenizde **ENTER** veya **Return** tuşuna basarsanız, Istem bunun yerine **izin ver**' i seçerek ek istemlere neden olabilir.  

### <a name="install-company-portal-app"></a>Şirket Portalı uygulamasını yükler  
1. Mac 'i [Kaydet](https://go.microsoft.com/fwlink/?linkid=853070)'e gidin.  
2. Şirket Portalı Installer. pkg dosyası indirilir. Yükleyiciyi açın ve adımlarla devam edin. 
3. Yazılım lisans sözleşmesini kabul edin. 
4. Yazılımı yüklemek için cihaz parolanızı veya kayıtlı parmak izini girin.  
5. Şirket Portalı açın. 

> [!IMPORTANT]
> Microsoft yazılımlarını güncelleştirmek için Microsoft otomatik güncelleştirme açılabilir. Tüm güncelleştirmeler yüklendikten sonra Şirket Portalı uygulamasını açın. En iyi kurulum deneyimi için en son Microsoft otomatik güncelleştirme ve Şirket Portalı sürümlerini kurun.  


### <a name="enroll-your-mac"></a>Mac 'nizi kaydetme  


1. İş veya okul hesabınızla Şirket Portalı için oturum açın.  
2. Uygulama açıldığında **Başlat**' ı seçin.  
3. Kuruluşunuzun kayıtlı cihazınızda [neleri görebileceğini ve neleri görebileceklerini](what-info-can-your-company-see-when-you-enroll-your-device-in-intune.md) gözden geçirin. Daha sonra **Devam** seçeneğini belirleyin.
4. **Yönetim profilini yükle** ekranında **profil indir**' i seçin.  

    ![Şirket Portalı örnek ekran görüntüsü, yönetim profilini yükler ekranı, parola istemi 'ni vurgular.](./media/install-management-profile-macos-2006.png)   

5. Cihazınızın sistem tercihleri açılır.  
    a. **Yüklemeyi** seçin ve sonra yeniden **Kur** ' u seçin.  
    b. İstenirse, cihaz parolanızı girin.   
6. Profil yüklendikten sonra, **Yönetim profili**altındaki profiller listesinde görünür.
    ![Sistem Tercihleri, Yönetim profili ekranının, "Onayla" düğmesinin örnek ekran görüntüsü.](./media/management-profile-approve-macos-2006.png)   
7. Şirket Portalı dön.    
8. Kuruluşunuz, cihaz ayarlarınızı güncelleştirmenizi gerektirebilir. Ayarları güncelleştirmeyi tamamladığınızda **yeniden dene**' yi seçin.  

    ![Şirket Portalı örnek ekran görüntüsü, cihaz ayarlarını güncelleştirme ekranının, yeniden deneme düğmesini vurgulanması.](./media/update-settings-mac-2006.png)  
9. Kurulum tamamlandığında **bitti**' yi seçin.  


 ## <a name="troubleshooting-and-feedback"></a>Sorun giderme ve geri bildirim   

Kayıt sırasında sorunlarla karşılaşırsanız, **Help**  >  Microsoft uygulama geliştiricilerine sorunu bildirmek için Yardım**Tanılama raporu gönder** ' e gidin. Bu bilgiler, uygulamanın iyileştirilmesine yardımcı olmak için kullanılır. Bu bilgiler ayrıca, BT 'nin yardım almak için BT 'yi desteklemesi durumunda sorunu çözmeye yardımcı olması için de kullanılır.  

Sorunu Microsoft 'a bildirdikten sonra, deneyiminizin ayrıntılarını BT destek sorumlunuza gönderebilirsiniz. **E-posta ayrıntılarını**seçin. E-postanın gövdesinde karşılaştığınız şeyleri yazın. Destek sorumlunuza ait e-posta adresini bulmak için Şirket Portalı App > **Contact**adresine gidin. Veya [Şirket portalı Web sitesini](https://go.microsoft.com/fwlink/?linkid=2010980)denetleyin.  
 

Ayrıca, Microsoft Intune Şirket Portalı ekibi görüşlerinizi duymak için çok sevecekti. **Help**  >  Düşüncelerinizi ve fikirlerinizi paylaşmak için yardıma**geri bildirim gönder** sayfasına gidin.  

## <a name="unverified-profiles"></a>Doğrulanmamış profiller  
Yüklü mobil cihaz yönetimi (MDM) profillerini **Sistem Tercihleri**  >  **profillerinde**görüntülediğinizde, bazı profiller doğrulanmamış bir durum gösterebilir. Yönetim profilinde doğrulanmış bir durum olduğu sürece, endişelenmeniz gerekmez.  

MDM kanalı bağlantısını tanımlayan yönetim profilidir. Yönetim profili doğrulanmadığı sürece, bu kanal aracılığıyla makineye teslim edilen diğer profiller, yönetim profilinin güvenlik nitelikleri de devralınır.  

## <a name="updating-the-company-portal-app"></a>Şirket Portalı uygulamasını güncelleştirme

Şirket Portalı uygulamasının güncelleştirilmesi, macOS için Microsoft otomatik güncelleştirme aracılığıyla diğer Office uygulamaları ile aynı şekilde yapılır. [MacOS Için Microsoft uygulamalarını güncelleştirme](https://support.office.com/article/Check-for-Office-for-Mac-updates-automatically-bfd1e497-c24d-4754-92ab-910a4074d7c1)hakkında daha fazla bilgi edinin.  

## <a name="next-steps"></a>Sonraki Adımlar  
Bu bilgiler yardımcı olmadı mı? Şirketinizin destek bölümüne başvurun. Kişi bilgileri için [Şirket Portalı Web sitesine](https://go.microsoft.com/fwlink/?linkid=2010980) bakın.  


