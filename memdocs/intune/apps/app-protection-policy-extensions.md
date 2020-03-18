---
title: Uzantılar için uygulama koruma ilkeleri
titleSuffix: Microsoft Intune
description: Bu konuda, uzantılar için uygulama koruma ilkesi (APP) açıklanmaktadır.
keywords: ''
author: Erikre
ms.author: erikre
manager: dougeby
ms.date: 01/06/2020
ms.topic: conceptual
ms.service: microsoft-intune
ms.subservice: apps
ms.localizationpriority: high
ms.technology: ''
ms.assetid: ''
ms.reviewer: demerson
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: d7de306a7d4f632b3eedf321323e12c7ad95b713
ms.sourcegitcommit: 3d895be2844bda2177c2c85dc2f09612a1be5490
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/13/2020
ms.locfileid: "79326210"
---
# <a name="protecting-application-extensions"></a>Uygulama uzantılarını koruma

Bu makalede, Microsoft Intune uzantılar için uygulama koruma ilkeleri açıklanmaktadır.

## <a name="add-ins-for-outlook-app"></a>Outlook uygulaması için eklentiler

Outlook eklentileri, popüler uygulamaları e-posta istemcisiyle tümleştirmenize imkan tanır. Outlook için eklentiler Web, Windows, Mac ve Android ve iOS/ıpados için Outlook 'ta kullanılabilir. Intune uygulama SDK 'Sı ve Intune uygulama koruma ilkeleri Outlook eklentilerini yönetme desteğini içermez, ancak kullanımlarını sınırlamak için başka yollar vardır. Eklentiler Microsoft Exchange yoluyla yönetildiğinden, eklentiler kullanıcı için Exchange tarafından kapatılmadığı sürece, kullanıcılar Outlook ile yönetilmeyen eklenti uygulamaları arasında verileri ve iletileri paylaşabilirler.

Son kullanıcılarınızın Outlook eklentilerine erişmesini ve bunları yüklemesini durdurmak isterseniz (bu işlem tüm Outlook istemcilerini etkiler), Exchange yönetim merkezinde rollerde aşağıdaki değişikliklerin yapıldığından emin olun:

- Kullanıcıların Office Mağazası eklentilerini yüklemesini engellemek için, onlardan Marketim rolünü kaldırın.
- Kullanıcıların dışarıdan eklenti yüklemesini engellemek için, onlardan Özel Uygulamalarım rolünü kaldırın.
- Kullanıcıların tüm eklentileri yüklemesini engellemek için, onlardan hem Özel Uygulamalarım rolünü hem de Marketim rolünü kaldırın.

Bu yönergeler Office 365, Exchange 2016, Exchange 2013’te Web üzerinde Outlook genelinde, Windows, Mac ve mobil için geçerlidir.

- [Outlook için eklentiler](https://technet.microsoft.com/library/jj943753(v=exchg.150).aspx) hakkında daha fazla bilgi edinin.
- [Outlook uygulaması için eklentileri yükleyebilecek ve yönetebilecek kullanıcıları ve yöneticileri belirleme](https://technet.microsoft.com/library/jj943754(v=exchg.150).aspx) hakkında daha fazla bilgi edinin.

## <a name="linkedin-account-connections-for-microsoft-apps"></a>Microsoft uygulamaları için LinkedIn hesap bağlantıları

LinkedIn hesap bağlantıları, kullanıcıların belirli Microsoft uygulamalarında LinkedIn profil bilgilerini görmesini sağlar. Varsayılan olarak, kullanıcılarınız ek LinkedIn bilgilerini görmek için LinkedIn ve Microsoft iş veya okul hesaplarını bağlamayı seçebilir. 

> [!NOTE]
> LinkedIn tümleştirmesi şu anda Birleşik Devletler Kamu müşterileri ve Avustralya, Kanada, Çin, Fransa, Almanya, Hindistan, Güney Kore, Birleşik Krallık, Japonya ve Güney Afrika’da barındırılan Exchange Online posta kutularına sahip olan kuruluşlar için kullanılamamaktadır.

Intune SDK’sı ve Intune uygulama koruma ilkeleri, LinkedIn hesap bağlantılarını yönetme desteği içermez. Ancak bunları yönetmenin başka yolları vardır. Tüm kuruluşunuz için LinkedIn hesabı bağlantılarını devre dışı bırakabilir veya kuruluşunuzda seçili kullanıcı grupları için LinkedIn bağlantılarını etkinleştirebilirsiniz. Bu ayar tüm platformlarda (web, mobil ve masaüstü) tüm Office 365 uygulamalarındaki LinkedIn bağlantılarını etkiler. Şunları yapabilirsiniz:

- Azure portalında kiracınız için LinkedIn hesap bağlantılarını etkinleştirin veya devre dışı bırakın. 
- Grup İlkesini kullanarak kuruluşunuzun Office 2016 uygulamalarında LinkedIn hesabı bağlantılarını etkinleştirin veya devre dışı bırakın.

Kiracınız için LinkedIn tümleştirmesi etkinse kuruluşunuzdaki kullanıcılar LinkedIn ve Microsoft iş veya okul hesaplarını bağladıklarında iki seçenekleri bulunur: 

- İki hesap arasında verileri paylaşmak için izin verebilirler. Bu, LinkedIn hesaplarının Microsoft iş veya okul hesaplarıyla veri paylaşmasına ve Microsoft iş veya okul hesaplarının LinkedIn hesaplarıyla veri paylaşmasına izin verdikleri anlamına gelir. LinkedIn ile paylaşılan veriler çevrimiçi hizmetlerden ayrılır. 
- Yalnızca LinkedIn hesaplarından Microsoft iş ve okul hesaplarına veri paylaşmak için izin verebilirler

Bir kullanıcı, Office eklentilerinde olduğu gibi hesaplar arasında veri paylaşımına izin verirse LinkedIn tümleştirmesi mevcut Microsoft Graph API’lerini kullanır. LinkedIn tümleştirmesi, Office eklentileri için kullanılabilir API’lerin yalnızca bir alt kümesini kullanır ve çeşitli dışlamaları destekler.


|Microsoft Graph izinleri  |Açıklama  |
|---------|---------|
|[Kişiler](https://developer.microsoft.com/graph/docs/concepts/permissions_reference#people-permissions) için okuma izinleri     |Uygulamanın oturum açan kullanıcıyla ilgili kişilerin puanlanmış bir listesini okumasına izin verir. Liste; yerel kişileri, sosyal ağ veya kuruluşunuzun dizinindeki kişileri ve son iletişim kurulan kişileri (e-posta ve Skype gibi) içerebilir.         |
|[Takvimler](https://developer.microsoft.com/graph/docs/concepts/permissions_reference#calendars-permissions) için okuma izinleri     |Uygulamanın kullanıcı takvimlerindeki etkinlikleri okumasına izin verir. Oturum açan kullanıcının takvimindeki toplantıları, zamanlarını, yerlerini ve katılımcıları içerir.         |
|[Kullanıcı Profili](https://developer.microsoft.com/graph/docs/concepts/permissions_reference#user-permissions) için okuma izinleri     |Kullanıcıların uygulamada oturum açmasını sağlar ve uygulamanın oturum açan kullanıcıların profilini okumasına izin verir. Ayrıca uygulamanın oturum açan kullanıcılar için temel şirket bilgilerini okumasına izin verir.         |
|Abonelikler     |Bu kapsam mevcut değil ve henüz kullanılmıyor. Kullanıcının kuruluşu tarafından sağlanan Office 365 gibi Microsoft uygulamaları ve hizmetleri aboneliklerini içerir.         |
|İçgörüler     |Bu kapsam mevcut değil ve henüz kullanılmıyor. Oturum açan kullanıcı hesabıyla ilişkili Microsoft hizmetleri kullanımını temel alan ilgi alanlarını içerir.         |

### <a name="learn-more"></a>Daha fazla bilgi

- [Microsoft uygulamalarınızdaki LinkedIn bilgileri ve özellikleri](https://go.microsoft.com/fwlink/?linkid=850740) hakkında bilgi edinin.
- [Office 365 Yol haritası sayfasında](https://products.office.com/en-US/business/office-365-roadmap?filters=%26freeformsearch=linkedin#abc) LinkedIn hesap bağlantıları yayını hakkında bilgi edinin. 
- [LinkedIn hesap bağlantılarını yapılandırma](https://docs.microsoft.com/azure/active-directory/linkedin-integration) hakkında bilgi edinin.
- Kullanıcıların LinkedIn ve Microsoft iş veya okul hesapları arasında paylaşılan veriler hakkında daha fazla bilgi için bkz. [İş veya okulunuzda Microsoft uygulamalarında LinkedIn](https://www.linkedin.com/help/linkedin/answer/84077).

