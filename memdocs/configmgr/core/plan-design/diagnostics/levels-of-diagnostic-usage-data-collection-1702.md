---
title: 1702 için tanılama verileri
titleSuffix: Configuration Manager
description: Configuration Manager sürüm 1702 tarafından toplanan tanılama ve kullanım verilerinin düzeyleri hakkında bilgi edinin.
ms.date: 03/27/2017
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: reference
ms.assetid: d43ab033-2902-4681-8716-b4b17a6df372
author: aczechowski
ms.author: aaroncz
manager: dougeby
ROBOTS: NOINDEX
ms.openlocfilehash: c3859d77726b49973257da47233fedde28f705a1
ms.sourcegitcommit: fde92731a7e27c892d32c63f515cf19545e02ceb
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/27/2020
ms.locfileid: "88994829"
---
# <a name="levels-of-diagnostic-usage-data-collection-for-version-1702-of-configuration-manager"></a>Configuration Manager sürüm 1702 için tanılama kullanım verileri toplama düzeyleri

*Uygulama hedefi: Configuration Manager (geçerli dal)*

Configuration Manager sürüm 1702, üç düzeyde tanılama ve kullanım verisi toplar: **temel**, **Gelişmiş**ve **tam**. Varsayılan olarak, bu özellik Gelişmiş düzeye ayarlanmıştır. Aşağıdaki bölümler, her bir düzeyin topladığı veriler hakkında ek ayrıntılar sağlar.

Önceki sürümlerden yapılan değişiklikler ***[yeni]***, ***[güncelleştirildi]***, ***[kaldırıldı]*** veya ***[taşındı]*** ile belirtilmiştir.


> [!IMPORTANT]
>  Configuration Manager, temel veya gelişmiş düzeylerde site kodlarını, site adlarını, IP adreslerini, Kullanıcı adlarını, bilgisayar adlarını, fiziksel adresleri ya da e-posta adreslerini toplamaz. Bu bilgilerin tam düzeyinde toplanması, büyük olasılıkla günlük dosyaları veya bellek anlık görüntüleri gibi gelişmiş tanılama bilgilerine dahil değildir. Microsoft bu bilgileri sizi tanımlamak, sizinle iletişim kurmak veya reklam geliştirmek için kullanmaz.



##  <a name="how-to-change-the-level"></a><a name="bkmk_change"></a> Düzeyi değiştirme
 **Site** nesne sınıfında **değiştirme** izinlerini içeren rol tabanlı yönetim kapsamına sahip yöneticiler, Configuration Manager konsolundaki tanılama ve kullanım verileri ayarlarında toplanan veri düzeyini değiştirebilir.

**Yönetim**  >  **genel bakış**  >  **site yapılandırma**  >  **siteleri**' ne giderek veri toplama düzeyini konsolunun içinden değiştirirsiniz. **Hiyerarşi ayarları**' nı açın ve ardından kullanmak istediğiniz veri düzeyini seçin.  



##  <a name="level-1---basic"></a><a name="bkmk_level1"></a> Düzey 1 - Temel
Temel düzey, hiyerarşiniz hakkındaki verileri, yüklemenizin veya yükseltme deneyiminizin artırılmasına yardımcı olması gereken verileri ve hiyerarşiniz için geçerli Configuration Manager güncelleştirmelerinin belirlenmesine yardımcı olan verileri içerir.

Configuration Manager sürüm 1702 için, bu düzey aşağıdakileri içerir:

- Yönetici Konsolu:
   - Konsol bağlantıları (işletim sistemi sürümü, dil, SKU ve mimari, sistem belleği, mantıksal işlemci sayısı, bağlantı site KIMLIĞI, yüklü .NET sürümleri ve konsol dil paketleri) hakkında istatistikler

- Temel uygulama ve dağıtım türü sayıları (Toplam uygulama, birden çok dağıtım türüne sahip toplam uygulama, bağımlılıklara sahip toplam uygulama, yenisiyle değiştirilen Toplam uygulama sayısı ve kullanımdaki dağıtım teknolojilerinin sayısı)

- Temel Configuration Manager site hiyerarşisi verileri (site listesi, türü, sürümü, durumu, istemci sayısı ve saat dilimi)

- Temel veritabanı yapılandırması (işlemciler, küme yapılandırması ve dağıtılmış görünümlerin yapılandırması)

- ***[Güncelleştirilmiş]*** Sitenin tamamen Azure Active Directory hizmetleriyle çalıştığı zaman dahil olmak üzere temel bulma istatistikleri (bulma sayısı ve en düşük/en yüksek/ortalama Grup boyutları).

- Temel Endpoint Protection bilgileri (kötü amaçlı yazılımdan koruma istemci sürümleri)

- Temel işletim sistemi dağıtımı (OSD) sayıları (görüntüler)

- Temel site sistemi sunucusu bilgileri (kullanılan site sistemi rolleri, Internet ve SSL durumu, işletim sistemi, işlemciler, fiziksel veya sanal makine)

- Configuration Manager veritabanı şeması (tüm nesne tanımlarının karması)

- Yapılandırılan telemetri düzeyi, mod (çevrimiçi veya çevrimdışı) ve hızlı güncelleştirme yapılandırması

- İstemci dillerinin ve yerel ayarların sayısı

- Configuration Manager istemci sürümleri ve işletim sistemi sürümleri sayısı

- Exchange Connector tarafından ayarlanan yönetilen cihazlar ve ilkeler için işletim sistemi sayısı

- Dala ve derlemeye göre Windows 10 cihazlarının sayısı

- Veritabanı performans ölçümleri (çoğaltma işleme bilgileri, işlemciye göre en çok kullanılan SQL Server saklı yordamları ve disk kullanımı)

- Dağıtım noktası ve yönetim noktası türleri ile temel yapılandırma bilgileri (korumalı, önceden hazırlanan, PXE, çok noktaya yayın, SSL durumu, çekme/eş dağıtım noktaları, MDM etkin, SSL etkin, vb.)

- Kurulum bilgileri:
     - Yapı, install türü, dil paketleri, etkinleştirdiğiniz Özellikler   

     - Yayın öncesi kullanımı, kurulum medya türü, dal türü

     - Yazılım Güvencesi sona erme tarihi      

     - Güncelleştirme paketi dağıtım durumu ve hataları, İndirme ilerlemesi ve önkoşul hataları 

     - Güncelleştirme hızlı halkası kullanımı

     - Yükseltme sonrası betiği sürümü

- SQL sürümü, hizmet paketi düzeyi, sürüm, harmanlama KIMLIĞI ve karakter kümesi     
- Telemetri istatistikleri (çalışma sırasında, çalışma zamanı, hatalar)

- Ağ bulma kullanımı (etkin veya devre dışı)




##  <a name="level-2---enhanced"></a><a name="bkmk_level2"></a> Düzey 2 - Gelişmiş
Gelişmiş düzey, Kurulum bittikten sonra varsayılandır. Bu düzey, temel düzeyde ve özelliğe özgü veriler (kullanım sıklığı ve süresi), Configuration Manager istemci ayarları (bileşen adı, durumu ve yoklama aralıkları gibi belirli ayarlar) ile yazılım güncelleştirmeleri hakkındaki temel bilgiler içinde toplanan verileri içerir.

Bu düzey, Microsoft 'un, ürün ve hizmetlerin gelecekteki sürümlerinde yararlı geliştirmeler yapmak için gereken en düşük verileri sağladığı için önerilir. Bu düzey, nesne adlarını (siteler, kullanıcılar, bilgisayarlar veya nesneler), güvenlikle ilgili nesnelerin ayrıntılarını veya yazılım güncelleştirmesi gerektiren sistem sayısı gibi güvenlik açıklarını toplamaz.

Configuration Manager sürüm 1702 için, bu düzey aşağıdakileri içerir:

- **Uygulama Yönetimi:**  

   - Uygulama gereksinimleri (dağıtım teknolojisi ile yerleşik koşulların sayısına başvurulur)

   - Uygulama yerine geçme, en yüksek zincir derinliği

   - Uygulama onay istatistikleri ve kullanım sıklığı

   - ***[Güncelleştirilmiş]*** Uygulama dağıtım bilgileri (yükleme ve kaldırma karşılaştırması, onay, Kullanıcı etkileşimi etkin/devre dışı, bağımlılık, yenisiyle değiştirme ve yükleme davranışı özelliğinin kullanım sayısını gerektirir)  

   - Uygulama ilkesi boyutu ve karmaşıklık istatistikleri

   - Mevcut uygulama isteği istatistikleri

   - ***[Yeni]*** Paketler ve programlar için temel yapılandırma bilgileri (dağıtım seçenekleri ve program bayrakları)

   - Kuruluş içinde kullanılan dağıtım türleri için temel kullanım/hedefleme bilgileri (Kullanıcı ve cihaz hedefli, gerekli ve kullanılabilir ve evrensel uygulamalar)

   - Sınır grubu istatistikleri (kaç hızlı, kaç tane yavaş ve grup başına sayı)

   - App-V ortamları ve dağıtım özellikleri sayısı

   - İşletim sistemine göre uygulama uygulanabilirliği sayısı  

   - ***[Yeni]*** Bir görev dizisi tarafından başvurulan uygulama sayısı

   - Türe göre paket sayısı  

   - Paket/program dağıtımı sayısı  

   - Windows 10 lisanslı uygulama lisansı sayısı  

   - Iş uygulamaları için Windows Mağazası ve eşitleme istatistikleri (özetlenen uygulama türleri, lisanslanmış uygulama durumu ve çevrimiçi ve çevrimdışı lisanslanmış uygulama sayısı dahil)  

   - Bakım penceresi türü ve süresi  

   - Her zaman süresi içinde Kullanıcı/cihaz başına en düşük/en yüksek/ortalama uygulama dağıtımı sayısı

   - ***[Yeni]*** Dağıtım teknolojisine göre en sık kullanılan uygulama yükleme hatası kodları

   - MSI yapılandırma seçenekleri ve sayıları

   - ***[Yeni]*** Gerekli yazılım dağıtımları için bildirim ile son kullanıcı etkileşimi ile ilgili istatistikler   

   - Evrensel veri erişimi (UDA) kullanımı, nasıl oluşturulur




- **İstemcilerinin**  

   - Etkin yönetim teknolojisi (AMT) istemci sürümü

   - Yıl içinde BIOS yaşı

   - İstemci otomatik yükseltme: istemci pilolama ve dışlama kullanımı (genişletilmiş birlikte çalışabilirlik istemcisi) dahil dağıtım yapılandırması

   - İstemci önbellek boyutu yapılandırması

   - İstemci dağıtımı indirme hataları

   - İstemci sistem durumu istatistikleri ve en önemli sorun Özeti

   - İstemci bildirim işlemi eylem durumu (her birinin kaç kez çalıştığı, en fazla hedeflenen istemci sayısı ve ortalama başarı oranı)
   - Kaynak konum türlerinden gelen istemci yüklemelerinin sayısı  

   - İstemci yüklemesi hatalarının sayısı  

   - ***[Yeni]*** Hyper-V veya Azure tarafından sanallaştırılmış cihazların sayısı  

   - Yazılım Merkezi eylemlerinin sayısı   

   - ***[Yeni]*** UEFı özellikli cihazların sayısı

   - Dağıtım yöntemi başına istemci ve istemci sayısı için kullanılan dağıtım yöntemleri

   - Etkinleştirilmiş istemci aracıları listesi/sayısı  

   - Ay içinde işletim sistemi yaşı

   - Donanım envanteri sınıfları, yazılım envanteri kuralları ve dosya toplama kuralları sayısı

   - ***[Yeni]*** Çoğu yaygın hata kodu, şirket içi sunucu sayısı ve çeşitli durumlardaki cihaz sayısı dahil olmak üzere cihaz sistem durumu kanıtlama istatistikleri.



- **Cloud Services:**

  - Bulut Yönetimi Ağ Geçidi yapılandırma ve kullanım istatistikleri

  - ***[Yeni]*** Azure Active Directory hizmetlerine katılmış istemci sayısı

  - Operations Management Suite ile eşitlenen koleksiyonların sayısı

  - Upgrade Analytics Bağlayıcısı sayısı

  - Operations Management Suite Bulut bağlayıcısının etkin olup olmadığı




- **Koleksiyonlarıyla**

    - Koleksiyon KIMLIĞI kullanımı (kimlik dışı)

    - Koleksiyon değerlendirme istatistikleri (sorgu süresi, atanan ve atanmamış sayımlar, türe göre sayılar, KIMLIK geçişi ve kural kullanımı)

    - Dağıtım olmadan Koleksiyonlar




- **Uyumluluk ayarları:**  

    - Temel yapılandırma temeli bilgileri (sayısı, dağıtım sayısı ve başvuru sayısı)  

    - Türe göre yapılandırma öğesi sayısı  

    - Yerleşik ayarlara başvuran dağıtımların sayısı (Şu anda düzeltme ayarları)  

    - Özel ayarlar için oluşturulan kuralların ve dağıtımların sayısı (Şimdi, düzeltme için yakalama)  
    -  Dağıtılan Basit Sertifika Kayıt Protokolü (SCEP), VPN, Wi-Fi, sertifika (. pfx) ve uyumluluk Ilkesi şablonlarının sayısı

    - Platforma göre SCEP sertifikası, VPN, Wi-Fi, sertifika (. pfx) ve uyumluluk Ilkesi dağıtımları sayısı

    - Iş için Passport ilkesi (oluşturuldu, dağıtıldı)



- **İçeriði**  

    - Sınır grubu bilgileri (her sınır grubuna atanan sınır ve site sistemi sayısı)  

    - Sınır grubu ilişkileri ve geri dönüş yapılandırması

    - İstemci içeriği indirme istatistikleri

    - Türe göre sınır sayısı  

    - Eş önbellek istemcisi sayısı ve kullanım istatistikleri

    - Dağıtım Yöneticisi yapılandırma bilgileri (iş parçacıkları, yeniden deneme gecikmesi, yeniden deneme sayısı ve istek temelli dağıtım noktası ayarları)  

    - Dağıtım noktası yapılandırma bilgileri (dal önbelleği ve dağıtım noktası izlemenin kullanımı)

    - Dağıtım noktası grubu bilgileri (her dağıtım noktası grubuna atanan paket ve dağıtım noktası sayısı)  



- **Endpoint Protection:**  

   - Gelişmiş tehdit koruması (ATP) Ilkeleri (ilke sayısı ve ilkelerin dağıtılıp dağıtılmayacağı)

   - Endpoint Protection özelliği için yapılandırılmış uyarı sayısı  

   - Endpoint Protection panosunda görünmesi için seçilen koleksiyon sayısı  

   - Endpoint Protection dağıtım hataları (Endpoint Protection İlkesi dağıtımı hata kodlarının sayısı)  

   - Kötü amaçlı yazılımdan koruma ve Windows Güvenlik Duvarı İlkesi kullanımını Endpoint Protection (gruba atanan benzersiz ilkelerin sayısı)<br /><br /> Bu, ilkede yer alan ayarlarla ilgili herhangi bir bilgi içermez.  



- **Geçiş**

  - Geçirilen nesne sayısı (geçiş sihirbazının kullanımı)



- **Mobil cihaz yönetimi (MDM):**  

    - Verilen mobil cihaz eylemlerinin sayısı: kilitleme, PIN Rest, Temizleme, devre dışı bırakma ve şimdi eşitleme komutları

    - Mobil cihaz ilke sayısı  

    - Configuration Manager ve Microsoft Intune tarafından yönetilen mobil cihaz sayısı ve nasıl kaydedildikleri (toplu, Kullanıcı tabanlı)  

    - Birden çok kayıtlı mobil cihazı olan kullanıcı sayısı  

    - Mobil cihaz yoklama zamanlaması ve mobil cihaz iade süresi istatistikleri  




- **Microsoft Intune sorun giderme:**

    - Microsoft Intune çoğaltılan cihaz eylemlerinin sayısı ve boyutu (silme, devre dışı bırakma, kilitleme), telemetri ve veri iletileri

    - Microsoft Intune 'ten indirilen durum, durum, envanter, RDR, DDR, UDX, kiracı durumu, POL, LOG, CERT, CRP, yeniden eşitleme, CFD, RDO, BEX, ıSM ve uyumluluk iletilerinin sayısı ve boyutu

    - Microsoft Intune için tam ve Delta Kullanıcı eşitleme istatistikleri



- **Şirket içi mobil cihaz yönetimi (MDM):**  

    - Windows 10 toplu kayıt paketleri ve profillerinin sayısı  

    - Şirket içi MDM uygulama dağıtımları için dağıtım başarı/hata istatistikleri  




- **İşletim sistemi dağıtımı:**  

    - Önyükleme görüntüleri, sürücüler, sürücü paketleri, çok noktaya yayını destekleyen dağıtım noktaları, PXE özellikli dağıtım noktaları ve görev dizileri sayısı  

    - Sürüm yükseltme ilkelerinin sayısı

    - Görev dizisi adım kullanım sayısı



- **Site güncelleştirmeleri:**

    - Yüklü Configuration Manager düzeltmelerinin sürümleri



- **Yazılım güncelleştirmeleri:**  

    - Otomatik dağıtım kurallarında kullanılan kullanılabilir ve son tarih değişimleri  

    - Güncelleştirme başına ortalama ve en yüksek atama sayısı  

    - İstemci güncelleştirme değerlendirmesi ve tarama zaman çizelgeleri  

    - Yazılım güncelleştirme noktası tarafından eşitlenen sınıflandırmalar

    - Küme düzeltme eki uygulama istatistikleri  

    - Windows 10 Express güncelleştirmelerinin yapılandırması

    - Etkin Windows 10 bakım planları için kullanılan konfigürasyonlar  

    - Dağıtılan Microsoft 365 güncelleştirme sayısı  

    - Güncelleştirme grupları ve atamalarının sayısı  

    - Güncelleştirme paketi sayısı ve paketlerle hedeflenen dağıtım noktalarının en yüksek/en düşük/ortalama sayısı  

    - System Center Update Publisher ile oluşturulan ve dağıtılan güncelleştirmelerin sayısı  

    - Iş için Windows Update kullanan Windows 10 istemcileri sayısı  

    - Eşitlemeye bağlı otomatik dağıtım kuralları sayısı  

    - Yeni bir grup oluşturan veya mevcut bir gruba güncelleştirme ekleyen otomatik dağıtım kuralları sayısı  

    - Birden çok dağıtıma sahip otomatik dağıtım kuralları sayısı  
    - Güncelleştirme grubu sayısı ve güncelleştirme grubu başına en düşük/en yüksek/ortalama güncelleştirme sayısı  

    - Dağıtılan, zaman aşımına geçilen, yenisiyle değiştirilen, indirilen ve EULA 'Lar içeren güncelleştirmelerin güncelleştirme sayısı ve yüzdesi  

    - Yazılım güncelleştirme noktası yük dengeleme istatistikleri

    - Yazılım güncelleştirme noktası eşitleme zaman çizelgesi  

    - Yazılım güncelleştirme dağıtımları olan koleksiyonların toplam/ortalama sayısı ve dağıtılan güncelleştirmelerin en yüksek/ortalama sayısı  

    - Güncelleştirme taraması hata kodları ve makine sayısı  

    - Windows 10 panosu içerik sürümleri  



- **SQL/performans verileri:**  

    - ***[Yeni]*** Site özetlemesinin yapılandırması ve süresi

    - En büyük veritabanı tablolarının sayısı  

    - Bulgu işlem istatistikleri (bulunan nesne sayısı)

    - Bulma türleri, etkin ve zamanlama (tam, artımlı)

    - SQL AlwaysOn çoğaltma bilgileri, kullanımı ve sistem durumu

    - SQL değişiklik izleme performansı sorunları, saklama süresi ve otomatik temizleme durumu

    - SQL değişiklik izleme tutma süresi

    - ***[Yeni]*** En yaygın ve en pahalı ileti türlerini içeren durum ve durum iletisi performans istatistikleri



- **Çeşitli**

    - ***[Yeni]*** Eşitleme zamanlaması ve ortalama süre dahil olmak üzere veri ambarı hizmet noktası yapılandırması

    - LAN 'da uyandırma (WOL) ile site sayısı

    - Raporlama kullanımı ve performans istatistikleri  



##  <a name="level-3---full"></a><a name="bkmk_level3"></a> Düzey 3 - Tam
Tam düzey, temel ve gelişmiş düzeylerdeki tüm verileri içerir. Aynı zamanda Uç Nokta Koruma, güncelleştirme uyumluluğu yüzdeleri ve yazılım güncelleştirme bilgileri hakkında ek bilgiler de içerir.  Bu düzey, yakalama sırasında bellekte veya günlük dosyalarında bulunan kişisel bilgileri içerebilen sistem dosyaları ve bellek anlık görüntüleri gibi gelişmiş tanı bilgilerini de içerebilir.

Configuration Manager sürüm 1702 için, bu düzey aşağıdakileri içerir:

- Otomatik dağıtım kuralı değerlendirmesi zaman çizelgesi bilgileri

- ATP sistem durumu Özeti

- Koleksiyon değerlendirme ve yenileme istatistikleri

- Uyumluluk ayarları: SCEP, VPN, Wi-Fi ve uyumluluk Ilkesi şablonu yapılandırma ayrıntıları, zaman aşımına uğradı yazılım güncelleştirmeleri olan grupların sayısı

- Configuration Manager kullanımı için DCM yapılandırma paketi

- Ayrıntılı istemci dağıtımı yükleme hataları
- Uç Nokta Koruma durum özeti (korunan, risk altında olan, bilinmeyen ve desteklenmeyen istemci sayısı dahil)

- Uç Nokta Koruma ilkesi yapılandırma

- ***[Yeni]*** Uygulamalar için yükleme davranışı ile yapılandırılan işlemlerin listesi

- Son güncelleştirmeden bu yana geçen en düşük/en yüksek/ortalama saat sayısı

- Yazılım güncelleştirme dağıtımı koleksiyonlarında etkin olmayan istemcilerin en düşük/en yüksek/ortalama sayısı

- Yazılım güncelleştirmelerinin paket başına en düşük/en yüksek/ortalama sayısı

- MSI ürün kodu (müşterilerin dağıtabolduğu ortak uygulamalar)

- Yazılım güncelleştirme dağıtımlarının genel uyumluluğu

- Yazılım güncelleştirme dağıtımı hata kodları ve sayısı

- Yazılım güncelleştirme dağıtım bilgileri (istemci ile UTC zamanına göre hedeflenen dağıtım yüzdesi, gerekli ve isteğe bağlı ve sessiz ve yeniden başlatma gizleme)

- Yazılım güncelleştirme noktası tarafından eşitlenen yazılım güncelleştirme ürünleri

- Yazılım güncelleştirme taraması başarı yüzdeleri

- Ortamda en iyi 50 CPU

- Intune tarafından yönetilen cihazlar için EAS koşullu erişim ilkelerinin (blok veya karantina) türü

- Iş için Windows Mağazası uygulama ayrıntıları (AppID, çevrimiçi durum veya çevrimdışı durum ve toplam satın alınan lisans sayısı dahil eşitlenmiş uygulamaların toplama olmayan listesi)
