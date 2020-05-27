---
title: Microsoft Intune şifreli cihazlar için şifreleme raporu
titleSuffix: Microsoft Intune
description: İOS/ıpados veya Windows cihaz şifreleme durumunuz üzerinde bir rapor görüntüleyin ve Microsoft Intune portalından dosya kasası ve BitLocker Kurtarma anahtarlarına erişin.
keywords: ''
author: brenduns
ms.author: brenduns
manager: dougeby
ms.date: 11/18/2019
ms.topic: how-to
ms.service: microsoft-intune
ms.subservice: protect
ms.localizationpriority: high
ms.technology: ''
ms.assetid: ''
ms.reviewer: shpate
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.openlocfilehash: 1199c6db96325a103394cfb53a4ca70092cd3767
ms.sourcegitcommit: 302556d3b03f1a4eb9a5a9ce6138b8119d901575
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 05/27/2020
ms.locfileid: "83989657"
---
# <a name="monitor-device-encryption-with-intune"></a>Intune ile cihaz şifrelemesini izleme

Microsoft Intune şifreleme raporu, cihazın şifreleme durumu hakkındaki ayrıntıları görüntülemek ve cihaz kurtarma anahtarlarını yönetmek için seçenekleri bulmak için merkezi bir konumdur. Kullanılabilir kurtarma anahtarı seçenekleri, görüntülemekte olduğunuz cihazın türüne bağlıdır.

Raporu bulmak için [Microsoft Endpoint Manager Yönetim Merkezi](https://go.microsoft.com/fwlink/?linkid=2109431)' nde oturum açın. **Cihazlar**  >  **İzleyicisi**' ni seçin ve sonra *yapılandırma*altında **şifreleme raporu**' nu seçin.

## <a name="view-encryption-details"></a>Şifreleme ayrıntılarını görüntüle

Şifreleme raporu, yönettiğiniz desteklenen cihazlar genelinde ortak ayrıntıları gösterir. Aşağıdaki bölümlerde, Intune 'un raporda sunduğu bilgiler hakkındaki ayrıntılar sağlanmaktadır.

### <a name="prerequisites"></a>Ön koşullar

Şifreleme raporu, aşağıdaki işletim sistemi sürümlerini çalıştıran cihazlarda raporlamayı destekler:

- macOS 10,13 veya üzeri
- Windows sürüm 1607 veya üzeri

### <a name="report-details"></a>Rapor ayrıntıları

Şifreleme raporu bölmesinde, bu cihazlarla ilgili üst düzey ayrıntılarla yönettiğiniz cihazların bir listesi görüntülenir. Ayrıntıya git ' i listeden bir cihaz seçebilir ve cihazlar [Cihaz şifreleme durumu](#device-encryption-status) bölmesinden ek ayrıntılar görüntüleyebilirsiniz.

- **Cihaz adı** -cihazın adı.
- **Işletim sistemi** – Windows veya MacOS gibi cihaz platformu.
- **Işletim sistemi sürümü** : cihazdaki Windows veya MacOS sürümü.
- **TPM sürümü** *(yalnızca Windows 10 için geçerlidir)* – Windows 10 cihazında Güvenilir Platform Modülü (TPM) yongasının sürümü.
- **Şifrelemeye hazır olma** : cihazların değerlendirilmesi, BitLocker veya filekasası Şifrelemesi gibi uygun bir şifreleme teknolojisini desteklemeye hazır olma. Cihazlar şu şekilde tanımlanır:
  - **Hazırlanıyor**: cihaz, cihazın aşağıdaki gereksinimleri KARŞıLAMASı gereken MDM ilkesi kullanılarak şifrelenebilir:

    **MacOS cihazları için**:
    - macOS sürüm 10,13 veya üzeri

    **Windows 10 cihazları için**:
    - Sürüm 1709 veya üzeri, *iş*, *Kurumsal*, *eğitim*veya sürüm 1809 ya da *Pro* 'nun daha yeni sürümü
    - Cihazda bir TPM yongasının olması gerekir

    Daha fazla bilgi için Windows belgelerindeki [BitLocker yapılandırma hizmeti sağlayıcısına (CSP)](https://docs.microsoft.com/windows/client-management/mdm/bitlocker-csp) bakın.

  - **Yok**: cihazın tam şifreleme becerileri yoktur, ancak yine de şifrelemeyi destekler. Örneğin, bir Windows cihazı, bir kullanıcı tarafından el ile veya TPM olmadan şifrelemeye izin vermek üzere ayarlanabilir grup ilkesi aracılığıyla şifrelenmiş olabilir.
  - **Uygulanamaz**: Bu cihazı sınıflandırmak için yeterli bilgi yok.

- **Şifreleme durumu** – işletim sistemi sürücüsünün şifrelenip şifrelenmediği.

- **Kullanıcı asıl adı** -cihazın birincil kullanıcısı.

### <a name="device-encryption-status"></a>Cihaz şifreleme durumu

Şifreleme raporundan bir cihaz seçtiğinizde, Intune **Cihaz şifreleme durumu** bölmesini görüntüler. Bu bölme aşağıdaki ayrıntıları sağlar:

- **Cihaz adı** – görüntülemekte olduğunuz cihazın adı.

- **Şifreleme hazırlığı** -CIHAZLARıN değerlendirmesi MDM ilkesi aracılığıyla şifrelemeyi desteklemeye hazır.

  Örneğin: bir Windows 10 cihazının *hazır olmadığı hazır*olmadığında, şifrelemeyi desteklemeye devam edebilir. Hazırlama *atamasını sağlamak* Için, Windows 10 CIHAZıNıN bir TPM yongasına sahip olması gerekir. Şifrelemeyi desteklemek için TPM yongaları gerekli değildir. (Daha fazla bilgi için, önceki bölümde *şifreleme hazırlığı* bölümüne bakın.)

- **Şifreleme durumu** -işletim sistemi sürücüsünün şifreli olup olmadığı. Intune 'un bir cihazın şifreleme durumunu veya bu duruma yönelik bir değişikliği rapor etmek 24 saate kadar sürebilir. Bu süre, işletim sisteminin şifrelenmesi için zaman ve cihazın Intune 'a geri rapor olması için zaman içerir.

  Cihaz iade etme işlemi normalde gerçekleşmeden önce, Filekasası şifreleme durumunun raporlanmasını hızlandırmak için, şifreleme tamamlandıktan sonra kullanıcıların cihazlarını eşitlemesini sağlayabilirsiniz.

- **Profiller** – bu cihaza uygulanan ve aşağıdaki değerlerle yapılandırılmış olan *cihaz yapılandırma* profillerinin bir listesi:

  - MacOS
    - Profil türü = *Endpoint Protection*
    - Ayarlar > Filekasası > Filekasası = *Etkinleştir*

  - Windows 10:
    - Profil türü = *Endpoint Protection*
    - Ayarlar > Windows şifrelemesi > şifreleme cihazları = *iste*

  *Profil durumu özetinden* sorun olduğunu belirlemek için profil listesini tek tek gözden geçirmek için kullanabilirsiniz.

- **Profil durumu Özeti** : Bu cihaza uygulanan profillerin Özeti. Özet, uygulanabilir profiller genelinde en az iyi koşulu temsil eder. Örneğin, birkaç uygulanabilir profilden yalnızca biri bir hata ile sonuçlanırsa, *profil durumu Özeti* *hata*görüntüler.

  Bir durumun daha fazla ayrıntılarını görüntülemek için **Intune**  >  **cihaz yapılandırma**  >  **profilleri**' ne gidin ve profili seçin. İsteğe bağlı olarak, **cihaz durumu** ' nu seçin ve ardından bir cihaz seçin.

- **Durum ayrıntıları** – cihazın şifreleme durumu hakkında gelişmiş ayrıntılar.

  > [!IMPORTANT]
  > Windows 10 cihazlarında, Intune yalnızca *Windows 10 nisan 2019 güncelleştirme* veya üstünü çalıştıran cihazların *durum ayrıntılarını* gösterir.

  Bu alan, algılanabildiği her bir hata için bilgileri görüntüler. Bu bilgileri, bir cihazın neden şifreleme için hazırlanamadığına ilişkin bir neden olduğunu anlamak için kullanabilirsiniz.

  Intune 'un rapor verebir durum ayrıntıları aşağıda verilmiştir:

  **MacOS**:
  - Kurtarma anahtarı henüz alınmadı ve henüz depolanmadı. Büyük olasılıkla, cihazın kilidi açık değil veya iade edilmedi.

    *Göz önünde bulundurun: Bu sonuç bir hata koşulunu temsil etmelidir, ancak cihazda, şifreleme isteği cihaza gönderilmeden önce kurtarma anahtarları için Emanet 'in ayarlanmış olması gereken, geçici bir durum olabilir. Bu durum Ayrıca cihazın kilitli kaldığını veya son zamanlarda Intune ile iade edilmedi olduğunu gösteriyor olabilir. Son olarak, bir cihaz takılıncaya kadar Filekasası şifrelemesi başlamadığı için, bir kullanıcının henüz şifrelenmeyen bir cihaz için kurtarma anahtarı alması mümkündür*.

  - Kullanıcı şifrelemeyi erteleniyor veya şu anda şifreleme sürecinde.

    *Göz önünde bulundurun: Kullanıcı, şifreleme isteğini aldıktan sonra henüz oturum açmamış, çünkü dosya kasasının cihazı şifreleyebilmesi için gerekli olan veya kullanıcının cihazı el ile şifresini açtığı durumda. Intune, bir kullanıcının cihazının şifresini çözmesini engellemez.*

  - Cihaz zaten şifrelendi. Devam etmek için cihazın Kullanıcı tarafından şifresinin çözülmesi gerekir.

    *Göz önünde bulundurun: Intune zaten şifrelenmiş bir cihazda Filekasasını ayarlayamıyorum. Bunun yerine, bir cihaz yapılandırma ilkesi ve Intune tarafından yönetilebilmesi için kullanıcının cihazının el ile şifresinin çözülmesi gerekir*.

  - Filekasasının, kullanıcının macOS Catalina ve üzeri bir yönetim profilini onaylaması gerekir.

    *Göz önünde bulundurun: macOS sürüm 10,15 (Catalina) Ile başlayarak, kullanıcının onayladığı kayıt ayarları, kullanıcıların dosya kasasını şifrelemeyi el ile onaylama gereksinimine neden olabilir. Daha fazla bilgi için bkz. Intune belgelerinde [Kullanıcı onaylı kayıt](../enrollment/macos-enroll.md) *.

  - Bilinmeyen.

    *Göz önünde bulundurun: bilinmeyen bir durumun nedeni, cihazın kilitlenmesinden ve Intune 'un Emanet veya şifreleme işlemini başlatamamasına neden olabilir. Cihazın kilidi açıldıktan sonra, ilerleme devam edebilir*.

  **Windows 10**:
  - BitLocker ilkesi için Kullanıcı onayı 'Nın, işletim sistemi biriminin şifrelemesini başlatmak üzere BitLocker Sürücü Şifrelemesi Sihirbazı 'Nı başlatması gerekir, ancak Kullanıcı onay vermedi.

  - İşletim sistemi biriminin şifreleme yöntemi BitLocker ilkesiyle eşleşmiyor.

  - BitLocker, işletim sistemi birimini korumak için bir TPM koruyucusu gerektirir, ancak TPM kullanılmaz.

  - BitLocker ilkesi, işletim sistemi birimi için salt TPM koruyucusu gerektirir, ancak TPM koruması kullanılmaz.

  - BitLocker ilkesi, işletim sistemi birimi için TPM + PIN koruması gerektirir, ancak TPM + PIN koruyucusu kullanılmaz.

  - BitLocker ilkesi, işletim sistemi birimi için TPM + başlangıç anahtarı koruması gerektirir, ancak TPM + başlangıç anahtarı koruyucusu kullanılmaz.

  - BitLocker ilkesi, işletim sistemi birimi için TPM + PIN + başlangıç anahtarı koruması gerektirir, ancak TPM + PIN + başlangıç anahtarı koruyucusu kullanılmaz.

  - İşletim sistemi birimi korumasız.

  - Kurtarma anahtarı yedeklemesi başarısız oldu.

  - Sabit bir sürücü korumasız.

  - Sabit sürücünün şifreleme yöntemi BitLocker ilkesiyle eşleşmiyor.

  - Sürücüleri şifrelemek için BitLocker ilkesi kullanıcının yönetici olarak oturum açmasını ya da cihazın Azure AD 'ye katılmasını gerektiriyorsa, AllowStandardUserEncryption ilkesinin 1 olarak ayarlanması gerekir.

  - Windows kurtarma ortamı (WinRE) yapılandırılmadı.

  - TPM, mevcut olmadığı, kayıt defterinde kullanılamaz hale getirilen ya da işletim sistemi çıkarılabilir bir sürücüde olan BitLocker için kullanılamaz.

  - TPM BitLocker için yok.

  - Ağ kullanılabilir değil, kurtarma anahtarı yedeklemesi için gereklidir.

## <a name="export-report-details"></a>Rapor ayrıntılarını dışarı aktar

Şifreleme Raporu bölmesini görüntülerken, rapor ayrıntılarının bir *. csv* dosyası indirmesi oluşturmak Için **dışarı aktar** ' ı seçebilirsiniz. Bu rapor, yönettiğiniz her cihaz için *şifreleme raporu* bölmesi ve *Cihaz şifreleme durumu* ayrıntılarının üst düzey ayrıntılarını içerir.

![Dışarı aktarma ayrıntıları](./media/encryption-monitor/export.png)

Bu rapor, cihaz gruplarıyla ilgili sorunları belirlemek için kullanılabilir. Örneğin, tüm rapor *Dosya kasasının Kullanıcı tarafından zaten etkinleştirilmiş olduğu*MacOS cihazlarının listesini tanımlamak için raporu kullanabilirsiniz. Bu, Intune 'un dosya Kasası Ayarlarını yönetebilmesi için el ile şifresinin çözülmesi gereken cihazları gösterir.

## <a name="manage-recovery-keys"></a>Kurtarma anahtarlarını yönetme

Kurtarma anahtarlarını yönetme hakkında daha fazla bilgi için, Intune belgelerinde aşağıdakilere bakın:

macOS Filekasası:
- [Kişisel kurtarma anahtarını al](../protect/encrypt-devices-filevault.md#retrieve-personal-recovery-key)
- [Kurtarma anahtarlarını döndür](../protect/encrypt-devices-filevault.md#rotate-recovery-keys)
- [Kurtarma anahtarlarını kurtar](../protect/encrypt-devices-filevault.md#recover-recovery-keys)

Windows 10 BitLocker:
- [BitLocker kurtarma anahtarlarını döndür](../protect/encrypt-devices.md#rotate-bitlocker-recovery-keys)

## <a name="next-steps"></a>Sonraki adımlar

[BitLocker ilkesini yönetme](../protect/encrypt-devices.md)

[FileVault ilkesini yönetme](encrypt-devices-filevault.md)
