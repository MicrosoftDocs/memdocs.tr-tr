---
title: Intune tarafından yönetilen mobil cihazlara uzaktan yardımcı olun
description: Kullanıcılara mobil cihazlarıyla uzaktan yardımcı olmak için dört farklı seçenek kullanabilirsiniz.
keywords: ''
author: ErikjeMS
ms.author: erikje
manager: dougeby
ms.date: 03/20/2020
ms.topic: conceptual
ms.service: microsoft-intune
ms.subservice: remote-actions
ms.localizationpriority: high
ms.technology: ''
ms.assetid: ''
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: 548f63dcbd1635c106573fda40f8cc7bf312866e
ms.sourcegitcommit: 017b93345d8d8de962debfe3db5fc1bda7719079
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/21/2020
ms.locfileid: "80086269"
---
# <a name="remotely-assist-mobile-devices-managed-by-microsoft-endpoint-manager"></a>Microsoft Endpoint Manager tarafından yönetilen mobil cihazlara uzaktan yardımcı olun

Microsoft Endpoint Manager tarafından yönetilen cihazları uzaktan yönetmek için kullanabileceğiniz dört seçenek vardır:

- [Microsoft ekipleri](https://products.office.com/microsoft-teams/) , nerede olursanız olsun sohbet edebilir, karşılayabilir ve işbirliği yapabileceğiniz ekip çalışmaları için merkezdir.
- [Hızlı yardım](https://support.microsoft.com/help/4027243/windows-10-solve-pc-problems-with-quick-assist) , iki kişinin bir cihazı uzak bağlantı üzerinden paylaşmasına imkan tanıyan bir Windows 10 uygulamasıdır.
- [TeamViewer](https://www.teamviewer.com/) , ayrı olarak satın aldığınız üçüncü taraf bir programdır. Kapsamlı bir uzaktan erişim ve destek özellikleri kümesi sağlar. Intune ve [TeamViewer tümleştirmesi](teamviewer-support.md) , TeamViewer kullanarak uzaktan destek sunar ve bağlayıcı doğrudan Intune 'da yönetilir.
- [Uzaktan denetim](https://docs.microsoft.com/configmgr/core/clients/manage/remote-control/introduction-to-remote-control) , Microsoft uç noktası Configuration Manager eklenmiştir. Uzaktan yönetmek, yardım sağlamak veya herhangi bir çalışma grubu bilgisayarını ve etki alanına katılmış bilgisayarları görüntülemek için kullanılır.

| Özellikler, platformlar, lisanslama | **Ekipler** | Hızlı yardım | TeamViewer (Intune) | Uzaktan denetim (ConfigMgr) |
|:---:|:---:|:---:|:---:|:---:|
| Uzaktan görünüm ve denetim |![Onay işareti](../enrollment/media/enrollment-method-capab/checkmark.png)|![Onay işareti](../enrollment/media/enrollment-method-capab/checkmark.png)|![Onay işareti](../enrollment/media/enrollment-method-capab/checkmark.png)|![Onay işareti](../enrollment/media/enrollment-method-capab/checkmark.png)|
| 'İ |![Onay işareti](../enrollment/media/enrollment-method-capab/checkmark.png)||![Onay işareti](../enrollment/media/enrollment-method-capab/checkmark.png)||
| Dosya aktarımı |![Onay işareti](../enrollment/media/enrollment-method-capab/checkmark.png)|![Onay işareti](../enrollment/media/enrollment-method-capab/checkmark.png)|![Onay işareti](../enrollment/media/enrollment-method-capab/checkmark.png)|![Onay işareti](../enrollment/media/enrollment-method-capab/checkmark.png)|
| Yükseltilmiş yönetici erişimi |||![Onay işareti](../enrollment/media/enrollment-method-capab/checkmark.png)|![Onay işareti](../enrollment/media/enrollment-method-capab/checkmark.png)|
| Katılımsız erişim |||![Onay işareti](../enrollment/media/enrollment-method-capab/checkmark.png)|![Onay işareti](../enrollment/media/enrollment-method-capab/checkmark.png)|
| Eşzamanlı uzaktan denetim |![Onay işareti](../enrollment/media/enrollment-method-capab/checkmark.png)|![Onay işareti](../enrollment/media/enrollment-method-capab/checkmark.png)|||
| Çok kullanıcı desteği |||![Onay işareti](../enrollment/media/enrollment-method-capab/checkmark.png)|![Onay işareti](../enrollment/media/enrollment-method-capab/checkmark.png)|
| Uzak eylemler ||![Onay işareti](../enrollment/media/enrollment-method-capab/checkmark.png)|![Onay işareti](../enrollment/media/enrollment-method-capab/checkmark.png)|![Onay işareti](../enrollment/media/enrollment-method-capab/checkmark.png)|
| Internet üzerinden destek |![Onay işareti](../enrollment/media/enrollment-method-capab/checkmark.png)|![Onay işareti](../enrollment/media/enrollment-method-capab/checkmark.png)|![Onay işareti](../enrollment/media/enrollment-method-capab/checkmark.png)||
| Denetim raporlaması |![Onay işareti](../enrollment/media/enrollment-method-capab/checkmark.png)||![Onay işareti](../enrollment/media/enrollment-method-capab/checkmark.png)|![Onay işareti](../enrollment/media/enrollment-method-capab/checkmark.png)|
| Tüm platformlar için destek (Windows, iOS, Android, macOS) |![Onay işareti](../enrollment/media/enrollment-method-capab/checkmark.png)||![Onay işareti](../enrollment/media/enrollment-method-capab/checkmark.png)||
| Windows 10 ile tümleşik – ek uygulama gerekmez ||![Onay işareti](../enrollment/media/enrollment-method-capab/checkmark.png)|||
| Cihazın Configuration Manager ve Intune tarafından ortak yönetilmesi gerekir ||||![Onay işareti](../enrollment/media/enrollment-method-capab/checkmark.png)|
| Ek lisanslama\* gerekir |![Onay işareti](../enrollment/media/enrollment-method-capab/checkmark.png)||![Onay işareti](../enrollment/media/enrollment-method-capab/checkmark.png)|![Onay işareti](../enrollment/media/enrollment-method-capab/checkmark.png)|

\* ekipler O365 veya M365 lisanslama gerektirir. TeamViewer ve Intune kullanımı, hem TeamViewer hem de Intune 'dan lisanslamayı gerektirir. Uzaktan denetim bir Configuration Manager özelliğidir ve Configuration Manager lisanslamayı gerektirir.