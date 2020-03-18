---
title: Intune yazılım istemcisini çalıştıran bilgisayarlar için yazılım lisans sözleşmelerini yönetme
titleSuffix: Microsoft Intune
description: Microsoft Toplu Lisanslama sözleşmeleriyle satın alınmış yazılımlar ve diğer yöntemlerle satın alınmış yazılımlar için lisans sözleşmelerini yönetmek amacıyla Intune’u kullanın.
keywords: ''
author: dougeby
ms.author: dougeby
manager: dougeby
ms.date: 01/01/2018
ms.topic: archived
ms.service: microsoft-intune
ms.subservice: fundamentals
ms.localizationpriority: medium
ms.assetid: c59d8635-3f66-40f5-824a-a71c738e0341
ms.reviewer: owenyen
ms.suite: ems
search.appverid: MET150
ms.custom: intune-classic-keep
ms.collection: M365-identity-device-management
ms.openlocfilehash: 64d1bce08186c47e63a83b3148b59a2593a761f5
ms.sourcegitcommit: 3d895be2844bda2177c2c85dc2f09612a1be5490
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/13/2020
ms.locfileid: "79332458"
---
# <a name="manage-license-agreements-for-windows-pc-software-in-microsoft-intune"></a>Microsoft Intune’da Windows bilgisayarı yazılımları için lisans sözleşmelerini yönetme

[!INCLUDE [classic-portal](../includes/classic-portal.md)]

Microsoft Intune, Microsoft Toplu Lisans sözleşmeleriyle satın alınmış yazılımlar için lisans sözleşmesi bilgilerini eklemenize ve yönetmenize olanak sağlar. Bunu başka bir yolla satın alınmış Microsoft yazılımları veya Microsoft dışı yazılımlar için de gerçekleştirebilirsiniz. Bu bilgileri mantıksal gruplar halinde düzenleyebilirsiniz.

> [!IMPORTANT]
> Bu özellik yalnızca kolaylık sağlamak için sunulmuştur ve doğruluğu garanti edilmez. Microsoft Toplu Lisanslama sözleşmeleri ile uyumluluğu buna dayanarak doğrulamamalısınız. Microsoft, bizimle yaptığınız lisans sözleşmelerinin olası ihlal veya uyumunu araştırmak için toplanan verilerden hiçbirini kullanmaz.
>
> Intune’a eklediğiniz lisanslar, yazılımınızı kullanma yetkilendirmelerinizi veya lisans sözleşmelerinizi etkilemez. Örneğin, Intune’dan bir lisans/anlaşma çiftini silerseniz, sizinle Microsoft arasındaki lisans sözleşmeleri silinmez veya iptal edilmez.

Intune yönetim konsolunun **Lisanslar** çalışma alanında şunları yapabilirsiniz:

- Microsoft Toplu Lisanslama sözleşmelerini ekleyin ve düzenleyin.

- Diğer yazılım lisansı anlaşmalarını ekleyin ve düzenleyin.

- Lisansları ve grupları yönetin.

- Intune tarafından Toplu Lisanslama Hizmeti Merkezi’nden (VLSC) alınan yetkilendirme bilgilerini, yönetilen Windows bilgisayarlarında Intune tarafından algılanan Microsoft yazılım envanteri ile karşılaştırın.

Buna ek olarak, yazılım başlıkları için yükleme ve lisans sayılarını gösteren lisans raporları da oluşturabilirsiniz. Lisans raporları, Microsoft yazılımı ve Microsoft olmayan yazılım başlıkları için tam lisans konumunuzu değerlendirmenize yardımcı olabilir.

> [!TIP]
> **Lisanslar** çalışma alanının yönetici konsolunda gösterilmesi için, Intune Windows bilgisayar istemcisiyle en az bir Windows bilgisayarını yönetmeniz gerekir.

## <a name="add-microsoft-volume-licensing-agreements"></a>Microsoft Toplu Lisanslama sözleşmelerini ekleme
Intune Toplu Lisans sözleşmeleri, Microsoft Toplu Lisanslama sözleşmeleri ile satın alınan yazılımlar için lisans bilgileri sağlar. Eşleşen anlaşma numarası çiftleri sağlayarak Intune’a Microsoft Toplu Lisanslama anlaşmaları ekleyebilirsiniz. Sözleşme veya yetkilendirme sayıları, doğru lisans ya da kayıt sayılarıyla eşleşmelidir. [Toplu Lisanslama Hizmet Merkezi (VLSC)](https://go.microsoft.com/fwlink/?LinkID=223842)içinden lisans sözleşmelerini satın aldığınızda anlaşma numarası çiftleri elde edilir.

1. [Microsoft Intune yönetici konsolunda](https://admin.manage.microsoft.com/)**Lisanslar**’ı seçin.

2. **Anlaşma Ekle** sayfasındaki **Anlaşma Türünü Seç**’in altında **Toplu Lisanslama anlaşması**’nı seçin.

3. **Anlaşma Ayrıntıları Ekle** bölümünde, karşıya bir dosya yüklemek mi yoksa ayrıntıları el ile girmek mi istediğinizi belirtin.

    - **Anlaşma ayrıntılarını içeren CSV dosyası yükle**. **Gözat**’ı seçip karşıya yüklemek istediğiniz CSV dosyasını seçin.

        - Dosya iki veya üç sütun içerebilir. yalnızca sözleşmesi çiftleri için iki tane veya her bir sözleşme çifti için kolay ad eklemek istiyorsanız üç tane.

        - Bir anlaşma numarası çiftindeki toplam karakter sayısı 16 ASCII karakterden uzun olamaz.

        - Yalnızca ASCII karakterleri desteklenir.

        - Sözleşme adında Şu karakterlere izin verilmez: **~! @ # $ ^ &#42; &amp; () = + [] {} \ |;: ' "&lt; &gt; /** . Adda boşluklara izin verilir.

        - Dosya adı 128 karakterden uzun olmamalıdır.

        - Dosya en az bir sözleşme çifti içermelidir ve 5.000'den fazla sözleşme çifti içeremez.

        **Dosya için biçimlendirme**

        VLSC’ye kaydettiğiniz kuruluş türüne bağlı olarak aşağıdaki biçimlerden birinde bir düz metin belgesine anlaşma çiftlerinizi ekleyerek bu dosyayı oluşturabilirsiniz. Her satırda tek bir anlaşma numarası çifti belirtin.

        - **Açık değer müşterileri:** *anlaşma numarası*, *tekrar anlaşma numarası*, *anlaşma adı*

        - **Açık müşteriler:** *Yetkilendirme numarası*, *ilgili lisans numarası*, *anlaşma adı*

        - **Select ve Enterprise müşterileri:** *anlaşma numarası*, *ilgili kayıt numarası*, *anlaşma adı*

        **Anlaşma Ekle** formunda, yeni bir anlaşma eklediğinizde bu dosyaya göz atmanız istenir.

        Aşağıda, Açık Değer müşterisi için .csv dosyası içeriğine bir örnek verilmiştir.

        `01-07001, 01-07001, Office agreements`

    - **Anlaşma ayrıntılarını el ile ekle**. Aşağıdaki bilgileri sağlayın ve **Yetkilendirme/Anlaşma numarası** ve **Lisans/Kayıt/Müşteri numarası** kutularına anlaşma numarası çiftlerini yazın. Her iki numarayı da yazdıktan sonra **Çift ekle** simgesini seçerek numaralarınızı kaydedin ve isteğe bağlı olarak yeni bir çift ekleyin.

        - **Anlaşma adı** - Anlaşma için benzersiz bir ad belirtin.

            Anlaşma adı en fazla 256 karakter uzunluğunda olabilir ve şu karakterleri içeremez: **~! @ # $ ^ &#42; &amp; () = + [] {} \ |;: ' "&lt; &gt; /** . Adda boşluklara izin verilir.

        - **Yetkilendirme/Anlaşma numarası** - Lisans çiftinin yetkilendirme/anlaşma numarasını girin.

        - **Lisans/Kayıt/Müşteri numarası** - Lisans çiftinin lisans/kayıt/müşteri numarasını girin.

        > [!NOTE]
        > Birkaç anlaşma numarası çifti eklerseniz Intune, belirttiğiniz adla tek bir anlaşma oluşturur ve eklediğiniz tüm çiftler bu anlaşmanın bir parçası olur.

    Başka bir anlaşma numarası çifti eklemek için **+** öğesini veya daha önce girdiğiniz bir anlaşma numarası çiftini kaldırmak için **-** öğesini seçebilirsiniz.

4. **Lisans Grubu Seç** alanında aşağıdakilerden birini yapın:

    - **Anlaşmaları Atanmamış Anlaşmalar grubuna ekle**. Yeni anlaşmaları bir lisans grubuna eklemek istemiyorsanız bunu seçin.

    - **Anlaşmaları yeni bir lisans grubuna ekle**. Yeni lisans grubu için bir ad sağlayın.

    - **Anlaşmaları var olan lisans grubuna ekle**. **Grup adı** listesinde, anlaşmaları eklemek istediğiniz lisans grubunu seçin.

5. **Tamam**’ı seçin.

**Tüm Anlaşmalar** görünümü gösterilir ve Intune, sağladığınız anlaşma numarası çiftlerini doğrulamak için Microsoft VLSC’ye bağlanır.

Intune’da lisans sözleşmelerini ekledikten sonra toplu lisans bilgilerini güncelleştirmek için **Lisanslara Genel Bakış** sayfasında **Şimdi Yenile**‘yi seçin. Bu eylem, [Microsoft Toplu Lisanslama Hizmet Merkezi (VLSC)](https://go.microsoft.com/fwlink/?LinkId=223842)içinden geçerli lisans bilgilerini alır.

> [!IMPORTANT]
> Toplu lisanslama bilgilerini yenileyinceye kadar, **Anlaşmalara Genel Bakış** sayfasında yetkilendirme bilgilerini ve anlaşma listesinde farklı bilgiler görebilirsiniz.

Toplu lisans bilgilerini yeniledikten sonra lisans bilgilerini, **Uygulamalar** çalışma alanındaki algılanan Microsoft yazılımınızla karşılaştırabilirsiniz. Aşağıdaki lisans raporlarını da çalıştırabilirsiniz:

- **Lisan Satın Alma Raporları** - Kapsamın açıklarını bulmanıza yardımcı olmak için, seçtiğiniz lisans gruplarındaki lisanslı yazılımları görüntülemenizi sağlar.

- **Lisans Yükleme Raporları** - Lisans sözleşmenizin kapsamının yeterli olup olmadığını saptamanıza yardımcı olur.

> [!NOTE]
> Tüm Microsoft Toplu Lisans anlaşmaları için görüntülenen **Ürün Başlığı** **Kullanılamaz**.

## <a name="add-and-edit-other-software-licensing-agreements"></a>Diğer yazılım lisansı anlaşmalarını ekleme ve düzenleme
Intune’a, Microsoft Toplu Lisanslama sözleşmelerinin yanı sıra, başka türlerde lisans sözleşmeleri de ekleyebilirsiniz. Bu sözleşmeler, bir perakendeciden satın alınan Microsoft dışı yazılımları veya Microsoft yazılımlarını içerebilir.

> [!IMPORTANT]
> Sözleşme ekleyebilmeniz için önce Intune’a en az bir Windows bilgisayarınız kayıtlı olmalıdır.  Ayrıca, en az bir kayıtlı bilgisayarda, lisans sözleşmesi eklemek istediğiniz, lisanslanabilir bir yazılım paketi de yüklemiş olmalıdır.

### <a name="to-add-other-software-agreements"></a>Diğer yazılım anlaşmalarını eklemek için

1. [Microsoft Intune yönetici konsolunda](https://admin.manage.microsoft.com/)**Lisanslar**’ı seçin.

2. **Diğer Yazılım Lisanslama Anlaşmaları** bölümünde **Anlaşma Ekle**‘yi seçin.

3. **Anlaşma Ekle** sayfasının **Anlaşma Türünü Seç** bölümünde **Diğer yazılım lisanslama anlaşması** öğesini seçin.

4. **Anlaşma Ayrıntıları Ekle** alanında şunları belirtin:

    - **Agreement name** (zorunlu). Anlaşma adı en fazla 256 karakter uzunluğunda olabilir ve şu karakterleri içeremez: **~! @ # $ ^ &#42; &amp; () = + [] {} \ |;: ' "&lt; &gt; /** . Adda boşluklara izin verilir.

    - **Yayımcı** (gerekli). Bir yayımcı adı yazmaya başladığınızda hizmet yazdığınız harfleri içeren tüm yayımcı adlarını getirir. Örneğin, "soft" yazarsanız hizmet, adında “soft” geçen tüm yayımcı adlarını getirir; örneğin, “Microsoft" ve "Microsoft Research". Yayımcı adları, Yazılım Varlığı Kataloğundan alınır. Ürün başlığını girebilmeniz için önce yayımcıyı seçmeniz gerekir.

        > [!IMPORTANT]
        > Eklemek istediğiniz şirket bu listede gösterilmiyor olabilir. Yalnızca yazılım varlık kataloğunda zaten var olan şirketler için yazılım anlaşmaları ekleyebilirsiniz. Bununla birlikte, Microsoft en popüler yazılım başlıklarını eklemek için sürekli çalışmaktadır. Bir şirketin bu listeye eklenmesine yönelik bir istek göndermek isterseniz, [Intune Uservoice sitesinde](https://microsoftintune.uservoice.com/) bunu yapabilirsiniz.

    - **Ürün başlığı** (gerekli). Bir ürün başlığı yazmaya başladığınızda hizmet yazdığınız harfleri içeren tüm ürün başlıklarını getirir. Bir **Ürün başlığı** belirtebilmeniz için önce bir **Yayımcı**belirtmeniz gerekir.

    - **Lisans sayısı** (gerekli). Satın alınan lisans sayısını girin.

    - **Lisans başlangıç tarihi**. Lisans kapsamı başlangıç tarihini girin.

    - **Lisans bitiş tarihi**. Lisans kapsamı bitiş tarihini girin.

    - **Anlaşma ayrıntıları**. İsteğe bağlı olarak, kişi bilgilerini, kayıt anahtarlarını ve diğer bilgileri belirtebilirsiniz.

5. **Lisans Grubu Seç** alanında aşağıdakilerden birini yapın:

    - Yeni veya varolan bir lisans grubuna yeni anlaşmalar eklemek istemiyorsanız **Anlaşmaları Atanmamış Anlaşmalar grubuna ekle** öğesini seçin. İstediğiniz zaman kullanıcı tanımlı lisans gruplarına anlaşmalar ekleyebilirsiniz.

    - Yeni lisans grubuna yeni anlaşmalar eklemek için **Anlaşmaları yeni bir lisans grubuna ekle** öğesini seçin. Yeni lisans grubu için bir ad sağlamanız istenir.

    - Yeni anlaşmaları varolan bir lisans grubuna eklemek için **Anlaşmaları var olan bir lisans grubuna ekle** öğesini seçin. **Grup adı** listesinde, anlaşmaları eklemek istediğiniz lisans grubunu seçin.

6. **Tamam**’ı seçin.

**Tüm Anlaşmalar** liste görünümü görüntülenir.

## <a name="manage-license-agreements"></a>Lisans anlaşmalarını yönetme
Yazılım lisanslama anlaşmaları, lisans gruplarına eklenebilir. Lisans sözleşmelerinizi kuruluşunuz için mantıksal birimler halinde düzenlemek için lisans gruplarını kullanabilirsiniz. Buna ek olarak, daha önce oluşturmuş olduğunuz lisans sözleşmelerini silebilirsiniz.


|                            |                                                                                                                                                                                                                                                                                                                                                                          |
|----------------------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
|            Görev            |                                                                                                                                                                                 Ayrıntılar                                                                                                                                                                                  |
|   Lisans grubu oluşturma   |                                                            <strong>Lisanslar</strong> çalışma alanının <strong>Genel Bakış</strong> sayfasındaki <strong>Görevler</strong> menüsünde <strong>Lisans Grubu Oluştur</strong>’u seçin. <strong>Not:</strong> Toplamda en fazla 500 lisans grubu oluşturabilirsiniz.                                                             |
|   Lisans grubunu yeniden adlandırma   |                                                                                                      <strong>Lisanslar</strong> çalışma alanında bir lisans grubu seçin ve ardından <strong>Görevler</strong> menüsünde <strong>Lisans Grubunu Düzenle</strong>’yi seçin.                                                                                                       |
|   Lisans grubunu silme   |                                 <strong>Lisanslar</strong> çalışma alanında bir lisans grubu seçin ve ardından <strong>Görevler</strong> menüsünde <strong>Lisans Grubunu Sil</strong>’i seçin. <strong>İpucu:</strong> Silinen grubun içindeki tüm lisanslar <strong>Atanmamış anlaşmalar</strong> lisans grubuna taşınır.                                 |
| Lisans sözleşmesini silme | <strong>Lisanslar</strong> çalışma alanında bir anlaşma seçin ve sonra da <strong>Sil</strong>’i seçin. <strong>İpucu:</strong> Toplu Lisanslama anlaşmalarını sildikten sonra, lisans bilgilerini güncelleştirmek için, belirli bir lisans grubu için <strong>Genel</strong> sekmesinde veya <strong>Lisanslara Genel Bakış</strong> sayfasında <strong>Şimdi Yenile</strong>‘yi seçin. |

