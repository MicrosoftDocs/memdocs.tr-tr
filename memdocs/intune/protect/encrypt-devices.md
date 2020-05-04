---
title: Platformlar desteklenen şifreleme yöntemiyle cihazları şifreleyin
titleSuffix: Microsoft Intune
description: BitLocker veya Filekasası gibi yerleşik şifreleme yöntemleriyle cihazları şifreleyin ve bu şifrelenmiş cihazların kurtarma anahtarlarını Intune portalından yönetin.
keywords: ''
author: brenduns
ms.author: brenduns
manager: dougeby
ms.date: 03/03/2020
ms.topic: conceptual
ms.service: microsoft-intune
ms.subservice: protect
ms.localizationpriority: high
ms.technology: ''
ms.assetid: ''
ms.reviewer: annovich
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.openlocfilehash: d79f97da88a939d95b68a9ef747da87cf3844598
ms.sourcegitcommit: 7f17d6eb9dd41b031a6af4148863d2ffc4f49551
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 04/21/2020
ms.locfileid: "80322463"
---
# <a name="use-device-encryption-with-intune"></a>Intune ile cihaz şifrelemesini kullanma

Cihazlarda verileri korumak üzere yerleşik bir diski veya sürücü şifrelemeyi yönetmek için Intune 'U kullanın.

Uç nokta koruma için cihaz yapılandırma profilinin bir parçası olarak disk şifrelemeyi yapılandırın. Intune tarafından aşağıdaki platformlar ve şifreleme teknolojileri desteklenir:

- macOS: Filekasası
- Windows 10 ve üzeri: BitLocker

Intune Ayrıca, tüm yönetilen cihazlarınızda cihazların şifreleme durumu hakkında ayrıntılı bilgiler sunan yerleşik bir [şifreleme raporu](encryption-monitor.md) sağlar.

## <a name="filevault-encryption-for-macos"></a>MacOS için dosya Kasası şifrelemesi

MacOS çalıştıran cihazlarda Filekasadisk şifrelemesini yapılandırmak için Intune 'U kullanın. Daha sonra, bu cihazların şifreleme ayrıntılarını görüntülemek ve Filekasasına şifrelenmiş cihazların kurtarma anahtarlarını yönetmek için Intune şifreleme raporunu kullanın.

Dosya kasasının cihazda çalışması için Kullanıcı tarafından onaylanan cihaz kaydı gereklidir. Kullanıcının kaydın Kullanıcı tarafından onaylanabilmesi için sistem tercihlerinden yönetim profilini el ile onaylaması gerekir.

Filekasası, macOS ile birlikte gelen bir tam disk şifreleme programıdır. **MacOS 10,13 veya üstünü**çalıştıran cihazlarda dosya kasasını yapılandırmak Için Intune 'u kullanabilirsiniz.

Filekasasını yapılandırmak için, macOS platformu için Endpoint Protection için bir [cihaz yapılandırma profili](endpoint-protection-configure.md) oluşturun. Filekasası ayarları, macOS Endpoint Protection için kullanılabilir ayar kategorilerinden biridir.

Cihazları dosya kasası ile şifrelemek için bir ilke oluşturduktan sonra, ilke iki aşamada cihazlara uygulanır. İlk olarak cihaz, Intune 'un kurtarma anahtarını alıp yedeklemesini sağlamak için hazır hale getirilir. Bu eyleme Emanet denir. Anahtar alındıktan sonra, disk şifrelemesi başlayabilir.

![Dosya Kasası ayarları](./media/encrypt-devices/filevault-settings.png)

Intune ile yönetebileceğiniz Filekasası ayarı hakkında ayrıntılı bilgi için bkz. macOS Endpoint Protection ayarları için Intune makalesindeki [filekasası](endpoint-protection-macos.md#filevault) .

### <a name="permissions-to-manage-filevault"></a>Dosya kasasını yönetme izinleri

Intune 'da Filekasasını yönetmek için hesabınızın ilgili Intune [rol tabanlı erişim denetimi](../fundamentals/role-based-access-control.md) (RBAC) izinlerine sahip olması gerekir.

Aşağıda, **uzak görevler** kategorisinin bir parçası olan ve izin veren yerleşik RBAC rollerinin yer aldığı dosya Kasası izinleri verilmiştir:
 
- **Dosya Kasası anahtarını al**:
  - Yardım Masası Işleci
  - Uç nokta güvenlik yöneticisi

- **Filekasa anahtarını döndür**
  - Yardım Masası Işleci

### <a name="how-to-configure-macos-filevault"></a>MacOS Filekasasını yapılandırma

1. [Microsoft Endpoint Manager Yönetim merkezinde](https://go.microsoft.com/fwlink/?linkid=2109431)oturum açın.

2. **Cihaz** > **yapılandırma profilleri** > **Profil oluştur**' u seçin.

3. Aşağıdaki seçenekleri ayarlayın:

   - Platform: macOS
   - Profil türü: Endpoint Protection

4. **Ayarlar** > **Dosya Kasası**' nı seçin.

5. *Filekasası*için **Etkinleştir**' i seçin.

6. *Kurtarma anahtarı türü*Için yalnızca **kişisel anahtar** desteklenir.

   Son kullanıcılara cihazlarıyla ilgili kurtarma anahtarını alma hakkında yardım almak için bir ileti eklemeyi düşünün. Bu bilgiler, kişisel kurtarma anahtarı döndürme ayarını kullandığınızda son kullanıcılarınız için yararlı olabilir. Bu, düzenli aralıklarla bir cihaz için otomatik olarak yeni bir kurtarma anahtarı üretebilirler.

   Örneğin: kayıp veya son döndürülen kurtarma anahtarını almak Için herhangi bir cihazdan Intune Şirket Portalı Web sitesinde oturum açın. Portalda *cihazlar* ' a gidin ve filekasasının etkinleştirildiği cihazı seçin ve ardından *Kurtarma anahtarını al*' ı seçin. Geçerli kurtarma anahtarı görüntülenir.

7. Kalan [Filekasası ayarlarını](endpoint-protection-macos.md#filevault) iş gereksinimlerinizi karşılayacak şekilde yapılandırın ve ardından **Tamam**' ı seçin.

  8. Ek ayarların yapılandırmasını tamamladıktan sonra profili kaydedin.  

### <a name="manage-filevault"></a>Dosya kasasını yönetme

Intune, bir macOS cihazını Filekasasıyla şifreledikten sonra, Intune [şifreleme raporunu](encryption-monitor.md)görüntülerken filekasasını kurtarma anahtarlarını görüntüleyebilir ve yönetebilirsiniz.

Intune bir macOS cihazını Filekasasıyla şifreledikten sonra, bu cihazın kişisel kurtarma anahtarını herhangi bir cihazdaki Web Şirket Portalı görüntüleyebilirsiniz. Web Şirket Portalı bir kez, şifrelenen macOS cihazını seçin ve ardından "kurtarma anahtarını al" seçeneğini bir uzak cihaz eylemi olarak belirleyin.

### <a name="retrieve-personal-recovery-key-from-mem-encrypted-macos-devices"></a>MEM şifreli macOS cihazlarından kişisel kurtarma anahtarını alma

Son kullanıcılar, iOS Şirket Portalı uygulaması, Android Şirket Portalı uygulaması veya Android Intune uygulaması aracılığıyla kişisel kurtarma anahtarını (Filekasası anahtarı) alabilir. Kişisel kurtarma anahtarına sahip olan cihaz Intune 'a kaydolmalıdır ve Intune aracılığıyla Filekasasıyla şifrelenir. İOS Şirket Portalı uygulamasını, Android Şirket Portalı uygulamasını, Android Intune uygulamasını veya Şirket Portalı Web sitesini kullanarak, son kullanıcı Mac cihazlarına erişmek için gereken **Filekasasını** kurtarma anahtarını görebilir. Son kullanıcılar *, şifrelenmiş ve kayıtlı MacOS cihazı* > **Kurtarma anahtarı al**' ı seçerek **cihazları** > seçebilir. Tarayıcıda Web Şirket Portalı gösterilir ve kurtarma anahtarı görüntülenir. 

## <a name="bitlocker-encryption-for-windows-10"></a>Windows 10 için BitLocker şifrelemesi

Windows 10 çalıştıran cihazlarda BitLocker Sürücü Şifrelemesi yapılandırmak için Intune 'u kullanın. Ardından, bu cihazların şifreleme ayrıntılarını görüntülemek için Intune şifreleme raporunu kullanın. Ayrıca, Azure Active Directory (Azure AD) içinde bulunan ve cihazlarınızdan BitLocker için önemli bilgilere erişebilirsiniz.

BitLocker, **Windows 10 veya üzerini**çalıştıran cihazlarda kullanılabilir.

Windows 10 veya sonraki bir platformda Endpoint Protection için bir [cihaz yapılandırma profili](endpoint-protection-configure.md) oluşturduğunuzda BitLocker 'ı yapılandırın. BitLocker ayarları, Windows 10 Endpoint Protection için Windows şifreleme ayarları kategorisinde bulunur.

![BitLocker ayarları](./media/encrypt-devices/bitlocker-settings.png)

### <a name="how-to-configure-windows-10-bitlocker"></a>Windows 10 BitLocker 'ı yapılandırma

1. [Microsoft Endpoint Manager Yönetim merkezinde](https://go.microsoft.com/fwlink/?linkid=2109431)oturum açın.

2. **Cihaz** > **yapılandırma profilleri** > **Profil oluştur**' u seçin.

3. Aşağıdaki seçenekleri ayarlayın:

   - Platform: Windows 10 ve üzeri
   - Profil türü: Endpoint Protection

4. **Ayarlar** > **Windows şifrelemesi**' ni seçin.

5. BitLocker ayarlarını iş gereksinimlerinizi karşılayacak şekilde yapılandırın ve ardından **Tamam**' ı seçin.

6. Ek ayarların yapılandırmasını tamamladıktan sonra profili kaydedin.

### <a name="silently-enable-bitlocker-on-devices"></a>Cihazlarda BitLocker 'ı sessizce etkinleştirin

Bir cihazda BitLocker 'ı otomatik olarak ve sessizce etkinleştirmenizi sağlayan bir BitLocker ilkesi yapılandırabilirsiniz. Diğer bir deyişle, bu kullanıcı cihazda yerel yönetici olmasa bile, BitLocker son kullanıcıya herhangi bir kullanıcı ARABIRIMI sunmadan başarıyla etkinleştirilir.

**Cihaz önkoşulları**:

Bir cihazın BitLocker 'ı sessizce etkinleştirmek için uygun olması için aşağıdaki koşullara uyması gerekir:

- Cihazın Windows 10 sürüm 1809 veya üstünü çalıştırması gerekir
- Cihazın Azure AD 'ye katılmış olması gerekir  

**BitLocker ilke yapılandırması**:

BitLocker [temel ayarları](../protect/endpoint-protection-windows-10.md#bitlocker-base-settings) için aşağıdaki Iki ayar BitLocker ilkesinde yapılandırılmalıdır:

- **Diğer disk şifreleme** = *bloğu*uyarısı.
- **Azure AD JOIN** = *izin verme* sırasında standart kullanıcıların şifrelemeyi etkinleştirmesine izin ver

BitLocker ilkesi, bir başlangıç PIN 'ı veya başlangıç anahtarı kullanımını **gerektirmemelidir** . TPM başlangıç PIN 'ı veya başlangıç anahtarı *gerektiğinde*, BitLocker sessizce etkinleştirilemez ve son kullanıcıdan etkileşim gerektirir.  Bu gereksinim, aynı ilkedeki aşağıdaki üç [BitLocker işletim sistemi sürücü ayarı](../protect/endpoint-protection-windows-10.md#bitlocker-os-drive-settings) aracılığıyla karşılanır:

- **Uyumlu TPM başlangıç PIN 'ı** *TPM Ile başlangıç PIN 'i gerektirecek* şekilde ayarlanmamış olmalıdır
- **Uyumlu TPM başlangıç anahtarı** *TPM Ile başlangıç anahtarı gerektirecek* şekilde ayarlanmamış olmalıdır
- **Uyumlu TPM başlangıç anahtarı ve PIN 'ı** *TPM ile başlangıç anahtarı ve PIN gerektirecek* şekilde ayarlanmamış olmalıdır



### <a name="manage-bitlocker"></a>seçin,

Intune bir Windows 10 cihazını BitLocker ile şifreledikten sonra, Intune [şifreleme raporunu](encryption-monitor.md)görüntülerken BitLocker kurtarma anahtarlarını görüntüleyebilir ve alabilirsiniz.

### <a name="rotate-bitlocker-recovery-keys"></a>BitLocker kurtarma anahtarlarını döndür

Windows 10 sürüm 1909 veya üstünü çalıştıran bir cihazın BitLocker kurtarma anahtarını uzaktan döndürmek için bir Intune cihaz eylemini kullanabilirsiniz.

#### <a name="prerequisites"></a>Önkoşullar

Cihazların BitLocker kurtarma anahtarının döndürmesini desteklemek için aşağıdaki önkoşulları karşılaması gerekir:

- Cihazların Windows 10 sürüm 1909 veya üstünü çalıştırması gerekir

- Azure AD 'ye katılmış ve Hibriya katılmış cihazlarda anahtar döndürme özelliğinin etkinleştirilmesi için destek bulunmalıdır:

  - **İstemci tabanlı kurtarma parolası döndürme**

  Bu ayar, Windows 10 Endpoint Protection cihaz yapılandırma ilkesinin bir parçası olarak *Windows şifrelemesi* altında bulunur.
  
#### <a name="to-rotate-the-bitlocker-recovery-key"></a>BitLocker kurtarma anahtarını döndürmek için

1. [Microsoft Endpoint Manager Yönetim merkezinde](https://go.microsoft.com/fwlink/?linkid=2109431)oturum açın.

2. **Cihazlar** > **tüm cihazlar**' ı seçin.

3. Yönettiğiniz cihazların listesinde bir cihaz seçin, **daha fazla**' yı seçin ve ardından **BitLocker anahtar döndürme** cihazı uzak eylemi ' ni seçin.

## <a name="next-steps"></a>Sonraki adımlar

[Bir cihaz uyumluluk](compliance-policy-create-windows.md) ilkesi oluşturun.

Yönetmek için şifreleme raporunu kullanın:

- [BitLocker kurtarma anahtarları](encryption-monitor.md#bitlocker-recovery-keys)
- [Filekasası kurtarma anahtarları](encryption-monitor.md#filevault-recovery-keys)

Intune ile yapılandırabileceğiniz şifreleme ayarlarını inceleyerek şunları yapabilirsiniz:

- [Kurulumu](endpoint-protection-windows-10.md#windows-encryption)
- [FileVault](endpoint-protection-macos.md#filevault)
