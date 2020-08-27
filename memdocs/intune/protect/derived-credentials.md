---
title: Microsoft Intune-Azure 'da mobil cihazlar için türetilmiş kimlik bilgilerini kullanma | Microsoft Docs
description: Intune VPN, e-posta, Wi-Fi profilleri, uygulamalar ve S/MIME ve şifreleme için bir kimlik doğrulama yöntemi olarak mobil cihazlarda türetilmiş kimlik bilgilerini kullanın. Türetilmiş kimlik bilgileri, özel yayın 800-157 için NıST yönergelerinin bir uygulamasıdır.
keywords: ''
author: brenduns
ms.author: brenduns
manager: dougeby
ms.date: 07/17/2020
ms.topic: how-to
ms.service: microsoft-intune
ms.subservice: protect
ms.localizationpriority: high
ms.technology: ''
ms.assetid: ''
ms.reviewer: lacranda
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: a83d6301ffe5663abd6025c8f52b2e7a7e0b7982
ms.sourcegitcommit: 0c7e6b9b47788930dca543d86a95348da4b0d902
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/26/2020
ms.locfileid: "88911123"
---
# <a name="use-derived-credentials-in-microsoft-intune"></a>Microsoft Intune ' de türetilmiş kimlik bilgilerini kullan

*Bu makale, 7,0 ve üzeri sürümleri çalıştıran iOS/ıpados, Android kurumsal tam yönetilen cihazlar ve Windows çalıştıran cihazlar için geçerlidir.*

Akıllı kartların kimlik doğrulama veya şifreleme ve imzalama için gerekli olduğu bir ortamda, mobil cihazları kullanıcının akıllı kartından türetilmiş bir sertifikayla sağlamak için artık Intune 'u kullanabilirsiniz. Bu sertifikaya *türetilmiş kimlik bilgileri*denir. Intune, [çeşitli türetilmiş kimlik bilgileri verenler destekler](#supported-issuers), ancak her seferinde her kiracı için yalnızca tek bir veren kullanabilirsiniz.

Türetilmiş kimlik bilgileri, özel yayın (SP) 800-157 kapsamında türetilmiş kişisel kimlik doğrulama (PıV) kimlik bilgileri için ulusal standartlar ve Teknoloji Enstitüsü (NıST) kuralları uygulamasıdır.

**Intune uygulamasıyla**:

- Intune Yöneticisi, kiraclarını desteklenen bir türetilmiş kimlik bilgisi verenle çalışacak şekilde yapılandırır. Türetilmiş kimlik bilgileri verenin sisteminde herhangi bir Intune 'A özgü ayarı yapılandırmanız gerekmez.
- Intune Yöneticisi, aşağıdaki nesneler için *kimlik doğrulama yöntemi* olarak **türetilmiş kimlik bilgilerini** belirtir:
  
  **Android kurumsal tam yönetilen cihazlar için**:
  - Wi-Fi ve VPN gibi ortak profil türleri
  - Uygulama kimlik doğrulaması

  **İOS/ıpados için**:
  - İOS/ıpados Native Mail uygulamasını içeren Wi-Fi, VPN ve e-posta gibi ortak profil türleri
  - Uygulama kimlik doğrulaması
  - S/MIME imzalama ve şifreleme

  **Windows için**:
  - Wi-Fi ve VPN gibi ortak profil türleri
  
- Android ve iOS/ıpados için, kullanıcılar türetilmiş kimlik bilgileri verende kimlik doğrulaması yapmak için bir bilgisayardaki akıllı kartlarını kullanarak türetilmiş bir kimlik bilgisi alır. Veren, daha sonra akıllı kartlarından türetilen bir sertifika olan mobil cihaza sorun verir. Windows için kullanıcılar, uygulamayı daha sonra kullanılmak üzere cihaza yükleyen türetilmiş kimlik bilgisi sağlayıcısından yükler.
- Cihaz türetilmiş kimlik bilgilerini aldıktan sonra, uygulamalar veya kaynak erişim profilleri türetilmiş kimlik bilgisini gerektirdiğinde, kimlik doğrulaması ve S/MIME imzalama ve şifreleme için kullanılır.

## <a name="prerequisites"></a>Önkoşullar

Kiracınızı türetilmiş kimlik bilgilerini kullanacak şekilde yapılandırmadan önce aşağıdaki bilgileri gözden geçirin.

### <a name="supported-platforms"></a>Desteklenen platformlar

Intune, aşağıdaki platformlarda türetilmiş kimlik bilgilerini destekler:

- iOS/iPadOS
- Android kurumsal tam yönetilen cihazlar (sürüm 7,0 ve üzeri)
- Android kurumsal-şirkete ait iş profili
- Windows 10 ve üzeri

### <a name="supported-issuers"></a>Desteklenen verenler

Intune, kiracı başına tek bir türetilmiş kimlik bilgisi veren destekler. Intune 'U, aşağıdaki verenler ile çalışacak şekilde yapılandırabilirsiniz:

- **Dışa purebred**: https://public.cyber.mil/pki-pke/purebred/
- **Entrust Datacard**: https://www.entrustdatacard.com/
- **Intercede**: https://www.intercede.com/

Farklı verenler kullanma hakkında önemli ayrıntılar için bu veren için kılavuzu gözden geçirin. Daha fazla bilgi için bu makaledeki [türetilmiş kimlik bilgilerini planlayın](#plan-for-derived-credentials) bölümüne bakın.

> [!IMPORTANT]
> Kiracıdan türetilmiş bir kimlik bilgisi veren silerseniz, bu veren aracılığıyla ayarlanan türetilmiş kimlik bilgileri artık çalışmaz.
>
> Bu makalenin ilerleyen kısımlarında bulunan [türetilmiş kimlik bilgisi verenini değiştirme](#change-the-derived-credential-issuer) bölümüne bakın.

### <a name="company-portal-app"></a>Şirket Portalı uygulaması

Intune Şirket Portalı uygulamayı türetilmiş bir kimlik bilgisi için kaydedilecek cihazlara dağıtmayı planlayın. Cihaz kullanıcıları kimlik bilgileri kayıt işlemini başlatmak için Şirket Portalı uygulamasını kullanır.

- İOS cihazları için bkz. [Microsoft Intune iOS Mağazası uygulamaları ekleme](../apps/store-apps-ios.md).
- Android cihazlar için bkz. [Microsoft Intune Android Mağazası uygulamaları ekleme](../apps/store-apps-android.md).

## <a name="plan-for-derived-credentials"></a>Türetilmiş kimlik bilgilerini planlayın

Android ve iOS/ıpados için türetilmiş bir kimlik bilgisi veren ayarlamadan önce aşağıdaki hususları anlayın.

Windows cihazları için, bu makalenin devamındaki [Windows Için türetilmiş kimlik bilgileri](#derived-credentials-for-windows)bölümüne bakın.

### <a name="1-review-the-documentation-for-your-chosen-derived-credential-issuer"></a>1) seçtiğiniz türetilmiş kimlik bilgisi veren için belgeleri gözden geçirin

Bir veren yapılandırmadan önce, sistemin cihazlara türetilmiş kimlik bilgilerini nasıl sağladığını anlamak için bu verenin belgelerini gözden geçirin.

Seçtiğiniz verene bağlı olarak, kullanıcıların işlemi tamamına yardımcı olmak için kayıt sırasında personelin kullanılabilir olması gerekebilir. Ayrıca, cihazların veya kullanıcıların kimlik bilgisi isteğini tamamlaması için gerekli olan erişimi engellemediğinden emin olmak için geçerli Intune yapılandırmalarınızı gözden geçirin.

Örneğin, uyumlu olmayan cihazlar için e-postaya erişimi engellemek üzere koşullu erişimi kullanabilirsiniz. Kullanıcıya türetilmiş kimlik bilgileri kayıt işlemini başlatmasını bildirmek için e-posta bildirimlerini kullandıysanız, kullanıcılarınız ilkeyle uyumlu olana kadar bu yönergeleri alamayabilir.

Benzer şekilde, bazı türetilmiş kimlik bilgileri istek iş akışları, bir ekran QR kodunu taramak için cihaz kamerasının kullanılmasını gerektirir. Bu kod, bu cihazı, kullanıcının akıllı kart kimlik bilgileriyle türetilmiş kimlik bilgisi verenle karşı gerçekleşen kimlik doğrulama isteğine bağlar. Cihaz yapılandırma ilkeleri kamera kullanımını engellerseniz, Kullanıcı türetilmiş kimlik bilgileri kayıt isteğini tamamlayamıyor.

**Genel bilgiler**:

- Her seferinde kiracı başına tek bir veren yapılandırabilirsiniz ve bu veren, kiracınızdaki tüm kullanıcılar ve desteklenen cihazlar için kullanılabilir.

- Kullanıcılara, türetilmiş kimlik bilgileri gerektiren bir ilkeyle hedeflendirilene kadar türetilmiş kimlik bilgilerine kaydolmaları gerektiğini bilgilendirilmez.

- Bildirim Şirket Portalı, e-posta veya her ikisi için de uygulama bildirimi aracılığıyla olabilir. E-posta bildirimlerini kullanmayı tercih ederseniz ve koşullu erişimi etkinleştirdiyseniz, kullanıcılar cihaz uyumlu değilse e-posta bildirimini almayabilir.

### <a name="2-review-the-end-user-workflow-for-your-chosen-issuer"></a>2) seçtiğiniz veren için son kullanıcı iş akışını gözden geçirin

Desteklenen her iş ortağı için önemli konular aşağıda verilmiştir.  Intune ilkelerinizin ve yapılandırmalarının, Kullanıcı ve cihazların, bu verenden türetilmiş bir kimlik bilgisi kaydını başarıyla tamamlamasını engellemek için bu bilgileri öğrenmiş olun.

#### <a name="disa-purebred"></a>DıŞA purebred

Türetilmiş kimlik bilgileriyle kullanacağınız cihazlar için platforma özgü Kullanıcı iş akışını gözden geçirin.

- [iOS ve ıpados](/intune-user-help/enroll-ios-device-disa-purebred)
- [Android kurumsal tam yönetilen cihazlar](../user-help/enroll-android-device-disa-purebred.md)

**Temel gereksinimler şunlardır**:

- Kullanıcıların, verenin kimliğini doğrulamak için akıllı kartlarını kullanabilecekleri bir bilgisayar veya bilgi noktası erişimine ihtiyacı vardır.
- Türetilmiş bir kimlik bilgisine kaydedilecek cihazların Intune Şirket Portalı uygulamasını yüklemeleri gerekir.
- Türetilmiş bir kimlik bilgisi için kaydedilecek cihazlara [, dışa ınpurebred uygulamasını dağıtmak](#deploy-the-disa-purebred-app) için Intune 'u kullanın. Bu uygulama, yönetilmek üzere Intune aracılığıyla dağıtılmalıdır ve daha sonra Intune Şirket Portalı uygulamayla çalışabilir. Bu uygulama, derlenen kimlik bilgisi isteğini tamamlaması için cihaz kullanıcıları tarafından kullanılır.
- DıŞA yönelik olarak, uygulamanın türetilmiş kimlik bilgileri için kayıt sırasında DıŞA Üflere erişebildiğinden emin olmak için, bir [uygulama BAŞıNA VPN](../configuration/vpn-settings-configure.md) gerekir.
- Kayıt işlemi sırasında cihaz kullanıcılarının canlı bir aracıyla çalışması gerekir. Kayıt sırasında, kayıt işlemi boyunca devam ettikleri sürece kullanıcıya zaman sınırlı bir kerelik geçiş kodları verilir.
- Yeni bir Wi-Fi profili oluşturma gibi türetilmiş kimlik bilgilerini kullanan bir ilkede değişiklik yapıldığında iOS ve ıpados kullanıcıları Şirket Portalı uygulamasını açmak üzere bilgilendirilir.
- Kullanıcılara, türetilmiş kimlik bilgilerini yenilemeleri gerektiğinde Şirket Portalı uygulamayı açması bildirilir.

DıŞA ınpurebred uygulamasını alma ve yapılandırma hakkında bilgi için bu makalenin ilerleyen kısımlarında bulunan [dışa ınpurebred uygulamasını dağıtma](#deploy-the-disa-purebred-app) bölümüne bakın.

#### <a name="entrust-datacard"></a>Entrust Datacard

Türetilmiş kimlik bilgileriyle kullanacağınız cihazlar için platforma özgü Kullanıcı iş akışını gözden geçirin.

- [iOS ve ıpados](/intune-user-help/enroll-ios-device-entrust-datacard)
- [Android kurumsal tam yönetilen cihazlar](../user-help/enroll-android-device-entrust-datacard.md)

**Temel gereksinimler şunlardır**:

- Kullanıcıların, verenin kimliğini doğrulamak için akıllı kartlarını kullanabilecekleri bir bilgisayar veya bilgi noktası erişimine ihtiyacı vardır.
- Türetilmiş bir kimlik bilgisine kaydedilecek cihazların Intune Şirket Portalı uygulamasını yüklemeleri gerekir.
- Mobil cihazdan türetilmiş kimlik bilgisi isteğine kimlik doğrulama isteğini bağlayan bir QR kodunu taramak için bir cihaz Kamerası kullanın.
- Kullanıcılardan Şirket Portalı uygulaması veya türetilmiş kimlik bilgilerine kaydolmak için e-posta üzerinden sorulur.
- Yeni bir Wi-Fi profili oluşturma gibi türetilmiş kimlik bilgilerini kullanan bir ilkede değişiklik yapıldığında:
  - **iOS ve ıpados** -kullanıcılara şirket portalı uygulamasını açmak için bildirim yapılır.
  - **Android kurumsal tam yönetilen cihazlar** -Şirket portalı uygulamasının açılması gerekmez.
- Kullanıcılara, türetilmiş kimlik bilgilerini yenilemeleri gerektiğinde Şirket Portalı uygulamayı açması bildirilir.

#### <a name="intercede"></a>Intercede

Türetilmiş kimlik bilgileriyle kullanacağınız cihazlar için platforma özgü Kullanıcı iş akışını gözden geçirin.

- [iOS ve ıpados](/intune-user-help/enroll-ios-device-intercede)
- [Android kurumsal tam yönetilen cihazlar](../user-help/enroll-android-device-intercede.md)

**Temel gereksinimler şunlardır**:

- Kullanıcıların, verenin kimliğini doğrulamak için akıllı kartlarını kullanabilecekleri bir bilgisayar veya bilgi noktası erişimine ihtiyacı vardır.
- Türetilmiş bir kimlik bilgisine kaydedilecek cihazların Intune Şirket Portalı uygulamasını yüklemeleri gerekir.
- Mobil cihazdan türetilmiş kimlik bilgisi isteğine kimlik doğrulama isteğini bağlayan bir QR kodunu taramak için bir cihaz Kamerası kullanın.
- Kullanıcılardan Şirket Portalı uygulaması veya türetilmiş kimlik bilgilerine kaydolmak için e-posta üzerinden sorulur.
- Yeni bir Wi-Fi profili oluşturma gibi türetilmiş kimlik bilgilerini kullanan bir ilkede değişiklik yapıldığında:
  - **iOS ve ıpados** -kullanıcılara şirket portalı uygulamasını açmak için bildirim yapılır.
  - **Android kurumsal tam yönetilen cihazlar** -Şirket portalı uygulamasının açılması gerekmez.
- Kullanıcılara, türetilmiş kimlik bilgilerini yenilemeleri gerektiğinde Şirket Portalı uygulamayı açması bildirilir.

### <a name="3-deploy-a-trusted-root-certificate-to-devices"></a>3) cihazlara güvenilen bir kök sertifika dağıtın

Güvenilen bir kök sertifika, türetilmiş kimlik bilgileri Sertifika zincirinin geçerli ve güvenilir olduğunu doğrulamak için, türetilen kimlik bilgileriyle birlikte kullanılır. İlke tarafından doğrudan başvurulmamışsa bile, güvenilen bir kök sertifika gereklidir. Bkz. [Microsoft Intune cihazlarınız için sertifika profili yapılandırma](certificates-configure.md).

### <a name="4-provide-end-user-instructions-for-how-to-get-the-derived-credential"></a>4) türetilmiş kimlik bilgisinin nasıl alınacağı hakkında Son Kullanıcı talimatları sağlama

Türetilmiş kimlik bilgileri kayıt işlemini başlatma ve size seçtiğiniz veren için türetilmiş kimlik bilgileri kayıt iş akışında gezinmek üzere kullanıcılarınıza rehberlik oluşturun ve bu bilgileri girin.

Kılavuzunuzu barındıracak bir URL sağlamanızı öneririz. Bu URL 'yi, kiracınız için türetilmiş kimlik bilgisi veren yapılandırdığınızda ve bu URL Şirket Portalı uygulamasının içinden kullanılabilir hale geldiğinde belirtirsiniz. Kendi URL 'nizi belirtmezseniz, Intune genel ayrıntılara bir bağlantı sağlar. Bu ayrıntılar tüm senaryoları kapsamamaktadır ve ortamınız için doğru olmayabilir.

### <a name="dive-idsupported-objects-5-deploy-intune-policies-that-require-derived-credentials"></a><dive id="supported-objects"> 5) türetilmiş kimlik bilgileri gerektiren Intune ilkelerini dağıtma

Türetilmiş kimlik bilgilerini kullanmak için yeni ilkeler oluşturun veya var olan ilkeleri düzenleyin. Türetilmiş kimlik bilgileri aşağıdaki nesneler için diğer kimlik doğrulama yöntemlerinin yerini alır:

- Uygulama kimlik doğrulaması
- Wi-Fi
- VPN
- e-posta (yalnızca iOS)
- Outlook (yalnızca iOS) dahil olmak üzere, S/MIME imzalama ve şifreleme

Türetilmiş kimlik bilgilerini elde etmek için kullandığınız bir işleme erişmek üzere türetilmiş bir kimlik bilgisinin kullanılması gereğini önleyin, çünkü kullanıcıların isteği tamamlamasına engel olabilir.

## <a name="set-up-a-derived-credential-issuer"></a>Türetilmiş bir kimlik bilgisi veren ayarlama

Türetilmiş bir kimlik bilgisinin kullanılması gereken ilkeler oluşturmadan önce, Intune konsolunda bir kimlik bilgisi veren ayarlayın. Türetilmiş bir kimlik bilgisi veren, kiracı genelinde bir ayardır. Kiracılar aynı anda yalnızca tek bir veren destekler.

1. [Microsoft Endpoint Manager Yönetim merkezinde](https://go.microsoft.com/fwlink/?linkid=2109431)oturum açın.
2. **Kiracı Yönetimi**  >  **bağlayıcıları ' nı ve**  >  **türetilmiş kimlik bilgileri**belirteçlerini seçin.

    > [!div class="mx-imgBorder"]
    > ![Konsolundaki türetilmiş kimlik bilgilerini yapılandırma](./media/derived-credentials/configure-provider.png)

3. Türetilmiş kimlik bilgisi veren ilkesi için kolay bir **görünen ad** belirtin.  Bu ad, cihaz kullanıcılarınıza gösterilmez.

4. **Türetilmiş kimlik bilgisi veren**için, kiracınız için seçtiğiniz türetilmiş kimlik bilgisi verenini seçin:
   - DıŞA purebred (yalnızca iOS)
   - Entrust Datacard
   - Intercede  

5. Kullanıcıların kuruluşunuz için türetilmiş kimlik bilgilerini elde etmenize yardımcı olacak özel yönergeler içeren bir konum bağlantısı sağlamak için **türetilmiş bir kimlik bilgisi yardım URL 'si** belirtin. Yönergeler kuruluşunuza ve seçtiğiniz sertifika vereninizden bir kimlik bilgisi almak için gereken iş akışına özgü olmalıdır. Bağlantı Şirket Portalı uygulamasında görüntülenir ve cihazdan erişilebilir olmalıdır.

   Kendi URL 'nizi belirtmezseniz, Intune tüm senaryoları kapsaymamakta olan genel ayrıntılara bir bağlantı sağlar. Bu genel kılavuz, ortamınız için doğru olmayabilir.

6. **Bildirim türü**için bir veya daha fazla seçenek belirleyin. Bildirim türleri, kullanıcıları aşağıdaki senaryolar hakkında bilgilendirmek için kullandığınız yöntemlerdir:

   - Yeni bir türetilmiş kimlik bilgisi almak için bir cihazı veren ile kaydedin.
   - Geçerli kimlik bilgisi sona ermeden yeni bir türetilmiş kimlik bilgisi alın.
   - [Desteklenen bir nesneyle](#supported-objects)türetilmiş bir kimlik bilgisi kullanın.

7. Hazırlandığınızda, türetilmiş kimlik bilgisi verenin yapılandırmasını tamamladıktan sonra **Kaydet** ' i seçin.

Yapılandırmayı kaydettikten sonra, *türetilmiş kimlik bilgisi veren*hariç tüm alanlarda değişiklik yapabilirsiniz.  Sertifikayı veren değiştirmek için bkz. [türetilmiş kimlik bilgisi vereni değiştirme](#change-the-derived-credential-issuer).

## <a name="deploy-the-disa-purebred-app"></a>DıŞA Popurebred uygulamasını dağıtma

*Bu bölüm yalnızca dışa ınpurebred kullandığınızda geçerlidir*.

Intune için türetilmiş kimlik bilgisi veren olarak **rekred** 'yi kullanmak IÇIN, dışa geçmiş yeniden bred uygulamasını almanız ve ardından Intune 'u kullanarak uygulamayı cihazlara dağıtmanız gerekir. Cihaz kullanıcıları, DıŞA alınan kimlik bilgisini, DıŞA purebred 'den istemek için cihazındaki uygulamayı kullanır.

Uygulamayı Intune ile dağıtmaya ek olarak, DıŞA Popurebred uygulaması için bir Intune uygulama başına VPN yapılandırın.

**Aşağıdaki görevleri doldurun**:
  
1. DıŞA Popurebred uygulamasını indirin: https: \/ /Cyber.mil/pki-PKE/purebred/.

2. Diğer Intune 'da bulunan DıŞA ınpurebred uygulamasını dağıtın. 

   - [Microsoft Intune için bir iOS iş kolu uygulaması ekleme](../apps/lob-apps-ios.md)bölümüne bakın.
   - [Microsoft Intune Için Android iş kolu uygulaması ekleme](../apps/lob-apps-android.md) bölümüne bakın

3. DıŞA purebred uygulaması için [uygulama BAŞıNA VPN oluşturun](../configuration/vpn-settings-configure.md) .

## <a name="use-derived-credentials-for-authentication-and-smime-signing-and-encryption"></a>Kimlik doğrulaması ve S/MIME imzalama ve şifreleme için türetilmiş kimlik bilgilerini kullan

Aşağıdaki profil türleri ve amaçları için **türetilmiş kimlik bilgilerini** belirtebilirsiniz:

- [Uygulamalar](#use-derived-credentials-for-app-authentication)
- E-posta:
  - [iOS ve ıpados](../configuration/email-settings-ios.md)
  - [Android Kurumsal](../configuration/email-settings-android-enterprise.md)
- SANAL
  - [iOS ve ıpados](../configuration/vpn-settings-ios.md)
  - [Android Kurumsal](../configuration/vpn-settings-android-enterprise.md)
- [S/MIME imzalama ve şifreleme](certificates-s-mime-encryption-sign.md)
- Wi-Fi:
  - [iOS ve ıpados](../configuration/wi-fi-settings-ios.md)
  - [Android Kurumsal](../configuration/wi-fi-settings-android-enterprise.md)

  Wi-Fi profilleri için, *kimlik doğrulama yöntemi* yalnızca **EAP türü** aşağıdaki değerlerden birine ayarlandığında kullanılabilir:
  - EAP – TLS
  - EAP-TTLS
  - PEAP

### <a name="use-derived-credentials-for-app-authentication"></a>Uygulama kimlik doğrulaması için türetilmiş kimlik bilgilerini kullan

Web siteleri ve uygulamalarına sertifika tabanlı kimlik doğrulaması için türetilmiş kimlik bilgilerini kullanın. Uygulama kimlik doğrulaması için türetilmiş bir kimlik bilgisi teslim etmek için:

1. [Microsoft Endpoint Manager Yönetim merkezinde](https://go.microsoft.com/fwlink/?linkid=2109431)oturum açın.
2. **Cihaz**  >  **yapılandırma profilleri**  >  **Profil oluştur**' u seçin.
3. Aşağıdaki ayarları girin:

   İOS ve ıpados için:
   - **Ad**: profil için açıklayıcı bir ad girin. Profillerinizi daha sonra kolayca tanıyacak şekilde adlandırın. Örneğin, iyi bir profil adı, **iOS cihazlar profili Için türetilmiş kimlik bilgileridir**.
   - **Açıklama**: Ayara genel bir bakış sağlayan ve diğer önemli ayrıntıları veren bir açıklama girin.
   - **Platform**: **IOS/ıpados**' ı seçin.
   - **Profil türü**: **türetilmiş kimlik bilgilerini**seçin.

   Android Enterprise için:
   - **Ad**: profil için açıklayıcı bir ad girin. Profillerinizi daha sonra kolayca tanıyacak şekilde adlandırın. Örneğin, iyi bir profil adı, **Android kurumsal cihazlar profili Için türetilmiş kimlik bilgileridir**.
   - **Açıklama**: Ayara genel bir bakış sağlayan ve diğer önemli ayrıntıları veren bir açıklama girin.
   - **Platform**: **Android kurumsal**' i seçin.
   - **Profil türü**: *tam olarak yönetilen, adanmış ve şirkete ait iş profili*altında, **türetilmiş kimlik bilgileri**' ni seçin.

4. Değişikliklerinizi kaydetmek için **Tamam**’ı seçin.
5. İşiniz bittiğinde, **OK**  >  Intune profilini oluşturmak için Tamam**Oluştur** ' u seçin. Bu tamamlandığında, profiliniz **cihazlar-yapılandırma profilleri** listesinde gösterilir.
6. Yeni profilinizi > **atamaları**' nı seçin. İlkeyi alması gereken grupları seçin.

Kullanıcılar, türetilmiş kimlik bilgileri verenini ayarlarken belirttiğiniz ayarlara bağlı olarak uygulamayı veya e-posta bildirimini alır. Bildirim, kullanıcıdan türetilmiş kimlik bilgileri ilkelerinin işlenebilmesi için Şirket Portalı başlatması konusunda bilgilendirir.

## <a name="derived-credentials-for-windows"></a>Windows için türetilmiş kimlik bilgileri

Windows cihazlarında Wi-Fi ve VPN profilleri için bir kimlik doğrulama yöntemi olarak türetilmiş sertifikaları kullanabilirsiniz. Android ve iOS/ıpados cihazları tarafından desteklenen aynı sağlayıcılar, Windows için sağlayıcılar olarak desteklenir:

- **DıŞA purebred**
- **Entrust Datacard**
- **Intercede**

Windows için kullanıcılar, türetilmiş kimlik bilgileri olarak kullanılmak üzere bir sertifika almak için bir akıllı kart kayıt süreci aracılığıyla çalışmaz. Bunun yerine, kullanıcının türetilmiş kimlik bilgisi sağlayıcısından alınan Windows uygulamasını yüklemesi gerekir. Windows ile türetilmiş kimlik bilgilerini kullanmak için aşağıdaki konfigürasyonları doldurun:

1. **Uygulamayı Windows cihazdaki türetilmiş kimlik bilgisi sağlayıcılarından yükler**.

   Windows uygulamasını bir Windows aygıtındaki türetilmiş bir kimlik bilgisi sağlayıcısından yüklediğinizde, türetilen sertifika bu cihazların Windows sertifika deposu 'na eklenir. Sertifika cihaza eklendikten sonra, bu, türetilmiş bir kimlik bilgisi kimlik doğrulama yöntemi kullanmak için kullanılabilir hale gelir.

   Uygulamayı seçtiğiniz sağlayıcıdan aldıktan sonra, uygulama kullanıcılara dağıtılabilir veya cihazın kullanıcısı tarafından doğrudan yüklenmiş olabilir.

2. **Wi-Fi ve VPN profillerini kimlik doğrulama yöntemi olarak türetilmiş kimlik bilgilerini kullanacak şekilde yapılandırın**.

   Wi-Fi veya VPN için bir Windows profilini yapılandırırken, *kimlik doğrulama yöntemi*için **türetilmiş kimlik bilgisi** ' ni seçin. Bu yapılandırmayla, profil, sağlayıcılar uygulaması yüklendiğinde cihaza yüklenen sertifikayı kullanır.

## <a name="renew-a-derived-credential"></a>Türetilmiş bir kimlik bilgisini Yenile

Android veya iOS/ıpados cihazlarının türetilmiş kimlik bilgileri genişletilemez veya yenilenemez. Bunun yerine, kullanıcıların, cihazları için yeni bir türetilmiş kimlik bilgisi istemek üzere kimlik bilgisi isteği iş akışını kullanmaları gerekir. Windows cihazları için, türetilmiş kimlik bilgisi sağlayıcınızdan uygulamaya yönelik belgelere başvurun.

**Bildirim türü**için bir veya daha fazla yöntem yapılandırırsanız, Intune, geçerli türetilen kimlik bilgisi kullanım ömrü boyunca %80 ' a ulaştığında kullanıcılara otomatik olarak bildirimde bulunur. Bildirim, kullanıcıların, yeni bir türetilmiş kimlik bilgisi almak için kimlik bilgisi istek işlemini gitmesini yönlendirir.

Bir cihaz yeni bir türetilmiş kimlik bilgisi aldıktan sonra, türetilmiş kimlik bilgilerini kullanan ilkeler o cihaza yeniden dağıtırsınız.

## <a name="change-the-derived-credential-issuer"></a>Türetilmiş kimlik bilgisi vereni değiştirme

Kiracı düzeyinde, kiracı için tek seferde yalnızca bir veren destekleniyor olsa da, kimlik bilgisi vereninizi değiştirebilirsiniz.

Veren 'i değiştirdikten sonra kullanıcılardan yeni veren tarafından yeni bir türetilmiş kimlik bilgisi alması istenir. Kimlik doğrulaması için türetilmiş bir kimlik bilgisi kullanabilmesi için önce bunları kullanmaları gerekir.

### <a name="change-the-issuer-for-your-tenant"></a>Kiracınız için sertifikayı değiştirme

> [!IMPORTANT]
> Sertifikayı bir veren siler ve hemen yeniden yapılandırırsanız, bu veren 'ten türetilmiş kimlik bilgilerini kullanmak için profilleri ve cihazları yine de güncelleştirmeniz gerekir. Veren silinmeden önce elde edilen türetilmiş kimlik bilgileri artık geçerli değil.

1. [Microsoft Endpoint Manager Yönetim merkezinde](https://go.microsoft.com/fwlink/?linkid=2109431)oturum açın.
2. **Kiracı Yönetimi**  >  **bağlayıcıları ' nı ve**  >  **türetilmiş kimlik bilgileri**belirteçlerini seçin.
3. Geçerli türetilmiş kimlik bilgisi verenini kaldırmak için **Sil** ' i seçin.
4. Yeni bir veren yapılandırın.

### <a name="update-profiles-that-use-derived-credentials"></a>Türetilmiş kimlik bilgilerini kullanan profilleri güncelleştirme

Bir veren sildikten sonra yeni bir tane ekledikten sonra, türetilmiş kimlik bilgilerini kullanan her bir profili düzenleyin. Bu kural, önceki sertifikayı geri yüklediğinizde bile geçerlidir. Profilin herhangi bir düzenlemesi, profil *açıklamasına*basit bir düzenleme da dahil olmak üzere bir güncelleştirme tetikleyecektir.

### <a name="update-derived-credentials-on-devices"></a>Cihazlarda türetilmiş kimlik bilgilerini güncelleştir

Bir veren sildikten sonra yeni bir tane ekledikten sonra cihaz kullanıcıları yeni bir türetilmiş kimlik bilgisi istemelidir. Bu kural, kaldırdığınız sertifikayı eklediğinizde bile geçerlidir. Yeni türetilmiş kimlik bilgilerini isteme işlemi, yeni bir cihazı kaydetme veya mevcut bir kimlik bilgisini yenileme ile aynıdır.

## <a name="next-steps"></a>Sonraki adımlar

[Cihaz yapılandırma profilleri oluşturun](../configuration/device-profile-create.md).