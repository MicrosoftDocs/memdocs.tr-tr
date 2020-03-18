---
title: Windows bilgisayarları için Endpoint Protection
titleSuffix: Microsoft Intune
description: Kötü amaçlı yazılım tehditlerine karşı gerçek zamanlı koruma sağlayan Endpoint Protection ile yönetilen bilgisayarlarınızın güvenliğini koruyun.
keywords: ''
author: dougeby
ms.author: dougeby
manager: dougeby
ms.date: 11/12/2019
ms.topic: archived
ms.service: microsoft-intune
ms.subservice: fundamentals
ms.localizationpriority: medium
ms.technology: ''
ms.assetid: 002241bf-6cd0-4c75-a4f0-891ac7e6721a
ms.reviewer: damionw
ms.suite: ems
search.appverid: MET150
ms.custom: intune-classic-keep
ms.collection: M365-identity-device-management
ms.openlocfilehash: 8c5a0a1405ceda93317dbefa6d80ec24cc0156bb
ms.sourcegitcommit: 3d895be2844bda2177c2c85dc2f09612a1be5490
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/13/2020
ms.locfileid: "79332482"
---
# <a name="help-secure-windows-pcs-with-endpoint-protection-for-microsoft-intune"></a>Microsoft Intune için Endpoint Protection ile Windows bilgisayarların korunmasına yardımcı olma

[!INCLUDE [classic-portal](../includes/classic-portal.md)]

Microsoft Intune, kötü amaçlı yazılım tehditlerine karşı gerçek zamanlı koruma sağlayan, kötü amaçlı yazılım tanımlarını güncel tutan ve bilgisayarları otomatik olarak tarayan Endpoint Protection ile yönetilen bilgisayarlarınızın korunmasına yardımcı olabilir. Endpoint Protection, kötü amaçlı yazılım saldırılarını yönetmek ve izlemek için yardımcı araçlar da sağlar.

Intune istemcisini bilgisayarlarınıza henüz yüklemediyseniz, bkz. [Microsoft Intune ile Windows bilgisayarı istemcisini yükleme](install-the-windows-pc-client-with-microsoft-intune.md).

Aşağıdaki bölümlerde yer alan bilgiler, Endpoint Protection’ı yapılandırmanıza, dağıtmanıza ve izlemenize yardımcı olur.

## <a name="choose-when-to-use-endpoint-protection"></a>Endpoint Protection’ın ne zaman kullanılacağını seçme
Bir BT yöneticisi olarak en önemli önceliklerinizden biri, yönettiğiniz bilgisayarlara kötü amaçlı yazılım ve virüs bulaşmasını engellemektir. Windows bilgisayarlara Intune’u dağıtmadan önce, aşağıdaki seçeneklerden birini seçerek ve ilişkili ilke ayarlarını yapılandırarak bilgisayarların güvenliğini nasıl koruyacağınıza karar vermeniz gerekir:


|                                                                                                                                                                       Şunları yapmak istiyorsunuz:                                                                                                                                                                        |                                                                                                       Endpoint Protection ilke ayarları                                                                                                        |                                                                                                                                                  Daha fazla bilgi                                                                                                                                                  |
|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
|                                             Ancak bir üçüncü taraf uç noktası koruma uygulaması yüklenmediyse, Microsoft Intune Endpoint Protection’ı kullanma<br /><br />Microsoft Intune Endpoint Protection’ı, bir üçüncü taraf uç nokta koruma uygulaması yüklü olmayan tüm bilgisayarlarda kullanabilirsiniz.                                              | Endpoint Protection Yükle = <strong>Evet</strong><br /><br />Endpoint Protection'ı Etkinleştir = <strong>Evet</strong><br /><br />Bir üçüncü taraf uç nokta koruma uygulaması yüklü olsa bile Endpoint Protection yükle = <strong>Hayır</strong>  |                                                                      Bir üçüncü taraf uç nokta koruma uygulaması algılanırsa Microsoft Intune Endpoint Protection yüklenmez ve daha önce yüklenmişse kaldırılır.                                                                       |
| Bir üçüncü taraf uç noktası koruma uygulaması yüklenmiş olsa bile, Microsoft Intune Endpoint Protection’ı kullanabilirsiniz.<br /><br />Bu yaklaşımda, Microsoft Intune Endpoint Protection’ı ve üçüncü taraf uç nokta koruma uygulamasını aynı anda çalıştırırsınız. Olası performans sorunları nedeniyle bu yapılandırma önerilmez. | Endpoint Protection Yükle = <strong>Evet</strong><br /><br />Endpoint Protection'ı Etkinleştir = <strong>Evet</strong><br /><br />Bir üçüncü taraf uç nokta koruma uygulaması yüklü olsa bile Endpoint Protection yükle = <strong>Evet</strong> |                        Şu durumlarda kullanın:<br /><br />-   Microsoft Intune Endpoint Protection’ı kullanmaya geçmek istiyorsunuz.<br />-   Microsoft Intune Endpoint Protection’ı kullanacak yeni bir istemci dağıttınız.<br />-   Tüm istemcileri Microsoft Intune Endpoint Protection’ı kullanacak şekilde yükseltiyorsunuz.                         |
|                                                                                                             Intune’u Microsoft Intune Endpoint Protection olmadan kullanma. Bunun yerine, bir üçüncü taraf uç nokta koruma uygulamasına güvenirsiniz.                                                                                                             |                                                                                                Endpoint Protection Yükle = <strong>Hayır</strong>                                                                                                 | Bir üçüncü taraf uç nokta koruma uygulaması kullanmıyorsanız, kuruluşunuzdaki bilgisayarları kötü amaçlı yazılım veya diğer saldırılara maruz bırakabileceğinden bu yapılandırma önerilmez.<br /><br />Microsoft Intune Endpoint Protection yüklenmez ve daha önce yüklenmişse kaldırılır. |

Geçerli uç nokta koruma uygulamanızdan Microsoft Intune Endpoint Protection’a geçmek için aşağıdakileri yapın:

1. Intune istemci yazılımını bu bilgisayarlara dağıtırken geçerli uç nokta koruma uygulamasını çalışır durumda bırakın.

2. Microsoft Intune Endpoint Protection’ın yüklendiğini ve istemci bilgisayarların güvenliğini sağlamaya yardımcı olduğunu doğrulayın.

3. Üçüncü taraf uç nokta koruma yazılımını şu yolla kaldırın:

    - Intune yazılım dağıtım özelliğini kullanarak, üçüncü taraf uç nokta koruma uygulaması üreticisi tarafından sağlanan yazılım kaldırma aracını dağıtın. Daha fazla bilgi için bkz. [Microsoft Intune ile uygulamaları dağıtma](../apps/apps-deploy.md).

    - Üçüncü taraf uç nokta koruma uygulamasını el ile kaldırma.

> [!NOTE]
> Intune, üçüncü taraf uç nokta koruma uygulamalarını otomatik olarak kaldırmaz.

## <a name="configure-microsoft-intune-endpoint-protection"></a>Microsoft Intune Endpoint Protection’ı yapılandırma
Aşağıdaki adımlar, Microsoft Intune için Endpoint Protection’ı yapılandırmada size yardımcı olacaktır.

1. [Microsoft Intune yönetim konsolunda](https://manage.microsoft.com/)**İlke** > **İlke Ekle**’yi seçin.

2. **Bilgisayar Yönetimi**’ni genişletin ve **Microsoft Intune Aracısı Ayarları**’nı seçin. Endpoint Protection ayarlarına yönelik ilke belirtmek için **Özel İlke Oluştur ve Dağıt**’ı seçin. Ardından **İlke Oluştur** düğmesini seçin.

Önerilen ayarları kullanabilir veya ayarları özelleştirebilirsiniz. İlke oluşturma ve dağıtma hakkında daha fazla bilgiye ihtiyacınız olursa, [Microsoft Intune bilgisayar istemcisi ile genel Windows bilgisayarları yönetim görevleri](common-windows-pc-management-tasks-with-the-microsoft-intune-computer-client.md) konusuna bakın.

  ![Endpoint Protection ayarları](./media/help-secure-windows-pcs-with-endpoint-protection-for-microsoft-intune/pol-sa-pc-endpoint-policy.png)

Dağıtılan Endpoint Protection ilkesini, **İlke** çalışma alanının **Tüm İlkeler** sayfasında görüntüleyebilirsiniz.

## <a name="specify-endpoint-protection-service-settings"></a>Endpoint Protection hizmet ayarlarını belirtin

|                                                 İlke ayarı                                                  |                                                                                                                                                                                                                                                                                                                                                                                                             Ayrıntılar                                                                                                                                                                                                                                                                                                                                                                                                             |
|-----------------------------------------------------------------------------------------------------------------|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
|                                  <strong>Endpoint Protection'ı yükleme</strong>                                   | Endpoint Protection’ı yönetilen bilgisayarlarda yüklemek için <strong>Evet</strong> olarak ayarlayın. Yükleme sırasında bir üçüncü taraf uç nokta koruma uygulaması algılanırsa, <strong>Bir üçüncü taraf uç nokta koruma uygulaması yüklü olsa bile Endpoint Protection’ı yükle</strong> ayarı <strong>Evet</strong> olarak ayarlanmadığı sürece Endpoint Protection yüklenmez. <strong>Not:</strong> Intune Endpoint Protection, yönetilen bilgisayarlara varsayılan olarak yüklenir. Yönetilen bilgisayarlarınıza Endpoint Protection yüklemek istemiyorsanız, bu ilkeyi açıkça <strong>Hayır</strong> olarak ayarlamalısınız. Endpoint Protection önceden yüklenmişse ve ilke <strong>Hayır</strong> olarak güncelleştirilirse, Endpoint Protection istemcisi kaldırılır.<br />Önerilen değer: <strong>Evet</strong> |
| <strong>Bir üçüncü taraf uç nokta koruma uygulaması yüklü olsa bile Endpoint Protection’ı yükleme</strong> |                                                                                                                                                                                                                                                                                                                Üçüncü taraf uç nokta uygulaması algılansa bile Microsoft Intune Endpoint Protection’ı yüklemek için <strong>Evet</strong> olarak ayarlayın.<br /><br />Önerilen değer: <strong>Evet</strong>                                                                                                                                                                                                                                                                                                                |
|                                   <strong>Endpoint Protection'ı etkinleştir</strong>                                   |                                                                                                                                                                                                            Endpoint Protection istemcisinin bulunduğu bilgisayarlarda Microsoft Intune Endpoint Protection’ı etkinleştirmek için <strong>Evet</strong> olarak ayarlayın.<br /><br /><strong>Hayır</strong> olarak ayarlanırsa ve Microsoft Intune Endpoint Protection yüklüyse, Endpoint Protection istemcisi kullanıcı arabirimi, kullanıcılara gösterilmez ve tüm koruma özellikleri devre dışı kalır.<br /><br />Önerilen değer: <strong>Evet</strong>                                                                                                                                                                                                             |
|                                       <strong>İstemci Kullanıcı Arabirimi'ni devre dışı bırak</strong>                                        |                                                                                                                                                                                                                                                                                                      Microsoft Intune Endpoint Protection istemcisinin kullanıcı arabirimini kullanıcılardan gizlemek için <strong>Evet</strong> olarak ayarlayın (geçerlilik kazanması için istemci bilgisayarın yeniden başlatılması gerekir).<br /><br />Önerilen değer: <strong>Hayır</strong>                                                                                                                                                                                                                                                                                                       |
| <strong>Bir üçüncü taraf uç nokta koruma uygulaması yüklü olsa bile Endpoint Protection’ı yükleme</strong> |                                                                                                                                                                                                                                                                                                       Üçüncü taraf uç nokta uygulaması algılansa bile Microsoft Intune Endpoint Protection’ın yüklenmesini zorunlu tutmak için <strong>Evet</strong> olarak ayarlayın.<br /><br />Önerilen değer: <strong>Hayır</strong>                                                                                                                                                                                                                                                                                                       |
|                    <strong>Kötü amaçlı yazılım düzeltme işleminden önce sistem geri yükleme noktası oluştur</strong>                    |                                                                                                                                                                                                                                                                                                                                 Herhangi bir kötü amaçlı yazılım düzeltme işlemi başlamadan önce Windows Sistem Geri Yükleme Noktası oluşturmak için <strong>Evet</strong> olarak ayarlayın.<br /><br />Önerilen değer: <strong>Evet</strong>                                                                                                                                                                                                                                                                                                                                  |
|                                 <strong>Çözümlenen kötü amaçlı yazılımları izle (gün)</strong>                                  |                                                                                                                                                                                                                                                                                      Daha önce etkilenen bilgisayarları el ile denetleyebilmeniz için Endpoint Protection’ın çözümlenen kötü amaçlı yazılımları belirli bir süre izlemesine olanak sağlar.<br /><br />0 ile 30 gün arasında bir değer belirtebilirsiniz.<br /><br />Önerilen değer: <strong>7 gün</strong>                                                                                                                                                                                                                                                                                       |

**Endpoint Protection'ı Yükle** ve **Endpoint Protection'ı Etkinleştir** ayarları için ilke değerlerini **Evet** olarak, **Bir üçüncü taraf uç nokta koruma uygulaması yüklü olsa bile Endpoint Protection’ı yükle** ilke ayarını **Hayır** olarak ayarladıysanız, Microsoft Intune Endpoint Protection başka bir uç nokta koruma uygulamasının yüklü olduğunu algılar. Bu, Endpoint Protection’ın yüklenmeyeceği veya zaten yüklüyse kaldırılacağı anlamına gelir. Bununla birlikte, Microsoft Intune Endpoint Protection, Intune’daki diğer uç nokta koruma uygulamasının durumu hakkında bildirimde bulunur.

  Virüsler ve casus yazılımlar gibi olası tehditler, kendilerini bilgisayarınıza yüklemeyi veya çalıştırmayı denediklerinde Microsoft Security Essentials sizi gerçek zamanlı koruma ile uyarır. Böyle bir durum olduğu anda, görev çubuğunun sağ tarafındaki bildirim alanında bir ileti görürsünüz.

### <a name="specify-real-time-protection-settings"></a>Gerçek zamanlı koruma ayarlarını belirtin

|İlke ayarı|Ayrıntılar|
|------------------|--------------------|
|**Gerçek zamanlı korumayı etkinleştir**|Erişilen tüm dosya ve uygulamaların izlenmesini ve taranmasını sağlar. Ayrıca, herhangi bir kötü amaçlı dosya ve uygulamayı da bilgisayarlarda çalıştırılmadan önce engeller.<br /><br />Önerilen değer: **Evet**|
|**Tüm indirmeleri tara**|İnternet'ten bilgisayarlara indirilen tüm dosya ve eklerin taranmasını sağlar.<br /><br />Önerilen değer: **Evet**|
|**Bilgisayarlarda dosya ve program etkinliğini izle**|Bilgisayarlarda gelen ve giden dosyaların yanı sıra program etkinliğinin izlenmesini sağlar. Bu ayarla, dosyalar ve programlar çalışmaya başladığında Endpoint Protection bunları izleyebilir ve gerçekleştirdikleri herhangi bir eylem veya bunlar üzerinde gerçekleştirilen eylemler hakkında sizi uyarır.<br /><br />Önerilen değer: **Evet**|
|**İzlenen dosyalar**|Yalnızca gelen, yalnızca giden veya tüm dosyaların izlenmesi arasında seçim yapmanızı sağlar.<br /><br />Önerilen değer: **Tüm dosyaları izle**|
|**Davranış izlemeyi etkinleştir**|Microsoft Intune Endpoint Protection’ın istemci bilgisayarlarda belirli şüpheli etkinlik düzenlerini denetlemesini etkinleştirir.<br /><br />Önerilen değer: **Evet**|
|**Ağ İnceleme Sistemi'ni Etkinleştir**|İstemci bilgisayarlarda Ağ Denetleme Sistemi'ni (NIS) etkinleştirir. NIS, kötü amaçlı ağ trafiğin algılanmasına ve engellenmesine yardımcı olmak üzere, [Microsoft Kötü Amaçlı Yazılımdan Koruma Merkezi](https://go.microsoft.com/fwlink/?LinkId=234249) 'nden edinilen bilinen açıklara yönelik imzaları kullanır.<br /><br />Önerilen değer: **Evet**|

  ![Endpoint Protection’ın gerçek zamanlı çalışma ayarları](./media/help-secure-windows-pcs-with-endpoint-protection-for-microsoft-intune/pol-sa-pc-policy-realtime.png)

### <a name="specify-scan-schedule-settings"></a>Tarama zamanlaması ayarlarını belirtin

|İlke ayarı|Daha fazla bilgi|
|------------------|--------------------|
|**Günlük hızlı tarama zamanla**|Bilgisayarlarda hem sık kullanılan dosyalara hem de önemli sistem dosyalarına yönelik bir günlük hızlı tarama zamanlar. Bu hızlı taramanın performans üzerindeki etkisi çok azdır.<br /><br />Önerilen değer: **Evet**|
|**Arka arkaya iki tarama kaçırıldığında bir hızlı tarama çalıştır**|Endpoint Protection’ı, arka arkaya iki hızlı taramanın kaçırılması durumunda bilgisayarlarda otomatik olarak bir hızlı tarama çalıştıracak biçimde yapılandırır.<br /><br />Önerilen değer: **Evet**|
|**Tam tarama zamanla**|Bilgisayarların yerel sabit disklerdeki tüm dosyalara ve kaynaklara yönelik tam tarama yapılandırır. Bu tarama zaman alabilir ve bilgisayar performansını etkileyebilir (bu süre, taranan dosya ve kaynakların sayısına bağlıdır).<br /><br />Önerilen değer: **Hayır**|
|**Arka arkaya iki tam tarama kaçırıldığında bir tam tarama çalıştır**|Endpoint Protection’ı, arka arkaya iki taramanın kaçırılması durumunda bilgisayarlarda otomatik olarak bir tam tarama çalıştıracak biçimde yapılandırır.<br /><br />Önerilen değer: Yapılandırılmadı|

### <a name="specify-scan-options-settings"></a>Tarama seçenekleri ayarlarını belirtin

|İlke ayarı|Ayrıntılar|
|------------------|--------------------|
|**Endpoint Protection yüklendikten sonra bir tam tarama çalıştır**|Endpoint Protection’ın bilgisayarlara yüklendikten sonra otomatik tam sistem taraması çalıştırması için **Evet**’i seçin. Bu tarama, kullanıcı üretkenliğine olan etkiyi en aza indirmek için yalnızca bilgisayarlar boştayken çalıştırılır.<br /><br />Önerilen değer: **Evet**|
|**Gerektiğinde, kötü amaçlı yazılım kaldırma işleminin ardından otomatik olarak bir tam tarama çalıştır**|Endpoint Protection’ın kötü amaçlı yazılım kaldırıldıktan sonra diğer dosyaların etkilenmediğini doğrulamak için bilgisayarlarda otomatik olarak tam tarama çalıştırmasına izin vermek için **Evet** olarak ayarlayın.<br /><br />Önerilen değer: **Evet**|
|**Zamanlanmış bir taramayı yalnızca bilgisayar boşta olduğunda başlat**|Herhangi bir kullanıcı üretkenlik kaybını önlemek amacıyla, zamanlanmış taramaların bilgisayarlar kullanımdayken başlatılmasını önlemek için **Evet** olarak ayarlayın.<br /><br />Önerilen değer: **Evet**|
|**Bir tarama başlatmadan önce en son kötü amaçlı yazılım tanımlarını denetle**|Endpoint Protection’ın bilgisayarlarda bir tarama başlatmadan önce otomatik olarak en son kötü amaçlı yazılım tanımlarını denetlemesine izin vermek için **Evet** olarak ayarlayın.<br /><br />Önerilen değer: **Evet**|
|**Arşiv dosyalarını tara**|Endpoint Protection’ı, bilgisayarlardaki arşiv dosyalarında (.zip veya .cab dosyaları gibi) kötü amaçlı yazılım taraması gerçekleştirecek biçimde yapılandırmak için **Evet** olarak ayarlayın.<br /><br />Önerilen değer: **Hayır**|
|**E-posta iletilerini tara**|Endpoint Protection’ı, bilgisayarlara gelen e-posta iletilerini tarayacak biçimde yapılandırmak için **Evet** olarak ayarlayın.<br /><br />Önerilen değer: **Evet**|
|**Paylaşılan ağ klasörlerinden açılan dosyaları tara**|Endpoint Protection’ı, ağda paylaşılan klasörlerden açılan dosyaları tarayacak biçimde yapılandırmak için **Evet** olarak ayarlayın. Bunlar genellikle bir Evrensel Adlandırma Kuralı (UNC) yolu kullanılarak erişilen dosyalardır. Bu özelliği etkinleştirmek, salt okunur erişime sahip olduğundan kötü amaçlı yazılımları kaldıramayan kullanıcılar için sorunlara neden olabilir.<br /><br />Önerilen değer: **Hayır**|
|**Eşlenen ağ sürücülerini tara**|Endpoint Protection’ı, eşlenen ağ sürücülerindeki dosyaları tarayacak biçimde yapılandırmak için **Evet** olarak ayarlayın. Bu özelliği etkinleştirmek, salt okunur erişime sahip olduğundan kötü amaçlı yazılımları kaldıramayan kullanıcılar için sorunlara neden olabilir.<br /><br />Önerilen değer: **Hayır**|
|**Çıkarılabilir sürücüleri tara**|Bilgisayarlarda tam tarama çalıştırdığınızda, Endpoint Protection’ı USB flash sürücü gibi çıkarılabilir sürücülerde kötü amaçlı yazılım ve istenmeyen yazılım taraması gerçekleştirecek biçimde yapılandırmak için **Evet** olarak ayarlayın.<br /><br />Önerilen değer: **Evet**|
|**Tarama sırasında CPU kullanımını sınırla**|Bilgisayarlarda gerçekleştirilen zamanlanmış taramalar sırasında kullanılacak en fazla CPU yüzdesini ayarlayın. Bunu, %1 ile %100 arasında bir değer olarak ayarlayabilirsiniz.<br /><br />Önerilen değer: **%50**|

### <a name="choose-default-actions-settings"></a>Varsayılan eylemler ayarlarını seçme

**Endpoint Protection’ın şu uyarı düzeylerindeki kötü amaçlı yazılımları nasıl ele alacağını seçin** ayarı, çeşitli uyarı düzeylerinde kötü amaçlı yazılım algılandığında Endpoint Protection’ın gerçekleştireceği varsayılan eylemi belirtir. Her uyarı düzeyi için kötü amaçlı yazılımı kaldırma, karantinaya alma veya Microsoft'un önerdiği eylemi gerçekleştirme seçeneğiniz vardır.

Önerilen değer: Endpoint Protection’ın eylem önermesine olanak sağlayan **önerilen eylem**.   

### <a name="decide-whether-to-choose-the-excluded-files-and-folders-settings"></a>Dışlanan dosya ve klasörler ayarlarını seçip seçmeyeceğinize karar verin

**Tarama çalışırken veya gerçek zamanlı koruma dışlanan dosya ve klasörler** ayarı, bilgisayarlarda tarama çalıştırıldığında veya gerçek zamanlı koruma kullanıldığında belirli dosyaları veya klasörleri işlemin dışında tutar.

### <a name="decide-whether-to-choose-the-excluded-processes-settings"></a>Dışlanan işlemler ayarlarını seçip seçmeyeceğinize karar verme

**Bir tarama çalıştırılırken veya gerçek zamanlı koruma kullanılırken dışlanacak işlemler** ayarı, bilgisayarlarda tarama çalıştırıldığında veya gerçek zamanlı koruma kullanıldığında belirli işlemleri dışlamanızı sağlar. Yalnızca şu uzantılara sahip dosyaları dışlayabilirsiniz: **.exe**, **.com** veya **.scr**.

### <a name="decide-whether-to-choose-the-excluded-file-types-settings"></a>Dışlanan dosya türleri ayarlarını seçip seçmeyeceğinize karar verme

**Bir tarama çalıştırılırken veya gerçek zamanlı koruma kullanılırken dışlanacak dosya uzantıları** ayarı, bilgisayarlarda tarama çalıştırıldığında veya gerçek zamanlı koruma kullanıldığında belirli dosya adı uzantılarını dışlamanızı sağlar.

### <a name="specify-microsoft-active-protection-service-settings"></a>Microsoft Etkin Koruma Hizmeti Ayarlarını belirtin
Microsoft Etkin Koruma Hizmeti, olası risklere nasıl yanıt vereceğinize karar vermenize yardımcı olan çevrimiçi bir topluluktur. Topluluk, yeni kötü amaçlı yazılımların yayılmasını engellemeye de yardımcı olur. **Evet**’i seçerek ve ardından **Üyelik Düzeyinizi** belirterek **Microsoft Etkin Koruma Hizmeti’ne katılabilirsiniz**:
- **Temel** - Algılanan kötü amaçlı yazılımla ilgili temel bilgileri Microsoft'a gönderir. Bu bilgiler yazılımın nereden geldiği, uyguladığınız eylemler veya Endpoint Protection tarafından otomatik olarak uygulanan eylemler ve bunların başarılı olup olmadığını içerir.
- **Gelişmiş** - Kötü amaçlı yazılım, casus yazılım ve olası istenmeyen yazılım hakkında Microsoft'a daha fazla bilgi gönderir. Bu, yazılımın konumu, dosya adları, yazılımın nasıl çalıştığı ve bilgisayarınızı nasıl etkilediği hakkında bilgiler içerir.

Ayrıca, **Microsoft Etkin Koruma Hizmeti raporlarına dayalı olarak dinamik tanımlar alabilirsiniz**.

## <a name="choose-management-tasks-for-endpoint-protection"></a>Endpoint Protection için yönetim görevlerini seçme
Aşağıdaki görevler, Endpoint Protection’ın çalıştırıldığı yönetilen bilgisayarlarda çeşitli yönetim görevlerini gerçekleştirmenize yardımcı olur:
- Kötü amaçlı yazılım tanımlarını güncelleştirme
  - Intune konsolu - **Gruplar** çalışma alanından, güncelleştirmek istediğiniz bilgisayarları seçin. **Kötü amaçlı yazılım tanımlarını güncelleştirmek**&gt; **uzak görevler** ' i seçin.
  - Yönetilen bilgisayar - Windows bildirim alanından Endpoint Protection istemci yazılımını başlatın. **Güncelleştir** sekmesini ve ardından **Güncelleştir**'i seçin.
- Kötü amaçlı yazılım taraması çalıştırma:
  - Intune konsolu - **Gruplar** çalışma alanından, tarama gerçekleştirmek istediğiniz bilgisayarları seçin. **Tam Kötü Amaçlı Yazılım Taraması Çalıştır** veya **Hızlı Kötü Amaçlı Yazılım Taraması Çalıştır**'ı seçin.
  - Yönetilen bilgisayar - Windows bildirim alanından Endpoint Protection istemci yazılımını başlatın. **Hızlı**, **Tam**veya **Özel**'i seçtikten sonra **Şimdi tara**'yı seçin.

Bir uzak görevin durumunu, Intune konsolunun sağ alt köşesindeki **Uzak Görevler** bağlantısını seçerek görüntüleyebilirsiniz. **Uzak Görev Durumu** iletişim kutusu, geçerli uzak görevler, görev durumu, cihaz adı ve bildirilen hataları listeler. Ayrıca uygun durumlarda sorun giderme bilgilerine bir bağlantı sağlar.

## <a name="monitor-endpoint-protection"></a>Endpoint Protection'ı izleme
**Microsoft Intune yönetim konsolunun**[Koruma](https://manage.microsoft.com/)çalışma alanını kullanarak bilgisayarlarınızda kötü amaçlı yazılımların durumunu izlersiniz. Bu çalışma alanı iki sayfa içerir:
- **Endpoint Protection’a Genel Bakış** - Önemli sorunları, daha fazla bilgi edinmek için seçebileceğiniz bağlantılar halinde görüntüler. Görüntülenebilecek sorunlardan bazıları şunlardır:
  - **İzleme gerektiren kötü amaçlı yazılım örnekleri** – Sorunu çözmek için yapılması gereken ek eylemler dahil olmak üzere kötü amaçlı yazılım sorunları listesini görmek için bağlantıya tıklayın. Hangi bilgisayarların etkilendiğini görmek için bu listenin ayrıntılarına bakabilirsiniz.
  - **İzleme gerektiren kötü amaçlı yazılım bulunan bilgisayarlar** – Çözümlenmemiş kötü amaçlı yazılım sorunları olan bilgisayarları ve sorunu çözmek için yapılması gereken eylemleri görmek için bağlantıya tıklayın.
  - **Korumalı olmayan cihazlar** – Herhangi bir yazılım yüklü olmadığından veya bir hata olduğundan hiçbir uç nokta koruma yazılımı tarafından korunmayan bilgisayarları görmek için bağlantıya tıklayın. Daha fazla ayrıntı görüntülemek için bir bilgisayarı seçin.
  - **Başka bir uç nokta koruma uygulaması çalışan cihazlar** – Üçüncü taraf bir uç nokta koruma uygulaması çalıştıran bilgisayarları görmek için bağlantıya tıklayın.
- **Tüm kötü amaçlı yazılımlar** -bilgisayarlarınızda bulunan tüm etkin kötü amaçlı yazılımların listesini görüntüler. Belirli bir kötü amaçlı yazılımdan etkilenen tüm bilgisayarları görmek için bu listeyi inceleyebilir veya aşağıdaki görevlerden birini seçebilirsiniz:
  - **Özellikleri Görüntüle** – Seçili kötü amaçlı yazılım hakkında daha fazla bilgi içeren bir sayfa açar.
  - **Bu Kötü Amaçlı Yazılım Hakkında Bilgi Edin** – Microsoft Kötü Amaçlı Yazılımdan Koruma Merkezi'nden kötü amaçlı yazılım hakkında daha fazla bilgi içeren bir konuyu açar.

> [!IMPORTANT]
> **Endpoint Protection** çalışma alanı, istemciyi yükleyene ve en az bir bilgisayar istemcisini yönetene kadar yönetim konsolunda görüntülenmez.

  ![Endpoint Protection'ı izleme](./media/help-secure-windows-pcs-with-endpoint-protection-for-microsoft-intune/pol-sa-ep-monitor.png)

### <a name="how-to-view-recent-detection-paths-for-malware-on-computers"></a>Bilgisayarlarda kötü amaçlı yazılımların En Son Algılama Yollarını görüntüleme
Intune, cihazda en son algılanan kötü amaçlı yazılım yollarının en fazla 10’unu görüntüleyebilir. **En Son Algılama Yolu** varsayılan olarak devre dışı bırakılır. Bu görünümü etkinleştirmek için:

1. [Microsoft Intune yönetim konsolunda](https://manage.microsoft.com/)**Gruplar** > **Tüm Cihazlar** > **Tüm Bilgisayarlar**'ı seçin.
2. Son algılama yollarını görmek istediğiniz bilgisayara sağ tıklayın ve **Özellikler**’i seçin.
3. Üstteki sekmelerden **Kötü Amaçlı Yazılım**’ı seçin.

   ![Kötü Amaçlı Yazılım sekmesini seçin ve ardından En Son Algılama Yolları onay kutusunu işaretleyin](./media/help-secure-windows-pcs-with-endpoint-protection-for-microsoft-intune/malware-path-column.png)
4. Sütun başlığına sağ tıklayın. Kullanılabilir sütunlar listesi görüntülenir. Listede **Son Algılama Yolları** onay kutusunu seçin. **Son Algılama Yolları** sütunu görüntülenir ve cihazda en son izlenen en fazla 10 kötü amaçlı yazılım örneğini gösterir.

## <a name="run-a-malware-scan-or-update-malware-definitions-on-a-computer"></a>Bilgisayarda kötü amaçlı yazılım taraması çalıştırma veya kötü amaçlı yazılım tanımlarını güncelleştirme
Intune, Intune istemcisinin yüklü olduğu uzaktan yönetilen bir bılgısayarda Endpoint Protection veya Microsoft Defender kullanarak tam veya hızlı kötü amaçlı yazılım taraması çalıştırabilir.

1. [Microsoft Intune yönetim konsolunda](https://manage.microsoft.com/)**Gruplar** > **Genel Bakış** > **Tüm Cihazlar** > **Tüm Bilgisayarlar**’a gidin ve ardından hedeflemek istediğiniz bilgisayarı seçin.

2. **Uzak Görevler** açılan listesini seçin ve uzak bilgisayarda çalıştırılacak görevi seçin.

## <a name="need-more-help"></a>Daha fazla yardıma mı ihtiyacınız var?
Daha fazla yardım ve destek için bkz. [Microsoft Intune Endpoint Protection’da sorun giderme](troubleshoot-endpoint-protection-in-microsoft-intune.md).

## <a name="see-also"></a>Ayrıca bkz.
[Windows bilgisayarlarını koruma ilkeleri](policies-to-protect-windows-pcs-in-microsoft-intune.md)
