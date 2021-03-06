---
title: Microsoft Intune-Azure 'da Yönetim Şablonları kullanarak Microsoft 365 güncelleştirme | Microsoft Docs
description: Microsoft 365 uygulamalarını en son sürüme güncelleştirmek için Microsoft Intune Yönetim şablonlarını kullanın ve Office 'in güncelleştirmeleri ne sıklıkta denetleyeceğini seçin. Office Update 'e yönelik bir Intune ilkesi uygulandığında güncelleştirilecek cihaz kayıt defteri anahtarlarına bakın.
keywords: ''
author: MandiOhlinger
ms.author: mandia
manager: dougeby
ms.date: 05/11/2020
ms.topic: how-to
ms.service: microsoft-intune
ms.subservice: configuration
ms.localizationpriority: high
ms.technology: ''
ms.reviewer: ''
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: 2af6784db43b2513b57d850d85fa4deaa3052613
ms.sourcegitcommit: 94e86320b9340507becc9e6ce4b6eb744f09fcd8
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/31/2020
ms.locfileid: "89193853"
---
# <a name="use-update-channel-and-target-version-settings-to-update-microsoft-365-with-microsoft-intune-administrative-templates"></a>Microsoft Intune Microsoft 365 güncelleştirmek için kanalı güncelleştirme ve hedef sürüm ayarlarını kullanın Yönetim Şablonları

Intune 'da, [Grup İlkesi ayarlarını yapılandırmak Için Windows 10 şablonlarını](administrative-templates-windows.md)kullanabilirsiniz. Bu makalede, Intune 'da yönetim şablonu kullanarak Microsoft 365 güncelleştirme hakkında yönergeler verilmektedir. Ayrıca, ilkelerinizin başarıyla uygulandığını onaylama konusunda rehberlik sağlar. Bu bilgiler, sorun gidermede de yardımcı olur.

Bu senaryoda, Intune 'da cihazlarınızda Microsoft 365 güncelleştiren bir yönetim şablonu oluşturacaksınız.

Yönetim Şablonları hakkında daha fazla bilgi için bkz. [Windows 10 şablonları Grup İlkesi ayarlarını yapılandırmak için](administrative-templates-windows.md).

Aşağıdakiler cihazlar için geçerlidir:

- Windows 10 ve üzeri
- Microsoft 365

## <a name="prerequisites"></a>Ön koşullar

Office uygulamalarınız için [Microsoft 365 Apps otomatik güncelleştirmelerini](/deployoffice/configure-update-settings-for-office-365-proplus) etkinleştirdiğinizden emin olun. Bunu Grup İlkesi veya Intune Office 2016 ADMX şablonu kullanarak yapabilirsiniz:

> [!div class="mx-imgBorder"]
> ![Intune yönetim şablonunda, Office için otomatik güncelleştirmeleri etkinleştir ayarını ayarlayın](./media/administrative-templates-update-office/admx-enable-automatic-updates.png)

## <a name="set-the-update-channel-in-the-intune-administrative-template"></a>Intune yönetim şablonunda güncelleştirme kanalını ayarlama

1. [Intune yönetim şablonunuzda](administrative-templates-windows.md#create-the-template), **kanalı Güncelleştir** ayarına gidin ve istediğiniz kanalı girin. Örneğin şunları seçin `Semi-Annual Channel` :

    > [!div class="mx-imgBorder"]
    > ![Intune yönetim şablonunda, Office için güncelleştirme kanalı ayarını ayarlayın](./media/administrative-templates-update-office/admx-enable-update-channel-setting.png)

    > [!NOTE]
    > Daha sık güncelleştirmeniz önerilir. Yarı yıllık yalnızca örnek olarak kullanılır.

2. İlkeyi Windows 10 cihazlarınıza [atadığınızdan](device-profile-assign.md) emin olun. İlkenizi daha erken test etmek için ilkeyi de eşitleyebilirsiniz:

    - [Intune 'da ilkeyi eşitleme](../remote-actions/device-sync.md)
    - [Cihazdaki ilkeyi el ile eşitleme](../user-help/sync-your-device-manually-windows.md#sync-from-settings-app)

## <a name="check-the-intune-registry-keys"></a>Intune kayıt defteri anahtarlarını denetleme

İlkeyi atadıktan sonra cihaz eşitlendikten sonra, ilkenin uygulandığını doğrulayabilirsiniz:

1. Cihazda, **kayıt defteri Düzenleyicisi** uygulamasını açın.
2. Intune ilke yoluna gidin: `Computer\HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\PolicyManager\Providers\<Provider ID>\default\Device\office16~Policy~L_MicrosoftOfficemachine~L_Updates` .

    > [!TIP]
    > `<Provider ID>`Kayıt defteri anahtarında değişiklik yapılır. Cihazınızın sağlayıcı KIMLIĞINI bulmak için, **kayıt defteri Düzenleyicisi** uygulamasını açın ve adresine gidin `Computer\HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\PolicyManager\AdmxInstalled` . Sağlayıcı KIMLIĞI gösterilir.

    İlke uygulandığında, aşağıdaki kayıt defteri anahtarlarını görürsünüz:

    - `L_UpdateBranch`
    - `L_UpdateTargetVersion`

    Aşağıdaki örneğe bakarak, `L_UpdateBranch` aşağıdakine benzer bir değer görürsünüz `<enabled /><data id="L_UpdateBranchID" value="Deferred" />` . Bu değer, yarı yıllık kanal olarak ayarlanan anlamına gelir:

    > [!div class="mx-imgBorder"]
    > ![Yönetim şablonu L_Updatebranch kayıt defteri anahtarı örneği](./media/administrative-templates-update-office/admx-update-branch-registry-key.png)

    > [!TIP]
    > Değerleri Configuration Manager listeler ve bunların anlamları [olan Microsoft 365 uygulamaları yönetin](/configmgr/sum/deploy-use/manage-office-365-proplus-updates#bkmk_channel) . Kayıt defteri değerleri, seçilen dağıtım kanalını temel alır:
    >
    >- Aylık kanal-değer = "geçerli"
    >- Aylık kanal (hedeflenen)-değer = "geçerli"
    >- Yarı yıllık kanal-değer = "geçerli"
    >- Yarı yıllık kanal (hedefli)-değer = "Firstreleaseertelenmiş"
    >- Insider hızlı-değer = "InsiderFast"

Bu noktada, Intune ilkesi cihaza başarıyla uygulandı.

## <a name="check-the-office-registry-keys"></a>Office kayıt defteri anahtarlarını denetleme

1. Cihazda, **kayıt defteri Düzenleyicisi** uygulamasını açın.
2. Office ilkesi yoluna gidin: `Computer\HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Office\ClickToRun\Configuration` .

    Aşağıdaki kayıt defteri anahtarlarını görürsünüz:

    - `UpdateChannel`: Yapılandırılan ayarlara bağlı olarak değişen dinamik anahtar.
    - `CDNBaseUrl`: Microsoft 365 cihaza yüklediğinde ayarlayın.

3. `UpdateChannel`Değere bakın. Bu değer, Office 'in ne sıklıkla güncelleştirileceğini söyler. Değerleri Configuration Manager listeler ve olarak ayarlandığı [Microsoft 365 uygulamaları yönetin](/configmgr/sum/deploy-use/manage-office-365-proplus-updates#bkmk_channel) .

    Aşağıdaki örneğe bakarak, ' nin, `UpdateChannel` aylık olarak ayarlandığını görürsünüz `http://officecdn.microsoft.com/pr/492350f6-3a01-4f97-b9c0-c7c6ddf67d60` : **monthly**

    > [!div class="mx-imgBorder"]
    > ![Yönetim şablonu Office UpdateChannel kayıt defteri anahtarı örneği](./media/administrative-templates-update-office/admx-update-channel-office-registry-key.png)

    Bu örnek, kısmen **yıllık**değil, hala **aylık**olarak ayarlandığı için ilkenin henüz uygulanmadığı anlamına gelir.

Bu kayıt defteri anahtarı, **Görev Zamanlayıcı**  >  **Office otomatik güncelleştirmeleri 2,0** çalıştırıldığında veya Kullanıcı cihazda oturum açtığında güncelleştirilir. Onaylamak için **Office otomatik güncelleştirmeler 2,0** görev > **tetikleyicilerini**açın. Tetikleyicilere bağlı olarak, `UpdateChannel` kayıt defteri anahtarı güncellendiğinden en az bir gün ve daha fazlasını alabilir.

## <a name="force-office-automatic-updates-to-run"></a>Office otomatik güncelleştirmelerini çalıştırmaya zorla

İlkenizi test etmek için, cihazdaki ilke ayarlarını zorlayabilirsiniz. Aşağıdaki adımlar kayıt defterini güncelleştirir. Her zaman, kayıt defteri güncelleştirilirken dikkatli olun.

1. Kayıt defteri anahtarını temizleyin:

    1. `Computer\HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Office\ClickToRun\Updates` öğesine gidin.
    2. Anahtarı çift seçin `UpdateDetectionLastRunTime` , **Tamam**> değer verisini silin.

2. Office otomatik güncelleştirmeler görevini çalıştırın:

    1. Cihazda **Görev Zamanlayıcı** uygulamasını açın.
    2. **Görev Zamanlayıcı Kitaplığı**  >  **Microsoft**  >  **Office**' i genişletin.
    3. **Office otomatik güncelleştirmeleri 2,0**  >  **Çalıştır**'ı seçin:

        > [!div class="mx-imgBorder"]
        > ![Görev zamanlamasını açın ve Office otomatik güncelleştirmelerini çalıştırın](./media/administrative-templates-update-office/admx-task-scheduler-office-automatic-updates.png)

        Görevin bitmesini bekleyin, bu işlem birkaç dakika sürebilir.

3. **Kayıt defteri Düzenleyicisi** uygulamasında öğesine gidin `Computer\HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Office\ClickToRun\Configuration` . Değeri denetleyin `UpdateChannel` .

    İlkede ayarlanan değerle birlikte güncelleştirilmeleri gerekir. Örneğimizde, değer olarak ayarlanmalıdır `http://officecdn.microsoft.com/pr/7ffbc6bf-bc32-4f92-8982-f9dd17fd3114` .

Bu noktada, Office güncelleştirme kanalı cihazda başarıyla değiştirilmiştir. Durumu denetlemek için, bu güncelleştirmeyi alan bir kullanıcı için bir Microsoft 365 uygulaması açabilirsiniz.

## <a name="force-the-office-synchronization-to-update-account-information"></a>Hesap bilgilerini güncelleştirmek için Office eşitlemesini zorla  

Daha fazlasını yapmak istiyorsanız, Office 'i en son sürüm güncelleştirmesini almaya zorlayabilirsiniz. Aşağıdaki adımlar yalnızca bir onay olarak yapılmalıdır ya da cihazların en son sürüm güncelleştirmesini bu kanaldan hızlıca alması gerekiyorsa. Aksi takdirde, Office 'in işini yapmasına ve otomatik olarak güncelleştirmesine izin verin.

### <a name="step-1-force-the-office-version-to-update"></a>1. Adım: Office sürümünü güncelleştirmek için zorlayın

1. Office sürümünün tercih ettiğiniz güncelleştirme kanalını desteklediğini onaylayın. [Microsoft 365 uygulamalar Için güncelleştirme geçmişi](/officeupdates/update-history-office365-proplus-by-date) , farklı güncelleştirme kanallarını destekleyen yapı numaralarını listeler.

2. [Intune yönetim şablonunuzda](administrative-templates-windows.md#create-the-template), **hedef sürüm** ayarına gidin ve istediğiniz sürümü girin.

    **Hedef sürüm** ayarınız aşağıdaki ayara benzer şekilde görünür:

    > [!div class="mx-imgBorder"]
    > ![Intune yönetim şablonunda, Office için hedef sürüm ayarını ayarlayın](./media/administrative-templates-update-office/admx-enable-target-version-setting.png)

> [!IMPORTANT]
>
> - İlkeyi atadığınızdan emin olun.
> - Var olan bir ilkeyi değiştirirseniz, değişiklikleriniz tüm atanan kullanıcıları etkiler.
> - Bu özelliği test ediyorsanız, bir test ilkesi oluşturmanız ve ilkeyi bir Kullanıcı test grubuna atamanız önerilir.

### <a name="step-2-check-the-office-version"></a>2. Adım: Office sürümünü denetleme

İlkeyi tüm kullanıcılara dağıtmadan önce ilkenizi test etmek için bu adımları kullanmayı göz önünde bulundurun.

1. **Kayıt defteri Düzenleyicisi** uygulamasında şuraya gidin`Computer\HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\PolicyManager\Providers\<Provider ID>\default\Device\office16~Policy~L_MicrosoftOfficemachine~L_Updates`

2. `L_UpdateTargetVersion`Değere bakın. İlke uygulandıktan sonra değer, girdiğiniz sürüme ayarlanır, örneğin `<enabled /><data id="L_UpdateTargetVersionID" value="16.0.10730.20344" />` .

    Bu noktada, Intune ilkesi cihaza başarıyla uygulandı.

3. Ardından, Office 'i güncelleştirmeye zorlayabilirsiniz. Excel gibi bir Office uygulaması açın. Şimdi güncelleştirmeyi seçin (muhtemelen **Hesap** menüsünde).

    Güncelleştirme birkaç dakika sürer. Office 'in girdiğiniz sürümü almaya çalışıyor olduğunu doğrulayabilirsiniz:

      1. Cihazda öğesine gidin `C:\Program Files (x86)\Microsoft Office\Updates\Detection\Version` .
      2. Dosyasını açın `VersionDescriptor.xml` ve `<Version>` bölümüne gidin. Kullanılabilir sürüm, Intune ilkesinde girdiğiniz sürümle aynı olmalıdır, örneğin:

          > [!div class="mx-imgBorder"]
          > ![Sürüm tanımlayıcısı Office XML dosyasındaki sürüm bölümünü denetleyin](./media/administrative-templates-update-office/office-version-descriptor-xml-example.png)

4. Güncelleştirme yüklendikten sonra Office uygulaması yeni sürümü (örneğin, **Hesap** menüsünde) göstermelidir

## <a name="next-steps"></a>Sonraki adımlar

[Microsoft 365 istemcileri için kanal değerlerini Güncelleştir](/configmgr/sum/deploy-use/manage-office-365-proplus-updates#bkmk_channel)

[Microsoft 365 uygulamalar için Office bulut ilkesi hizmetine genel bakış](/deployoffice/overview-office-cloud-policy-service)

[Microsoft Intune 'de Grup İlkesi ayarlarını (ADMX şablonları) yapılandırmak için Windows 10 şablonlarını kullanın](administrative-templates-windows.md)