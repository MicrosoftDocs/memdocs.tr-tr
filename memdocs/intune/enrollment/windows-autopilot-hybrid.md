---
title: Karma Azure AD 'ye katılmış cihazlar için kayıt-Windows Autopilot
titleSuffix: ''
description: Microsoft Intune ' de karma Azure AD 'ye katılmış cihazları kaydetmek için Windows Autopilot kullanın.
keywords: ''
author: ErikjeMS
ms.author: erikje
manager: dougeby
ms.date: 07/01/2019
ms.topic: conceptual
ms.service: microsoft-intune
ms.subservice: enrollment
ms.localizationpriority: high
ms.technology: ''
ms.assetid: 8518d8fa-a0de-449d-89b6-8a33fad7b3eb
ms.reviewer: priyar
ms.suite: ems
search.appverid: MET150
ms.custom: seodec18
ms.collection: M365-identity-device-management
ms.openlocfilehash: 84d14943a37cf29a224c94364317d899b65ffef0
ms.sourcegitcommit: bbb63f69ff8a755a2f2d86f2ea0c5984ffda4970
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/18/2020
ms.locfileid: "79526335"
---
# <a name="deploy-hybrid-azure-ad-joined-devices-by-using-intune-and-windows-autopilot"></a>Intune ve Windows Autopilot kullanarak karma Azure AD 'ye katılmış cihazları dağıtma
Karma Azure Active Directory (Azure AD) ile birleştirilmiş cihazları ayarlamak için Intune ve Windows Autopilot kullanabilirsiniz. Bunu yapmak için bu makaledeki adımları izleyin.

## <a name="prerequisites"></a>Önkoşullar

[Hibrit Azure AD 'ye katılmış cihazlarınız](https://docs.microsoft.com/azure/active-directory/devices/hybrid-azuread-join-plan)başarıyla yapılandırılır. Get-MsolDevice cmdlet 'ini kullanarak [cihaz kaydınızı doğruladığınızdan](https://docs.microsoft.com/azure/active-directory/devices/hybrid-azuread-join-managed-domains#verify-the-registration) emin olun.

Kaydedilecek cihazlar ayrıca:
- Windows 10 v1809 veya üstünü çalıştırıyor olun.
- [Belgelenen Windows Autopilot Network gereksinimlerini izleyerek](https://docs.microsoft.com/windows/deployment/windows-autopilot/windows-autopilot-requirements#networking-requirements)internet erişimi vardır.
- Bir Active Directory etki alanı denetleyicisine erişiminiz olduğundan, kuruluşun ağına bağlanması gerekir (burada, AD etki alanı ve AD etki alanı denetleyicisi için DNS kayıtlarını çözümleyebilir ve kullanıcının kimliğini doğrulamak için etki alanı denetleyicisiyle iletişim kurabilir). VPN bağlantısı şu anda desteklenmiyor).
- Katılmayı denediğiniz etki alanının etki alanı denetleyicisine ping atabiliyor.
- Proxy kullanılıyorsa, WPAD proxy ayarları seçeneğinin etkinleştirilmesi ve yapılandırılması gerekir.
- Kullanıma hazır deneyimin (OOBE) altına gidin.
- Azure Active Directory OOBE 'de desteklenen bir yetkilendirme türü kullanın.


## <a name="set-up-windows-10-automatic-enrollment"></a>Windows 10 otomatik kaydını ayarlama

1. Azure 'da oturum açın, sol bölmede **Azure Active Directory**' yi seçin.

   ![Azure portal](./media/windows-autopilot-hybrid/auto-enroll-azure-main.png)

1. **Mobility (MDM ve MAM)** seçeneğini belirleyin.

   ![Azure Active Directory bölmesi](./media/windows-autopilot-hybrid/auto-enroll-mdm.png)

1. **Microsoft Intune**'u seçin.

   ![Mobility (MDM ve MAM) bölmesi](./media/windows-autopilot-hybrid/auto-enroll-intune.png)

1. Intune ve Windows kullanarak Azure AD 'ye katılmış cihazları dağıtan kullanıcıların **MDM Kullanıcı kapsamınızda**bulunan bir grubun üyesi olduğundan emin olun.

   ![Mobility (MDM ve MAM) yapılandırma bölmesi](./media/windows-autopilot-hybrid/auto-enroll-scope.png)

1. **Mdm kullanım koşulları URL 'si**, **MDM bulma URL**'SI ve **MDM uyumluluk URL 'si** kutularındaki varsayılan değerleri kullanın ve ardından **Kaydet**' i seçin.

## <a name="increase-the-computer-account-limit-in-the-organizational-unit"></a>Kuruluş Birimi’nde bilgisayar hesabı sınırını artırma

Active Directory Intune Bağlayıcısı, şirket içi Active Directory etki alanında Autopilot kayıtlı bilgisayarlar oluşturur. Intune bağlayıcısını barındıran bilgisayarın, etki alanı içinde bilgisayar nesneleri oluşturma haklarına sahip olması gerekir. 

Bazı etki alanlarında bilgisayarlara bilgisayar oluşturma hakkı verilmez. Ayrıca, etki alanları, bilgisayar nesneleri oluşturmak için hak atanmamış tüm kullanıcılar ve bilgisayarlar için geçerli olan yerleşik bir sınıra (varsayılan 10) sahiptir. Bu nedenle, hakların, karma Azure AD 'ye katılmış cihazların oluşturulduğu kurumsal birimde Intune bağlayıcısını barındıran bilgisayarlara temsilci seçilmiş olması gerekir.

Bilgisayar oluşturma hakları verilen kuruluş biriminin eşleşmesi gerekir:
- Etki alanına katılması profilinde girilen kuruluş birimi.
- Profil seçilmezse, etki alanınız için bilgisayarın etki alanı adı.

1. **Active Directory Kullanıcıları ve bilgisayarları (dsa. msc)** açın.

1. Karma Azure AD 'ye katılmış bilgisayarları oluşturmak için kullanacağınız kurumsal birime sağ tıklayın ve ardından **denetimi temsilci**Seç ' i seçin.

    ![Temsilci denetimi komutu](./media/windows-autopilot-hybrid/delegate-control.png)

1. **Denetim temsili** sihirbazında, **İleri** ' yi seçerek > **nesne türleri** **ekleyin** > .

1. **Nesne türleri** bölmesinde, **bilgisayarlar** onay kutusunu seçin ve ardından **Tamam**' ı seçin.

    ![Nesne türleri bölmesi](./media/windows-autopilot-hybrid/object-types-computers.png)

1. **Kullanıcıları, bilgisayarları veya grupları seçin** bölmesinde **Seçilecek nesne adlarını girin** kutusuna bağlayıcının yüklendiği bilgisayarın adını girin.

    ![Kullanıcıları, bilgisayarları veya Grupları Seç bölmesi](./media/windows-autopilot-hybrid/enter-object-names.png)

1. Girdinizi doğrulamak için **adları denetle** ' yi seçin, **Tamam**' ı seçin ve ardından **İleri**' yi seçin.

1.  > **devretmek için özel bir görev oluştur** ' u seçin.

1. Klasör onay kutusunda **yalnızca şu nesneleri** seçin ve ardından **bilgisayar nesnelerini**seçin, **Bu klasörde seçili nesneleri oluşturun**ve **Seçili nesneleri bu klasörde silin** onay kutularını işaretleyin.

    ![Active Directory nesne türü bölmesi](./media/windows-autopilot-hybrid/only-following-objects.png)
    
1. **İleri**'yi seçin.

1. **İzinler**altında **tam denetim** onay kutusunu seçin.  
    Bu eylem diğer tüm seçenekleri seçer.

    ![Izinler bölmesi](./media/windows-autopilot-hybrid/full-control.png)

1. **İleri**' yi ve ardından **son**' u seçin.

## <a name="install-the-intune-connector"></a>Intune Bağlayıcısını yükleme

Active Directory için Intune Bağlayıcısı, Windows Server 2016 veya üstünü çalıştıran bir bilgisayarda yüklü olmalıdır. Bilgisayarın Internet erişimi de ve Active Directory aynı zamanda erişimine sahip olması gerekir. Birden fazla Active Directory etki alanını desteklemek üzere ölçek ve kullanılabilirliği artırmak için ortamınıza birden fazla bağlayıcı yükleyebilirsiniz. Bağlayıcıyı, başka bir Intune Bağlayıcısı çalıştırmayan bir sunucuya yüklemenizi öneririz.

1. [Microsoft Endpoint Manager Yönetim Merkezi](https://go.microsoft.com/fwlink/?linkid=2109431)'nde, Active Directory > **ekle**için **Windows** > **Windows kayıt** > **Intune Bağlayıcısı** > **cihazlar** ' ı seçin. 
2. Bağlayıcıyı indirmek için yönergeleri izleyin.
3. Bağlayıcıyı yüklemek için, yüklenen bağlayıcı kurulum dosyasını *Odjconnectorbootstrapper. exe*' yi açın.
4. Kurulumun sonunda **Yapılandır**' ı seçin.
5. **Oturum aç '** ı seçin.
6. Kullanıcı genel yöneticisi veya Intune yönetici rolü kimlik bilgilerini girin.  
   Kullanıcı hesabının atanmış bir Intune lisansı olmalıdır.
7. Active Directory için **windows > ** **Windows kayıt** > **Intune Bağlayıcısı** > **cihazlar** ' a gidin ve ardından bağlantı durumunun **etkin**olduğunu doğrulayın.

> [!NOTE]
> Bağlayıcıya oturum açtıktan sonra, [Microsoft Endpoint Manager Yönetim merkezinde](https://go.microsoft.com/fwlink/?linkid=2109431)görünmesi birkaç dakika sürebilir. Yalnızca Intune hizmetiyle başarıyla iletişim kurabiliyorsa görünür.

### <a name="turn-off-ie-enhanced-security-configuration"></a>IE artırılmış güvenlik yapılandırmasını kapatma
Varsayılan olarak, Windows Server 'da Internet Explorer Artırılmış Güvenlik Yapılandırması açıktır. Active Directory için Intune bağlayıcısında oturum açamıyor ve ardından, yönetici için IE artırılmış güvenlik yapılandırmasını devre dışı bırakabilirsiniz. [Internet Explorer Artırılmış güvenlik yapılandırmasını kapatma](https://blogs.technet.microsoft.com/chenley/2011/03/10/how-to-turn-off-internet-explorer-enhanced-security-configuration)

### <a name="configure-web-proxy-settings"></a>Web proxy ayarlarını yapılandırma

Ağ ortamınızda bir Web proxy 'niz varsa, Active Directory Intune bağlayıcısının [mevcut şirket içi ara sunucularla çalışmaya](autopilot-hybrid-connector-proxy.md)başvurarak düzgün şekilde çalıştığından emin olun.


## <a name="create-a-device-group"></a>Bir cihaz grubu oluşturma
1. [Microsoft Endpoint Manager Yönetim Merkezi](https://go.microsoft.com/fwlink/?linkid=2109431)'nde **gruplar** > **Yeni Grup**' u seçin.

1. **Grup** bölmesinde şunları yapın:

    a. **Grup türü**için **güvenlik**' i seçin.

    b. Bir **Grup adı** ve **Grup açıklaması**girin.

    c. Bir **üyelik türü**seçin.

1. Üyelik türü için **dinamik cihazlar** ' ı seçtiyseniz, **Grup** bölmesinde, **dinamik cihaz üyeleri** ' ni seçin ve ardından **Gelişmiş kural** kutusunda aşağıdakilerden birini yapın:
    - Tüm Autopilot cihazlarınızı içeren bir grup oluşturmak için `(device.devicePhysicalIDs -any _ -contains "[ZTDId]")`girin.
    - Intune 'un Grup etiketi alanı, Azure AD cihazlarındaki OrderID özniteliğiyle eşlenir. Belirli bir grup etiketi (OrderID) ile tüm Autopilot cihazlarınızı içeren bir grup oluşturmak istiyorsanız şunu yazmanız gerekir: `(device.devicePhysicalIds -any _ -eq "[OrderID]:179887111881")`
    - Belirli bir satın alma siparişi KIMLIĞINE sahip tüm Autopilot cihazlarınızı içeren bir grup oluşturmak için `(device.devicePhysicalIds -any _ -eq "[PurchaseOrderId]:76222342342")`girin.
    
1. **Kaydet**’i seçin.

1. **Oluştur**’u seçin.  

## <a name="register-your-autopilot-devices"></a>Autopilot cihazlarınızı kaydetme

Autopilot cihazlarınızı kaydetmek için aşağıdaki yollarla birini seçin.

### <a name="register-autopilot-devices-that-are-already-enrolled"></a>Daha önceden kaydedilmiş Autopilot cihazları kaydetme

1. **Hedeflenen cihazların tümünü Autopilot’a dönüştür** ayarı **Evet** olarak belirlenmiş bir Autopilot dağıtım profili oluşturun. 
2. Profili, Autopilot ile otomatik olarak kaydetmek istediğiniz üyeleri içeren bir gruba atayın.

Daha fazla bilgi için bkz. [Bir Autopilot dağıtım profili oluşturma](enrollment-autopilot.md#create-an-autopilot-deployment-profile).

### <a name="register-autopilot-devices-that-arent-enrolled"></a>Daha önceden kaydedilmemiş Autopilot cihazları kaydetme

Henüz kaydedilmemiş cihazlarınız varsa, bunları kendiniz kaydedebilirsiniz. Daha fazla bilgi için bkz. [Cihaz ekleme](enrollment-autopilot.md#add-devices).

### <a name="register-devices-from-an-oem"></a>OEM cihazlarını kaydetme

Yeni cihaz satın alırken bazı OEM’ler cihazları sizin için kaydedebilir. Daha fazla bilgi için bkz. [Windows Autopilot sayfası](https://aka.ms/WindowsAutopilot).

Autopilot cihazlarınız *kaydolduktan*sonra Intune 'a kaydolmadan önce, üç yerde (adları seri numaralarına ayarlanmış adlarla) görüntülenir:
- Azure portal Intune 'daki **Autopilot cihazları** bölmesi. **Cihaz kaydı** > **Windows kayıt** > **cihazları**' nı seçin.
- Azure portal Intune 'daki **Azure AD cihazları** bölmesi. **Azure AD cihazları** > **cihazları** seçin.
- **Tüm**cihazlar > **cihazlar** ' a seçerek Azure Portal Azure Active Directory **Azure AD tüm cihazlar** bölmesi.

Autopilot cihazlarınız kaydedildikten *sonra, bunlar*dört yerde görüntülenir:
- Azure portal Intune 'daki **Autopilot cihazları** bölmesi. **Cihaz kaydı** > **Windows kayıt** > **cihazları**' nı seçin.
- Azure portal Intune 'daki **Azure AD cihazları** bölmesi. **Azure AD cihazları** > **cihazları** seçin.
- Azure portal Azure Active Directory **Azure AD tüm cihazlar** bölmesi. **Tüm cihazlar** > **cihazları** seçin.
- Azure portal Intune 'da bulunan **tüm cihazlar** bölmesi. **Tüm cihazlar** > **cihazları** seçin.

Autopilot cihazlarınız kaydedildikten sonra, adları cihazın ana bilgisayar adı olur. Varsayılan olarak, ana bilgisayar adı *Desktop-* ile başlar.


## <a name="create-and-assign-an-autopilot-deployment-profile"></a>Bir Autopilot dağıtım profili oluşturma ve atama
Autopilot dağıtım profilleri, Autopilot cihazlarını yapılandırmak için kullanılır.

1. [Microsoft Endpoint Manager Yönetim Merkezi](https://go.microsoft.com/fwlink/?linkid=2109431)'Nde, **Windows** > **windows kayıt** > **dağıtım profilleri** > **Profil oluştur** > **cihazlar** ' ı seçin.
2. **Temel bilgiler** sayfasında, bir **ad** ve isteğe bağlı bir **Açıklama**yazın.
3. Atanan gruplardaki tüm cihazların otomatik olarak Autopilot'a dönüştürülmesini istiyorsanız **Hedeflenen tüm cihazları Autopilot'a dönüştür** seçeneğini **Evet** olarak ayarlayın. Atanan gruplardaki şirkete ait olmayan tüm Autopilot cihazları Autopilot dağıtım hizmetine kaydolacaktır. Kişiye ait cihazlar Autopilot 'e dönüştürülmeyecektir. Kaydın işlenmesi için 48 saat kadar bekleyin. Kaydı kaldırılıp sıfırlandığında Autopilot cihazı kaydeder. Bir cihaz bu şekilde kaydedildikten sonra bu seçeneğin devre dışı bırakılması veya profil atamasının kaldırılması cihazı Autopilot dağıtım hizmetinden kaldırmaz. Bunun yerine [cihazı doğrudan kaldırmanız](enrollment-autopilot.md#delete-autopilot-devices) gerekir.
4. **İleri**'yi seçin.
5. **Kullanıma hazır deneyim (OOBE)** sayfasında, **dağıtım modu**için **Kullanıcı odaklı**' ı seçin.
6. **Azure AD 'ye katıl** kutusunda **karma Azure AD 'ye katılmış**' i seçin.
7. **Kullanıma hazır deneyim (OOBE)** sayfasında yer alan diğer seçenekleri gerektiği şekilde yapılandırın.
8. **İleri**'yi seçin.
9. **Kapsam etiketleri** sayfasında bu profil için [kapsam etiketleri](../fundamentals/scope-tags.md) ' ni seçin.
10. **İleri**'yi seçin.
11. **Atamalar** sayfasında, **dahil etmek istediğiniz grupları seçin** > seçin **ve > cihaz grubunu seçin.**
12. **Oluştur** > **İleri ' yi** seçin.

Cihaz profili durumunun *atama* ve, son olarak *atanan* *olarak değiştirilmesi* yaklaşık 15 dakika sürer.

## <a name="optional-turn-on-the-enrollment-status-page"></a>Seçim Kayıt durumu sayfasını aç

1. [Microsoft Endpoint Manager Yönetim Merkezi](https://go.microsoft.com/fwlink/?linkid=2109431)'Nde, **Windows** > **Windows kaydı** > **kayıt durumu sayfası** > **cihazlar** ' ı seçin.
1. **Kayıt durumu sayfası** bölmesinde **varsayılan** > **ayarları**' nı seçin.
1. **Uygulama ve profil yükleme ilerleme durumunu göster** kutusunda **Evet**' i seçin.
1. Diğer seçenekleri gerektiği şekilde yapılandırın.
1. **Kaydet**’i seçin.

## <a name="create-and-assign-a-domain-join-profile"></a>Etki Alanına Katılım profili oluşturma ve atama

1. [Microsoft Endpoint Manager Yönetim Merkezi](https://go.microsoft.com/fwlink/?linkid=2109431)'Nde, **cihaz** > **yapılandırma profilleri** > **Profil oluştur**' u seçin.
2. Aşağıdaki özellikleri girin:
   - **Ad**: Yeni profil için açıklayıcı bir ad girin.
   - **Açıklama**: Profil için bir açıklama girin.
   - **Platform**: **Windows 10 ve üstünü**seçin.
   - **Profil türü**: **etki alanına katılmayı (Önizleme)** seçin.
3. **Ayarlar**' ı seçin ve ardından bir **bilgisayar adı ön eki**, **etki alanı adı**sağlayın.
4. Seçim [DN biçiminde](https://docs.microsoft.com/windows/desktop/ad/object-names-and-identities#distinguished-name)bir **kuruluş birimi** (OU) sağlayın. Seçenekleriniz şunlardır:
   - Intune bağlayıcısını çalıştıran Windows 2016 cihazınıza denetim temsilcisi seçtiğiniz bir OU sağlayın.
   - Şirket içi Active Directory kök bilgisayarlara denetim için temsilci seçtiğiniz bir OU sağlayın.
   - Bu alanı boş bırakırsanız, bilgisayar nesnesi Active Directory varsayılan kapsayıcısında (CN = bilgisayarlar hiçbir [şekilde değiştirilemezse](https://support.microsoft.com/en-us/help/324949/redirecting-the-users-and-computers-containers-in-active-directory-dom)) oluşturulur.
   
   Aşağıda bazı geçerli örnekler verilmiştir:
   - OU = düzey 1, OU = Level2, DC = contoso, DC = com
   - OU = Mine, DC = contoso, DC = com
   
   Geçerli olmayan bazı örnekler şunlardır:
   - CN = Computers, DC = contoso, DC = com (bir kapsayıcı belirtemezsiniz, bunun yerine, etki alanı için varsayılan değerini kullanmak için değeri boş bırakın)
   - OU = Mine (etki alanını DC = öznitelikler aracılığıyla belirtmeniz gerekir)
     
   > [!NOTE]
   > **Kuruluş birimindeki**değerin etrafında tırnak işareti kullanmayın.
5. **Oluştur** > **Tamam ' ı** seçin.  
    Profil oluşturulur ve listede görüntülenir.
6. Profili atamak için, [Cihaz profili atama](../configuration/device-profile-assign.md#assign-a-device-profile) ' nın altındaki adımları izleyin ve profili bu adımda kullanılan gruba atayın [bir cihaz grubu oluşturun](windows-autopilot-hybrid.md#create-a-device-group). Alternatif olarak, farklı etki alanlarına veya OU 'Lara cihaz katılması gerektiğinde farklı gruplar kullanılabilir.

> [!NOTE]
> Karma Azure AD 'ye yönelik Windows Autopilot için adlandırma özellikleri,% SERI% gibi değişkenleri desteklemez ve yalnızca bilgisayar adı için önekleri destekler.

## <a name="next-steps"></a>Sonraki adımlar

Windows Autopilot’ı yapılandırdıktan sonra, bu cihazları nasıl yöneteceğinizi öğrenin. Daha fazla bilgi için bkz. [cihaz yönetimi Microsoft Intune nedir?](../remote-actions/device-management.md).
