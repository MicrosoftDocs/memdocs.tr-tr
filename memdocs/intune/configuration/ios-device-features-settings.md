---
title: iOS/ıpados cihaz özelliği ayarları Microsoft Intune-Azure | Microsoft Docs
description: İOS ve ıpados cihazlarını AirPrint için yapılandırma, giriş ekranı düzeni, uygulama bildirimleri, paylaşılan cihaz, çoklu oturum açma ve Microsoft Intune içindeki Web içeriği filtresi ayarları için tüm ayarları görüntüleyin. Bu ayarları, kuruluşunuzda bu Apple özelliklerini kullanmak üzere iOS/ıpados cihazlarını yapılandırmak için bir cihaz yapılandırma profilinde kullanın.
keywords: ''
author: MandiOhlinger
ms.author: mandia
manager: dougeby
ms.date: 03/09/2020
ms.topic: reference
ms.service: microsoft-intune
ms.subservice: configuration
ms.localizationpriority: medium
ms.technology: ''
ms.reviewer: ''
ms.suite: ems
search.appverid: ''
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: 351c6ade59d98ce620b939c5ff6238e650390a5f
ms.sourcegitcommit: 3d895be2844bda2177c2c85dc2f09612a1be5490
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/13/2020
ms.locfileid: "79332094"
---
# <a name="ios-and-ipados-device-settings-to-use-common-iosipados-features-in-intune"></a>Intune 'da ortak iOS/ıpados özelliklerini kullanmak için iOS ve ıpados cihaz ayarları

Intune, iOS/ıpados kullanıcılarının cihazlarında farklı Apple özellikleri kullanmasına izin veren bazı yerleşik ayarlar içerir. Örneğin, Yöneticiler iOS/ıpados kullanıcılarının AirPrint yazıcılarını nasıl kullandığını denetleyebilir, giriş ekranındaki yerleştirme ve sayfalara uygulama ve klasör ekleme, uygulama bildirimlerini gösterme, kilit ekranında varlık etiketi ayrıntılarını gösterme, çoklu oturum açma kimlik doğrulaması kullanma ve sertifikalarla kullanıcıların kimliğini doğrulama işlemlerinin nasıl yapılacağını denetleyebilir.

Bu özellikleri, mobil cihaz yönetimi (MDM) çözümünüzün bir parçası olarak iOS/ıpados cihazlarını denetlemek için kullanın.

Bu makale, bu ayarları listeler ve her ayarın ne yaptığını açıklar. Bu özellikler hakkında daha fazla bilgi için [iOS/ıpados veya macOS cihaz özelliği ayarları ekle](device-features-configure.md)' ye gidin.

## <a name="before-you-begin"></a>Başlamadan önce

[İOS/ıpados cihaz yapılandırma profili oluşturun](device-features-configure.md).

> [!NOTE]
> Bu ayarlar, bazı ayarların tüm kayıt seçeneklerine uygulanmasıyla farklı kayıt türleri için geçerlidir. Farklı kayıt türleri hakkında daha fazla bilgi için bkz. [iOS/ıpados kaydı](../enrollment/ios-enroll.md).

## <a name="airprint"></a>AirPrint

### <a name="settings-apply-to-all-enrollment-types"></a>Ayarlar için geçerlidir: tüm kayıt türleri

> [!NOTE]
> Tüm yazıcıları aynı profile eklediğinizden emin olun. Apple, birden çok AirPrint profilinin aynı cihazı hedeflemesini önler.

- **IP adresi**: yazıcının IPv4 veya IPv6 adresini girin. Yazıcıları tanımlamak için ana bilgisayar adları kullanırsanız, terminaldeki yazıcıya ping ekleyerek IP adresini alabilirsiniz. IP adresini ve yolu al (Bu makalede) daha fazla ayrıntı sağlar.
- **Yol**: yol, genellikle ağınızdaki yazıcılar için `ipp/print`. IP adresini ve yolu al (Bu makalede) daha fazla ayrıntı sağlar.
- **Bağlantı noktası**: AirPrint hedefinin dinleme bağlantı noktasını girin. Bu özelliği boş bırakırsanız AirPrint varsayılan bağlantı noktasını kullanır. İOS 11.0 + ve ıpados 13.0 + ' da kullanılabilir.
- **TLS**: Aktarım katmanı GÜVENLIĞI (TLS) Ile AirPrint bağlantılarını güvenli hale getirmek için **Etkinleştir** ' i seçin. İOS 11.0 + ve ıpados 13.0 + ' da kullanılabilir.

AirPrint sunucuları eklemek için şunları yapabilirsiniz:

- **Ekle** , AirPrint sunucusunu listeye ekler. Birçok AirPrint sunucusu eklenebilir.
- Bu bilgilerle, virgülle ayrılmış bir dosyayı (. csv) **Içeri aktarın** . Ya da, eklediğiniz AirPrint sunucularının bir listesini oluşturmak için **dışa aktarın** .

### <a name="get-server-ip-address-resource-path-and-port"></a>Sunucu IP adresi, kaynak yolu ve bağlantı noktası al

AirPrinter sunucuları eklemek için, yazıcının IP adresi, kaynak yolu ve bağlantı noktası gerekir. Aşağıdaki adımlarda bu bilgilerin nasıl alınacağı gösterilmektedir.

1. AirPrint yazıcıları ile aynı yerel ağa (alt ağ) bağlı bir Mac üzerinde, açık **Terminal** ( **/Applications/Utilities**).
2. Terminalde `ippfind`yazın ve ENTER ' u seçin.

    Yazıcı bilgilerini aklınızda edin. Örneğin, `ipp://myprinter.local.:631/ipp/port1`benzer bir işlem döndürebilir. İlk bölüm, yazıcının adıdır. Son Bölüm (`ipp/port1`) kaynak yoludur.

3. Terminalde `ping myprinter.local`yazın ve ENTER ' u seçin.

   IP adresini aklınızda edin. Örneğin, `PING myprinter.local (10.50.25.21)`benzer bir işlem döndürebilir.

4. IP adresi ve kaynak yolu değerlerini kullanın. Bu örnekte, IP adresi `10.50.25.21`ve kaynak yolu `/ipp/port1`.

## <a name="home-screen-layout"></a>Giriş ekranı düzeni

Bu özellik şu platformlarda geçerlidir:

- iOS 9,3 veya üzeri
- ıpados 13,0 ve üzeri

### <a name="settings-apply-to-automated-device-enrollment-supervised"></a>Ayarlar için geçerlidir: otomatik cihaz kaydı (denetimli)

### <a name="dock"></a>Dock

İOS/ıpados ekranının Dock 'a en fazla altı öğe veya klasör eklemek için **yerleştirme** ayarlarını kullanın. Birçok cihaz daha az öğeyi destekler. Örneğin, iPhone cihazları en fazla dört öğeyi destekler. Bu durumda, cihazda yalnızca eklediğiniz ilk dört öğe gösterilir.

Cihaz yuvası için en fazla **altı** öğe (birleştirilmiş uygulamalar ve klasörler) ekleyebilirsiniz.

- **Ekle**: cihazdaki yuvaya uygulama veya klasör ekler.
- **Tür**: bir **uygulama** veya **klasör**ekleyin:

  - **Uygulama**: ekrandaki yerleştirmeyi uygulama eklemek için bu seçeneği belirleyin. Girin:

    - **Uygulama adı**: uygulama için bir ad girin. Bu ad, Microsoft Endpoint Manager Yönetim Merkezi ' nde başvurunuz için kullanılır. İOS/ıpados *cihazında gösterilmez.*
    - **Uygulama PAKETI kimliği**: UYGULAMANıN paket kimliğini girin. Bazı örnekler için bkz. [yerleşik iOS/ıpados uygulamaları Için paket kimlikleri](bundle-ids-built-in-ios-apps.md) .

  - **Klasör**: ekrandaki yerleştirmeyi bir klasör eklemek için bu seçeneği belirleyin.

    Bir klasördeki bir sayfaya eklediğiniz uygulamalar, soldan sağa ve listeyle aynı sırada düzenlenir. Bir sayfaya sığmayacak kadar fazla uygulama eklerseniz, uygulamalar başka bir sayfaya taşınır.

    - **Klasör adı**: klasörün adını girin. Bu ad, cihazlarındaki kullanıcılara gösterilir.
    - **Sayfaların listesi**: sayfa **ekleyin** ve aşağıdaki özellikleri girin:

      - **Sayfa adı**: sayfa için bir ad girin. Bu ad, Microsoft Endpoint Manager Yönetim Merkezi ' nde başvurunuz için kullanılır. İOS/ıpados *cihazında gösterilmez.*
      - **Uygulama adı**: uygulama için bir ad girin. Bu ad, Microsoft Endpoint Manager Yönetim Merkezi ' nde başvurunuz için kullanılır. İOS/ıpados *cihazında gösterilmez.*
      - **Uygulama PAKETI kimliği**: UYGULAMANıN paket kimliğini girin. Bazı örnekler için bkz. [yerleşik iOS/ıpados uygulamaları Için paket kimlikleri](bundle-ids-built-in-ios-apps.md) .

      Cihaz yuvası için en fazla **20** sayfa ekleyebilirsiniz.

> [!NOTE]
> Yerleştirme ayarlarını kullanarak simgeler eklediğinizde, ana ekrandaki ve sayfalardaki simgeler kilitlenir ve taşınamaz. Bu, iOS/ıpados ve Apple 'ın MDM ilkeleriyle tasarım sağlayabilir.

#### <a name="example"></a>Örnek

Aşağıdaki örnekte, Dock ekranında yalnızca Safari, mail ve hisse senetleri uygulamaları gösterilmektedir. Posta uygulaması özelliklerini göstermek için seçilmiştir:

![Örnek iOS/ıpados yerleştirme ayarları](./media/ios-device-features-settings/FfFiUcP.png)

İlkeyi bir iPhone 'a atadığınızda, yuva aşağıdaki resme benzer şekilde görünür:

![İPhone 'daki örnek iOS/ıpados yerleştirme düzeni](./media/ios-device-features-settings/bAgCe8F.png)

### <a name="pages"></a>Pages

Giriş ekranında görünmesini istediğiniz sayfaları ve her sayfada görünmesini istediğiniz uygulamaları ekleyin. Bir sayfaya eklediğiniz uygulamalar, listeyle aynı sırada, soldan sağa düzenlenir. Bir sayfaya sığmayacak kadar fazla uygulama eklerseniz, uygulamalar başka bir sayfaya taşınır.

> [!TIP]
> Herhangi bir giriş ekranında ve sayfa listelerindeki öğeleri yeniden sıralamak için, onları sürükleyip bırakabilirsiniz.

Bir cihaza en fazla **40** sayfa ekleyebilirsiniz.

- **Sayfaların listesi**: sayfa **ekleyin** ve aşağıdaki özellikleri girin:

  - **Sayfa adı**: sayfa için bir ad girin. Bu ad, Microsoft Endpoint Manager Yönetim Merkezi ' nde başvurunuz için *kullanılır ve iOS* /ıpados cihazında gösterilmez.

  Bir cihaza en fazla **60** öğe (birleştirilmiş uygulamalar ve klasör) ekleyebilirsiniz.

  - **Ekle**: cihazdaki bir sayfaya uygulamalar veya klasörler ekler.

    - **Tür**: bir **uygulama** veya **klasör**ekleyin:

      - **Uygulama**: ekrandaki bir sayfaya uygulama eklemek için bu seçeneği belirleyin. Şunları da girin:

        - **Uygulama adı**: uygulama için bir ad girin. Bu ad, Microsoft Endpoint Manager Yönetim Merkezi ' nde başvurunuz için kullanılır. İOS/ıpados *cihazında gösterilmez.*
        - **Uygulama PAKETI kimliği**: UYGULAMANıN paket kimliğini girin. Bazı örnekler için bkz. [yerleşik iOS/ıpados uygulamaları Için paket kimlikleri](bundle-ids-built-in-ios-apps.md) .

      - **Klasör**: ekrandaki yerleştirmeyi bir klasör eklemek için bu seçeneği belirleyin.

        Bir klasördeki bir sayfaya eklediğiniz uygulamalar, soldan sağa ve listeyle aynı sırada düzenlenir. Bir sayfaya sığmayacak kadar fazla uygulama eklerseniz, uygulamalar başka bir sayfaya taşınır.

        - **Klasör adı**: klasör için bir ad girin. Bu ad, cihazdaki kullanıcılara gösterilir.
        - **Ekle**: klasöre sayfa ekler. Aşağıdaki özellikleri de girin:

          - **Sayfa adı**: sayfa için bir ad girin. Bu ad, Microsoft Endpoint Manager Yönetim Merkezi ' nde başvurunuz için kullanılır. İOS/ıpados *cihazında gösterilmez.*
          - **Uygulama adı**: uygulama için bir ad girin. Bu ad, Microsoft Endpoint Manager Yönetim Merkezi ' nde başvurunuz için kullanılır. İOS/ıpados *cihazında gösterilmez.*
          - **Uygulama PAKETI kimliği**: UYGULAMANıN paket kimliğini girin. Bazı örnekler için bkz. [yerleşik iOS/ıpados uygulamaları Için paket kimlikleri](bundle-ids-built-in-ios-apps.md) .

#### <a name="example"></a>Örnek

Aşağıdaki örnekte, **contoso** adlı yeni bir sayfa eklenmiştir. Sayfa, arkadaşları ve ayarları bul uygulamalarını gösterir. Ayarlar uygulaması özelliklerini göstermek için seçilmiştir:

![Intune 'da iOS/ıpados giriş ekranı ayarları örneği](./media/ios-device-features-settings/Jc2OxyX.png)

İlkeyi bir iPhone 'a atadığınızda, sayfa aşağıdaki resme benzer şekilde görünür:

![Intune 'da değiştirilmiş giriş ekranına sahip iOS/ıpados cihazı](./media/ios-device-features-settings/Bd37PHa.png)

## <a name="app-notifications"></a>Uygulama bildirimleri

### <a name="settings-apply-to-automated-device-enrollment-supervised"></a>Ayarlar için geçerlidir: otomatik cihaz kaydı (denetimli)

- **Ekle**: uygulamalar için bildirim ekleme:

    ![Intune 'da iOS/ıpados profilinde uygulama bildirimi ekleme](./media/ios-device-features-settings/ios-macos-app-notifications.png)

  - **Uygulama PAKETI kimliği**: eklemek Istediğiniz uygulamanın **uygulama paket kimliğini** girin. Bazı örnekler için bkz. [yerleşik iOS/ıpados uygulamaları Için paket kimlikleri](bundle-ids-built-in-ios-apps.md) .
  - **Uygulama adı**: eklemek istediğiniz uygulamanın adını girin. Bu ad, Microsoft Endpoint Manager Yönetim Merkezi ' nde başvurunuz için kullanılır. Cihazda *gösterilmez.*
  - **Yayımcı**: eklemekte olduğunuz uygulamanın yayımcısını girin. Bu ad, Microsoft Endpoint Manager Yönetim Merkezi ' nde başvurunuz için kullanılır. Cihazda *gösterilmez.*
  - **Bildirimler**: uygulamanın cihaza bildirim göndermesini **etkinleştirin** veya **devre dışı bırakın** .
    - **Bildirim merkezinde göster**: **Etkinleştir** , uygulamanın cihaz bildirim merkezinde bildirimleri göstermesini sağlar. **Devre dışı bırak ayarı** , uygulamanın bildirim merkezinde bildirimleri göstermesini önler.
    - **Kilit ekranında göster**: cihaz kilidi ekranında uygulamadan bildirimleri görmek için **Etkinleştir** ' i seçin. **Devre dışı bırak ayarı** , uygulamanın kilit ekranında bildirimleri göstermesini önler.
    - **Uyarı türü**: cihazın kilidi açıldığında, bildirimin nasıl gösterileceğini seçin. Seçenekleriniz şunlardır:
      - **Hiçbiri**: hiçbir bildirim gösterilmez.
      - **Başlık**: bir başlık, bildirimle kısaca gösterilir.
      - **Kalıcı**: bildirim gösterilir ve kullanıcının cihazı kullanmaya devam etmeden önce el ile kapatması gerekir.
    - **Uygulama simgesinde rozet**: uygulama simgesine rozet eklemek için **Etkinleştir** ' i seçin. Rozet, uygulamanın bir bildirim gönderdiği anlamına gelir.
    - **Sesler**: bir bildirim teslim edildiğinde ses çalmak için **Etkinleştir** ' i seçin.

## <a name="lock-screen-message"></a>Kilit ekranı iletisi

Bu özellik şu platformlarda geçerlidir:

- iOS 9.3 ve üzeri
- ıpados 13,0 ve üzeri

### <a name="settings-apply-to-automated-device-enrollment-supervised"></a>Ayarlar için geçerlidir: otomatik cihaz kaydı (denetimli)

- **Varlık etiketi bilgileri**: cihazın varlık etiketiyle ilgili bilgileri girin. Örneğin `Owned by Contoso Corp` veya `Serial Number: {{serialnumber}}` girin.

  Girdiğiniz metin, cihazdaki oturum açma penceresinde ve kilit ekranında görüntülenir.

- **Kilit ekranı dipnotu**: Cihaz kaybolur veya çalınırsa, cihazın döndürülmesini sağlamaya yardımcı olabilecek bir durum girin. İstediğiniz herhangi bir metin girebilirsiniz. Örneğin `If found, call Contoso at ...` gibi bir URL girebilirsiniz.

  Cihaz belirteçleri, bu alanlara cihaza özgü bilgiler eklemek için de kullanılabilir. Örneğin, seri numarasını göstermek için `Serial Number: {{serialnumber}}`girin. Kilit ekranında metin `Serial Number 123456789ABC`benzer şekilde görünür. Değişken girerken `{{ }}`kaşlı ayraç kullandığınızdan emin olun. [Uygulama yapılandırma belirteçleri](../apps/app-configuration-policies-use-ios.md#tokens-used-in-the-property-list) , kullanılabilecek değişkenlerin bir listesini içerir. `deviceName` veya başka bir cihaza özgü değeri de kullanabilirsiniz.

  > [!NOTE]
  > Değişkenler kullanıcı arabiriminde doğrulanmaz ve büyük/küçük harfe duyarlıdır. Sonuç olarak, yanlış girişle kaydedilmiş profiller görebilirsiniz. Örneğin, `{{deviceid}}`yerine `{{DeviceID}}` girerseniz, aygıtın benzersiz KIMLIĞI yerine değişmez dize gösterilir. Doğru bilgileri girdiğinizden emin olun.

## <a name="single-sign-on"></a>Çoklu oturum açma

### <a name="settings-apply-to-device-enrollment-automated-device-enrollment-supervised"></a>Ayarlar için geçerlidir: cihaz kaydı, otomatik cihaz kaydı (denetimli)

- **AAD’den kullanıcı adı özniteliği**: Intune, Azure AD’deki her kullanıcı için bu özniteliği arar. Ardından Intune, cihaza yüklenen XML oluşturmadan önce ilgili alanı (UPN gibi) doldurur. Seçenekleriniz şunlardır:

  - **Kullanıcı asıl adı**: UPN aşağıdaki şekilde ayrıştırılır:

    ![Intune 'da iOS/ıpados Kullanıcı adı SSO özniteliği](./media/ios-device-features-settings/User-name-attribute.png)

    Ayrıca, **Bölge** metin kutusuna girdiğiniz metinle bölge değerinin üzerine yazabilirsiniz.

    Örneğin contoso, Avrupa, Asya ve Kuzey Amerika dahil olmak üzere birkaç bölgeye sahiptir. Contoso, Asya kullanıcılarının SSO kullanmasını istemektedir ve uygulama `username@asia.contoso.com` biçiminde UPN gerektirir. **Kullanıcı asıl adı**' nı seçtiğinizde, her bir kullanıcının BÖLGESI Azure AD 'den alınır ve bu `contoso.com`. Böylece, Asya 'daki kullanıcılar için **Kullanıcı asıl adı**' nı seçin ve `asia.contoso.com`girin. Son kullanıcının UPN 'si `username@contoso.com`yerine `username@asia.contoso.com`olur.

  - **Intune CIHAZ kimliği**: Intune, ıNTUNE cihaz kimliğini otomatik olarak seçer.

    Varsayılan olarak, uygulamaların yalnızca cihaz kimliğini kullanması gerekir. Ancak, uygulamanız bölge ve cihaz KIMLIĞINI kullanıyorsa, bölgeyi bölge metin kutusuna yazabilirsiniz.

    > [!NOTE]
    > Varsayılan olarak, cihaz kimliğini kullanıyorsanız bölgeyi boş bırakın.

  - **Azure AD cihaz KIMLIĞI**

- **Bölge**: URL 'nin etki alanı parçasını girin. Örneğin, şunu girin: `contoso.com`.
- **Çoklu Oturum Açma kullanacak URL ön ekleri**: Kuruluşunuzda kullanıcının çoklu oturum açma kimlik doğrulaması yapmasını gerektiren tüm URL’leri **ekleyin**.

  Örneğin, bir Kullanıcı bu sitelerden birine bağlanırsa, iOS/ıpados cihazı çoklu oturum açma kimlik bilgilerini kullanır. Kullanıcının başka kimlik bilgisi girmesi gerekmez. Multi-Factor Authentication etkinleştirilirse, kullanıcıların ikinci kimlik doğrulamasını girmesi gerekir.

  > [!NOTE]
  > Bu URL'ler düzgün biçimlendirilmiş FQDN'ler olmalıdır. Apple bunların `http://<yourURL.domain>` biçiminde olmasını gerektirir.

  URL eşleştirme desenleri `http://` veya `https://` ile başlamalıdır. Basit bir dize eşleşmesi çalıştırılır, bu nedenle `http://www.contoso.com/` URL öneki `http://www.contoso.com:80/`eşleşmez. İOS 10.0 + ve ıpados 13.0 + ile, eşleşen tüm değerleri girmek için tek bir joker \* kullanılabilir. Örneğin, `http://*.contoso.com/` hem `http://store.contoso.com/` hem de `http://www.contoso.com`eşleşir.

  `http://.com` ve `https://.com` desenleri sırasıyla tüm HTTP ve HTTPS URL 'Leriyle eşleşir.

- **Çoklu Oturum Açma kullanan uygulamalar**: Son kullanıcıların cihazlarına çoklu oturum açma kullanabilecek uygulamalar **ekleyin**.

  `AppIdentifierMatches` dizi, uygulama paketi kimlikleriyle eşleşen dizeler içermelidir. Bu dizeler, `com.contoso.myapp`gibi tam eşleşmeler olabilir veya \* joker karakterini kullanarak paket KIMLIĞINDE bir önek eşleşmesi girebilirsiniz. Joker karakter, bir nokta karakterinden (.) sonra görünmelidir ve dizenin sonunda, `com.contoso.*`gibi yalnızca bir kez görünebilir. Joker karakter eklendiğinde, paket kimlikleri bu ön ekle başlayan tüm uygulamaların hesaba erişimine izin verilir.

  **Uygulama Adı**’nı kullanarak paket kimliğini ayırt etmenize yardımcı olacak bir kolay ad ekleyin.

- **Kimlik bilgisi yenileme sertifikası**: kimlik doğrulaması için Sertifikalar (parolalar değil) kullanılıyorsa, kimlik doğrulama sertifikası olarak mevcut SCEP veya PFX sertifikasını seçin. Genellikle, bu sertifika, kullanıcıya VPN, Wi-Fi veya e-posta gibi diğer profiller için dağıtılan sertifikadır.

## <a name="web-content-filter"></a>Web içeriği filtresi

### <a name="settings-apply-to-automated-device-enrollment-supervised"></a>Ayarlar için geçerlidir: otomatik cihaz kaydı (denetimli)

- **Filtre türü**: belirli Web sitelerine izin vermeyi seçin. Seçenekleriniz şunlardır:

  - **URL 'Leri yapılandırma**: doğrudan küfür ve açık cinsel dil dahil olmak üzere yetişkin koşullarını gösteren yerleşik Web filtresini kullanın. Bu özellik her bir Web sayfasını yüklendiği şekilde değerlendirir ve uygun olmayan içeriği tanımlar ve engeller. Filtre tarafından denetlenmesini istemediğiniz URL 'Ler de ekleyebilirsiniz. Ya da Apple 'ın filtre ayarlarından bağımsız olarak belirli URL 'Leri engelleyin.

    - İzin **verilen URL 'ler**: izin vermek Istediğiniz URL 'leri **ekleyin** . Bu URL 'Ler Apple 'ın Web filtresini atlar.

        > [!NOTE]
        > Girdiğiniz URL 'ler, Apple Web filtresi tarafından evauluated istemediğiniz URL 'lerdir. Bu URL 'Ler, izin verilen Web sitelerinin bir listesi değildir. İzin verilen Web sitelerinin bir listesini oluşturmak için **filtre türünü** **yalnızca belirli Web siteleri**olarak ayarlayın.

    - **Engellenen URL 'ler** **: Apple** Web Filter ayarlarından bağımsız olarak, durdurmak istediğiniz URL 'leri açmayı açın.

  - **Yalnızca belirli Web siteleri** (yalnızca Safari Web tarayıcısı için): Bu URL 'ler Safari tarayıcısının yer işaretlerine eklenir. Kullanıcının **yalnızca** bu siteleri ziyaret etme izni vardır; başka hiçbir site açılamaz. Bu seçeneği yalnızca kullanıcıların erişebileceği URL'lerin tam listesini biliyorsanız kullanın.

    - **URL**: izin vermek istediğiniz Web sitesinin URL 'sini girin. Örneğin, şunu girin: `https://www.contoso.com`.
    - **Yer Işareti yolu**: Apple bu ayarı değiştirdi. Tüm yer işaretleri **onaylanan siteler** klasörüne gider. Yer işaretleri girdiğiniz yer işareti yoluna gitmez.
    - **Başlık**: yer işareti için açıklayıcı bir başlık girin.

    Herhangi bir URL girmezseniz, son kullanıcılar `microsoft.com`, `microsoft.net`ve `apple.com`dışındaki web sitelerine erişemez. Bu URL 'Lere Intune tarafından otomatik olarak izin verilir.

## <a name="single-sign-on-app-extension"></a>Çoklu oturum açma uygulama uzantısı

Bu özellik şu platformlarda geçerlidir:

- iOS 13,0 ve üzeri
- ıpados 13,0 ve üzeri

### <a name="settings-apply-to-all-enrollment-types"></a>Ayarlar için geçerlidir: tüm kayıt türleri

- **SSO uygulama uzantısı türü**: SSO uygulama uzantısının türünü seçin. Seçenekleriniz şunlardır:

  - **Yapılandırılmadı**: uygulama uzantıları kullanılmıyor. Bir uygulama uzantısını devre dışı bırakmak için, SSO uygulama uzantısı türü ' ni **Yapılandırılmadı**' ya geçirebilirsiniz.
  - **Yeniden yönlendir**: Modern kimlik doğrulama akışlarıyla SSO gerçekleştirmek için genel, özelleştirilebilir bir yeniden yönlendirme uygulama uzantısı kullanın. Kuruluşunuzun uygulama uzantısının uzantı KIMLIĞINI öğrendiğinizden emin olun.
  - **Kimlik bilgisi**: sınama ve yanıt kimlik doğrulama akışlarıyla SSO gerçekleştirmek için genel, özelleştirilebilir bir kimlik bilgisi uygulama uzantısı kullanın. Kuruluşunuzun uygulama uzantısının uzantı KIMLIĞINI öğrendiğinizden emin olun.
  - **Kerberos**: iOS 13.0 + ve ıpados 13.0 + ' da bulunan Apple 'ın yerleşik Kerberos uzantısını kullanın. Bu seçenek, **kimlik bilgisi** uygulama uzantısının Kerberos 'a özgü bir sürümüdür.

  > [!TIP]
  > **Yeniden yönlendirme** ve **kimlik bilgisi** türleriyle, uzantıdan geçirilecek kendi yapılandırma değerlerinizi eklersiniz. **Kimlik bilgisi**kullanıyorsanız, Apple tarafından **Kerberos** türünde sunulan yerleşik yapılandırma ayarlarını kullanmayı göz önünde bulundurun.

- **UZANTı kimliği** (yeniden yönlendirme ve kimlik bilgisi): `com.apple.extensiblesso`gibi SSO uygulama uzantınızı tanımlayan paket tanımlayıcısını girin.

- **Takım Kimliği** (yeniden yönlendirme ve kimlik bilgisi): SSO uygulama uzantınızın ekip tanımlayıcısını girin. Takım tanımlayıcısı, Apple tarafından oluşturulan `ABCDE12345`gibi 10 karakterlik alfasayısal bir dizedir (sayılar ve harfler). Takım KIMLIĞI gerekli değildir.

  [Takım kimliğinizi bulun](https://help.apple.com/developer-account/#/dev55c3c710c) (Apple 'ın Web sitesini açar) daha fazla bilgi içerir.

- **Bölge** (kimlik bilgileri ve Kerberos): kimlik doğrulama Realm adını girin. Bölge adı, `CONTOSO.COM`gibi büyük harfli olmalıdır. Genellikle, bölge adınız DNS etki alanı adınızla aynıdır, ancak tümü büyük harfle aynıdır.

- **Etki alanları** (kimlik bilgileri ve Kerberos): SSO aracılığıyla kimlik doğrulayabilecek sitelerin etki alanı veya ana bilgisayar adlarını girin. Örneğin, Web siteniz `mysite.contoso.com`, `mysite` ana bilgisayar adıdır ve `contoso.com` etki alanı adıdır. Kullanıcılar bu sitelerden birine bağlandıklarında, uygulama uzantısı kimlik doğrulama sınamasını işler. Bu kimlik doğrulaması, kullanıcıların oturum açmak için yüz KIMLIĞI, Touch ID veya Apple pincode/geçiş kodu kullanmasına izin verir.

  - Çoklu oturum açma uygulama uzantılarınızın Intune profillerindeki tüm etki alanları benzersiz olmalıdır. Farklı türlerde SSO uygulama uzantıları kullanıyor olsanız bile, bir etki alanını hiçbir oturum açma uygulama uzantısı profilinde tekrarlayamıyorum.
  - Bu etki alanları büyük/küçük harfe duyarlı değildir.

- **URL 'ler** (yalnızca yeniden yönlendir): kimlik SAĞLAYıCıLARıNıZıN URL öneklerini girin adına yeniden yönlendirme uygulama uzantısı SSO 'yu gerçekleştirir. Bir Kullanıcı bu URL 'lere yeniden yönlendirildiğinde, SSO uygulama uzantısı, SSO 'yu ve bu URL 'yi istemez.

  - Intune çoklu oturum açma uygulama uzantısı profillerindeki tüm URL 'Lerin benzersiz olması gerekir. Farklı türlerde SSO uygulama uzantıları kullanıyor olsanız bile, hiçbir SSO uygulama uzantısı profilinde bir etki alanını tekrarlayabilirsiniz.
  - URL 'Lerin http://veya https://ile başlaması gerekir.

- **Ek yapılandırma** (yeniden yönlendirme ve kimlik bilgileri): SSO uygulama uzantısına geçirilecek uzantıya özgü ek veriler girin:
  - **Anahtar**: `user name`gibi eklemek istediğiniz öğenin adını girin.
  - **Tür**: veri türünü girin. Seçenekleriniz şunlardır:

    - Dize
    - Boole: **yapılandırma değeri**' nde `True` veya `False`girin.
    - Tamsayı: **yapılandırma değeri**alanına bir sayı girin.
    
  - **Değer**: verileri girin.

  - **Ekle**: yapılandırma anahtarlarınızı eklemek için seçin.

- **Anahtarlık kullanımı** (yalnızca Kerberos): parolaların anahtarlıkta kaydedilmesini ve saklanmasını engellemek için **Engelle** ' yi seçin. Engellenirse, kullanıcıdan parolasını kaydetmesi istenmez ve Kerberos biletinin süresi dolmuşsa parolayı yeniden girmesi gerekir. **Yapılandırılmadı** (varsayılan), parolaların anahtarlıkta kaydedilmesine ve depolanmasına izin verir. Anahtarın süresi dolarsa kullanıcılardan parolasını yeniden girmesi istenmez.
- **Yüz kimliği, Touch ID veya geçiş kodu** (yalnızca Kerberos): Kerberos biletini yenilemek için kimlik bilgisi gerektiğinde KULLANıCıLARıN yüz kimliğini, Touch ID 'sini veya cihaz geçiş kodunu girmesini **zorunlu** kılar. **Yapılandırılmadı** (varsayılan), Kerberos biletini yenilemek için kullanıcıların biyometri veya cihaz geçiş kodu kullanmalarını gerektirmez. **Anahtarlık kullanımı** engellenirse, bu ayar uygulanmaz.
- **Varsayılan bölge** (yalnızca Kerberos): Girdiğiniz **bölge** değerini varsayılan bölge olarak ayarlamak Için **Etkinleştir** ' i seçin. **Yapılandırılmadı** (varsayılan) varsayılan bir bölge yapmaz.

  > [!TIP]
  > - Kuruluşunuzda birden çok Kerberos SSO uygulama uzantısını yapılandırıyorsanız, bu ayarı **etkinleştirin** .
  > - Birden çok bölge kullanıyorsanız bu ayarı **etkinleştirin** . Girdiğiniz **bölge** değerini varsayılan bölge olarak ayarlar.
  > - Yalnızca bir bölge varsa, **Yapılandırılmadı** (varsayılan) olarak bırakın.

- **Asıl ad** (yalnızca Kerberos): Kerberos sorumlusunun Kullanıcı adını girin. Bölge adını eklemeniz gerekmez. Örneğin, `user@contoso.com``user` asıl addır ve `contoso.com` bölge adıdır.

  > [!TIP]
  > - Büyük köşeli ayraç `{{ }}`girerek asıl ad içindeki değişkenleri de kullanabilirsiniz. Örneğin, Kullanıcı adını göstermek için `Username: {{username}}`girin. 
  > - Ancak, değişkenler kullanıcı arabiriminde doğrulanmamış ve büyük/küçük harfe duyarlı olduğundan değişken değiştirme konusunda dikkatli olun. Doğru bilgileri girdiğinizden emin olun.

- **Active Directory site kodu** (yalnızca Kerberos): Kerberos uzantısının kullanması gereken Active Directory sitenin adını girin. Kerberos uzantısı Active Directory site kodunu otomatik olarak bulagerekebilmeniz için bu değeri değiştirmeniz gerekebilir.
- **Önbellek adı** (yalnızca Kerberos): Kerberos önbelleğinin genel güvenlik HIZMETLERI (GSS) adını girin. Büyük olasılıkla bu değeri ayarlamanız gerekmez.
- **Uygulama paketi kimlikleri** (yalnızca Kerberos): cihazlarınızda çoklu oturum açma kullanması gereken uygulama paketi tanımlayıcılarını **ekleyin** . Bu uygulamalara, Kerberos Anahtar verme bileti, kimlik doğrulama bileti ve kullanıcılara erişim yetkisi oldukları hizmetler için kimlik doğrulaması erişimi verilir.
- **Etki alanı bölge eşlemesi** (yalnızca Kerberos): bölge ile eşleşmesi gereken etkı alanı DNS soneklerini **ekleyin** . Ana bilgisayarların DNS adları bölge adıyla eşleşmezse bu ayarı kullanın. Büyük olasılıkla bu özel etki alanı/bölge eşlemesini oluşturmanız gerekmez.
- **PKINIT sertifikası** (yalnızca Kerberos): Kerberos kimlik doğrulaması Için kullanılabilecek Ilk kimlik doğrulaması (PKI) sertifikası Için ortak anahtar şifrelemesini **seçin** . Intune 'A eklediğiniz [PKCS](../protect/certficates-pfx-configure.md) veya [SCEP](../protect/certificates-scep-configure.md) sertifikaları arasından seçim yapabilirsiniz. Sertifikalar hakkında daha fazla bilgi için bkz. [Microsoft Intune kimlik doğrulaması için sertifikaları kullanma](../protect/certificates-configure.md).

## <a name="wallpaper"></a>Duvar

Var olan bir görüntüye sahip cihazlara sahip olmayan bir profil atandığında beklenmeyen davranışlarla karşılaşabilirsiniz. Örneğin, görüntü olmadan bir profil oluşturursunuz. Bu profil, zaten bir görüntüsü olan cihazlara atanır. Bu senaryoda, görüntü cihaz varsayılana değişebilir veya orijinal görüntü cihazda kalabilir. Bu davranış, Apple 'ın MDM platformu tarafından denetlenir ve sınırlandırılmıştır.

### <a name="settings-apply-to-automated-device-enrollment-supervised"></a>Ayarlar için geçerlidir: otomatik cihaz kaydı (denetimli)

- **Duvar kağıdı görüntü konumu**: görüntüyü göstermek için cihazda bir konum seçin. Seçenekleriniz şunlardır:
  - **Yapılandırılmadı**: cihaza özel bir görüntü eklenmez. Cihaz, işletim sistemi varsayılanını kullanır.
  - **Kilit ekranı**: görüntüyü kilit ekranına ekler.
  - **Ana ekran**: görüntüyü giriş ekranına ekler.
  - **Kilit ekranı ve giriş ekranı**: kilit ekranında ve ana ekranda aynı görüntüyü kullanır.
- **Duvar kağıdı resmi**: kullanmak istediğiniz var olan bir. png,. jpg veya. JPEG görüntüsünü karşıya yükleyin. Dosya boyutunun 750 KB 'tan az olduğundan emin olun. Ayrıca, eklediğiniz bir görüntüyü de **kaldırabilirsiniz** .

> [!TIP]
> Kilit ekranında ve ana ekranda farklı görüntüleri göstermek için, kilit ekranı görüntüsüyle bir profil oluşturun. Giriş ekranı görüntüsüyle başka bir profil oluşturun. Her iki profili de iOS/ıpados Kullanıcı veya cihaz gruplarına atayın.

## <a name="next-steps"></a>Sonraki adımlar

[Profili atama](device-profile-assign.md) ve [durumunu izleme](device-profile-monitor.md).

[MacOS](macos-device-features-settings.md) cihazları için cihaz özelliği profilleri de oluşturabilirsiniz.
