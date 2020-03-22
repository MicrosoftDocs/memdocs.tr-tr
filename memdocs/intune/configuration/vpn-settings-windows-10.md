---
title: Microsoft Intune-Azure 'da Windows 10 VPN ayarları | Microsoft Docs
description: Windows 10 ve Windows holographic for Business cihazlarında trafik kuralları, koşullu erişim ve DNS ve proxy ayarları dahil olmak üzere Microsoft Intune tüm kullanılabilir VPN ayarlarını ve bunların ne yaptığını öğrenin.
keywords: ''
author: MandiOhlinger
ms.author: mandia
manager: dougeby
ms.date: 03/19/2020
ms.topic: reference
ms.service: microsoft-intune
ms.subservice: configuration
ms.localizationpriority: medium
ms.technology: ''
ms.suite: ems
search.appverid: MET150
ms.reviewer: tycast
ms.custom: intune-azure; seodec18
ms.collection: M365-identity-device-management
ms.openlocfilehash: 8d2f671e88b1221961e978d1945e28c7cec474cb
ms.sourcegitcommit: 017b93345d8d8de962debfe3db5fc1bda7719079
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/21/2020
ms.locfileid: "80086502"
---
# <a name="windows-10-and-windows-holographic-device-settings-to-add-vpn-connections-using-intune"></a>Intune kullanarak VPN bağlantıları eklemek için Windows 10 ve Windows holographic cihaz ayarları

Microsoft Intune kullanarak aygıtlar için VPN bağlantıları ekleyebilir ve yapılandırabilirsiniz. Bu makalede, sanal özel ağlar (VPN 'Ler) oluştururken yaygın olarak kullanılan ayarlar ve özellikler listelenmiştir ve açıklanmaktadır. Bu VPN ayarları ve özellikleri, Intune 'da gönderilen veya cihazlara dağıtılan cihaz yapılandırma profillerinde kullanılır.

Mobil cihaz yönetimi (MDM) çözümünüzün bir parçası olarak bu ayarları, VPN satıcısı kullanma, her zaman açık etkinleştirme, DNS kullanma, bir ara sunucu ekleme ve daha fazlası gibi özelliklere izin vermek veya devre dışı bırakmak için kullanın.

Bu ayarlar, çalıştıran cihazlar için geçerlidir:

- Windows 10
- Windows 10 Holographic for Business

Seçtiğiniz ayarlara bağlı olarak, değerlerden bazıları yapılandırılamayabilir.

## <a name="before-you-begin"></a>Başlamadan önce

[BIR VPN cihaz yapılandırma profili oluşturun](vpn-settings-configure.md).

## <a name="base-vpn-settings"></a>Temel VPN ayarları

- **Bağlantı adı**: Bu bağlantı için bir ad girin. Cihazlarındaki kullanılabilir VPN bağlantılarına göz atan son kullanıcılar bu adı görür.
- **Sunucular**: Cihazların bağlandığı bir veya birden çok VPN sunucusu ekleyin. Sunucu eklerken aşağıdaki bilgileri girersiniz:
  - **Açıklama**: sunucu IÇIN **contoso VPN sunucusu**gibi açıklayıcı bir ad girin.
  - **IP adresi veya FQDN**: CIHAZLARıN bağlanacağı VPN sunucusunun IP adresini veya tam etki alanı adını (FQDN) girin, örneğin **192.168.1.1** veya **VPN.contoso.com**.
  - **Varsayılan sunucu**: Bu sunucuyu, cihazların bağlantı oluşturmak için kullandığı varsayılan sunucu olarak etkinleştirir. Varsayılan sunucu olarak tek bir sunucu ayarlayın.
  - **İçeri Aktar**: Açıklama, IP adresi veya FQDN, Varsayılan sunucu biçiminde sunucu listesini içeren virgülle ayrılmış bir dosyaya göz atın. **Tamam**'ı seçerek bu sunucuları **Sunucular** listesine içeri aktarın.
  - **Dışarı aktar**: sunucu listesini virgülle ayrılmış değerler (CSV) dosyasına aktarır.

- **Dahili DNS ile IP adresi kaydetme** Windows 10 VPN profilinin dahili DNS ile VPN arabirimine atanmış IP adresini dinamik olarak kaydetmek için **Etkinleştir**'i seçin. IP adreslerini dinamik olarak kaydetmek istemiyorsanız **Devre Dışı Bırak**’ı seçin.

- **Bağlantı türü**: Aşağıdaki satıcı listesinden VPN bağlantı türünü seçin:

  - **Pulse Secure**
  - **F5 Edge Client**
  - **SonicWALL Mobile Connect**
  - **Check Point Capsule VPN**
  - **Citrix**
  - **Palo Alto Networks GlobalProtect**
  - **Otomatik**
  - **IKEv2**
  - **L2TP**
  - **PPTP**

  VPN bağlantı türünü seçtiğinizde, aşağıdaki ayarları belirtmeniz de istenebilir:  
  - **Always on**: aşağıdaki olaylar gerçekleştiğinde VPN bağlantısına otomatik olarak bağlanmak için **Etkinleştir** ' i seçin:
    - Kullanıcılar cihazlarında oturum açtığında
    - Cihazdaki ağ değiştiğinde
    - Cihaz ekranı kapandıktan sonra yeniden açıldığında

  - **Kimlik doğrulama yöntemi**: Kullanıcıların VPN sunucusunda nasıl kimlik doğrulaması yapmasını istediğinizi seçin. **Sertifikaların** kullanılması sıfır temaslı deneyim, isteğe bağlı VPN ve uygulama başına VPN gibi iyileştirilmiş özellikler sağlar.
  - **Her oturum açışta kimlik bilgilerini hatırla**: Kimlik doğrulama bilgilerini önbelleğe almak için bunu seçin.
  - **Özel XML**: VPN bağlantısını yapılandıran tüm özel XML komutlarını girin.
  - **EAP Xml**: VPN bağlantısını yapılandıran tüm EAP XML komutlarını girin

### <a name="pulse-secure-example"></a>Pulse Secure örneği

```
<pulse-schema><isSingleSignOnCredential>true</isSingleSignOnCredential></pulse-schema>
```

### <a name="f5-edge-client-example"></a>F5 Edge Client örneği

```
<f5-vpn-conf><single-sign-on-credential /></f5-vpn-conf>
```

### <a name="sonicwall-mobile-connect-example"></a>SonicWALL Mobile Connect örneği
**Oturum açma grubu veya etki alanı**: VPN profilinde bu özellik ayarlanamaz. Bunun yerine, `username@domain` veya `DOMAIN\username` biçimlerinde kullanıcı adıyla etki alanı girildiğinde Mobile Connect bu değeri ayrıştırır.

Örnek:

```
<MobileConnect><Compression>false</Compression><debugLogging>True</debugLogging><packetCapture>False</packetCapture></MobileConnect>
```

### <a name="checkpoint-mobile-vpn-example"></a>CheckPoint Mobile VPN örneği

```
<CheckPointVPN port="443" name="CheckPointSelfhost" sso="true" debug="3" />
```

### <a name="writing-custom-xml"></a>Özel XML yazma
Özel XML komutları yazma hakkında daha fazla bilgi için her bir üreticinin VPN belgelerine başvurun.

Özel EAP XML oluşturma hakkında daha fazla bilgi için bkz. [EAP yapılandırması](https://docs.microsoft.com/windows/client-management/mdm/eap-configuration).

## <a name="apps-and-traffic-rules"></a>Uygulamalar ve Trafik Kuralları

- **WIP veya uygulamaları bu VPN ile ilişkilendir**: Yalnızca bazı uygulamaların VPN bağlantısını kullanmasını istiyorsanız bu ayarı etkinleştirin. Seçenekleriniz şunlardır:

  - **Bu bağlantıyla bir WIP'i ilişkilendir**: **Bu bağlantı için WIP etki alanını** girin
  - **Uygulamaları bu bağlantıyla ilişkilendir**: **VPN bağlantısını bu uygulamalarla kısıtlayabilir** ve ardından **İlişkili Uygulamalar** ekleyebilirsiniz. Girdiğiniz uygulamalar VPN bağlantısını otomatik olarak kullanır. Uygulamanın türü uygulama tanımlayıcısını belirler. Bir evrensel uygulama için paket aile adını girin. Bir masaüstü uygulaması için söz konusu uygulamanın dosya yolunu girin.
  >[!IMPORTANT]
  >Uygulama başına VPN'ler için oluşturulan tüm uygulama listelerini güvenlik altına almanızı öneririz. Yetkisiz bir kullanıcı bu listede değişiklik yaparsa ve bunu uygulama başına VPN uygulama listesine aktarırsanız, erişimi olmaması gereken uygulamalara VPN erişimi yetkisi verme olasılığınız vardır. Uygulama listelerini güvenlik altına almanın yollarından biri, erişim denetim listesi (ACL) kullanmaktır.

- **Bu VPN bağlantısının ağ trafiği kuralları**: VPN bağlantısı için hangi protokollerin, yerel ve uzak bağlantı noktasının ve adres aralıklarının etkinleştirileceğini seçin. Bir ağ trafiği kuralı oluşturmazsanız, bu durumda tüm protokoller, bağlantı noktaları ve adres aralıkları etkinleştirilir. Bir kural oluşturduktan sonra, VPN bağlantısı yalnızca bu kuralda veya ek kurallarda girdiğiniz protokolleri, bağlantı noktalarını ve adres aralıklarını kullanır.

## <a name="conditional-access"></a>Koşullu Erişim

- **Bu VPN bağlantısı Için koşullu erişim**: istemciden cihaz uyumluluk akışını mümkün olarak sunar. Etkinleştirildiğinde, VPN istemcisi kimlik doğrulama için kullanmak üzere bir sertifika almak için Azure Active Directory (AD) ile iletişim kurar. VPN’nin sertifika kimlik doğrulamasını kullanacak şekilde ayarlanmış olması ve VPN sunucusunun Azure AD tarafından döndürülen sunucuya güvenmesi gerekir.

- **Alternatif sertifika ile çoklu oturum açma (SSO)** : Cihaz uyumluluğu amacıyla Kerberos kimlik doğrulaması için VPN kimlik doğrulama sertifikasından farklı bir sertifika kullanın. Aşağıdaki ayarlarla sertifikayı girin:

  - **Ad**: Genişletilmiş anahtar kullanımı (EKU) adı
  - **Nesne Tanımlayıcısı**: EKU için nesne tanımlayıcısı
  - **Sertifikayı veren karması**: SSO sertifikası için parmak izi

## <a name="dns-settings"></a>DNS Ayarları

- **DNS son eki arama listesi**: **DNS son ekleri** alanına bir DNS soneki girin ve **Ekle**'yi seçin. Çok sayıda sonek ekleyebilirsiniz.

  DNS son ekleri kullanırken bir ağ kaynağını tam etki alanı adı (FQDN) yerine kısa adını kullanarak arayabilirsiniz. Kısa ad kullanılarak yapılan aramalarda, son ek otomatik olarak DNS sunucusu tarafından belirlenir. Örneğin, `utah.contoso.com` DNS son eki listesinde yer alır. `DEV-comp` ping yaparsınız. Bu senaryoda `DEV-comp.utah.contoso.com` olarak çözümlenir.

  DNS son ekleri listelenen sırayla çözümlenir ve bu sıra değiştirilebilir. Örneğin `colorado.contoso.com` ve `utah.contoso.com` DNS son eki listesindedir ve ikisinin de `DEV-comp` adlı bir kaynağı vardır. `colorado.contoso.com` listedeki ilk öğe olduğundan, `DEV-comp.colorado.contoso.com` olarak çözümlenir.
  
  Sırayı değiştirmek için DNS son ekinin solundaki noktalara tıklayın ve son eki en üste sürükleyin:

  ![Dns son ekini taşımak için üç noktaya tıklayın ve sürükleyin](./media/vpn-settings-windows-10/vpn-settings-windows10-move-dns-suffix.png)

- **Ad çözümleme ilkesi tablosu (NRPT) kuralları**: ad çözümleme ilkesi tablosu (NRPT) KURALLARı, VPN 'ye bağlıyken DNS 'in adları nasıl çözdüğünü tanımlar. VPN bağlantısı kurulduktan sonra, VPN bağlantısının hangi DNS sunucularını kullandığını seçersiniz.

  Girdiğiniz etki alanını çözümlemek için etki alanı, DNS sunucusu, proxy ve diğer ayrıntıları içeren tabloya kurallar ekleyebilirsiniz. VPN bağlantısı, kullanıcılar girdiğiniz etki alanlarına bağlandıklarında bu kuralları kullanır.

  Yeni bir kural eklemek için **Ekle** ' yi seçin. Her sunucu için şunları girin:

  - **Etki alanı**: kuralı uygulamak için tam etki alanı adını (FQDN) veya bir DNS sonekini girin. Ayrıca, DNS son ekinin başındaki bir nokta (.) girebilirsiniz. Örneğin `contoso.com` veya `.allcontososubdomains.com` girin.
  - **DNS sunucuları**: etki ALANıNı çözen IP ADRESINI veya DNS sunucusunu girin. Örneğin `10.0.0.3` veya `vpn.contoso.com` girin.
  - **Proxy**: etki alanını çözen Web proxy sunucusunu girin. Örneğin, şunu girin: `http://proxy.com`.
  - **Otomatik bağlan**: **etkinleştirildiğinde**, cihaz, girdiğiniz `contoso.com`gibi bir etki alanına bağlandığında, cihaz otomatik olarak VPN 'e bağlanır. **Yapılandırılmadığında** (varsayılan) cihaz VPN 'ye otomatik olarak bağlanmaz
  - **Persistent**: **etkin**olarak AYARLANDıĞıNDA, kural, VPN bağlantısı kesildikten sonra bile cihazdan El Ile kaldırılana kadar ad çözümleme ilkesi tablosunda (NRPT) kalır. **Yapılandırılmadı** (varsayılan) olarak ayarlandığında, VPN BAĞLANTıSı kesildiğinde VPN profilindeki NRPT kuralları cihazdan kaldırılır.

## <a name="proxy-settings"></a>Proxy ayarları

- **Otomatik yapılandırma betiği**: Proxy sunucusunu yapılandırmak için bir dosya kullanın. Yapılandırma dosyasını içeren **Proxy sunucu URL'sini** (örneğin, `http://proxy.contoso.com`) girin.
- **Adres**: Proxy sunucusu adresini girin (IP adresi veya `vpn.contoso.com` gibi)
- **Bağlantı noktası numarası**: Proxy sunucunuz tarafından kullanılan TCP bağlantı noktası numarasını girin
- **Yerel adresler için proxy atlama**: Yerel adresleriniz için proxy sunucusu kullanmak istemiyorsanız Etkinleştir'i seçin. VPN sunucunuz bağlantı için bir proxy sunucusu gerektiriyorsa, bu ayar uygulanır.

## <a name="split-tunneling"></a>Bölünmüş Tünel

- **Bölünmüş tünel**: Trafiğe bağlı olarak hangi bağlantının kullanılacağına cihazların karar vermesini sağlamak için bu seçeneği **Etkinleştirin** veya **Devre Dışı Bırakın**. Örneğin, oteldeki bir kullanıcı çalışma dosyalarına erişmek için VPN bağlantısını, web’e göz atmak için ise otelin standart ağını kullanır.
- **Bu VPN bağlantısının tünel oluşturma rotalarını ayırma**: Üçüncü taraf VPN sağlayıcıları için isteğe bağlı rotalar ekleyin. Her bağlantı için bir hedef ön eki ve ön ek boyutu girin.

## <a name="trusted-network-detection"></a>Güvenilen ağ algılama

**Güvenilen ağ DNS sonekleri**: kullanıcılar zaten güvenilen bir ağa bağlıyken CIHAZLARıN diğer VPN bağlantılarına otomatik olarak bağlanmasını engelleyebilirsiniz.

**DNS sonekleri**' nde, güvenmesini istediğiniz contoso.com gıbı bir DNS son eki girin ve **Ekle**' yi seçin. İstediğiniz sayıda sonek ekleyebilirsiniz.

Bir Kullanıcı listede bir DNS sonekine bağlıysa, Kullanıcı otomatik olarak başka bir VPN bağlantısına bağlanmaz. Kullanıcı, girdiğiniz DNS sonekleri güvenilen listesini kullanmaya devam eder. Güvenilir ağ, herhangi bir diğer tetikleyici ayarlanmış olsa bile kullanılmaya devam eder.

Örneğin, Kullanıcı zaten güvenilir bir DNS sonekine bağlandıysa, aşağıdaki yeniden Tetikleyiciler yok sayılır. Özellikle, listedeki DNS sonekleri, aşağıdakiler de dahil olmak üzere tüm diğer bağlantı oto tetikleyicilerini iptal eder:

- Her zaman açık
- Uygulama tabanlı tetikleyici
- DNS oto tetikleyicisi

## <a name="next-steps"></a>Sonraki adımlar

Profil oluşturulur ancak henüz herhangi bir işlem gerçekleştirmez. Sonra, [profili atayın](device-profile-assign.md)ve [durumunu izleyin](device-profile-monitor.md).

[Android](vpn-settings-android.md), [IOS/ıpados](vpn-settings-ios.md)ve [MacOS](vpn-settings-macos.md) cihazlarında VPN ayarlarını yapılandırın.
