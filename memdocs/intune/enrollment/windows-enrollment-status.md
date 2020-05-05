---
title: Kayıt durumu sayfası ayarlama
titleSuffix: Microsoft Intune
description: Windows 10 cihazlarını kaydeden kullanıcılar için karşılama sayfası ayarlayın.
keywords: ''
author: ErikjeMS
ms.author: erikje
manager: dougeby
ms.date: 11/26/2019
ms.topic: conceptual
ms.service: microsoft-intune
ms.subservice: enrollment
ms.localizationpriority: high
ms.technology: ''
ms.assetid: 8518d8fa-a0de-449d-89b6-8a33fad7b3eb
ms.reviewer: ericor
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure;seodec18
ms.collection: M365-identity-device-management
ms.openlocfilehash: 8ba3563a243b13b874608ad7a3ec918130e5bb80
ms.sourcegitcommit: fb84a87e46f9fa126c1c24ddea26974984bc9ccc
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 04/22/2020
ms.locfileid: "82022713"
---
# <a name="set-up-an-enrollment-status-page"></a>Kayıt durumu sayfası ayarlama
 
[!INCLUDE [azure_portal](../includes/azure_portal.md)]
 
Kayıt durumu sayfası (ESP) ilk cihaz kaydı sırasında Windows 10 cihazları (sürüm 1803 ve üzeri) hakkındaki yükleme bilgilerini görüntüler. Örneğin:
- [Windows Autopilot](https://docs.microsoft.com/windows/deployment/windows-autopilot/) kullanırken 
- ya da bir kayıt durumu sayfası ilkesi uygulandıktan sonra yönetilen bir cihaz ilk kez başlatılır. 

Kayıt durumu sayfası, kullanıcıların cihaz kurulumu sırasında cihazının durumunu anlamalarına yardımcı olur. Birden çok kayıt durumu sayfası profili oluşturabilir ve bunları, kullanıcıları içeren farklı gruplara uygulayabilirsiniz. Profiller, şunları yapacak şekilde ayarlanabilir:
- Yüklemenin ilerleme durumunu görüntüleme.
- Yükleme tamamlanana kadar kullanımı engelleme.
- Cihaz kurulumu başarısız olursa kullanıcının ne yapabileceğini belirtme.

Ayrıca, her bir profilin öncelik sırasını aynı kullanıcıya yönelik çakışan profil atamalarını hesaba atayabilirsiniz.

> [!NOTE]
> Kayıt durumu sayfası yalnızca atanan bir gruba ait olan bir kullanıcıyı hedefleyebilir ve ilkeyi, cihazı kullanan tüm kullanıcılar için kayıt sırasında ayarlar.  Kayıt durumu sayfası profillerinin cihaz hedeflemesi şu anda desteklenmiyor.

## <a name="available-settings"></a>Kullanılabilir ayarlar

 Aşağıdaki ayarlar, kayıt durumu sayfasının davranışını özelleştirmek için yapılandırılabilir:

<table>
<th align="left">Ayar<th align="left">Yes<th align="left">Hayır
<tr><td>Uygulama ve profil yükleme ilerlemesini göster<td>Kayıt durumu sayfası görüntülenir.<td>Kayıt durumu sayfası görüntülenmiyor.
<tr><td>Tüm uygulamalar ve profiller yüklenene kadar cihaz kullanımını engelle<td>Bu tablodaki ayarlar, kullanıcının olası yükleme sorunlarını ele abilmesi için kayıt durumu sayfasının davranışını özelleştirmek üzere kullanılabilir hale getirilir.
<td>Kayıt durumu sayfası, yükleme başarısızlıklarını ele almak için ek seçenek olmadan görüntülenir.
<tr><td>Yükleme hatası oluşursa kullanıcıların cihazı sıfırlamasına izin ver<td>Yükleme hatası varsa, <b>cihazı Sıfırla</b> düğmesi görüntülenir.<td>Yükleme hatası varsa, <b>cihazı Sıfırla</b> düğmesi gösterilmez.
<tr><td>Yükleme hatası oluşursa kullanıcıların cihazı kullanmasına izin ver<td>Yükleme hatası varsa <b>yine de devam et</b> düğmesi görüntülenir.<td>Yükleme hatası varsa <b>devam et</b> düğmesi gösterilmez.
<tr><td>Yükleme belirtilen dakika sayısından daha uzun sürerse zaman aşımı hatası göster<td colspan="2">Yüklemenin tamamlanmasını beklemek için beklenecek dakika sayısını belirtin. Varsayılan 60 dakikalık bir değer girilir.
<tr><td>Bir hata oluştuğunda özel iletiyi göster<td>Bir yükleme hatası oluşursa görüntülenecek özel bir ileti belirtebileceğiniz bir metin kutusu sağlanır.<td>Varsayılan ileti görüntülenir: <br><b>Yükleme, kuruluşunuz tarafından ayarlanan zaman sınırını aştı. Yardım almak için yeniden deneyin veya BT destek sorumlunuza başvurun.<b>
<tr><td>Kullanıcıların yükleme hatalarıyla ilgili günlükleri toplamasına izin ver<td>Yükleme hatası varsa, bir biriktirme <b>günlüğü</b> düğmesi görüntülenir. <br>Kullanıcı bu düğmeye tıkladığında, <b>Mdmdiagreport. cab</b> günlük dosyasını kaydetmek için bir konum seçmesi istenir<td>Yükleme hatası varsa <b>günlükleri topla</b> düğmesi gösterilmez.
<tr><td>Bu gerekli uygulamalar kullanıcıya/cihaza atanırsa yüklenene kadar cihaz kullanımını engelle<td colspan="2"><b>Tümü</b> veya <b>Seçili</b>öğesini seçin. <br><br><b>Seçili</b> seçilirse, cihazı etkinleştirmeden önce hangi uygulamaların yüklü olması gerektiğini seçmenize olanak sağlayan bir <b>uygulamalar seçin</b> düğmesi görüntülenir.
</table>

## <a name="turn-on-default-enrollment-status-page-for-all-users"></a>Tüm kullanıcılar için varsayılan kayıt durumu sayfasını aç

Kayıt durumu sayfasını açmak için aşağıdaki adımları izleyin.
 
1. [Microsoft Endpoint Manager Yönetim Merkezi](https://go.microsoft.com/fwlink/?linkid=2109431)'nde, **cihazlar** > **Windows** > **Windows kayıt** > **kayıt durumu sayfası**' nı seçin.
2. **Kayıt Durumu Sayfası** dikey penceresinde, **Varsayılan** > **Ayarlar**’ı seçin.
3. **Uygulama ve profil yükleme ilerleyişini göster** için **Evet**’i seçin.
4. Açmak istediğiniz diğer ayarları seçin ve **Kaydet**’i seçin.

## <a name="create-enrollment-status-page-profile-and-assign-to-a-group"></a>Kayıt durumu sayfası profili oluşturma ve gruba atama

1. [Microsoft Endpoint Manager Yönetim Merkezi](https://go.microsoft.com/fwlink/?linkid=2109431)'nde **cihazlar** > **Windows** > **Windows kayıt** > **kayıt durumu sayfası** > **Profil oluştur**' u seçin.
2. Bir **Ad** ve **Açıklama** sağlayın.
3. **Oluştur**’u seçin.
4. **Kayıt Durumu Sayfası** listesinde yeni profili seçin.
5. **Atamaları** > **seçin grupları seçin** > bu profili benimsemek istediğiniz grupları seçin >**Kaydet**' **i seçin** > .
6. **Ayarlar** > bu profile uygulamak istediğiniz ayarları seçin > **Kaydet**’i seçin.

## <a name="set-the-enrollment-status-page-priority"></a>Kayıt durumu sayfası önceliğini ayarlama

Bir kullanıcı birçok grupta olabilir ve birçok kayıt durumu sayfası profili bulunabilir. Bu tür çakışmaları işlemek için her bir profilin önceliklerini ayarlayabilirsiniz. Kaydetme sırasında, birisinin birden fazla kayıt durumu sayfası profili varsa, kaydolan cihaza yalnızca en yüksek öncelikli profil uygulanır.

1. [Microsoft Endpoint Manager Yönetim Merkezi](https://go.microsoft.com/fwlink/?linkid=2109431)'nde, **cihazlar** > **Windows** > **Windows kayıt** > **kayıt durumu sayfası**' nı seçin.
2. Listede profilin üzerine gelin.
3. Üç dikey noktayı kullanarak, profili listede dilediğiniz konuma sürükleyin.

## <a name="block-access-to-a-device-until-a-specific-application-is-installed"></a>Belirli bir uygulama yüklenene kadar cihaz erişimini engelleme

Kullanıcının masaüstüne erişebilmesi için yüklenmesi gereken uygulamaları belirtebilirsiniz.

1. [Microsoft Endpoint Manager Yönetim Merkezi](https://go.microsoft.com/fwlink/?linkid=2109431)'nde, **cihazlar** > **Windows** > **Windows kayıt** > **kayıt durumu sayfası**' nı seçin.
2. Bir profil seçip **Ayarlar**'a tıklayın.
3. **Uygulama ve profil yükleme ilerleyişini göster** için **Evet**'i seçin.
4. **Tüm uygulamalar ve profiller yüklenene kadar cihaz kullanımını engelle** için **Evet**'i seçin.
5. **Bu gerekli uygulamalar kullanıcıya/cihaza atanırsa, bu uygulamaların yüklenmesi Için seçili cihaz kullanımını engelle**' yi seçin. **Selected**
6. **Uygulama seç**'e tıklayın, uygulamaları seçin ve **Seç** > **Kaydet** yolunu izleyin.

Bu listede yer alan uygulamalar, engelleme olarak kabul edilmesi gereken listeyi filtrelemek için Intune tarafından kullanılır.  Hangi uygulamaların yükleneceğini belirtmez.  Örneğin, bu listeyi "uygulama 1", "uygulama 2" ve "uygulama 3" ve "uygulama 3" ve "App 4", cihaza veya kullanıcıya hedeflenmiş olarak yapılandırırsanız, kayıt durumu sayfası yalnızca "uygulama 3" i izler.  "App 4" yine de yüklenecek, ancak kayıt durumu sayfası işlemin tamamlanmasını bekleyemez.

En fazla 25 uygulama belirtilebilir.

## <a name="enrollment-status-page-tracking-information"></a>Kayıt durumu sayfası izleme bilgileri

Kayıt durumu sayfasının bilgileri izlediği üç aşama vardır; cihaz hazırlığı, cihaz kurulumu ve hesap kurulumu.

### <a name="device-preparation"></a>Cihaz hazırlığı

Cihaz hazırlığı için, kayıt durumu sayfası şunları izler:
- Güvenilir Platform Modülü (TPM) Key belirlediğimizi karşıladığımızı (varsa)
- birleştirme sırasında ilerleme Azure Active Directory
- Intune 'a kaydolma
- Intune yönetim uzantılarının yüklemesi

### <a name="device-setup"></a>Cihaz kurulumu

Kayıt durumu sayfası, aşağıdaki cihaz kurulum öğelerini izler (tüm cihazlara veya kaydolan cihazın üye olduğu bir cihaz grubuna atanırsa):
- Güvenlik ilkeleri
  - Tüm kayıtlar için tek bir yapılandırma hizmeti sağlayıcısı (CSP).
  - Intune tarafından yapılandırılan gerçek CSP’ler burada izlenmez.
- Uygulamalar
  - Makine başına iş kolu (LoB) MSI uygulamaları.
  - Yükleme bağlamı ile LoB mağaza uygulamaları = Cihaz.
  - Yükleme bağlamı ile çevrimdışı mağaza ve LoB mağaza uygulamaları = Cihaz.
  - Win32 uygulamaları (yalnızca Windows 10 sürüm 1903 ve üzeri) 
- Bağlantı profilleri
  - **Tüm Cihazlar**’a atanmış VPN veya Wi-Fi profilleri veya kaydedilen cihazın üyesi olduğu bir cihaz grubu (yalnızca Autopilot cihazları için)
- **Tüm Cihazlar**’a atanmış sertifika profilleri veya kaydedilen cihazın üyesi olduğu bir cihaz grubu (yalnızca Autopilot cihazları için)

### <a name="account-setup"></a>Hesap kurulumu
Hesap kurulumu için, kayıt durumu sayfası şu anda oturum açmış olan kullanıcıya atanırsa aşağıdaki öğeleri izler:
- Güvenlik ilkeleri
  - Tüm kayıtlar için tek CSP.
  - Intune tarafından yapılandırılan gerçek CSP’ler burada izlenmez.
- Uygulamalar
  - Tüm Cihazlar, Tüm Kullanıcılar veya cihazı kaydeden kullanıcının üyesi olduğu bir kullanıcı grubuna atanan kullanıcı başına LoB MSI uygulamaları.
  - Tüm Kullanıcılar veya cihazı kaydeden kullanıcının üyesi olduğu bir kullanıcı grubuna atanan makine başına LoB MSI uygulamaları.
  - Aşağıdaki nesnelerden birine atanan LoB Mağazası uygulamaları, çevrimiçi mağaza uygulamaları ve çevrimdışı mağaza uygulamaları:
    - All Devices
    - Tüm Kullanıcılar
    - Cihazı kaydeden Kullanıcı grubu, yükleme bağlamı Kullanıcı olarak ayarlanan bir üyedir.
  - Win32 uygulamaları (yalnızca Windows 10 sürüm 1903 ve üzeri) 
- Bağlantı profilleri
  - Tüm Kullanıcılar veya cihazı kaydeden kullanıcının üyesi olduğu bir kullanıcı grubuna atanan VPN veya Wi-Fi profilleri.
- Sertifikalar
  - Tüm Kullanıcılar veya cihazı kaydeden kullanıcının üyesi olduğu bir kullanıcı grubuna atanan sertifika profilleri.

### <a name="troubleshooting"></a>Sorun giderme
Sorun giderme için sık sorulan sorular.

- Uygulamalarım neden yüklenmedi ve kayıt durumu sayfası kullanılarak izlenmiyor?
  - Uygulamaların, kayıt durumu sayfası kullanılarak yüklenip izlendiğinden emin olmak için şunları yapın:
      - Uygulamalar, "gerekli" atama kullanılarak cihazı (cihaz hedefli uygulamalar için) veya kullanıcıyı (kullanıcı hedefli uygulamalar için) içeren bir Azure AD grubuna atanır.  (Cihaz hedefli uygulamalar, ESP 'nin cihaz aşamasında izlenir ve kullanıcı hedefli uygulamalar, ESP Kullanıcı aşamasında izlenir.)
      - **Tüm uygulamalar ve profiller yüklenene kadar cihaz kullanımını engelle ' i** veya **gerekli uygulamalar yüklenene kadar uygulamayı blok cihaza** Ekle ' ye dahil et ' i belirtin.
      - Uygulamalar cihaz bağlamına yüklenir ve hiçbir Kullanıcı bağlamı uygulanabilirlik kuralına sahip değildir.

- Autopilot olmayan dağıtımlar için kayıt durumu sayfası neden gösteriliyor. Örneğin, bir Kullanıcı Configuration Manager ortak yönetim tarafından kaydedilen bir cihazda ilk kez oturum açtığında?  
  - Kayıt durumu sayfası, aşağıdakiler dahil olmak üzere tüm kayıt yöntemleri için yükleme durumunu listeler.
      - Autopilot
      - Ortak yönetim Configuration Manager
      - ilk kez kayıt durumu sayfası ilkesi uygulanmış olan cihazda Yeni Kullanıcı oturum açtığında
      - **kullanıma hazır deneyim (OOBE) ayarı tarafından sağlanan cihazlara tek göster sayfası** açık ve ilke ayarlandıysa, yalnızca cihazda oturum açan Ilk Kullanıcı kayıt durumu sayfasını alır

- Cihazda yapılandırılmışsa, kayıt durumu sayfasını nasıl devre dışı bırakabilirim?
  - Kayıt durumu sayfası ilkesi, kayıt sırasında bir cihazda ayarlanır. Kayıt durumu sayfasını devre dışı bırakmak için Kullanıcı ve cihaz kayıt durumu sayfası bölümlerini devre dışı bırakmanız gerekir. Aşağıdaki yapılandırmalara sahip özel OMA-URI ayarları oluşturarak bölümleri devre dışı bırakabilirsiniz.

      Kullanıcı kayıt durumu sayfasını devre dışı bırak:

      ```
      Name:  Disable User ESP (choose a name you desire)
      Description:  (enter a description)
      OMA-URI:  ./Vendor/MSFT/DMClient/Provider/MS DM Server/FirstSyncStatus/SkipUserStatusPage
      Data type:  Boolean
      Value:  True 
      ```
      Cihaz kayıt durumu sayfasını devre dışı bırak:

      ```
      Name:  Disable Device ESP (choose a name you desire)
      Description:  (enter a description)
      OMA-URI:  ./Vendor/MSFT/DMClient/Provider/MS DM Server/FirstSyncStatus/SkipDeviceStatusPage
      Data type:  Boolean
      Value:  True 
      ```
- Günlük dosyalarını nasıl toplayabilirim?
  - Kayıt durumu sayfası günlük dosyalarının toplanabilmesi için iki yol vardır:
      - Kullanıcıların, ESP ilkesinde günlükleri toplama yeteneğini etkinleştirin. Kayıt durumu sayfasında bir zaman aşımı oluştuğunda, Son Kullanıcı **günlükleri toplama**seçeneğini belirleyebilir. Bir USB sürücü ekleyerek, günlük dosyaları sürücüye kopyalanabilir
      - SHIFT-F10 tuş sırasını girerek bir komut istemi açın ve günlük dosyalarını oluşturmak için aşağıdaki komut satırını girin: 

      ```
      mdmdiagnosticstool.exe -area Autopilot -cab <pathToOutputCabFile>.cab 
      ```

### <a name="known-issues"></a>Bilinen sorunlar
Aşağıda bilinen sorunlar verilmiştir. 
- ESP profilini devre dışı bırakmak cihazlardan ESP ilkesini kaldırmaz ve kullanıcılar cihazda ilk kez oturum açtıklarında yine de ESP almaya devam eder. ESP profili devre dışı bırakıldığında ilke kaldırılmaz. ESP 'yi devre dışı bırakmak için OMA-URI ' i dağıtmanız gerekir. OMA-URI kullanarak ESP 'yi devre dışı bırakma hakkında yönergeler için bkz. Yukarıdaki. 
- Cihaz kurulumu sırasında yeniden başlatma işlemi, kullanıcıyı hesap kurulum aşamasına geçmeden önce kimlik bilgilerini girmeye zorlar. Kullanıcı kimlik bilgileri, yeniden başlatma sırasında korunmaz. Kullanıcının kimlik bilgilerini girmesini sağlamak için kayıt durumu sayfası devam edebilir. 
- Kayıt durumu sayfası, 1903 ' den küçük Windows 10 sürümlerinde iş ve okul hesabı kaydı ekleme sırasında her zaman zaman aşımına uğrar. Kayıt durumu sayfası, Azure AD kaydının tamamlanmasını bekler. Sorun Windows 10 sürüm 1903 ve daha yeni sürümlerde düzeltildi.  
- ESP ile hibrit Azure AD Autopilot dağıtımı, ESP profilinde tanımlanan zaman aşımı süresinden daha uzun sürer. Karma Azure AD Autopilot dağıtımlarında, ESP, ESP profilinde ayarlanan değerden 40 dakika daha uzun sürer. Bu gecikme, şirket içi AD bağlayıcısının yeni cihaz kaydını Azure AD 'ye oluşturması için zaman kazandırır. 
- Windows oturum açma sayfası, Autopilot kullanıcı denetimli modundaki Kullanıcı adı ile önceden doldurulmuyor. ESP 'nin cihaz kurulumu aşamasında bir yeniden başlatma işlemi varsa:
    - Kullanıcı kimlik bilgileri korunmaz
    - Cihaz kurulum aşamasından hesap kurulum aşamasına geçmeden önce kullanıcının kimlik bilgilerini tekrar girmesi gerekir
- ESP uzun bir süre takılmış veya "tanımlama" aşamasını hiçbir zaman tamamlıyor. Intune, tanımlama aşamasında ESP ilkelerini hesaplar. Geçerli kullanıcıya bir Intune lisansı atanmış değilse bir cihaz, ESP ilkelerini hesaplama hiçbir şekilde tamamlanmayabilir.  
- Microsoft Defender uygulama denetimi 'nin yapılandırılması, Autopilot sırasında yeniden başlatma istemi oluşmasına neden olur. Microsoft Defender uygulamasının (AppLocker CSP) yapılandırılması için yeniden başlatma gerekir. Bu ilke yapılandırıldığında, Autopilot sırasında cihazın yeniden başlatılmasına neden olabilir. Şu anda, yeniden başlatmayı bastırmayı veya ertelemeyi yapmanın bir yolu yoktur.
- DeviceLock ilkesi (https://docs.microsoft.com/windows/client-management/mdm/policy-csp-devicelock) bir ESP profilinin bir parçası olarak etkinleştirildiğinde, iki nedenden dolayı OOBE veya Kullanıcı Masaüstü otomatik oturum açma işlemi unexpectantly hatası verebilir.
  - Cihaz, ESP cihaz kurulum aşamasından çıkmadan önce yeniden başlatmadıysanız, kullanıcıdan Azure AD kimlik bilgilerini girmesi istenebilir. Bu istem, kullanıcının Windows ilk oturum açma animasyonunu gördüğü başarılı bir otomatik oturum açma yerine oluşur.
  - Kullanıcı Azure AD kimlik bilgilerini girdikten sonra, ancak ESP cihaz kurulum aşamasından çıkmadan önce yeniden oturum açma işlemi başarısız olur. Bu hata, ESP cihaz Kurulum aşaması hiç tamamlanmadığından oluşur. Geçici çözüm, cihazı sıfırlamadır.

## <a name="next-steps"></a>Sonraki adımlar
Windows kayıt sayfalarını ayarladıktan sonra, Windows cihazlarını nasıl yöneteceğinizi öğrenin. Daha fazla bilgi için bkz. [Microsoft Intune cihaz yönetimi nedir?](../remote-actions/device-management.md)
