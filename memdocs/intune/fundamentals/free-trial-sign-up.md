---
title: Hızlı Başlangıç - Microsoft Intune'u ücretsiz deneyin
titleSuffix: ''
description: Bu hızlı başlangıçta ücretsiz bir deneme aboneliği oluşturacak, desteklenen yapılandırmaları ve ağ gereksinimlerini anlayacak ve isterseniz kendi etki alanı adınızı yapılandıracaksınız.
keywords: ''
author: Erikre
ms.author: erikre
manager: dougeby
ms.date: 01/16/2020
ms.topic: quickstart
ms.service: microsoft-intune
ms.subservice: fundamentals
ms.localizationpriority: high
ms.technology: ''
ms.assetid: 195931c0-8208-43bd-b0af-b1f8e469a32c
ms.reviewer: ''
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: 893981700ede9587a980faa0e4d6b0384c24e3d4
ms.sourcegitcommit: e7fb8cf2ffce29548b4a33b2a0c33a3a227c6bc4
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/30/2020
ms.locfileid: "80401496"
---
# <a name="quickstart-try-microsoft-intune-for-free"></a>Hızlı Başlangıç: Microsoft Intune'u ücretsiz deneyin

Microsoft Intune, cihaz ve uygulamaları yöneterek iş gücünüzün şirket verilerini korumanıza yardımcı olur. Bu hızlı başlangıçta Intune'u bir test ortamında denemek için ücretsiz bir abonelik oluşturacaksınız.

Intune, Microsoft Endpoint Manager Yönetim Merkezi kullanılarak yönetilen güvenli bir bulut tabanlı hizmetten mobil cihaz yönetimi (MDM) ve mobil uygulama yönetimi (MAM) sağlar. Intune kullanarak işgücünüzün şirket kaynaklarının (veriler, cihazlar ve uygulamalar) yapılandırmasının, erişiminin ve güncelleştirmesinin şirketinizin uyumluluk ilke ve gereksinimlerini karşılayacak şekilde doğru olmasını sağlayabilirsiniz.

## <a name="prerequisites"></a>Önkoşullar
Microsoft Intune'u kurmadan önce aşağıdaki gereksinimleri gözden geçirin:

- [Desteklenen işletim sistemleri ve tarayıcılar](supported-devices-browsers.md)
- [Ağ yapılandırma gereksinimleri ve bant genişliği](network-bandwidth-use.md)

## <a name="sign-up-for-a-microsoft-intune-free-trial"></a>Microsoft Intune ücretsiz denemesine kaydolma

Intune'u 30 gün boyunca ücretsiz deneyebilirsiniz. Zaten bir iş veya okul hesabınız varsa bu hesapla **oturum açın** ve aboneliklerinize Intune’u ekleyin. Veya bunun yerine kuruluşunuz için Intune kullanmak üzere yeni bir hesaba **kaydolun**.

> [!IMPORTANT]
> Yeni bir hesap için kaydolduktan sonra mevcut bir iş veya okul hesabını birleştirmeniz mümkün olmayacaktır.

1. [Microsoft Intune Deneme](https://go.microsoft.com/fwlink/?linkid=2019088) sayfasına gidin ve formu doldurun.

    ![Microsoft Intune Deneme hesabına kaydolma web sayfasının ekran görüntüsü](./media/free-trial-sign-up/account-sign-up-site-full-browser.png)

    BT işlemlerinizin ve kullanıcılarınızın çoğu sizinkinden başka bir bölgedeyse, **Ülke veya bölge** altından bu konumu seçmeniz doğru olur. Azure doğru hizmetleri sunmak için bölgesel bilgilerinizi kullanır. Bu ayar daha sonra değiştirilemez.

2. Şirketinizin adını ve arından **. onmicrosoft.com** dizesini kullanarak bir hesap oluşturun. 

    ![Intune deneme hesabı yeni kimlik bilgileri işleminin ekran görüntüsü](./media/free-trial-sign-up/account-sign-up-site-user-id.png)

    Kuruluşunuzun, **. onmicrosoft.com**olmadan kullanmak istediğiniz kendi özel etki alanı varsa, bu makalede daha sonra açıklanan Microsoft 365 Yönetim Merkezi ' nde bunu değiştirebilirsiniz.

3. Kaydolma işleminin sonunda yeni hesap bilgilerinizi görüntüleyin.

    ![Hesap bilgilerinizin görüntüsü](./media/free-trial-sign-up/intune-end-of-sign-up-process.png) 

## <a name="sign-in-to-intune-in-the-microsoft-endpoint-manager"></a>Microsoft uç nokta yöneticisinde Intune 'da oturum açma

Portalda zaten oturum açmadıysanız, aşağıdaki adımları izleyin:

1. Yeni bir tarayıcı penceresi açın ve adres çubuğuna **https://endpoint.microsoft.com** ifadesini girin. 
2. Oturum açmak için yukarıdaki adımlarda verilen kullanıcı KIMLIĞINI kullanın ( *yourID@yourdomain* . onmicrosoft.com).

    ![Portal oturum açma sayfasının görüntüsü](./media/free-trial-sign-up/azure-portal-signin.png)

Deneme için kaydolduğunuzda, hesap bilgilerinizi ve kayıt işlemi sırasında verdiğiniz e-posta adresini içeren bir e-posta iletisi de alırsınız. Bu e-posta, denemenizin etkin olduğunu doğrular.

> [!TIP]
> Microsoft Endpoint Manager ile çalışırken, özel mod yerine normal modda bir tarayıcıyla çalışan daha iyi sonuçlara sahip olabilirsiniz.

## <a name="confirm-the-mdm-authority-in-intune"></a>Intune 'da MDM yetkilisini onaylama

Varsayılan olarak, ücretsiz deneme sürümünüzü oluşturduğunuzda MDM yetkilisi ayarlanır. Aşağıdaki adımları kullanarak MDM yetkilisinin ayarlandığını doğrulayabilirsiniz:

1. Henüz oturum açmadıysanız Microsoft Uç Nokta Yöneticisi ' nde oturum açın.
2. **Kiracı Yönetimi**' ne tıklayın.
3. Kiracı ayrıntılarını görüntüleyin. **MDM yetkilisi** **Microsoft Intune**olarak ayarlanmalıdır.

Microsoft Uç Nokta Yöneticisi 'nde oturum açtıktan sonra, MDM yetkilisini henüz belirtmemeniz gerektiğini belirten bir turuncu başlık görürsünüz. Mobil cihaz yönetimi (MDM) yetkili ayarı, cihazlarınızı yönetme şeklinizi belirler. Kullanıcıların yönetime cihaz kaydetmeleri için bir MDM yetkilisi ayarlanması gerekir.

### <a name="to-set-the-mdm-authority-to-intune-follow-these-steps"></a>MDM yetkilisini Intune olarak ayarlamak için şu adımları izleyin:

1. Yeni bir tarayıcı penceresi açın ve adres çubuğuna **https://portal.azure.com** ifadesini girin. 
2. **Tüm hizmetler** > **Microsoft Intune**'u seçin.
3. Cihaz yönetimini etkinleştirmediğinizi gösteren başlığı veya başlığı göremiyorsanız **Cihaz kaydı**’nı seçin. Cihaz yönetimini henüz etkinleştirmediyseniz **MDM Yetkilisi seçin** dikey penceresi görüntülenir.

    > [!NOTE]
    > MDM yetkilisini ayarladıysanız, **cihaz kaydı** DIKEY penceresinde MDM yetkilisi değerini görürsünüz. Turuncu başlık, ancak henüz MDM yetkilisini ayarlamadıysanız görüntülenir. 

    ![MDM Yetkilisi seçin dikey penceresinin görüntüsü](./media/free-trial-sign-up/choose-mdm-authority.png) 

4. MDM yetkiliniz ayarlanmamışsa, **MDM yetkilisi seçin**altında MDM yetkilinizi **Intune MDM yetkilisi**olarak ayarlayın.

MDM yetkilisi hakkında daha fazla bilgi için bkz. [Mobil cihaz yönetimi yetkilisini ayarlama](mdm-authority-set.md).

## <a name="configure-your-custom-domain-name-optional"></a>Özel etki alanı adınızı yapılandırma (İsteğe bağlı)

Yukarıda belirtildiği gibi, kuruluşunuzun, **. onmicrosoft.com**olmadan kullanmak istediğiniz kendi özel etki alanı varsa, Microsoft 365 Yönetim merkezinde bunu değiştirebilirsiniz. Aşağıdaki adımları kullanarak özel etki alanı adınızı ekleyebilir, doğrulayabilirsiniz ve yapılandırabilirsiniz.  

> [!IMPORTANT]
> Etki alanı adının *ilk* **onmicrosoft.com** bölümünü yeniden adlandıramaz veya kaldıramazsınız. Ancak, iş kimliğinizi açık tutmak için Intune ile kullanılan *özel* etki alanı adlarını ekleyebilir, doğrulayabilirsiniz veya kaldırabilirsiniz. Daha fazla bilgi için bkz. [özel bir etki alanı adı yapılandırma](custom-domain-name-configure.md).

1. [Microsoft 365 Yönetim Merkezi](https://admin.microsoft.com) ' ne gidin ve yönetici hesabınızı kullanarak oturum açın.

2. Gezinme bölmesinde, **Kurulum** > **Etki alanları** > **Etki alanı ekle**'yi seçin.

3. Özel etki alanı adınızı yazın. Ardından **İleri**'yi seçin.

   ![Yönetim Merkezi Microsoft 365 ekran görüntüsü-etki alanı Ekle](./media/free-trial-sign-up/domain-custom-add.png)

4. Önceki adımda girdiğiniz etki alanının sahibi olduğunuzdan emin olun. 
    
    **Kodu e-posta yoluyla gönder** seçilirse, etki alanınızın kayıtlı iletişim sorumlusuna bir e-posta gönderilir. E-postayı aldıktan sonra kodu kopyalayın ve **Doğrulama kodunuzu buraya yazın** etiketli alana girin. Doğrulama kodu eşleşirse, etki alanı kiracınıza eklenir. Görüntülenen e-posta tanıdık görünmeyebilir. Bazı kayıt şirketlerinde gerçek e-posta adresini gizler. Ayrıca, e-posta adresi farklı olabilir ve bu, etki alanı kaydedildiğinde sağlanmıştı.

   ![Yönetim Merkezi Microsoft 365 ekran görüntüsü-etki alanını doğrula](./media/free-trial-sign-up/domain-custom-verify.png)

   > [!NOTE]
   > TXT kaydı doğrulama ayrıntıları için bkz. [Office 365 için DNS barındırma sağlayıcılarında DNS kayıtları oluşturma](https://support.office.com/article/Create-DNS-records-at-any-DNS-hosting-provider-for-Office-365-7B7B075D-79F9-4E37-8A9E-FB60C1D95166).

## <a name="admin-experiences"></a>Yönetici deneyimi

En sık kullanacağınız iki Portal vardır:
- Microsoft Endpoint Manager Yönetim Merkezi ([https://endpoint.microsoft.com/](https://endpoint.microsoft.com/)), [Intune 'un yeteneklerini](what-is-intune.md)keşfedebileceğiniz yerdir. Bu, yöneticinin Intune ile çalıştığı yerdir.
- Microsoft 365 Yönetim Merkezi ([https://admin.microsoft.com](https://admin.microsoft.com)), bu Azure Active Directory kullanmıyorsanız kullanıcıları ekleyebileceğiniz ve yönetebileceğiniz yerdir. Ayrıca hesabınızın faturalama ve destek gibi diğer yönlerini de yönetebilirsiniz.

## <a name="next-steps"></a>Sonraki adımlar

Bu hızlı başlangıçta Intune’u bir test ortamında denemek için ücretsiz bir abonelik oluşturdunuz. Intune’u ayarlama hakkında daha fazla bilgi için bkz. [Intune’u ayarlama](setup-steps.md).

Bu Intune hızlı başlangıç serisini takip etmek için bir sonraki hızlı başlangıca ilerleyin.

> [!div class="nextstepaction"]
> [Hızlı Başlangıç: Kullanıcı oluşturun ve ona bir lisans atayın](quickstart-create-user.md)
