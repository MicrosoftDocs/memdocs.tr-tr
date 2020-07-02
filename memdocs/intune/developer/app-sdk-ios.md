---
title: iOS için Microsoft Intune Uygulama SDK’sı geliştirici kılavuzu
description: iOS için Microsoft Intune Uygulama SDK’sı, Intune uygulama koruma ilkelerini (APP veya MAM ilkeleri olarak da bilinir) yerel iOS uygulamanıza eklemenizi sağlar.
keywords: ''
author: Erikre
ms.author: erikre
manager: dougeby
ms.date: 06/04/2020
ms.topic: reference
ms.service: microsoft-intune
ms.subservice: developer
ms.localizationpriority: medium
ms.technology: ''
ms.assetid: 8e280d23-2a25-4a84-9bcb-210b30c63c0b
ms.reviewer: aanavath
ms.suite: ems
search.appverid: MET150
ms.custom: has-adal-ref
ms.collection: M365-identity-device-management
ms.openlocfilehash: 60147f6b54ce608183914e00b65317abe0a580b6
ms.sourcegitcommit: 2c5fd7c8603b88b753765f3cc298d0a0bacaf521
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/01/2020
ms.locfileid: "85820044"
---
# <a name="microsoft-intune-app-sdk-for-ios-developer-guide"></a>iOS için Microsoft Intune Uygulama SDK’sı geliştirici kılavuzu

> [!NOTE]
> Desteklenen platformlarda tümleştirme için hazırlığın nasıl yapıldığını açıklayan [Intune Uygulama SDK’sı Kılavuzunu Kullanmaya Başlama](app-sdk-get-started.md) makalesini okumanız önerilir.
>
> SDK 'yı indirmek için bkz. [SDK dosyalarını indirme](../developer/app-sdk-get-started.md#download-the-sdk-files).

iOS için Microsoft Intune Uygulama SDK’sı, Intune uygulama koruma ilkelerini (APP veya MAM ilkeleri olarak da bilinir) yerel iOS uygulamanıza eklemenizi sağlar. MAM özellikli uygulamalar Intune Uygulama SDK’sı ile tümleşik çalışır. Intune uygulamayı etkin bir şekilde yönetirken, BT yöneticileri mobil uygulamanıza uygulama koruma ilkeleri dağıtabilir.

## <a name="prerequisites"></a>Ön koşullar

- OS X 10.12.6 veya üstünü çalıştıran bir Mac OS bilgisayara ihtiyacınız vardır ve Ayrıca Xcode 9 veya üzeri bir sürümü yüklü olur.

- Uygulamanız iOS 11 veya üzeri için hedeflenmelidir.

- [iOS için Intune Uygulama SDK'sı Lisans Koşulları](https://github.com/msintuneappsdk/ms-intune-app-sdk-ios/blob/master/Microsoft%20License%20Terms%20Intune%20App%20SDK%20for%20iOS.pdf)'nı gözden geçirmelisiniz. Kendi kayıtlarınız için lisans koşullarının bir kopyasını yazdırmalı ve saklamalısınız. iOS için Intune Uygulama SDK'sını indirip kullandığınızda bu lisans koşullarını kabul etmiş olursunuz.  Kabul etmiyorsanız, yazılımı kullanmayın.

- [GitHub](https://github.com/msintuneappsdk/ms-intune-app-sdk-ios)'da IOS Için Intune uygulama SDK 'sı dosyalarını indirin.

## <a name="whats-in-the-sdk-repository"></a>SDK deposundaki Özellikler

Aşağıdaki dosyalar, hiçbir Swift kodu içermeyen uygulamalar/uzantılara veya 10,2 ' dan önceki bir Xcode sürümü ile derlenerek geçerlidir:

* **IntuneMAM.framework**: Intune Uygulama SDK’sı çerçevesi. Intune istemci uygulama yönetimini etkinleştirmek için bu çerçeveyi uygulamanıza/uzantılara bağlamanız önerilir. Ancak bazı geliştiriciler statik kitaplığın performans avantajlarını tercih edebilir. Aşağıdakilere bakın.

* **libIntuneMAM.a**: Intune Uygulama SDK’sının statik kitaplığı. Geliştiriciler Framework yerine statik kitaplığı bağlamayı seçebilir. Statik kitaplıklar doğrudan uygulama/uzantı ikilisinde derleme zamanında katıştırıldığından, statik kitaplığı kullanmanın bazı başlatma zamanı performans avantajları vardır. Ancak, uygulamanızı uygulamanızla tümleştirmek daha karmaşık bir işlemdir. Uygulamanız herhangi bir uzantı içeriyorsa statik kitaplığı uygulamaya ve uzantılara bağlamak, statik kitaplık her bir uygulama/uzantı ikilisinde gömüleceğinden daha büyük bir uygulama paketi boyutuna neden olur. Framework kullanırken, uygulamalar ve uzantılar aynı Intune SDK ikilisini paylaşabilir, bu da daha küçük bir uygulama boyutuna neden olur.

* **Intunemamresources. demeti**: SDK 'nın bağımlı olduğu kaynakları içeren bir kaynak paketi. Kaynak demeti yalnızca statik kitaplığı (Libintunemad. a) tümleştiren uygulamalar için gereklidir.

Aşağıdaki dosyalar, Swift kodu içeren uygulamalar/uzantılar ile ilgilidir ve Xcode 10.2 + ile derlenir:

* **IntuneMAMSwift. Framework**: Intune uygulama SDK 'sı Swift çerçevesi. Bu çerçeve, uygulamanızın çağıracağız API 'Lerin tüm üst bilgilerini içerir. Intune istemci uygulama yönetimini etkinleştirmek için bu çerçeveyi uygulamanıza/uzantılara bağlayın.

* **Intunemamswiftstub. Framework**: Intune uygulama SDK 'Sı Swift saplama çerçevesi. Bu, uygulamaların/uzantıların bağlanması gereken IntuneMAMSwift. Framework için gerekli bir bağımlılığıdır.


Aşağıdaki dosyalar tüm uygulamalar/uzantılarını ile ilgilidir:

* **Intunemamconfigurator**: uygulamayı veya uzantının Info. plist bilgilerini Intune yönetimi için gereken en düşük değişikliklerle yapılandırmak için kullanılan bir araç. Uygulamanızın veya uzantınızın işlevselliğine bağlı olarak, Info. plist dosyasında el ile ek değişiklikler yapmanız gerekebilir.

* **Üst bilgiler**: genel Intune uygulama SDK 'Sı API 'lerini gösterir. Bu üst bilgiler ıntunemad/IntuneMAMSwift çerçeveleri içine dahil edilmiştir. böylece, çerçevelerden birini kullanan geliştiricilerin, üst bilgileri projesine el ile eklemesi gerekmez. Statik kitaplığa (Libintunemad. a) göre bağlamayı tercih eden geliştiricilerin, bu üst bilgileri projesine el ile eklemesi gerekir.

Aşağıdaki üst bilgi dosyaları, Intune Uygulama SDK’sı tarafından geliştiricilerin kullanımına sunulan API’ler, veri türleri ve protokollerini içerir:

-  IntuneMAMAppConfig.h
-  IntuneMAMAppConfigManager.h
-  IntuneMAMDataProtectionInfo.h
-  IntuneMAMDataProtectionManager.h
-  IntuneMAMDefs.h
-  Intunemamdiagnosticconsole. h
-  IntuneMAMEnrollmentDelegate.h
-  IntuneMAMEnrollmentManager.h
-  IntuneMAMEnrollmentStatus.h
-  IntuneMAMFileProtectionInfo.h
-  IntuneMAMFileProtectionManager.h
-  IntuneMAMLogger.h
-  IntuneMAMPolicy.h
-  IntuneMAMPolicyDelegate.h
-  IntuneMAMPolicyManager.h
-  IntuneMAMVersionInfo.h

Geliştiriciler yalnızca ıntunemam. h içeri aktararak tüm önceki üst bilgilerin içeriğini kullanılabilir hale getirir


## <a name="how-the-intune-app-sdk-works"></a>Intune Uygulama SDK’sı nasıl çalışır?

iOS için Intune Uygulama SDK'sının amacı, kodda minimum düzeyde değişiklik yaparak iOS uygulamalarına yönetim özellikleri eklemeyi sağlamaktır. Daha az kod, mobil uygulamanızın tutarlılığını ve kararlılığını etkilemeden, pazara daha az zaman değiştirir.


## <a name="build-the-sdk-into-your-mobile-app"></a>Mobil uygulamanızda SDK oluşturma

Intune Uygulama SDK'sını etkinleştirmek için aşağıdaki adımları izleyin:

1. **Seçenek 1-Framework (önerilir)**: Xcode 10.2 + kullanıyorsanız ve uygulamanız/uzantınız Swift kodu içeriyorsa ve `IntuneMAMSwift.framework` `IntuneMAMSwiftStub.framework` hedeflemenize ve hedeflemenize, bağlantı ve hedef Için `IntuneMAMSwift.framework` , `IntuneMAMSwiftStub.framework` proje hedefinin **katıştırılmış ikili dosyalar** listesine sürükleyin.

    Aksi takdirde, `IntuneMAM.framework` hedefle bağlantı: `IntuneMAM.framework` proje hedefinin **katıştırılmış Ikili dosyalar** listesine sürükleyin.

   > [!NOTE]
   > Çerçeveyi kullanırsanız, uygulamanızı App Store’a göndermeden önce evrensel çerçeveden simülatör mimarilerini kendiniz çıkarmanız gerekir. Daha fazla bilgi için bkz. [Uygulamanızı App Store'a gönderme](#submit-your-app-to-the-app-store).

   **Seçenek 2-statik kitaplık**: Bu seçenek yalnızca bir Swift kodu içermeyen veya 10,2 < Xcode ile oluşturulmuş uygulamalar/uzantılar için kullanılabilir. `libIntuneMAM.a`Kitaplık bağlantısı. `libIntuneMAM.a` kitaplığını proje hedefinin **Bağlantılı Çerçeveler ve Kitaplıklar** listesine sürükleyin.

    ![Intune Uygulama SDK’sı iOS: bağlantılı çerçeveler ve kitaplıklar](./media/app-sdk-ios/intune-app-sdk-ios-linked-frameworks-and-libraries.png)

    `{PATH_TO_LIB}` öğesini Intune Uygulama SDK'sı konumu ile değiştirerek `-force_load {PATH_TO_LIB}/libIntuneMAM.a` öğesini aşağıdakilerden birine ekleyin:
   * Projenin `OTHER_LDFLAGS` derleme yapılandırma ayarı.
   * Xcode Kullanıcı arabiriminin **diğer bağlayıcı bayrakları**.

     > [!NOTE]
     > `PATH_TO_LIB` öğesini bulmak için `libIntuneMAM.a` dosyasını seçin ve **Dosya** menüsünden **Bilgi Al** öğesini belirleyin. **Bilgi penceresinin** **genel** bölümündeki **buradaki** bilgileri (yol) kopyalayıp yapıştırın.

     `IntuneMAMResources.bundle` kaynak paketini **Derleme Aşamaları** içindeki **Paket Kaynaklarını Kopyala** altına sürükleyerek kaynak paketini projeye ekleyin.

     ![Intune Uygulama SDK'sı iOS: Paket kaynaklarını kopyalama](./media/app-sdk-ios/intune-app-sdk-ios-copy-bundle-resources.png)
         
2. Aşağıdaki iOS çerçevelerini projeye ekleyin:  
   -  MessageUI.framework  
   -  Security.framework  
   -  CoreServices. Framework  
   -  SystemConfiguration.framework  
   -  libsqlite3.tbd  
   -  libc++.tbd  
   -  ImageIO.framework  
   -  LocalAuthentication.framework  
   -  AudioToolbox.framework  
   -  QuartzCore.framework  
   -  WebKit.framework

3. Her bir proje hedefinde **Özellikler**’i seçip **Anahtar Zinciri Paylaşımı** anahtarını etkinleştirerek anahtar zinciri paylaşımını etkinleştirin (önceden etkinleştirilmemişse). Anahtarlık paylaşımı, sonraki adıma devam edebilmeniz için gereklidir.

   > [!NOTE]
   > Sağlama profilinizin, yeni anahtarlık paylaşımı değerlerini desteklemesi gerekir. Anahtarlık erişim grupları bir joker karakteri desteklemelidir. Bunu,. mobileprovision dosyasını bir metin düzenleyicisinde açıp **Anahtarlık erişim grupları**araması yaparak ve bir joker karakter olmasını sağlayarak denetleyebilirsiniz. Örneğin:
   >
   >  ```xml
   >  <key>keychain-access-groups</key>
   >  <array>
   >  <string>YOURBUNDLESEEDID.*</string>
   >  </array>
   >  ```

4. Anahtarlık paylaşımını etkinleştirdikten sonra Intune uygulama SDK 'sının verilerini depolayabileceği ayrı bir erişim grubu oluşturmak için adımları izleyin. Kullanıcı arabirimini veya yetkilendirmeler dosyasını kullanarak bir anahtarlık erişim grubu oluşturabilirsiniz. Anahtarlık erişim grubunu oluşturmak için Kullanıcı arabirimini kullanıyorsanız, şu adımları izlediğinizden emin olun:

     a. Mobil uygulamanızda tanımlanmış bir Anahtarlık erişim grubu yoksa, uygulamanın paket KIMLIĞINI **ilk** grup olarak ekleyin.
    
    b. `com.microsoft.intune.mam` paylaşılan anahtarlık grubunu var olan erişim gruplarınıza ekleyin. Intune Uygulama SDK'sı verileri depolamak için bu erişim grubunu kullanır.
    
    c. `com.microsoft.adalcache` öğesini var olan erişim gruplarınıza ekleyin.
    
      ![Intune Uygulama SDK’sı iOS: Anahtarlık paylaşımı](./media/app-sdk-ios/intune-app-sdk-ios-keychain-sharing.png)
    
    d. Anahtarlık erişim gruplarını oluşturmak için yukarıda gösterilen Xcode UI'ı kullanmak yerine doğrudan yetkilendirme dosyalarını düzenliyorsanız, anahtarlık erişim gruplarını `$(AppIdentifierPrefix)` öğesinin önüne ekleyin (Xcode bunu otomatik olarak işler). Örneğin:
    
      - `$(AppIdentifierPrefix)com.microsoft.intune.mam`
      - `$(AppIdentifierPrefix)com.microsoft.adalcache`
    
      > [!NOTE]
      > Yetkilendirme dosyası, mobil uygulamanıza özel, benzersiz bir XML dosyasıdır. iOS uygulamanızda özel izinler ve özellikler belirtmek için kullanılır. Uygulamanızın önceden bir yetkilendirme dosyası yoksa, anahtarlık paylaşımının etkinleştirilmesi (3. adım) Xcode'un uygulamanız için bir dosya oluşturmasına neden olacaktır. Uygulamanın paket KIMLIĞININ listedeki ilk girdi olduğundan emin olun.

5. Uygulamanızın `UIApplication canOpenURL` öğesine geçirdiği her protokolü, uygulamanızın Info.plist dosyasının `LSApplicationQueriesSchemes` dizisine dahil edin. Sonraki adıma ilerlemeden önce değişikliklerinizi kaydettiğinizden emin olun.

6. Uygulamanız zaten FaceID kullanmıyorsa [NSFaceIDUsageDescription info.plist anahtarının](https://developer.apple.com/library/archive/documentation/General/Reference/InfoPlistKeyReference/Articles/CocoaKeys.html#//apple_ref/doc/uid/TP40009251-SW75) bir varsayılan iletiyle yapılandırıldığından emin olun. Bu, iOS’un kullanıcıya uygulamanın FaceID’yi nasıl kullanacağını bildirmesi için gereklidir. Intune uygulama koruma ilke ayarları, bir BT yöneticisi tarafından yapılandırılırsa FaceID’nin uygulama erişimi için bir yöntem olarak kullanılmasına imkan verir.

7. Uygulamanızın Info.plist dosyasını yapılandırmayı bitirmek için, [SDK deposuna](https://github.com/msintuneappsdk/ms-intune-app-sdk-ios) eklenen IntuneMAMConfigurator aracını kullanın. Araç, üç parametreye sahiptir:

   |Özellik|Nasıl kullanılır?|
   |---------------|--------------------------------|
   |- i |  `<Path to the input plist>` |
   |- e | `<Path to the entitlements file>` |
   |- o |  Seçim`<Path to the output plist>` |

'-o' parametresi belirtilmezse, giriş dosyası yerinde değiştirilir. Araç bir kez etkilidir ve uygulamanın Info.plist dosyası her değiştirildiğinde veya yetkilendirmeler yapıldığında yeniden çalıştırılmalıdır. En son sürümde Info.plist yapılandırma gereksinimlerinin değişmesi durumunda, Intune SDK'sını güncelleştirirken de aracın en son sürümünü indirmeniz ve çalıştırmanız gerekir.

## <a name="configure-adalmsal"></a>ADAL/MSAL yapılandırma

Intune uygulama SDK 'sı, kimlik doğrulama ve koşullu başlatma senaryoları için [Azure Active Directory kimlik doğrulama kitaplığını](https://github.com/AzureAD/azure-activedirectory-library-for-objc) ya da [Microsoft kimlik doğrulama kitaplığını](https://github.com/AzureAD/microsoft-authentication-library-for-objc) kullanabilir. Ayrıca, Kullanıcı kimliğini cihaz kayıt senaryoları olmadan yönetim için MAM hizmetine kaydetmek için ADAL/MSAL kullanır.

Genellikle, ADAL/MSAL, uygulamaya verilen belirteçlerin güvenliğini sağlamak için uygulamaların Azure Active Directory (AAD) ile kaydolmanızı ve benzersiz bir istemci KIMLIĞI ve yeniden yönlendirme URI 'SI oluşturmasını gerektirir. Uygulamanız, kullanıcıların kimliğini doğrulamak için zaten ADAL veya MSAL kullanıyorsa, uygulamanın mevcut kayıt değerlerini kullanması ve Intune uygulama SDK 'sının varsayılan değerlerini geçersiz kılması gerekir. Bu, kullanıcılardan iki kez kimlik doğrulaması (Intune Uygulama SDK'sı ve uygulama tarafından) istenmemesini sağlar.

Uygulamanız zaten ADAL veya MSAL kullanmıyorsa ve herhangi bir AAD kaynağına erişmeniz gerekmiyorsa, ADAL 'i tümleştirmeyi seçerseniz AAD 'de bir istemci uygulama kaydı ayarlamanız gerekmez. MSAL tümleştirmeye karar verirseniz, bir uygulama kaydı yapılandırmanız ve varsayılan Intune istemci KIMLIĞINI ve yeniden yönlendirme URI 'sini geçersiz kılmanız gerekir.  

Uygulamanızın en son [adal](https://github.com/AzureAD/azure-activedirectory-library-for-objc/releases) veya [msal](https://github.com/AzureAD/microsoft-authentication-library-for-objc/releases)sürümüne bağlantısı olması önerilir.

### <a name="link-to-adal-or-msal-binaries"></a>ADAL veya MSAL ikili dosyalarına bağlantı

**Seçenek 1-** Uygulamanızı ADAL ikili dosyalarına bağlamak için [aşağıdaki adımları](https://github.com/AzureAD/azure-activedirectory-library-for-objc#download) izleyin.

**Seçenek 2-** Alternatif olarak, uygulamanızı MSAL ikilileriyle bağlamak için [Bu yönergeleri](https://github.com/AzureAD/microsoft-authentication-library-for-objc#installation) izleyebilirsiniz.

1. Uygulamanızda tanımlanmış bir Anahtarlık erişim grubu yoksa, uygulamanın paket KIMLIĞINI ilk grup olarak ekleyin.

2. Anahtarlık erişim gruplarına ekleyerek ADAL/MSAL çoklu oturum açma (SSO) özelliğini etkinleştirin `com.microsoft.adalcache` .

3. ADAL paylaşımlı önbellek anahtar zinciri grubunu açıkça ayarlıyorsanız, ayarın `<appidprefix>.com.microsoft.adalcache` olduğundan emin olun. Bu ayarı geçersiz kılmadığınız sürece ADAL bunu sizin için ayarlar. `com.microsoft.adalcache` öğesini değiştirmek için özel bir anahtarlık grubu belirtmek isterseniz, bunu IntuneMAMSettings altındaki Info.plist dosyası içinde `ADALCacheKeychainGroupOverride` anahtarını kullanarak belirtin.

### <a name="configure-adalmsal-settings-for-the-intune-app-sdk"></a>Intune uygulama SDK 'Sı için ADAL/MSAL ayarlarını yapılandırma

Uygulamanız kimlik doğrulaması için zaten ADAL veya MSAL kullanıyorsa ve kendi Azure Active Directory ayarlarını içeriyorsa, Intune uygulama SDK 'sını AAD 'ye göre kimlik doğrulaması sırasında aynı ayarları kullanacak şekilde zorlayabilirsiniz. Bu sayede uygulamanın kullanıcıdan iki kez kimlik doğrulaması istemesi engellenmiş olur. Aşağıdaki ayarları doldurma hakkında bilgi edinmek için [Intune Uygulama SDK'sı için ayarları yapılandırma](#configure-settings-for-the-intune-app-sdk) bölümüne göz atın:  

* ADALClientId
* ADALAuthority
* ADALRedirectUri
* ADALRedirectScheme
* ADALCacheKeychainGroupOverride

Uygulamanız zaten ADAL veya MSAL kullanıyorsa, aşağıdaki konfigürasyonlar gereklidir:

1. Projenin Info. plist dosyasında, anahtar adı ile **ıntunemamsettings** sözlüğü altında, `ADALClientId` adal çağrıları IÇIN kullanılacak istemci kimliğini belirtin.

2. Ayrıca, anahtar adlı **ıntunemamsettings** sözlüğü altında `ADALAuthority` , Azure AD yetkilisini belirtin.

3. Ayrıca, anahtar adlı **ıntunemamsettings** sözlüğü altında `ADALRedirectUri` , adal çağrıları için kullanılacak yeniden yönlendirme URI 'sini belirtin. Alternatif olarak, uygulamanın yeniden yönlendirme URI'si `scheme://bundle_id` biçimindeyse bunun yerine `ADALRedirectScheme` belirtebilirsiniz.

Ayrıca, uygulamalar çalışma zamanında bu Azure AD ayarlarını geçersiz kılabilir. Bunu yapmak için `IntuneMAMPolicyManager` örneğinde `aadAuthorityUriOverride`, `aadClientIdOverride` ve `aadRedirectUriOverride` özelliklerini ayarlamanız yeterlidir.

4. İOS uygulama izinlerinizi uygulama koruma ilkesi (APP) hizmetine verme adımlarının izlendiğinden emin olun. "[Uygulamanızın Intune uygulama koruma hizmeti 'ne erişmesine Izin verin (isteğe bağlı)](app-sdk-get-started.md#give-your-app-access-to-the-intune-app-protection-service-optional)" altındaki [Intune SDK 'sını](app-sdk-get-started.md#next-steps-after-integration) kullanmaya başlama yönergelerini kullanın.  

> [!NOTE]
> Statik olan ve çalışma zamanında saptanması gerekmeyen tüm ayarlar için Info.plist yaklaşımı önerilir. `IntuneMAMPolicyManager` özelliklerine atanan değerler, Info.plist dosyasında belirtilen ve bunlara karşılık gelen tüm değerlerden önceliklidir ve uygulama yeniden başlatıldıktan sonra bile kalıcı olmayı sürdürür. Kullanıcının kaydı silinene ya da değerler temizlenene veya değiştirilene kadar SDK ilke iadelerinde bunları kullanmaya devam edecektir.

### <a name="if-your-app-does-not-use-adal-or-msal"></a>Uygulamanız ADAL veya MSAL kullanmıyorsa

Daha önce belirtildiği gibi, Intune uygulama SDK 'sı kimlik doğrulaması ve koşullu başlatma senaryoları için [Azure Active Directory kimlik doğrulama kitaplığını](https://github.com/AzureAD/azure-activedirectory-library-for-objc) veya [Microsoft kimlik doğrulama kitaplığını](https://github.com/AzureAD/microsoft-authentication-library-for-objc) kullanabilir. Ayrıca, Kullanıcı kimliğini cihaz kayıt senaryoları olmadan yönetim için MAM hizmetine kaydetmek için ADAL/MSAL kullanır. **Uygulamanız kendi kimlik doğrulama mekanizması IÇIN adal veya msal kullanmıyorsa**, tümleştirmeyi seçtiğiniz kimlik doğrulama kitaplığına bağlı olarak özel AAD ayarlarını yapılandırmanız gerekebilir:   

ADAL-Intune uygulama SDK 'Sı, ADAL parametrelerinin varsayılan değerlerini sağlar ve Azure AD kimlik doğrulamasını işler. Geliştiricilerin daha önce bahsedilen ADAL ayarları için herhangi bir değer belirtmelerine gerek yoktur. 

MSAL-geliştiricilerin, [burada](https://github.com/AzureAD/microsoft-authentication-library-for-objc/wiki/Migrating-from-ADAL-Objective-C-to-MSAL-Objective-C#app-registration-migration)belirtilen biçimde özel bir yeniden yönlendirme URI 'SI ile AAD 'de bir uygulama kaydı oluşturması gerekir. Geliştiriciler `ADALClientID` `ADALRedirectUri` daha önce bahsedilen ve ayarlarını ya da `aadClientIdOverride` örnekteki eşdeğerini ve özellikleri ayarlamalıdır `aadRedirectUriOverride` `IntuneMAMPolicyManager` . Geliştiriciler, Intune uygulama koruma hizmeti 'ne uygulama kaydı erişimi sağlamak için önceki bölümde 4. adımı izlediklerinden emin olmalıdır.

### <a name="special-considerations-when-using-msal"></a>MSAL kullanılırken özel konular 

1. **WebView hesabınızı kontrol edin** ; uygulamaların, uygulama tarafından başlatılan msal etkileşimli kimlik doğrulama işlemlerinde Web görünümü olarak SFSafariViewController, SFAuthSession veya ASWebAuthSession kullanması önerilir. Bazı nedenlerle uygulamanızın herhangi bir etkileşimli MSAL auth işlemi için bu Web görünümlerinden birini kullanması gerekiyorsa, `SafariViewControllerBlockedOverride` `true` `IntuneMAMSettings` uygulamanın Info. plist dosyasındaki sözlük altında olarak da ayarlanmalıdır. Uyarı: Bu, kimlik doğrulama oturumunu etkinleştirmek üzere Intune 'un SafariViewController kancalarını devre dışı bırakır. Bu, uygulama kurumsal verileri görüntülemek için SafariViewController kullanıyorsa, uygulama bu Web görünümü türlerinden herhangi birinde kurumsal verileri göstermemelidir.
2. **Hem adal hem de msal** -geliştiricilerin bağlanması, Intune 'un bu senaryoda adal üzerinde msal 'yi tercih edebilecekleri şekilde kabul etmelidir. Varsayılan olarak, Intune desteklenen ADAL sürümlerini desteklenen MSAL sürümlerine, her ikisi de çalışma zamanında bağlanmışsa tercih edecektir. Intune, Intune 'un ilk kimlik doğrulama işlemi sırasında olduğunda yalnızca desteklenen bir MSAL sürümünü tercih eder `IntuneMAMUseMSALOnNextLaunch` `true` `NSUserDefaults` . `IntuneMAMUseMSALOnNextLaunch` `false` Veya ayarlanmamışsa, Intune varsayılan davranışa geri dönecektir. Adından da anlaşılacağı gibi, bir değişiklik `IntuneMAMUseMSALOnNextLaunch` sonraki başlatma üzerinde devreye girer.


## <a name="configure-settings-for-the-intune-app-sdk"></a>Intune Uygulama SDK'sı ayarlarını yapılandırma

Intune uygulama SDK 'sını ayarlamak ve yapılandırmak için uygulamanın Info. plist dosyasındaki **ıntunemamsettings** sözlüğünü kullanabilirsiniz. IntuneMAMSettings sözlüğü Info.plist dosyanızda görünmüyorsa, sözlüğü oluşturmalısınız.

IntuneMAMSettings sözlüğü altında, Intune Uygulama SDK'sını yapılandırmak için desteklenen şu ayarları kullanabilirsiniz.

Bu ayarlardan bazıları önceki bölümlerde ele alınmış olabilir ve bazıları tüm uygulamalar için geçerli değildir.

Ayar  | Tür  | Tanım | Gerekli mi?
--       |  --   |   --       |  --
ADALClientId  | Dize  | Uygulamanın Azure AD istemci tanımlayıcısı. | Intune olmayan bir AAD kaynağına erişen MSAL ve herhangi bir ADAL uygulamasını kullanan tüm uygulamalar için gereklidir. |
ADALAuthority | Dize | Uygulamanın Azure AD yetkilisi kullanımda. AAD hesaplarının yapılandırıldığı ortamınızı kullanmanız gerekir. | İsteğe bağlı. Uygulama, tek bir kuruluş/AAD kiracısı içinde kullanılmak üzere oluşturulmuş özel bir iş kolu uygulaması ise önerilir. Bu değer yoksa, ortak AAD yetkilisi kullanılır.|
ADALRedirectUri  | Dize  | Uygulamanın Azure AD yeniden yönlendirme URI 'SI. | MSAL kullanan tüm uygulamalar için ADALRedirectUri veya ADALRedirectScheme, Intune olmayan bir AAD kaynağına erişen herhangi bir ADAL uygulaması için gereklidir.  |
ADALRedirectScheme  | Dize  | Uygulamanın Azure AD yeniden yönlendirme şeması. Bu, uygulamanın yeniden yönlendirme URI'si `scheme://bundle_id` biçimindeyse ADALRedirectUri yerine kullanılabilir. | MSAL kullanan tüm uygulamalar için ADALRedirectUri veya ADALRedirectScheme, Intune olmayan bir AAD kaynağına erişen herhangi bir ADAL uygulaması için gereklidir. |
ADALLogOverrideDisabled | Boole  | SDK 'nın tüm ADAL/MSAL günlüklerini (varsa, uygulamadan gelen ADAL çağrıları dahil) kendi günlük dosyasına yönlendirip yönlendirmeyeceğini belirtir. Varsayılan ayar HAYIR’dır. Uygulama kendi ADAL/MSAL günlük geri aramasını ayarlayacaktır Evet olarak ayarlayın. | İsteğe bağlı. |
ADALCacheKeychainGroupOverride | Dize  | "Com. Microsoft. adalcache" yerine ADAL/MSAL önbelleği için kullanılacak Anahtarlık grubunu belirtir. Bunun uygulama kimliği öneki olmadığına unutmayın. Bu, çalışma zamanında sağlanan dizeye önek olarak eklenir. | İsteğe bağlı. |
AppGroupIdentifiers | Dizeler dizisi  | Uygulamanın yetkilendirmeleri com. Apple. Security. Application-Groups bölümündeki uygulama grupları dizisi. | Uygulama, uygulama grupları kullanıyorsa gereklidir. |
ContainingAppBundleId | Dize | Uzantının içeren uygulamanın paket KIMLIĞINI belirtir. | iOS uzantıları için gereklidir. |
DebugSettingsEnabled| Boole | EVET olarak ayarlanırsa, Ayarlar paketindeki sınama ilkeleri uygulanabilir. Uygulamalar bu ayar etkin olarak *gönderilmemelidir*. | İsteğe bağlı. Varsayılan ayar Hayır’dır. |
AutoEnrollOnLaunch| Boole| Mevcut bir yönetilen kimlik tespit edilirse ve bu kimlik henüz kaydedilmemişse uygulama başlatıldığında otomatik olarak kaydetmeye çalışılıp çalışılmayacağını belirtir. Varsayılan ayar HAYIR’dır. <br><br> Notlar: yönetilen kimlik bulunamazsa veya ADAL/MSAL önbelleğinde kimlik için geçerli bir belirteç yoksa, uygulama aynı zamanda MAMPolicyRequired Evet olarak ayarlanmadığı müddetçe kayıt girişimi kimlik bilgileri istenmeden sessizce başarısız olur. | İsteğe bağlı. Varsayılan ayar Hayır’dır. |
MAMPolicyRequired| Boole| Uygulamanın bir Intune uygulama koruma ilkesine sahip olmadığında başlatılmasının engellenip engellenmeyeceğini belirtir. Varsayılan ayar HAYIR’dır. <br><br> Not: MAMPolicyRequired ayarı EVET olarak ayarlanmışsa uygulamalar App Store’a gönderilemez. MAMPolicyRequired EVET olarak ayarlandığında AutoEnrollOnLaunch da EVET olarak ayarlanmalıdır. | İsteğe bağlı. Varsayılan ayar Hayır’dır. |
MAMPolicyWarnAbsent | Boole| Uygulamanın bir Intune uygulama koruma ilkesine sahip olmadığında başlatılırken kullanıcıyı uyarıp uyarmayacağını belirtir. <br><br> Not: Kullanıcılar, uyarı kapatıldıktan sonra da uygulamayı ilke olmadan kullanabilecektir. | İsteğe bağlı. Varsayılan ayar Hayır’dır. |
MultiIdentity | Boole| Uygulamanın çoklu kimliği fark edip edemediğini belirtir. | İsteğe bağlı. Varsayılan ayar Hayır’dır. |
SafariViewControllerBlockedOverride | Boole| SFSafariViewController, SFAuthSession veya ASWebAuthSession aracılığıyla MSAL kimlik doğrulamasını etkinleştirmek için Intune 'un SafariViewController kancalarını devre dışı bırakır. | İsteğe bağlı. Varsayılan ayar Hayır’dır. Uyarı: yanlış kullanıldığında veri sızıntısı oluşabilir. Yalnızca kesinlikle gerekliyse etkinleştirin. Ayrıntılar için [msal kullanırken özel noktalara](#special-considerations-when-using-msal) bakın.  |
SplashIconFile <br>SplashIconFile~ipad | Dize  | Intune giriş (başlangıç) simge dosyasını belirtir. | İsteğe bağlı. |
SplashDuration | Sayı | Intune başlangıç ekranının uygulama başlatılırken gösterileceği en kısa süre miktarı (saniye cinsinden). Varsayılan olarak 1,5’tir. | İsteğe bağlı. |
BackgroundColor| Dize| Intune SDK 'sının Kullanıcı arabirimi bileşenleri için arka plan rengini belirtir. #XXXXXX biçiminde bir onaltılık RGB dizesini kabul eder; burada X, 0-9 veya A-F aralığındadır. Diyez işareti atlanabilir.   | İsteğe bağlı. İOS sürümlerinde ve iOS koyu mod ayarına göre değişebilen sistem arka plan rengi varsayılan olarak değişir. |
ForegroundColor| Dize| Intune SDK 'sının Kullanıcı arabirimi bileşenlerinin metin rengi gibi ön plan rengini belirtir. #XXXXXX biçiminde bir onaltılık RGB dizesini kabul eder; burada X, 0-9 veya A-F aralığındadır. Diyez işareti atlanabilir.  | İsteğe bağlı. İOS sürümlerinde ve iOS koyu mod ayarına göre değişebilen sistem etiketi rengine varsayılan olarak izin verebilir. |
AccentColor | Dize| Intune SDK 'sının Kullanıcı arabirimi bileşenlerinin düğme metin rengi ve PIN kutusu vurgu rengi gibi vurgu rengini belirtir. #XXXXXX biçiminde bir onaltılık RGB dizesini kabul eder; burada X, 0-9 veya A-F aralığındadır. Diyez işareti atlanabilir.| İsteğe bağlı. Varsayılan olarak sistem mavisidir. |
SecondaryBackgroundColor| Dize| MTD ekranları için ikincil arka plan rengini belirtir. #XXXXXX biçiminde bir onaltılık RGB dizesini kabul eder; burada X, 0-9 veya A-F aralığındadır. Diyez işareti atlanabilir.   | İsteğe bağlı. Varsayılan olarak beyaz olur. |
SecondaryForegroundColor| Dize| MTD ekranları için dipnot rengi gibi ikincil ön plan rengini belirtir. #XXXXXX biçiminde bir onaltılık RGB dizesini kabul eder; burada X, 0-9 veya A-F aralığındadır. Diyez işareti atlanabilir.  | İsteğe bağlı. Varsayılan olarak gri olur. |
SupportsDarkMode| Boole | BackgroundColor/ForegroundColor/AccentColor için açık bir değer ayarlanmamışsa, Intune SDK 'sının Kullanıcı arabirimi renk düzeninin sistem koyu Mod ayarını gözlemeyeceğini belirtir | İsteğe bağlı. Varsayılan değer Evet ' tir. |
MAMTelemetryDisabled| Boole| SDK’nın arka ucuna herhangi bir telemetri verisi gönderip göndermeyeceğini belirtir.| İsteğe bağlı. Varsayılan ayar Hayır’dır. |
MAMTelemetryUsePPE | Boole | MAM SDK'sının PPE telemetri arka ucuna veri gönderip göndermeyeceğini belirtir. Sınama telemetri verilerinin müşteri verileriyle karışmaması için uygulamalarınızı Intune ilkesiyle sınarken bunu kullanın. | İsteğe bağlı. Varsayılan ayar Hayır’dır. |
MaxFileProtectionLevel | Dize | İsteğe bağlı. Uygulamanın destekleyebildiği maksimum `NSFileProtectionType` belirtmesine olanak tanır. Düzey uygulamanın destekleyebildiğinden daha yüksekse, bu değer hizmet tarafından gönderilen ilkeyi geçersiz kılar. Olası değerler: `NSFileProtectionComplete`, `NSFileProtectionCompleteUnlessOpen`, `NSFileProtectionCompleteUntilFirstUserAuthentication`, `NSFileProtectionNone`.|
OpenInActionExtension | Boole | Şurada aç Eylemi uzantıları için EVET olarak ayarlayın. Daha fazla bilgi için UIActivityViewController yoluyla Veri Paylaşımı bölümüne bakın. |
WebViewHandledURLSchemes | Dize Dizisi | Uygulamanızın WebView’unun işlediği URL şemalarını belirtir. | Uygulamanız URL'leri bağlantılar ve/veya javascript aracılığıyla işleyen bir WebView kullanıyorsa gereklidir. |
DocumentBrowserFileCachePath | Dize | Uygulamanız, [`UIDocumentBrowserViewController`](https://developer.apple.com/documentation/uikit/uidocumentbrowserviewcontroller?language=objc) çeşitli dosya sağlayıcılarındaki dosyalara göz atmak için kullanıyorsa, bu yolu uygulama korumalı alan ana dizinine göre ayarlayabilirsiniz, böylece ıNTUNE SDK şifresi çözülmüş yönetilen dosyaları bu klasöre bırakabilir. | İsteğe bağlı. Varsayılan olarak `/Documents/` dizini. |
VerboseLoggingEnabled | Boole | Evet olarak ayarlanırsa, Intune ayrıntılı modda günlüğe kaydedilir. | İsteğe bağlı. Varsayılan olarak Hayır |

## <a name="receive-app-protection-policy"></a>Uygulama koruma ilkesini alma

### <a name="overview"></a>Genel Bakış

Intune uygulama koruma ilkesini almak için, uygulamaların Intune MAM hizmetiyle bir kayıt isteği başlatmaları gerekir. Uygulamalar, Intune konsolunda cihaz kaydıyla veya cihaz kaydı olmadan uygulama koruma ilkesini almak için yapılandırılabilir. Kayıt olmadan uygulama koruma ilkesi (**APP-WE** veya MAM-WE olarak da bilinir), uygulamaların Intune mobil cihaz yönetimine (MDM) kaydedilmeden Intune tarafından yönetilmesine izin verir. Her iki durumda da, ilkeyi almak için Intune MAM hizmetine kaydolmak gereklidir.

> [!Important]
> İOS için Intune uygulama SDK 'Sı, uygulama koruma Ilkeleri tarafından şifreleme etkinleştirildiğinde 256 bitlik şifreleme anahtarlarını kullanır. Korunan veri paylaşımına izin vermek için tüm uygulamaların geçerli bir SDK sürümüne sahip olması gerekir.

### <a name="apps-that-already-use-adal-or-msal"></a>Zaten ADAL veya MSAL kullanan uygulamalar

Zaten ADAL veya MSAL kullanan uygulamalar, `registerAndEnrollAccount` `IntuneMAMEnrollmentManager` Kullanıcı başarıyla doğrulandıktan sonra örnekteki yöntemi çağırmalıdır:

```objc
/*
 *  This method will add the account to the list of registered accounts.
 *  An enrollment request will immediately be started.
 *  @param identity The UPN of the account to be registered with the SDK
 */

(void)registerAndEnrollAccount:(NSString *)identity;
```

SDK, `registerAndEnrollAccount` yöntemini çağırarak kullanıcı hesabını kaydeder ve uygulamayı bu hesap adına kaydetmeyi dener. Kayıt işlemi herhangi bir nedenle başarısız olursa SDK, kayıt işlemini 24 saat sonra otomatik olarak yeniden dener. Uygulama, hata ayıklama amacıyla herhangi bir kayıt isteğinin sonuçlarıyla ilgili bir temsilci aracılığıyla [bildirim](#status-result-and-debug-notifications)alabilir.

Bu API çağrıldıktan sonra, uygulama normal çalışmasına devam edebilir. Kayıt başarılı olursa, SDK kullanıcıya uygulamanın yeniden başlatılması gerektiğini bildirir. Bu sırada, kullanıcı uygulamayı hemen yeniden başlatabilir.

```objc
[[IntuneMAMEnrollmentManager instance] registerAndEnrollAccount:@"user@foo.com"];
```

### <a name="apps-that-do-not-use-adal-or-msal"></a>ADAL veya MSAL kullanmayan uygulamalar

ADAL veya MSAL kullanarak Kullanıcı oturumu olmayan uygulamalar, API 'yi çağırarak SDK 'nın bu kimlik doğrulamasını işlemesini sağlamak için Intune MAM hizmetinden uygulama koruma ilkesi alabilir. Azure AD ile bir kullanıcının kimlik doğrulamasını gerçekleştirmeyip, yine de verilerin korunmasına yardımcı olmak için uygulama koruma ilkesini alması gereken uygulamaların bu tekniği kullanması gerekir. Örneğin uygulamada oturum açmak için başka bir kimlik doğrulaması hizmeti kullanılıyor veya uygulama oturum açmayı hiç desteklemiyorsa. Bunu yapmak için, uygulamanın `IntuneMAMEnrollmentManager`örneğinden `loginAndEnrollAccount` yöntemini çağırabilir:

```objc
/**
 *  Creates an enrollment request which is started immediately.
 *  If no token can be retrieved for the identity, the user will be prompted
 *  to enter their credentials, after which enrollment will be retried.
 *  @param identity The UPN of the account to be logged in and enrolled.
 */
 (void)loginAndEnrollAccount: (NSString *)identity;
```

Mevcut herhangi bir belirteç bulunamazsa, SDK bu yöntemi çağırarak kullanıcıdan kimlik bilgilerini ister. Ardından SDK, sağlanan kullanıcı hesabı adına uygulamayı Intune MAM hizmetine kaydetmeyi dener. Yöntem, "nil" kimliği ile çağrılabilir. Bu durumda SDK cihazdaki mevcut yönetilen kullanıcıyı kaydeder (MDM'de) veya mevcut kullanıcı bulunamazsa kullanıcıdan kullanıcı adı girmesini ister.

Kayıt başarısız olursa, uygulama hatanın ayrıntılarına bağlı olarak bu API’yi gelecekte yeniden çağırmayı göz önünde bulundurmalıdır. Uygulama, bir temsilci yoluyla herhangi bir kayıt isteğinin sonuçlarıyla ilgili [bildirim](#status-result-and-debug-notifications) alabilir.

Bu API çağrıldıktan sonra, uygulama normal çalışmasına devam edebilir. Kayıt başarılı olursa, SDK kullanıcıya uygulamanın yeniden başlatılması gerektiğini bildirir.

Örnek:

```objc
[[IntuneMAMEnrollmentManager instance] loginAndEnrollAccount:@"user@foo.com"];
```

### <a name="let-intune-handle-authentication-and-enrollment-at-launch"></a>Intune'un başlatma sırasında kimlik doğrulama ve kayıt işlemlerini işlemesini sağlama

Intune SDK 'sının, uygulamanızın başlatılması tamamlanmadan önce ADAL/MSAL ve kayıt kullanarak tüm kimlik doğrulamasını işlemesini istiyorsanız ve uygulamanız her zaman uygulama ilkesi gerektirdiğinde, API 'yi kullanmanız gerekmez `loginAndEnrollAccount` . Uygulamanın Info.plist dosyasındaki IntuneMAMSettings sözlüğünde aşağıdaki iki ayarı EVET olarak ayarlamanız yeterli olur.

Ayar  | Tür  | Tanım |
--       |  --   |   --       |  
AutoEnrollOnLaunch| Boole| Mevcut bir yönetilen kimlik tespit edilirse ve bu kimlik henüz kaydedilmemişse uygulama başlatıldığında otomatik olarak kaydetmeye çalışılıp çalışılmayacağını belirtir. Varsayılan ayar HAYIR’dır. <br><br> Note: yönetilen kimlik bulunamazsa veya ADAL/MSAL önbelleğinde kimlik için geçerli bir belirteç yoksa, uygulama aynı zamanda MAMPolicyRequired Evet olarak ayarlanmadığı takdirde kayıt girişimi kimlik bilgileri istenmeden sessizce başarısız olur. |
MAMPolicyRequired| Boole| Uygulamanın bir Intune uygulama koruma ilkesine sahip olmadığında başlatılmasının engellenip engellenmeyeceğini belirtir. Varsayılan ayar HAYIR’dır. <br><br> Not: MAMPolicyRequired ayarı EVET olarak belirlenmişse uygulamalar App Store’a gönderilemez. MAMPolicyRequired EVET olarak ayarlandığında AutoEnrollOnLaunch da EVET olarak ayarlanmalıdır. |

Uygulamanız için bu seçeneği belirtirseniz, kayıt sonrasında uygulamanızı yeniden başlatma işlemini yapmanız gerekmez.

### <a name="deregister-user-accounts"></a>Kullanıcı hesaplarının kaydını kaldırma

Kullanıcı bir uygulamanın oturumunu kapatmadan önce, uygulamanın kullanıcı SDK kaydını kaldırması gerekir. Bu şunları sağlar:

1. Kayıt yeniden denemeleri Kullanıcı hesabı için artık gerçekleşmeyecektir.

2. Uygulama koruma ilkesi kaldırılır.

3. Bir uygulama seçmeli silme işlemi (isteğe bağlı) başlatırsa, tüm şirket verileri silinir.

Kullanıcı oturumunu kapatmadan önce, uygulamanın `IntuneMAMEnrollmentManager` örneğinde aşağıdaki yöntemi çağırması gerekir:

```objc
/*
 *  This method will remove the provided account from the list of
 *  registered accounts.  Once removed, if the account has enrolled
 *  the application, the account will be un-enrolled.
 *  @note In the case where an un-enroll is required, this method will block
 *  until the Intune APP AAD token is acquired, then return.  This method must be called before  
 *  the user is removed from the application (so that required AAD tokens are not purged
 *  before this method is called).
 *  @param identity The UPN of the account to be removed.
 *  @param doWipe   If YES, a selective wipe if the account is un-enrolled
 */
(void)deRegisterAndUnenrollAccount:(NSString *)identity withWipe:(BOOL)doWipe;
```

Bu yöntem, Kullanıcı hesabının Azure AD belirteçleri silinmeden önce çağrılmalıdır. SDK 'nın Kullanıcı adına Intune MAM hizmetine belirli istekler yapması için Kullanıcı hesabının AAD belirteçlerine ihtiyacı vardır.

Uygulama kullanıcının şirket verilerini kendi kendine silecektir, `doWipe` bayrak false olarak ayarlanabilir. Aksi takdirde uygulama, seçmeli temizleme işlemini SDK’nın başlatmasını sağlayabilir. Bu, uygulamanın seçmeli silme temsilcisine çağrı yapılmasına neden olur.

Örnek:

```objc
[[IntuneMAMEnrollmentManager instance] deRegisterAndUnenrollAccount:@"user@foo.com" withWipe:YES];
```

## <a name="status-result-and-debug-notifications"></a>Durum, sonuç ve hata ayıklama bildirimleri

Uygulama, Intune MAM hizmetine yapılan aşağıdaki istekler hakkında durum, sonuç ve hata ayıklama bildirimleri alabilir:

* Kayıt istekleri
* İlke güncelleştirme istekleri
* Kayıt kaldırma istekleri

Bildirimler temsilci yöntemleri aracılığıyla `IntuneMAMEnrollmentDelegate.h` içinde sunulur:

```objc
/**
 *  Called when an enrollment request operation is completed.
 * @param status status object containing debug information
 */

(void)enrollmentRequestWithStatus:(IntuneMAMEnrollmentStatus *)status;

/**
 *  Called when a MAM policy request operation is completed.
 *  @param status status object containing debug information
 */
(void)policyRequestWithStatus:(IntuneMAMEnrollmentStatus *)status;

/**
 *  Called when a un-enroll request operation is completed.
 *  @Note: when a user is un-enrolled, the user is also de-registered with the SDK
 *  @param status status object containing debug information
 */

(void)unenrollRequestWithStatus:(IntuneMAMEnrollmentStatus *)status;
```

Bu temsilci yöntemleri aşağıdaki bilgileri içeren bir `IntuneMAMEnrollmentStatus` nesnesi getirir:

* İstekle ilişkili hesabın kimliği
* İstek sonucunu gösteren bir durum kodu
* Durum kodunun açıklamasını içeren bir hata dizesi
* Bir `NSError` nesnesi. Bu nesne, getirilebilecek belirli durum kodlarıyla birlikte `IntuneMAMEnrollmentStatus.h` içinde tanımlanır.

### <a name="sample-code"></a>Örnek kod

Aşağıdakiler temsilci yöntemlerine örnek uygulamalardır:

```objc
- (void)enrollmentRequestWithStatus:(IntuneMAMEnrollmentStatus*)status
{
    NSLog(@"enrollment result for identity %@ with status code %ld", status.identity, (unsigned long)status.statusCode);
    NSLog(@"Debug Message: %@", status.errorString);
}

- (void)policyRequestWithStatus:(IntuneMAMEnrollmentStatus*)status
{
    NSLog(@"policy check-in result for identity %@ with status code %ld", status.identity, (unsigned long)status.statusCode);
    NSLog(@"Debug Message: %@", status.errorString);
}

- (void)unenrollRequestWithStatus:(IntuneMAMEnrollmentStatus*)status
{
    NSLog(@"un-enroll result for identity %@ with status code %ld", status.identity, (unsigned long)status.statusCode);
    NSLog(@"Debug Message: %@", status.errorString);
}
```

## <a name="application-restart"></a>Uygulama yeniden başlatma

Bir uygulama MAM ilkelerini ilk kez aldığında, gerekli kancaları uygulamak için yeniden başlatılması gerekir. Bir uygulamaya yeniden başlatma gerekliliğini bildirmek için, SDK `IntuneMAMPolicyDelegate.h` içinde bir temsilci yöntemi sağlar.

```objc
 - (BOOL) restartApplication
```

Bu yöntemin dönüş değeri, uygulamanın gerekli yeniden başlatma işlemini kendi yapmasının gerekip gerekmediğini SDK’ya bildirir:

* Dönüş değeri true olursa, uygulamanın yeniden başlatma işlemini kendi yapması gerekir.

* Dönüş değeri false olursa, SDK uygulamayı bu yöntemin dönüşünün ardından yeniden başlatır. SDK kullanıcıya uygulamayı hemen yeniden başlatmasını belirten bir iletişim kutusu gösterir.

## <a name="customize-your-apps-behavior-with-apis"></a>Uygulamanızın davranışını API’lerle özelleştirme

Intune Uygulama SDK'sında, uygulamaya dağıtılan Intune APP ilkesi hakkında bilgi almak için çağırabileceğiniz birkaç API vardır. Uygulamanızın davranışını özelleştirmek için bu verileri kullanabilirsiniz. Aşağıdaki tabloda, kullanacağınız bazı temel Intune sınıfları hakkında bilgi verilmektedir.

Sınıf | Açıklama
----- | -----------
IntuneMAMPolicyManager.h | IntuneMAMPolicyManager sınıfı, uygulamaya dağıtılan Intune APP ilkesini gösterir. Özellikle, [Çoklu kimliği etkinleştirme](app-sdk-ios.md#enable-multi-identity-optional) için faydalı olan API’leri gösterir. |
IntuneMAMPolicy.h | IntuneMAMPolicy sınıfı uygulamaya uygulanan bazı MAM ilkesi ayarlarını gösterir. Bu ilke ayarları, uygulamanın kendi kullanıcı arabirimini özelleştirebilmesi için gösterilir. İlke ayarlarının çoğu uygulama değil SDK tarafından zorlanır. Uygulamada kullanılması gereken tek ayar Farklı kaydet denetimidir. Bu sınıf Farklı kaydet'i uygulamak için gereken bazı API'leri gösterir. |
IntuneMAMFileProtectionManager.h | IntuneMAMFileProtectionManager sınıfı, uygulamanın sağlanan kimlik temelinde açıkça dosyaların ve dizinlerin güvenliğini sağlamak için kullanabileceği API'leri gösterir. Kimlik Inture tarafından yönetilebilir veya yönetilmeyen bir kimlik olabilir ve SDK uygun MAM ilkesini uygular. Bu sınıfın kullanımı isteğe bağlıdır. |
IntuneMAMDataProtectionManager.h | IntuneMAMDataProtectionManager sınıfı, uygulamanın sağlanan kimlik temelinde veri arabelleklerinin güvenliğini sağlamak için kullanabileceği API'leri gösterir. Kimlik Inture tarafından yönetilebilir veya yönetilmeyen bir kimlik olabilir ve SDK uygun şifrelemeyi uygular. |

## <a name="implement-allowed-accounts"></a>Izin verilen hesapları Uygula

Intune, BT yöneticilerinin Kullanıcı tarafından hangi hesapların oturum açgirebileceği belirtmesini sağlar. Uygulamalar, belirtilen izin verilen hesaplar listesi için Intune uygulama SDK 'sını sorgulayabilir ve sonra yalnızca izin verilen hesapların cihazda imzalandığından emin olabilir.

İzin verilen hesapları sorgulamak için uygulama `allowedAccounts` üzerinde özelliğini denetlemelidir `IntuneMAMEnrollmentManager` . `allowedAccounts`Özelliği, izin verilen hesapları içeren bir dizi ya da Nil. Özellik Nil ise izin verilen hesaplar belirtilmez.

Uygulamalar, `allowedAccounts` bildirimi gözlemleyerek özelliğin değişikliklerine de tepki verebilir `IntuneMAMAllowedAccountsDidChangeNotification` . Bildirim, `allowedAccounts` özellik değeri her değiştiğinde gönderilir.

## <a name="implement-save-as-and-open-from-controls"></a>Farklı Kaydet ve açılan denetimleri uygulama

Intune, BT yöneticilerinin yönetilen bir uygulamanın verileri hangi depolama konumlarına kaydedebileceği veya buradan veri açmasını sağlar. Uygulamalar, `isSaveToAllowedForLocation` içinde tanımlanan API 'yi kullanarak izin verilen kayıt depolama konumları Için ıNTUNE mam SDK 'sını sorgulayabilir `IntuneMAMPolicy.h` . Uygulamalar, `isOpenFromAllowedForLocation` içinde tanımlanan API 'yi kullanarak izin verilen açık depolama konumları Için ıNTUNE mam SDK 'sını de sorgulayabilir `IntuneMAMPolicy.h` .

Yönetilen verileri bulut depolama alanına veya yerel konumlara kaydetmeden önce, BT yöneticisinin o konuma veri kaydedilmesine izin verip vermediğini öğrenmek için uygulamaların `isSaveToAllowedForLocation` API’sini denetlemesi gerekir.
Bir bulut depolama alanından veya yerel bir konumdan bir uygulamaya veri açmadan önce, uygulamanın `isOpenFromAllowedForLocation` BT yöneticisinin veri üzerinde açılıp açılmadığını bilmesi için API 'yi denetlemesi gerekir.

Uygulamalar `isSaveToAllowedForLocation` veya `isOpenFromAllowedForLocation` API 'leri kullanırken, varsa, depolama konumu için UPN 'ye geçmesi gerekir.

### <a name="supported-save-locations"></a>Desteklenen kaydetme konumları

`isSaveToAllowedForLocation` API’si, BT yöneticisinin aşağıdaki konumlara veri kaydetme izni verip vermediğinin denetlenmesini sağlayan ve `IntuneMAMPolicy.h` içinde tanımlanan sabitler sağlar:

* IntuneMAMSaveLocationOther
* IntuneMAMSaveLocationOneDriveForBusiness
* IntuneMAMSaveLocationSharePoint
* IntuneMAMSaveLocationLocalDrive
* IntuneMAMSaveLocationCameraRoll
* Intunemamsavelocationaccountdocument

Uygulamalar, OneDrive İş gibi “yönetilen” veya “kişisel” olarak kabul edilen konumlara veri kaydedilip kaydedilemeyeceğini denetlemek için `isSaveToAllowedForLocation` içindeki sabitleri kullanmalıdır. Ayrıca uygulama bir konumun “yönetilen” veya “kişisel” olup olmadığını denetleyemiyorsa API kullanılmalıdır.

Uygulama yerel cihazdaki herhangi bir konuma veri kaydediyorsa `IntuneMAMSaveLocationLocalDrive` sabiti kullanılmalıdır. Benzer şekilde, `IntuneMAMSaveLocationCameraRoll` uygulama kamera rulosına bir fotoğraf kaydediyorsunuz sabiti kullanılmalıdır.

Hedef konum için hesap bilinmiyorsa, `nil` geçirilmesi gerekir. `IntuneMAMSaveLocationLocalDrive`Ve `IntuneMAMSaveLocationCameraRoll` konumları her zaman bir `nil` Hesapla eşleştirilmelidir.

### <a name="supported-open-locations"></a>Desteklenen açık konumlar

`isOpenFromAllowedForLocation`API, BT yöneticisinin ' de tanımlanan konumlardan veri açılmasına izin verip vermediğini denetlemek için sabitler sağlar `IntuneMAMPolicy.h` .

* Intunemamopenlocationother
* Intunemamopenlocationonedriveforbusiness
* Intunemamopenlocationsharepoint
* Intunemamopenlocationcamera
* Intunemamopenlocationlocalstorage
* Intunemamopenlocationaccountdocument

Uygulamalar, `isOpenFromAllowedForLocation` OneDrive iş veya "kişisel" gibi "yönetilen" olarak kabul edilen konumlardan verilerin açılıp açılmadığını denetlemek için içindeki sabitleri kullanmalıdır. Ayrıca, uygulama bir konumun "yönetilen" veya "kişisel" olup olmadığını denetleyemiyorum, API kullanılmalıdır.

`IntuneMAMOpenLocationCamera`Uygulama, kameradan veya fotoğraf albümünden verileri açarken sabit kullanılmalıdır.

`IntuneMAMOpenLocationLocalStorage`Uygulama yerel cihazdaki herhangi bir konumdan veri açarken sabit kullanılmalıdır.

`IntuneMAMOpenLocationAccountDocument`Uygulama, yönetilen hesap kimliği olan bir belgeyi açarken sabit kullanılmalıdır (aşağıdaki "paylaşılan veriler" bölümüne bakın)

Kaynak konumu hesabı bilinmiyorsa, `nil` geçirilmesi gerekir. `IntuneMAMOpenLocationLocalStorage`Ve `IntuneMAMOpenLocationCamera` konumları her zaman bir `nil` Hesapla eşleştirilmelidir.

### <a name="unknown-or-unlisted-locations"></a>Bilinmeyen veya listelenmemiş konumlar

İstenen konum `IntuneMAMSaveLocation` veya numaralandırmalar içinde listelenmediyse `IntuneMAMOpenLocation` veya bilinmiyorsa, iki konumdan birinin kullanılması gerekir.
* Bir yönetilen hesapla kaydetme konumuna erişiliyorsa, `IntuneMAMSaveLocationAccountDocument` konumun kullanılması gerekir ( `IntuneMAMOpenLocationAccountDocument` açma için).
* Aksi takdirde, `IntuneMAMSaveLocationOther` konumunu ( `IntuneMAMOpenLocationOther` açma için) kullanın.

Yönetilen hesap ile yönetilen hesabın UPN 'sini paylaşan bir hesap arasında ayrım yapmak önemlidir. Örneğin, "" UPN 'si ile yönetilen bir hesap, user@contoso.com OneDrive 'da oturum açmış "" UPN 'sine sahip bir hesapla aynı değildir user@contoso.com . Yönetilen hesapta oturum açarak bilinmeyen veya listelenmemiş bir hizmete erişiliyorsa (ör. " user@contoso.com " OneDrive 'da oturum açıldı), konum tarafından temsil edilmelidir `AccountDocument` . Bilinmeyen veya listelenmemiş hizmet başka bir hesapta oturum açarsa (ör. " user@contoso.com " Dropbox 'ta oturum açıldı), yönetilen bir hesapla konuma erişmez ve konum tarafından temsil edilmelidir `Other` .

### <a name="sharing-blocked-alert"></a>Paylaşım engellendi uyarısı

UI Yardımcısı işlevi, `isSaveToAllowedForLocation` veya `isOpenFromAllowedForLocation` API çağrıldığında ve Kaydet/Aç eylemini engelleyecek şekilde bulunursa kullanılabilir. Uygulama, kullanıcıya eylemin engellendiğini bildirmek isterse, `showSharingBlockedMessage` `IntuneMAMUIHelper.h` genel bir iletiyle bir uyarı görünümü sunmak için içinde tanımlanan API 'yi çağırabilir.

## <a name="share-data-via-uiactivityviewcontroller"></a>UIActivityViewController yoluyla Veri Paylaşımı

Sürüm 8.0.2'den başlayarak, yalnızca Intune tarafından yönetilen paylaşım konumları arasından seçim yapılmasını sağlamak üzere Intune Uygulama SDK'sı `UIActivityViewController` eylemlerini filtreleyebilir. Bu davranış, uygulama veri aktarımı ilkesi tarafından denetlenecektir.

### <a name="copy-to-actions"></a>' Kopyalama ' eylemleri

Ve aracılığıyla belge paylaşırken `UIActivityViewController` `UIDocumentInteractionController` , iOS, paylaşılan belgeyi açmayı destekleyen her uygulama Için ' Kopyala ' eylemlerini görüntüler. Uygulamalar, Info.plist dosyalarındaki `CFBundleDocumentTypes` ayarı yoluyla destekledikleri belge türlerini bildirir. İlke yönetilmeyen uygulamalara paylaşımı yasaklarsa, bu paylaşım türü artık kullanılabilir olmaz. Bunun yerine kullanıcı, kullanıcı arabirimi olmayan Eylem uzantısını ekleyip bunu Intune Uygulama SDK’sına bağlamak zorunda kalır. Eylem uzantısı, yalnızca bir saplamadır. SDK, dosya paylaşım davranışını uygular. Aşağıdaki adımları izleyin:

1. Uygulamanız, kendi Info. plist altında, onun karşılığına göre tanımlanmış en az bir ıgnmeurl içermelidir `CFBundleURLTypes` `-intunemam` . Örneğin:
    ```objc
    <key>CFBundleURLSchemes</key>
    <array>
        <string>launch-com.contoso.myapp</string>
        <string>launch-com.contoso.myapp-intunemam</string>
    </array>
    ```

2. Uygulamanızın ve eylem uzantınızın her ikisi de en az bir uygulama grubunu paylaşmalıdır ve uygulama grubu, `AppGroupIdentifiers` uygulamanın ve uzantısının ıntunemamsettings sözlüklerinin altındaki dizi altında listelenmelidir.

3. Hem uygulama hem de eylem uzantınız, Anahtarlık paylaşım özelliğine sahip olmalı ve `com.microsoft.intune.mam` Anahtarlık grubunu paylaşmalıdır.

4. "Aç" eylem uzantısını ve ardından uygulama adını adlandırın. Info.plist dosyasını ihtiyaca göre yerelleştirin.

5. [Apple 'ın geliştirici belgelerinde](https://developer.apple.com/ios/human-interface-guidelines/extensions/sharing-and-actions/)açıklandığı şekilde uzantı için bir şablon simgesi sağlayın. Alternatif olarak, bu görüntüleri uygulamanın .app dizininden oluşturmak için IntuneMAMConfigurator aracı kullanılabilir. Bunu yapmak için şunu çalıştırın:

    ```bash
    IntuneMAMConfigurator -generateOpenInIcons /path/to/app.app -o /path/to/output/directory
    ```

6. Uzantının Info. plist dosyasındaki ıntunemamsettings altında YES değeri ile adlı bir Boole ayarı ekleyin `OpenInActionExtension` .

7. Öğesini `NSExtensionActivationRule` tek bir dosyayı ve uygulamanın önekli tüm türleri destekleyecek şekilde yapılandırın `CFBundleDocumentTypes` `com.microsoft.intune.mam` . Örneğin uygulama public.text ve public.image destekliyorsa, etkinleştirme kuralı şu şekilde olur:

    ```objc
    SUBQUERY (
        extensionItems,
        $extensionItem,
        SUBQUERY (
            $extensionItem.attachments,
            $attachment,
            ANY $attachment.registeredTypeIdentifiers UTI-CONFORMS-TO "com.microsoft.intune.mam.public.text" ||
            ANY $attachment.registeredTypeIdentifiers UTI-CONFORMS-TO "com.microsoft.intune.mam.public.image").@count == 1
    ).@count == 1
    ```

### <a name="update-existing-share-and-action-extensions"></a>Mevcut Paylaşım ve Eylem uzantılarını güncelleştirme

Uygulamanız zaten Paylaşım ve Eylem uzantılarını barındırıyorsa bunların `NSExtensionActivationRule` ayarları, Intune türlerine izin verecek şekilde değiştirilmelidir. Uzantının desteklediği her tür için `com.microsoft.intune.mam` ön ekli bir tür daha ekleyin. Örneğin mevcut etkinleştirme kuralı şu ise:  

```objc
SUBQUERY (
    extensionItems,
    $extensionItem,
    SUBQUERY (
        $extensionItem.attachments,
        $attachment,
        ANY $attachment.registeredTypeIdentifiers UTI-CONFORMS-TO "public.url" ||
        ANY $attachment.registeredTypeIdentifiers UTI-CONFORMS-TO "public.plain-text" ||
        ANY $attachment.registeredTypeIdentifiers UTI-CONFORMS-TO "public.image" ||
        ANY $attachment.registeredTypeIdentifiers UTI-CONFORMS-TO "public.data"
    ).@count > 0
).@count > 0
```

Şu şekilde değiştirilmelidir:

```objc
SUBQUERY (
    extensionItems,
    $extensionItem,
    SUBQUERY (
        $extensionItem.attachments,
        $attachment,
        ANY $attachment.registeredTypeIdentifiers UTI-CONFORMS-TO "public.url" ||
        ANY $attachment.registeredTypeIdentifiers UTI-CONFORMS-TO "public.plain-text" ||
        ANY $attachment.registeredTypeIdentifiers UTI-CONFORMS-TO "public.image" ||
        ANY $attachment.registeredTypeIdentifiers UTI-CONFORMS-TO "public.data" ||
        ANY $attachment.registeredTypeIdentifiers UTI-CONFORMS-TO "com.microsoft.intune.mam.public.url" ||
        ANY $attachment.registeredTypeIdentifiers UTI-CONFORMS-TO "com.microsoft.intune.mam.public.plain-text" ||
        ANY $attachment.registeredTypeIdentifiers UTI-CONFORMS-TO "com.microsoft.intune.mam.public.image" ||
        ANY $attachment.registeredTypeIdentifiers UTI-CONFORMS-TO "com.microsoft.intune.mam.public.data"
    ).@count > 0
).@count > 0
```

> [!NOTE]
> Intune türlerini etkinleştirme kuralına eklemek için IntuneMAMConfigurator aracı kullanılabilir. Mevcut etkinleştirme kuralınız önceden tanımlı dize sabitleri (ör. NSExtensionActivationSupportsFileWithMaxCount, NSExtensionActivationSupportsText vb.) kullanıyorsa, koşul sözdizimi hayli karmaşıklaşabilir. IntuneMAMConfigurator aracı ayrıca, Intune türlerini eklerken etkinleştirme kuralını dize sabitlerinden koşul dizesine dönüştürmek için kullanılabilir.

### <a name="what-the-ui-should-look-like"></a>UI nasıl görünmeli?

Eski UI:

![Verileri paylaşma-iOS eski paylaşım Kullanıcı arabirimi](./media/app-sdk-ios/sharing-UI-old.png)

Yeni UI:

![Verileri paylaşma-iOS yeni paylaşım Kullanıcı arabirimi](./media/app-sdk-ios/sharing-UI-new.png)

## <a name="enable-targeted-configuration-appmam-app-config-for-your-ios-applications"></a>iOS uygulamalarınız için hedeflenen yapılandırmayı (APP/MAM uygulama yapılandırması) etkinleştirme

MAM'ı hedefleyen yapılandırma (MAM uygulama yapılandırması olarak da bilinir), bir uygulamanın Intune SDK'sı aracılığıyla yapılandırma verileri almasını sağlar. Bu verilerin biçimi ve çeşitleri, uygulamanın sahibi/geliştiricisi tarafından tanımlanmalı ve Intune müşterilerine bildirilmelidir.

Intune yöneticileri, yapılandırma verilerini Intune Azure portalı ve Intune Graph API aracılığıyla hedefleyip dağıtabilir. iOS için Intune Uygulama SDK’sının 7.0.1 sürümü itibarıyla, MAM’ı hedefleyen yapılandırmaya dahil olan uygulamalar, MAM Hizmeti aracılığıyla MAM’ı hedefleyen yapılandırma verileri sağlayabilmektedir. Uygulama yapılandırma verileri MDM kanalı yerine uygulamaya doğrudan MAM Hizmetimiz aracılığıyla iletilir. Intune Uygulama SDK'sı, bu konsollardan alınan verilere erişmesine erişmek için bir sınıf sağlar. Aşağıdaki öğeler önkoşullardır:

* MAM’ı hedefleyen yapılandırma kullanıcı arabirimine erişebilmeniz için uygulamanın Intune MAM hizmetine kaydedilmiş olması gerekir. Daha fazla bilgi için bkz. [Uygulama koruma ilkesi alma](#receive-app-protection-policy).

* Uygulamanızın kaynak dosyasına `IntuneMAMAppConfigManager.h` öğesini dahil edin.

* Uygulama Yapılandırma Nesnesini almak için `[[IntuneMAMAppConfigManager instance] appConfigForIdentity:]` öğesini çağırın.

* `IntuneMAMAppConfig` nesnesinde uygun seçiciyi çağırın. Örneğin, uygulamanızın anahtarı bir dizeyse `stringValueForKey` veya `allStringsForKey` kullanmanız uygun olur. Dönüş değerleri ve hata koşullarıyla ilgili ayrıntılı bir açıklama için bkz. `IntuneMAMAppConfig.h`.

Graph API’nin işlevleri hakkında daha fazla bilgi için bkz. [Graph API Başvurusu](https://developer.microsoft.com/graph/docs/concepts/overview).

İOS 'ta MAM hedefli uygulama yapılandırma ilkesi oluşturma hakkında daha fazla bilgi için [iOS/ıpados Microsoft Intune uygulama yapılandırma ilkeleri kullanma](../apps/app-configuration-policies-use-ios.md)konusunun mam hedefli uygulama yapılandırması bölümüne bakın.

## <a name="telemetry"></a>Telemetri

Varsayılan olarak iOS için Intune Uygulama SDK'sı, aşağıdaki tür olaylara ilişkin telemetrileri toplar:

* **Uygulama başlatma**: Microsoft Intune’un yönetim türüne göre MAM özellikli uygulama kullanımı hakkında bilgi almasına yardımcı olmak amaçlıdır (MDM ile MAM, MDM kaydı olmadan MAM vb.).

* **Kayıt çağrıları**: Microsoft Intune’un, başarı oranı hakkında ve istemci tarafından yapılan kayıt çağrılarının çeşitli diğer performans ölçümleriyle ilgili bilgi edinmesine yardımcı olmak amaçlıdır.

* **Intune eylemleri**: Sorunları tanılamaya ve Intune'un işlevselliğini güvence altına almaya yardımcı olması için, Intune SDK eylemleri hakkında bilgi toplarız.

> [!NOTE]
> Intune Uygulama SDK’sı telemetri verilerini mobil uygulamanızdan Microsoft Intune’a göndermemeyi seçerseniz, Intune Uygulama SDK’sının telemetre yakalama özelliğini devre dışı bırakmanız gerekir. IntuneMAMSettings sözlüğünde `MAMTelemetryDisabled` özelliğini EVET olarak ayarlayın.

## <a name="enable-multi-identity-optional"></a>Çoklu kimliği etkinleştirme (isteğe bağlı)

SDK varsayılan olarak, ilkeyi uygulamaya bir bütün olarak uygular. Çoklu kimlik, bir ilkeyi her bir kimlik düzeyinde uygulamak için etkinleştirebileceğiniz bir MAM özelliğidir. Bu, diğer MAM özelliklerine kıyasla daha fazla uygulama katılımı gerektirir.

Uygulama etkin kimliği değiştirmeyi amaçladığında, bunu uygulama SDK’sına bildirmesi gerekir. Ayrıca bir kimlik değişikliği gerektiğinde SDK bunu uygulamaya bildirir. Şu anda yalnızca tek bir yönetilen kimlik desteklenir. Kullanıcı cihaz veya uygulamayı kaydettikten sonra, SDK bu kimliği kullanır ve bunu birincil yönetilen kimlik olarak kabul eder. Uygulamadaki diğer kullanıcılar kısıtlanmamış ilke ayarlarıyla yönetilmeyen olarak kabul edilirler.

Bir kimliğin yalnızca dize olarak tanımlandığını aklınızda bulundurun. Kimlikler büyük/küçük harfe duyarlıdır. SDK’ya kimlik için yapılan istekler, kimlik ayarlandığı sırada kullanılan özgün büyük/küçük harf dizimiyle aynı olmadığı sürece sonuç getirmeyebilir.

### <a name="identity-overview"></a>Kimliğe genel bakış

Kimlik, bir hesabın kullanıcı adıdır (örneğin, user@contoso.com). Geliştiriciler uygulamanın kimliğini aşağıdaki düzeylerde ayarlayabilir:

* **İşlem kimliği**: İşlem genelindeki kimliği ayarlar ve genellikle tek kimlikli uygulamalar için kullanılır. Bu kimlik tüm görevleri, dosyaları ve UI’yi etkiler.

* **UI Kimliği**: Ana iş parçacığında UI görevlerine kes/kopyala/yapıştır, PIN, kimlik doğrulaması ve veri paylaşımı gibi ilkelerden hangilerinin uygulanacağını belirler. UI kimliği, şifreleme ve yedekleme gibi dosya görevlerini etkilemez.

* **İş parçacığı kimliği**: Geçerli iş parçacığında hangi ilkelerin uygulanacağını etkiler. Bu kimlik tüm görevleri, dosyaları ve UI’yi etkiler.

Kullanıcı yönetilse de yönetilmese de kimlikleri uygun olarak ayarlamak uygulamanın sorumluluğudur.

Herhangi bir zamanda, her iş parçacığı UI görevleri ve dosya görevleri için etkili bir kimliğe sahiptir. Bu, varsa hangi ilkelerin uygulanması gerektiğini denetlemek için kullanılan kimliktir. Kimlik, “kimliksiz” ise veya kullanıcı yönetilmiyorsa hiçbir ilke uygulanmaz. Aşağıdaki diyagramlar etkin kimliklerin nasıl belirlendiğini gösterir.

  ![Intune uygulama SDK 'Sı iOS: kimlik belirleme işlemi](./media/app-sdk-ios/ios-thread-identities.png)

### <a name="thread-queues"></a>İş parçacığı kuyrukları

Uygulamalar, iş parçacığı kuyruklarına sıklıkla zaman uyumsuz ve zaman uyumlu görevler gönderir. SDK, Genel Gönderme Merkezi (GCD) çağrılarını yakalar ve geçerli iş parçacığı kimliğini gönderilen görev ile ilişkilendirir. Görevler bittiğinde, SDK iş parçacığı kimliğini geçici olarak görev ile ilişkili kimlik olarak değiştirir, görevleri bitirir ve sonra özgün iş parçacığı kimliğini geri yükler.


`NSOperationQueue` GCD üzerinde oluşturulduğu için `NSOperations`, iş parçacığı kimliğinde görevler, `NSOperationQueue` öğesine eklendiği zaman çalışır. `NSOperations` veya doğrudan GCD üzerinde gönderilen işlevler ayrıca, geçerli iş parçacığı kimliğini çalıştıkları sırada değiştirebilirler. Bu kimlik, gönderen iş parçacığından devralınan kimliği geçersiz kılar.

### <a name="file-owner"></a>Dosya sahibi

SDK, yerel dosya sahiplerinin kimliklerini izler ve ilkeleri buna göre uygular. Dosya sahibi, bir dosya oluşturulduğunda veya bir dosya kesme modunda açıldığında belirlenir. Sahip, görevi gerçekleştiren iş parçacığının etkin dosya görevi kimliğine ayarlanır.

Alternatif olarak, uygulamalar `IntuneMAMFilePolicyManager` kullanarak sahip kimliğini açıkça ayarlayabilir. Uygulamalar, dosya sahibini almak ve UI kimliğini dosya içeriğini görüntülemeden önce ayarlamak için `IntuneMAMFilePolicyManager` kullanabilir.

### <a name="shared-data"></a>Paylaşılan veriler

Uygulama hem yönetilen hem de yönetilmeyen kullanıcıların verilerini içeren dosyalar oluşturursa, yönetilen kullanıcının verilerini şifrelemeden uygulama sorumludur. `IntuneMAMDataProtectionManager` içindeki `protect` ve `unprotect` API'lerini kullanarak veri şifreleyebilirsiniz.

`protect` yöntemi, bir kimliği yönetilen veya yönetilmeyen kullanıcı olarak kabul eder. Kullanıcı yönetiliyorsa, veriler şifrelenir. Kullanıcı yönetilmiyorsa, kimliği kodlayan verilere bir üst bilgi eklenir ancak veriler şifrelenmez. `protectionInfo`Verilerin sahibini almak için yöntemini kullanabilirsiniz.

### <a name="share-extensions"></a>Paylaşım uzantıları

Uygulama bir paylaşım uzantısı içeriyorsa, paylaşılan öğenin sahibi `IntuneMAMDataProtectionManager` içindeki `protectionInfoForItemProvider` yöntemiyle alınabilir. Paylaşılan öğe bir dosya ise, dosya sahibi ayarı SDK tarafından yapılır. Paylaşılan öğenin veri olması durumunda; bu veri bir dosyaya sabitlenmişse dosya sahibini ayarlamak ve bu veriyi UI’da göstermeden önce `setUIPolicyIdentity` API’sini çağırmak uygulamanın görevidir.

### <a name="turn-on-multi-identity"></a>Çoklu kimliği açma

Varsayılan olarak, uygulamalar tek kimlikli olarak değerlendirilir. SDK, kayıtlı kullanıcı için işlem kimliğini ayarlar. Çoklu kimlik desteğini etkinleştirmek için uygulamanın Info.plist dosyası içindeki IntuneMAMSettings sözlüğüne EVET değeri ve `MultiIdentity` adıyla bir Boole ayarı ekleyin.

> [!NOTE]
> Çoklu kimlik etkinleştirildiğinde işlem kimliği, UI kimliği ve iş parçacığı kimlikleri nil olarak ayarlanır. Uygulama, bunları uygun şekilde ayarlamaktan sorumludur.

### <a name="switch-identities"></a>Kimlikleri değiştirme

* **Uygulama tarafından başlatılan kimlik değişimi**:

    Başlatma sırasında, çoklu kimlik uygulamaları bilinmeyen, yönetilmeyen bir hesap altında çalışıyor gibi kabul edilir. Koşullu başlatma UI’si çalışmaz ve uygulamada hiçbir ilke uygulanmaz. Kimliğin değiştirilmesi gerektiğinde bunu SDK’ya bildirmek uygulamanın sorumluluğudur. Genellikle, bu durum uygulamanın belirli bir kullanıcı hesabına ait verileri göstermek üzere olduğu sırada gerçekleşir.

    Kullanıcının bir dizüstü bilgisayarda bir belge, posta kutusu veya sekme açmayı denemesi örnek olarak gösterilebilir. Dosya, posta kutusu veya sekme gerçekten açılmadan uygulamanın SDK’ya bildirimde bulunması gerekir. Bu `IntuneMAMPolicyManager` içindeki `setUIPolicyIdentity` API’si üzerinden yapılır. Bu API, kullanıcı yönetilse de yönetilmese de çağrılmalıdır. Kullanıcı yönetiliyorsa, SDK koşullu başlatma denetimleri gerçekleştirir (jailbreak algılama, PIN ve kimlik doğrulama gibi).

    Kimlik değişiminin sonucu, uygulamaya bir tamamlama işleyicisi üzerinden zaman uyumsuz olarak döndürülür. Uygulama; belge, posta kutusu veya sekmeyi açmayı başarılı sonuç kodu döndürülünceye kadar ertelemelidir. Kimlik değişimi başarısız olursa, uygulamanın görevi iptal etmesi gerekir.

* **SDK tarafından başlatılan kimlik değişimi**:

    SDK’nın uygulamadan belirli bir kimliğe değiştirilmesini istemesini gerektiren durumlar vardır. Çoklu kimlik uygulamalarının bu isteği işlemek için `IntuneMAMPolicyDelegate` içindeki `identitySwitchRequired` yöntemini uygulaması gerekir.

    Bu yöntem çağrıldığı zaman, uygulama belirli kimliğe değiştirilme isteğini yerine getirebiliyorsa, `IntuneMAMAddIdentityResultSuccess` öğesini tamamlama işleyicisine geçirmesi gerekir. Kimliği değiştirme işlemini yerine getiremiyorsa, uygulamanın `IntuneMAMAddIdentityResultFailed` öğesini tamamlama işleyicisine geçirmesi gerekir.

    Bu çağrıya yanıt olarak uygulamanın `setUIPolicyIdentity` öğesini çağırması gerekmez. SDK, uygulamanın yönetilmeyen bir kullanıcı hesabıyla değiştirilmesini gerektirirse, boş dize `identitySwitchRequired` çağrısına geçirilir.

* **Seçmeli Temizleme**:

    Uygulama seçmeli temizleme işlemiyle temizlendiğinde, SDK `IntuneMAMPolicyDelegate` içindeki `wipeDataForAccount` yöntemini çağırır. Uygulama, belirtilen kullanıcı hesabını ve onunla ilişkili tüm verileri kaldırmaktan sorumludur. SDK, kullanıcının sahip olduğu tüm dosyaları kaldırma özelliğine sahiptir ve uygulamanın `wipeDataForAccount` çağrısından FALSE sonucu getirmesi durumunda bunu uygular.

    Bu yöntemin bir arka plan iş parçacığından çağrıldığını unutmayın. Kullanıcıya yönelik tüm veriler kaldırılana kadar uygulama bir değer döndürmemelidir (uygulama FALSE döndürürse dosyalar hariç olmak üzere).

## <a name="siri-intents"></a>Siri amaçları
Uygulamanız Siri hedefleri ile tümleşiyorsa, `areSiriIntentsAllowed` `IntuneMAMPolicy.h` Bu senaryoyu destekleme yönergeleri için lütfen içindeki açıklamalarını okuduğunuzdan emin olun. 
    
## <a name="notifications"></a>Bildirimler
Uygulamanız bildirimler alırsa, `notificationPolicy` `IntuneMAMPolicy.h` Bu senaryoyu destekleme yönergeleri için lütfen içindeki açıklamalarını okuduğunuzdan emin olun.  Uygulamaların `IntuneMAMPolicyDidChangeNotification` ' de `IntuneMAMPolicyManager.h` açıklanabileceği ve bu değeri Anahtarlık aracılığıyla bu değerle iletişim kurması önerilir `UNNotificationServiceExtension` .
## <a name="displaying-web-content-within-application"></a>Uygulama Içinde Web Içeriğini görüntüleme
Uygulamanızın Web sitesinde Web sitelerini görüntüleyebilme özelliği varsa ve görüntülenen Web sayfaları rasgele sitelere gidebilme özelliğine sahipse, uygulama, yönetilen verilerin Web görünümü aracılığıyla sızmaması için geçerli kimliği ayarlamaktan sorumludur. Bunun örnekleri, bir arama motoruna doğrudan veya dolaylı bağlantıları olan ' bir özellik önerme ' veya ' geri bildirim ' Web sayfalarıdır.
Çoklu kimlik uygulamaları, web görünümünü görüntülemeden önce boş dizeyi geçirerek ıntunemampolicymanager Setuipolicyıdentity öğesini çağırmalıdır. Web görünümü kapatıldıktan sonra, uygulama geçerli kimliğe geçirerek Setuipolicyıdentity öğesini çağırmalıdır.
Tek kimlik uygulamaları, web görünümünü görüntülemeden önce boş dizeyi geçirerek ıntunemampolicymanager Setcurrentthreadıdentity çağrısını çağırmalıdır. Web görünümü kapatıldıktan sonra, uygulamanın Nil olarak Setcurrentthreadıdentity çağrısı gerekir.

## <a name="ios-best-practices"></a>iOS en iyi uygulamalar

iOS için geliştirmeye yönelik önerilen en iyi uygulamalar aşağıda verilmiştir:

* iOS dosya sistemi büyük/küçük harfe duyarlıdır. Büyük/küçük harf kullanımının `libIntuneMAM.a` ve `IntuneMAMResources.bundle` gibi adlar için doğru olduğundan emin olun.

* Xcode `libIntuneMAM.a` dosyasını bulamıyorsa, bu kitaplığın yolunu bağlayıcı arama yollarına ekleyerek sorunu düzeltebilirsiniz.

## <a name="faqs"></a>SSS

### <a name="are-all-of-the-apis-addressable-through-native-swift-or-the-objective-c-and-swift-interoperability"></a>Tüm API’ler yerel Swift veya Objective-C ile Swift birlikte çalışabilirliği aracılığıyla adreslenebilir mi?

Intune Uygulama SDK’sı API’leri yalnızca Objective-C içinde bulunur ve **yerel** Swift’i desteklemez. Objective-C ile Swift arasında birlikte çalışabilirlik gereklidir.

### <a name="do-all-users-of-my-application-need-to-be-registered-with-the-app-we-service"></a>Uygulamamın tüm kullanıcılarının APP-WE hizmetine kayıtlı olması gerekiyor mu?

Hayır. Aslında, yalnızca iş veya okul hesaplarının Intune uygulama SDK'sına kayıtlı olması gerekir. Bir hesabın iş veya okul bağlamında kullanıldığını belirlemek uygulamaların sorumluluğudur.

### <a name="what-about-users-that-have-already-signed-in-to-the-application-do-they-need-to-be-enrolled"></a>Uygulamada zaten oturum açmış kullanıcılar ne olacak? Kayıtlı olmaları gerekli mi?

Kullanıcıların kimliği başarıyla doğrulandıktan sonra kullanıcıları kaydetmek uygulamanın görevidir. Uygulama MDM bulunmayan MAM işlevselliğine sahip olmadan önce var olan hesapları kaydetmek de uygulamanın görevidir.

Bunu yapmak için uygulamanın `registeredAccounts:` yöntemini kullanması gerekir. Bu yöntem, Intune MAM hizmetine kayıtlı tüm hesapları içeren bir NSDictionary döndürür. Uygulamadaki herhangi bir mevcut hesap listede yoksa, uygulama bu hesapları `registerAndEnrollAccount:` aracılığıyla kaydetmelidir.

### <a name="how-often-does-the-sdk-retry-enrollments"></a>SDK, kayıtları ne sıklıkta yeniden dener?

SDK daha önce başarısız olan tüm kayıtları otomatik olarak 24 saatte bir yeniden dener. SDK bunu bir kullanıcının kuruluşunun, Kullanıcı uygulamada oturum açtıktan sonra MAM etkinleştirdiğinden emin olmak için, Kullanıcı başarıyla kayıt ve ilke alır.

SDK, bir kullanıcının uygulamayı başarıyla kaydettiğini algıladığında yeniden denemeyi durdurur. Bunun nedeni, bir uygulamayı belirli bir zamanda yalnızca bir kullanıcının kaydedebilmesidir. Kullanıcının kaydı silinirse, yeniden denemeler aynı 24 saatlik zaman aralığında yeniden başlar.

### <a name="why-does-the-user-need-to-be-deregistered"></a>Kullanıcının kaydının neden kaldırılması gerekir?

SDK şu eylemleri arka planda düzenli aralıklarla gerçekleştirir:

* Uygulama henüz kaydedilmemişse, tüm kayıtlı hesapları 24 saatte bir kaydetmeyi dener.
* Uygulama kaydedildiyse, SDK her 8 saatte bir MAM ilkesi güncelleştirmelerini denetler.

Bir kullanıcının kaydını kaldırmak SDK’ya kullanıcının uygulamayı artık kullanmayacağını bildirir ve söz konusu kullanıcı hesabına ait periyodik olayların tümünü durdurabilir. Ayrıca bir uygulama kaydı silme işlemi ve gerekirse seçmeli silme işlemi tetikler.

### <a name="should-i-set-the-dowipe-flag-to-true-in-the-deregister-method"></a>Kaydı kaldırma yönteminde doWipe bayrağını true olarak ayarlamalı mıyım?

Bu yöntem, kullanıcının uygulamadaki oturumunu kapatmasından önce çağrılmalıdır.  Kullanıcının verileri, oturum kapatma kapsamında uygulamadan silinirse, `doWipe` false olarak ayarlanabilir. Ancak uygulama kullanıcının verilerini kaldırmadığında, `doWipe` SDK 'nın verileri silebilmesi için true olarak ayarlanmalıdır.

### <a name="are-there-any-other-ways-that-an-application-can-be-un-enrolled"></a>Bir uygulama kaydının kaldırılmasının başka yolları var mı?

Evet, BT yöneticisi uygulamaya bir seçmeli silme komutu gönderebilir. Bu, kullanıcının kaydını silme ve kaydı geri alacak ve kullanıcının verilerini temizleyemez. SDK bu senaryoyu otomatik olarak işler ve kayıt silme temsilci yöntemiyle bir bildirim gönderir.

### <a name="is-there-a-sample-app-that-demonstrates-how-to-integrate-the-sdk"></a>SDK'nın nasıl tümleştirileceğini gösteren örnek bir uygulama var mı?

Evet! Açık kaynak örnek uygulamamız [Wagr for iOS](https://github.com/Microsoft/Wagr-Sample-Intune-iOS-App)'yi kısa süre önce yeniledik. Wagr artık Intune Uygulama SDK'sının kullanıldığı uygulama koruma ilkesi için etkinleştirildi.

### <a name="how-can-i-troubleshoot-my-app"></a>Uygulamamda nasıl sorun giderebilirim?

İOS için Intune SDK 9.0.3 +, ilkeleri ve günlüğe kaydetme hatalarını test etmek üzere mobil uygulama içinde bir Tanılama Konsolu ekleyebilme özelliğini destekler. `IntuneMAMDiagnosticConsole.h``IntuneMAMDiagnosticConsole`geliştiricilerin Intune tanılama konsolunu göstermek için kullanabileceği sınıf arabirimini tanımlar. Bu, test sırasında son kullanıcıların veya geliştiricilerin, sahip oldukları herhangi bir sorunu tanılamaya yardımcı olmak için Intune günlüklerini toplamasını ve paylaşmasını sağlar. Bu API, tümleştiricileri için isteğe bağlıdır.

## <a name="submit-your-app-to-the-app-store"></a>Uygulamanızı App Store’a gönderme

Intune Uygulama SDK’sının hem statik kitaplığı hem de çerçeve derlemesi evrensel ikili dosyalardır. Yani tüm cihaz ve benzetici mimarilerine yönelik kodları içerirler. Apple, App Store’a gönderilen uygulamaları benzetici kodu içermeleri durumunda reddeder. Yalnızca cihaz derlemeleri için statik kitaplığa karşı derleme yapıldığında, bağlayıcı, benzetici kodunu otomatik olarak çıkartır. Uygulamanızı App Store’a yüklemeden önce tüm benzetici kodunun kaldırıldığından emin olmak için aşağıdaki adımları uygulayın.

1. `IntuneMAM.framework` öğesinin masaüstünüzde olduğundan emin olun.

2. Şu komutları çalıştırın:

    ```bash
    lipo ~/Desktop/IntuneMAM.framework/IntuneMAM -remove i386 -remove x86_64 -output ~/Desktop/IntuneMAM.device_only
    ```

    ```bash
    cp ~/Desktop/IntuneMAM.device_only ~/Desktop/IntuneMAM.framework/IntuneMAM
    ```

    İlk komut, benzetici mimarilerini çerçevenin DYLIB dosyasından kaldırır. İkinci komut, yalnızca cihaz DYLIB dosyasını çerçeve klasörüne kopyalar.
