---
title: Intune Veri Ambarı Koleksiyonları
titleSuffix: Microsoft Intune
description: Intune Veri Ambarı koleksiyonları, Veri Ambarı API’siyle ilgili ayrıntılar sağlar.
keywords: ''
author: Erikre
ms.author: erikre
manager: dougeby
ms.date: 09/08/2020
ms.topic: reference
ms.service: microsoft-intune
ms.subservice: developer
ms.localizationpriority: medium
ms.technology: ''
ms.assetid: 29f09230-dc56-43db-b599-d961967bda49
ms.reviewer: aanavath
ms.suite: ems
search.appverid: MET150
ms.custom: intune
ms.collection: M365-identity-device-management
ms.openlocfilehash: e0a9ecebd86404d4218142d1a3acb591974b027d
ms.sourcegitcommit: 8fc1704ed0e1141f46662bdd32b52bec00fb93b4
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 09/09/2020
ms.locfileid: "89608086"
---
# <a name="intune-data-warehouse-collections"></a>Intune Veri Ambarı Koleksiyonları

Aşağıdaki Intune Veri Ambarı koleksiyonları, Veri Ambarı API’si varlıklarının v1.0 koleksiyonlarının özellikleri, açıklamaları ve örneklerini sağlar. 

## <a name="apprevisions"></a>appRevisions
**Apprevision** varlığı, tüm uygulama sürümlerini listeler.

|          Özellik          |                                      Açıklama                                      |                Örnek               |
|----------------------------|---------------------------------------------------------------------------------------|--------------------------------------|
| appKey                     | Uygulamanın benzersiz tanımlayıcısı.                                                         | 123                                  |
| applicationId              | Uygulamanın benzersiz tanımlayıcısı - AppKey’e benzerdir ancak doğal bir anahtardır.        | b66bc706-ffff-7437-0340-032819502773 |
| revision                   | İkili dosya karşıya yüklenirken yönetici tarafından bahsedilen sürüm.                   | 2                                    |
| başlık                      | Uygulama başlığı.                                                                     | Excel                                |
| yayımcı                  | Uygulama yayımcısı.                                                                 | Microsoft                            |
| uploadState                | Uygulamanın karşıya yüklenme durumu.                                                              | 1                                    |
| appTypeKey                 | Aşağıdaki bölümde açıklanan AppType özelliğine başvuru.                            | 1                                    |
| vppProgramTypeKey          | Aşağıda açıklanan VppProgramType özelliğine başvuru.                                        | 30876                                |
| creationTime               | Düzeltmenin oluşturulduğu saat.                                            | 23.11.2016 0:00                      |
| modifiedTime               | Bu düzeltmeyle ilgili herhangi bir şeyin en son değiştirildiği an.                            | 23.11.2016 0:00                      |
| size                       | İkili dosyanın bayt cinsinden boyutu.                                                          | 120.392.000                          |
| startDateInclusiveUTC      | Bu uygulama düzeltmesinin veri ambarında oluşturulma tarihi ve saati (UTC).      | 23.11.2016 0:00                      |
| endDateExclusiveUTC        | Bu uygulama düzeltmesinin kullanımdan kalkma tarihi ve saati (UTC).                        | 23.11.2016 0:00                      |
| IsCurrent                  | Uygulama sürümünün veri ambarında mevcut olup olmadığını gösterir.         | True/False                           |
| rowLastModifiedDateTimeUTC | Bu uygulama sürümünün veri ambarında son değiştirilme tarihi ve saati (UTC). | 23.11.2016 0:00                      |

## <a name="apptypes"></a>appTypes
**appTypes** varlığı, bir uygulamanın yükleme kaynağını listeler.

|   Özellik  |        Açıklama        |
|-------------|---------------------------|
| Apptypeıd   | Tür kimliği           |
| appTypeKey  | Anahtar için yedek anahtar |
| appTypeName | Uygulama türü                  |

### <a name="example"></a>Örnek

| AppTypeID |                Ad               |                     Açıklama                     |
|-----------|-----------------------------------|-----------------------------------------------------|
| 0         | Android mağazası uygulaması               | Bir Android mağazası uygulaması.                             |
| 1         | Android LOB uygulaması                 | Bir Android iş kolu uygulaması.                  |
| 2         | Yönetilen Android mağazası uygulaması (MAM) | Yönetimi etkin bir Android mağazası uygulaması. |
| 3         | iOS mağazası uygulaması                   | Bir iOS mağazası uygulaması.                                 |
| 4         | iOS LOB uygulaması                     | Bir iOS iş kolu uygulaması.                      |
| 5         | Yönetilen iOS mağazası uygulaması (MAM)     | Yönetimi etkin bir iOS mağazası uygulaması.       |
| 6         | Enterprise için Microsoft 365 uygulamalar        | Windows 10 için Microsoft 365 uygulamalar.     |
| 7         | Web uygulaması                         | Bir web uygulaması.                                        |
| 8         | Windows Phone 8.1 mağazası uygulaması     | Bir Windows Phone 8.1 mağazası uygulaması.                    |
| 9         | Windows mağazası uygulaması               | Bir Windows mağazası uygulaması.                              |
| 10        | Windows LOB uygulaması                | Bir Windows AppX iş kolu uygulaması.              |
| 11        | Windows Mobile MSI              | Bir MSI iş kolu uygulaması.                      |
| 12        | Windows Phone LOB uygulaması           | Bir Windows Phone iş kolu uygulaması.             |

## <a name="compliancepolicystatusdeviceactivities"></a>compliancePolicyStatusDeviceActivities
Aşağıdaki tablo, uyumluluk ilkelerinin cihazlara atanma durumunu özetler. Ve her bir uyumluluk durumunda bulunan cihaz sayısını listeler.

|    Özellik   |                                                                                      Açıklama                                                                                     |  Örnek |
|---------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|----------|
| dateKey       | Uyumluluk ilkesi için özet oluşturulduğu ana ait tarih anahtarı.                                                                                                                   | 20161204 |
| bilinmeyen       | Çevrimdışı olan veya Intune ya da Azure AD ile başka bir nedenle iletişim kuramayan cihaz sayısı.                                                                           | 5        |
| Notapplıcable | Yönetici tarafından hedeflenen cihaz uyumluluk ilkelerinin uygulanabilir olmadığı cihaz sayısı.                                                                                     | 201      |
| Uyumluluk     | Yönetici tarafından hedeflenen bir veya daha fazla cihaz uyumluluk ilkesini başarıyla uygulayan cihaz sayısı.                                                                        | 4083     |
| Yetkisizkullanımsüresinde | Uyumlu olmayan ancak yönetici tarafından belirlenen yetkisiz kullanım süresinde olan cihaz sayısı.                                                                                  | 57       |
| ızde  | Yönetici tarafından hedeflenen bir veya daha fazla cihaz uyumluluk ilkesi ayarını uygulayamayan veya kullanıcısı yönetici tarafından hedeflenen ilkeler ile uyum sağlayamayan cihaz sayısı. | 43       |
|    error      |    Intune veya Azure AD ile iletişim kuramayan ve hata iletisi döndüren cihaz sayısı.                                                                          |    3     |

## <a name="compliancepolicystatusdeviceperpolicyactivities"></a>compliancePolicyStatusDevicePerPolicyActivities
Aşağıdaki tablo, uyumluluk ilkelerinin cihazlara atanma durumunu ilke başına ve ilke türü başına olacak şekilde özetler. Ve her atanmış uyumluluk ilkesi için her bir uyumluluk durumunda bulunan cihaz sayısını listeler.

|      Özellik     |                                                                                      Açıklama                                                                                     |  Örnek |
|-------------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|----------|
| dateKey           | Uyumluluk ilkesi için özet oluşturulduğu ana ait tarih anahtarı.                                                                                                                   | 20161219 |
| policyKey         | Özetin oluşturulduğu uyumluluk ilkesi için anahtar.                                                                                                                   | 10178    |
| policyPlatformKey | Özetin oluşturulduğu uyumluluk ilkesinin platform türü için anahtar.                                                                                            | 5        |
| bilinmeyen           | Çevrimdışı olan veya Intune ya da Azure AD ile başka bir nedenle iletişim kuramayan cihaz sayısı.                                                                           | 13       |
| Notapplıcable     | Yönetici tarafından hedeflenen cihaz uyumluluk ilkelerinin uygulanabilir olmadığı cihaz sayısı.                                                                                     | 3        |
| Uyumluluk         | Yönetici tarafından hedeflenen bir veya daha fazla cihaz uyumluluk ilkesini başarıyla uygulayan cihaz sayısı.                                                                        | 45       |
| Yetkisizkullanımsüresinde     | Uyumlu olmayan ancak yönetici tarafından belirlenen yetkisiz kullanım süresinde olan cihaz sayısı.                                                                                  | 3        |
| ızde      | Yönetici tarafından hedeflenen bir veya daha fazla cihaz uyumluluk ilkesi ayarını uygulayamayan veya kullanıcısı yönetici tarafından hedeflenen ilkeler ile uyum sağlayamayan cihaz sayısı. | 7        |
| error             | Intune veya Azure AD ile iletişim kuramayan ve hata iletisi döndüren cihaz sayısı.                                                                             | 3        |
## <a name="compliancestates"></a>complianceStates

|      Özellik      |                       Açıklama                      |
|--------------------|--------------------------------------------------------|
| complianceStatus   | mdmStatusKey sahibi cihazların uyumluluk durumu       |
| complianceStateKey | Cihaz ve uyumluluk durumuyla eşleşen uyumluluk anahtarı |
| complianceStateID  | Bu uyumluluk durumuyla eşleşen kimlik                |

### <a name="example"></a>Örnek

|  complianceStatus  |                       Açıklama                      |
|--------------------|--------------------------------------------------------|
|    Bilinmiyor         |    Bilinmiyor.                                                                        |
|    Uyumlu       |    Uyumlu.                                                                      |
|    Uyumsuz    |       Cihazın durumu uyumsuz ve şirket kaynaklarına erişimi engelli.             |
|    Çakışma        |    Diğer kurallarla çakışıyor.                                                      |
|    Hata           |       Hata.                                                                       |
|    ConfigManager   |    Yapılandırma Yöneticisi tarafından yönetiliyor.                                                      |
|    InGracePeriod   |       Cihazın durumu uyumsuz ancak yine de şirket kaynaklarına erişimi var          |

## <a name="dates"></a>tarihler
**Date** varlığı, birden çok veri ambarı varlığında başvurulan tarihleri temsil eder.

|     Özellik    |                       Açıklama                      |    Örnek    |
|-----------------|--------------------------------------------------------|---------------|
| dateKey         | Veri ambarında bu tarihin benzersiz tanımlayıcısı. | 20160703      |
| fullDate        | Bu tarihin tam Tarih/Saat biçiminde temsili.        | 3.7.2016 0:00 |
| dayOfWeek       | Haftanın kaçıncı günü olduğu                                            | 1             |
| dayOfMonth      | Ayın kaçıncı günü olduğu                                           | 3             |
| dayOfYear       | Yılın kaçıncı günü olduğu                                            | 185           |
| weekOfYear      | Yılın kaçıncı haftası olduğu                                           | 28            |
| monthOfYear     | Yılın kaçıncı ayı olduğu                                      | 7             |
| calendarQuarter | Takvim çeyreği                                       | 3             |
| Takvim yılı    | Takvim yılı                                          | 2016          |
| dateKey         | Veri ambarında bu tarihin benzersiz tanımlayıcısı. | 20160703      |
| fullDate        | Bu tarihin tam Tarih/Saat biçiminde temsili.        | 3.7.2016 0:00 |
| dayOfWeek       | Haftanın kaçıncı günü olduğu                                            | 1             |
| dayOfMonth      | Ayın kaçıncı günü olduğu                                           | 3             |
| dayOfYear       | Yılın kaçıncı günü olduğu                                            | 185           |
| weekOfYear      | Yılın kaçıncı haftası olduğu                                           | 28            |
| monthOfYear     | Yılın kaçıncı ayı olduğu                                      | 7             |
| calendarQuarter | Takvim çeyreği                                       | 3             |
| Takvim yılı    | Takvim yılı                                          | 2016          |

## <a name="devicecategories"></a>deviceCategories

|      Özellik      |                                    Açıklama                                   |                Örnek               |
|--------------------|----------------------------------------------------------------------------------|--------------------------------------|
| deviceCategoryID   | Cihaz kategorisi için benzersiz tanımlayıcı.                                       | fb415ba2-7c08-41f6-a5e5-685b50da2c4c |
| deviceCategoryKey  | Veri ambarındaki cihaz kategorisinin benzersiz tanımlayıcısı - vekil anahtar | 1                                    |
| deviceCategoryName | Cihaz kategorisi için görünen ad.                                            | Smartphones                          |

## <a name="deviceconfigurationprofiledeviceactivities"></a>deviceConfigurationProfileDeviceActivities
**DeviceConfigurationProfileDeviceActivity** varlığı, başarılı, beklemede, başarısız veya hata durumundaki cihazların günlük sayısını listeler. Bu sayı, varlığa atanmış Cihaz Yapılandırma Profillerini gösterir. Örneğin, bir cihaz kendisine atanan tüm ilkeler için başarılı durumunda ise ilgili gün için başarılı sayacı bir artar. Cihaza biri başarılı diğeri hata durumunda olmak üzere iki profil atanmışsa varlık, başarılı sayacını artırır ve cihazı hata durumuna geçirir. Varlık, son 30 gün içindeki belirli bir gün için kaç cihazın hangi durumda olduğunu listeler.

|  Özellik |                                          Açıklama                                          |  Örnek |
|-----------|-----------------------------------------------------------------------------------------------|----------|
| dateKey   | Cihaz Yapılandırma Profilinin iade işleminin, veri ambarına kaydedildiği zamanı belirten Tarih Anahtarı. | 20160703 |
| bekleniyor   | Bekleme durumundaki benzersiz cihazların sayısı.                                                    | 123      |
| başarılı | Başarı durumundaki benzersiz cihazların sayısı.                                                    | 12       |
| error     | Hata durumundaki benzersiz cihazların sayısı.                                                      | 10       |
| başarısız    | Başarısız durumundaki benzersiz cihazların sayısı.                                                     | 2        |

## <a name="deviceconfigurationprofileuseractivities"></a>deviceConfigurationProfileUserActivities 
**DeviceConfigurationProfileUserActivity** varlığı; başarılı, beklemede, başarısız veya hata durumundaki kullanıcıların günlük sayısını listeler. Bu sayı, varlığa atanmış Cihaz Yapılandırma Profillerini gösterir. Örneğin, bir kullanıcı kendisine atanan tüm ilkeler için başarılı durumunda ise ilgili gün için başarılı sayacı bir artar. Bir kullanıcıya biri başarılı diğeri hata durumunda olmak üzere iki profil atanmışsa, kullanıcı hata durumunda olarak değerlendirilir. **DeviceConfigurationProfileUserActivity** varlığı, son 30 gün içindeki belirli bir gün için kaç kullanıcının hangi durumda olduğunu listeler. 

| Özellik  | Açıklama  | Örnek  |
|------------|----------------------------------------------------------------------------------------------|-----------|
| dateKey  | Cihaz Yapılandırma Profilinin iade işleminin, veri ambarına kaydedildiği zamanı belirten Tarih Anahtarı.  | 20160703  |
| bekleniyor  | Bekleme durumundaki benzersiz kullanıcıların sayısı.  | 123  |
| başarılı  | Başarı durumundaki benzersiz kullanıcıların sayısı.  | 12  |
| error  | Hata durumundaki benzersiz kullanıcıların sayısı.  | 10  |
| başarısız  | Başarısız durumundaki benzersiz kullanıcıların sayısı.  | 2  |

## <a name="devicepropertyhistories"></a>devicePropertyHistories

|          Özellik          |                                                                                      Açıklama                                                                                     |
|----------------------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| dateKey                    | Günü gösteren tarih tablosuna başvuru.                                                                                                                                          |
| deviceKey                  | Veri ambarındaki cihazın benzersiz tanımlayıcısı - vekil anahtar. Bu, Intune cihaz kimliğini barındıran Cihaz tablosuna bir başvurudur.                               |
| deviceName                 | Cihaz adlandırmaya izin veren platformlardaki cihaz adı. Buna izin vermeyen platformlarda ise Intune, diğer özelliklerden bir ad oluşturur. Bu öznitelik tüm cihazlarda kullanılamaz. |
| deviceRegistrationStateKey | Bu cihazın cihaz kayıt durumu özniteliğinin anahtarı.                                                                                                                    |
| ownerTypeKey               | Cihazın sahip türü özniteliğinin anahtarı: şirket, kişisel veya bilinmeyen.                                                                                                  |
| managementStateKey         | Cihazla ilişkili yönetim durumunun anahtarı, bir uzak eylemin en son durumunu veya cihazda jailbreak yapılıp yapılmamış ya da kök erişim izni verilip verilmemiş olduğunu gösterir.                                                |
| azureADRegistered          | Bu cihazın Azure Active Directory’ye kayıtlı olup olmadığını gösterir.                                                                                                                             |
| complianceStateKey         | Bir ComplianceState anahtarı.                                                                                                                                                            |
| oSVersion                  | İşletim sistemi sürümü.                                                                                                                                                                          |
| Jailbreak uygulanmış                 | Cihazda jailbreak yapılıp yapılmadığı veya kök erişim izni verilip verilmediğini gösterir.                                                                                                                                         |
| deviceCategoryKey          | Bu cihaz için cihaz kategorisi özniteliğinin anahtarı.                                                                                                                                    |
| Physicalmemorybytes      | Bayt cinsinden fiziksel bellek.                                                                                                                                    |
| totalStorageSpaceInBytes      | Toplam depolama kapasitesi (bayt cinsinden).                                                                                                                                    |


## <a name="deviceregistrationstates"></a>deviceRegistrationStates
**DeviceRegistrationState** varlığı, diğer veri ambarı koleksiyonları tarafından başvurulan kayıt türünü temsil eder. 

|           Özellik          |                                     Açıklama                                     |
|-----------------------------|-------------------------------------------------------------------------------------|
| deviceRegistrationStateID   | Kayıt durumu için benzersiz tanımlayıcı                                            |
| deviceRegistrationStateKey  | Veri ambarındaki kayıt durumunun benzersiz tanımlayıcısı - vekil anahtar |
| deviceRegistrationStateName | Kayıt durumu                                                                  |
|    notRegistered                     |    NotRegistered                                                                                                                                                                  |
|    kaydedilmeyecek                        |       Kaydedildi                                                                                                                                                                   |
|    mediyse                           |       Durum, BT yöneticisinin istemciyi engellediği anlamına gelir ve istemcinin engeli kaldırılabilir. Bir cihaz ayrıca, silindikten veya devre dışı bırakıldıktan sonra İptal Edildi durumunda olabilir.        |
|    keyConflict                       |    Anahtar Çakışması                                                                                                                                                                    |
|    approvalPending                   |    Onay Bekleniyor                                                                                                                                                                |
|    Sertifika Atereset                  |    Sertifikayı sıfırla                                                                                                                                                               |
|    notRegisteredPendingEnrollment    |    Kaydedilmedi kayıt bekleniyor                                                                                                                                               |
|    bilinmeyen                           |    Bilinmeyen durum                                                                                                                                                                   |

## <a name="devices"></a>cihazlar
**Device** varlığı, yönetime kaydedilen tüm cihazları ve bunlara karşılık gelen özellikleri listeler.

|          Özellik          |                                                                                       Açıklama                                                                                      |
|----------------------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| deviceKey                  | Veri ambarındaki cihazın benzersiz tanımlayıcısı - vekil anahtar.                                                                                                               |
| deviceId                   | Cihazın benzersiz tanımlayıcısı.                                                                                                                                                     |
| deviceName                 | Cihaz adlandırmaya izin veren platformlardaki cihaz adı. Diğer platformlarda ise Intune, diğer özelliklerden bir ad oluşturur. Bu öznitelik tüm cihazlarda kullanılamaz. |
| deviceTypeKey              | Bu cihazın cihaz türü özniteliğinin anahtarı.                                                                                                                                    |
| deviceRegistrationState    | Bu cihazın istemci kayıt durumu özniteliğinin anahtarı.                                                                                                                      |
| ownerTypeKey               | Cihaz için sahip türü özniteliğinin anahtarı: şirket, kişisel veya bilinmeyen.                                                                                                    |
| Kaydoleddatetime           | Bu cihazın kaydedildiği tarih ve saat.                                                                                                                                         |
| ethernetMacAddress           | Bu cihazın benzersiz ağ tanımlayıcısı.                                                                                                                                         |
| lastSyncDateTime           | Cihazın bilinen son Intune iadesi.                                                                                                                                              |
| managementAgentKey         | Bu cihazla ilişkili yönetim aracısının anahtarı.                                                                                                                             |
| managementStateKey         | Cihazla ilişkili yönetim durumunun anahtarı, bir uzak eylemin en son durumunu veya cihazda jailbreak yapılıp yapılmamış ya da kök erişim izni verilip verilmemiş olduğunu gösterir.                                                |
| Azureaddeviceıd            | Bu cihazın Azure cihaz kimliği.                                                                                                                                                  |
| azureADRegistered          | Bu cihazın Azure Active Directory’ye kayıtlı olup olmadığını gösterir.                                                                                                                             |
| deviceCategoryKey          | Cihazla ilişkili kategorinin anahtarı.                                                                                                                                     |
| Devicekayıtlarını Menttype       | Bu cihazla ilişkili kayıt türünün anahtarı, kayıt yöntemini gösterir.                                                                                             |
| complianceStateKey         | Cihazla ilişkili Uyumluluk durumu anahtarı.                                                                                                                             |
| office365Version           | Cihaza yüklü Microsoft 365 sürümü.                                                                                                                             |
| oSVersion                  | Cihazın işletim sistemi sürümü.                                                                                                                                                |
| Easdeviceıd                | Cihazın Exchange ActiveSync KIMLIĞI.                                                                                                                                                  |
| serialNumber               | SerialNumber                                                                                                                                                                           |
| userId                     | Cihazla ilişkili kullanıcının Benzersiz Tanımlayıcısı.                                                                                                                           |
| rowLastModifiedDateTimeUTC | Bu cihazın veri ambarında son değiştirilme tarihi ve saati (UTC).                                                                                                       |
| üretici               | Cihazın üreticisi                                                                                                                                                             |
| model                      | Cihazın modeli                                                                                                                                                                    |
| operatingSystem            | Cihazın işletim sistemi. Windows, iOS/ıpados, vb.                                                                                                                                   |
| isDeleted                  | Bu cihazın silinip silinmediğini gösteren ikili dosya.                                                                                                                                 |
| androidSecurityPatchLevel  | Android güvenlik düzeltme eki düzeyi                                                                                                                                                           |
| MEID                       | MEID                                                                                                                                                                                   |
| isSupervised               | Cihaz denetimli durumu                                                                                                                                                               |
| freeStorageSpaceInBytes    | Bayt cinsinden boş depolama alanı.                                                                                                                                                                 |
| encryptionState            | Cihazdaki şifreleme durumu.                                                                                                                                                      |
| subscriberCarrier          | Cihazın abone taşıyıcısı                                                                                                                                                       |
| phoneNumber                | Cihazın telefon numarası                                                                                                                                                             |
| IMEI                       | IMEI                                                                                                                                                                                   |
| cellularTechnology         | Cihazın hücresel teknolojisi.                                                                                                                                                    |
| wiFiMacAddress             | Wi-Fi MAC.                                                                                                                                                                              |
| windowsOsEdition             | Windows Işletim sistemi sürümü.                                                                                                                                                                              |


## <a name="devicetypes"></a>deviceTypes
**deviceType** varlığı, diğer veri ambarı varlıkları tarafından başvurulan cihaz türünü temsil eder. Cihaz türü genellikle cihaz modelini, üreticisini veya her ikisini de belirtir.

|    Özellik    |                                  Açıklama                                 |
|----------------|------------------------------------------------------------------------------|
| deviceTypeID   | Cihaz türünün benzersiz tanımlayıcısı                                       |
| deviceTypeKey  | Veri ambarındaki cihaz türünün benzersiz tanımlayıcısı - vekil anahtar |
| deviceTypeName | Cihaz türü                                                                |

### <a name="example"></a>Örnek

| deviceTypeID |        Ad       |                      Açıklama                      |
|--------------|-------------------|-------------------------------------------------------|
| -1           | Kullanılamıyor   | Cihaz türü kullanılamıyor.                     |
| 0            | Masaüstü           | Windows Masaüstü cihaz                              |
| 1            | Windows           | Windows cihaz                                      |
| 2            | WinMO6            | Windows Mobile 6.0 cihaz                           |
| 3            | Nokia             | Nokia cihaz                                        |
| 4            | WindowsPhone      | Windows Phone cihaz                                |
| 5            | Mac               | Mac cihaz                                          |
| 6            | WinCE             | Windows CE cihaz                                   |
| 7            | WinEmbedded       | Windows Embedded cihaz                             |
| 8            | IPhone            | iPhone cihaz                                       |
| 9            | IPad              | iPad cihaz                                         |
| 10           | IPod              | iPod cihaz                                         |
| 11           | Android           | Cihaz Yöneticisi ile yönetilen Android cihaz   |
| 12           | ISocConsumer      | iSoc Consumer cihaz                                |
| 13           | Unix              | Unix cihaz                                         |
| 14           | MacMDM            | Yerleşik MDM aracısıyla yönetilen OS X cihazı |
| 15           | HoloLens          | HoloLens cihazı                                       |
| 16           | SurfaceHub        | Surface Hub cihaz                                  |
| 17           | AndroidForWork    | Android cihaz - Android Profil Sahibi kullanılarak yönetiliyor  |
| 18           | AndroidEnterprise | Android kurumsal cihaz.                          |
| 100          | Blackberry        | Blackberry Cihaz                                   |
| 101          | Palm              | Palm cihaz                                         |
| 255          | Bilinmiyor           | Bilinmeyen cihaz türü                                 |

## <a name="deviceenrollmenttypes"></a>deviceEnrollmentTypes
**deviceEnrollmentType** varlığı, bir cihazın nasıl kaydedildiğini gösterir. Kayıt türü, kayıt yöntemini yakalar. Örnekler, farklı kayıt türlerini ve bunların ne anlama geldiğini listeler.

|         Özellik         |                                    Açıklama                                    |
|--------------------------|-----------------------------------------------------------------------------------|
| deviceEnrollmentTypeID   | Kayıt türünün benzersiz tanımlayıcısı.                                       |
| deviceEnrollmentTypeKey  | Veri ambarındaki kayıt türünün benzersiz tanımlayıcısı - vekil anahtar. |
| deviceEnrollmentTypeName | Kayıt türü adı.                                                           |

### <a name="example"></a>Örnek

| enrollmentTypeID |                Ad                |                                        Açıklama                                       |
|------------------|------------------------------------|------------------------------------------------------------------------------------------|
| 0                | Bilinmiyor                            | Kayıt türü toplanmadı                                                      |
| 1                | UserEnrollment                     | KCG kanalı üzerinden kullanıcı yoluyla kayıt.                                           |
| 2                | DeviceEnrollmentManager            | Cihaz kayıt yöneticisi hesabıyla kullanıcı kaydı.                              |
| 3                | AppleBulkWithUser                  | Kullanıcı sınaması ile Apple toplu kaydı. (DEP, Apple Configurator)                   |
| 4                | AppleBulkWithoutUser               | Kullanıcı sınaması olmadan Apple toplu kaydı.   (DEP, Apple Configurator, Mobil Yapılandırma) |
| 5                | WindowsAzureADJoin                 | Windows 10 Azure AD Katılımı.                                                                |
| 6                | WindowsBulkUserless                | Sertifika ile ICD yoluyla Windows 10 Toplu kaydı.                               |
| 7                | WindowsAutoEnrollment              | Windows 10 otomatik kayıt.   (İş hesabı ekleyin)                                    |
| 8                | WindowsBulkAzureDomainJoin         | Windows 10 toplu Azure AD Katılımı.                                                           |
| 9                | WindowsCoManagement                | AutoPilot veya grup ilkesi tarafından tetiklenen Windows 10 ortak yönetimi.                       |
| 10               | WindowsAzureADJoinsUsingDeviceAuth | Cihaz Kimlik Doğrulaması yoluyla Windows 10 Azure AD Katılımı.                                            |

## <a name="enrollmentactivities"></a>Kayıt \ tüm 
KayıtSayısı **varlığı,** bir cihaz kaydının etkinliğini gösterir.

| Özellik                      | Açıklama                                                               |
|-------------------------------|---------------------------------------------------------------------------|
| dateKey                       | Bu kayıt etkinliğinin kaydedildiği tarih anahtarı.               |
| deviceEnrollmentTypeKey       | Kayıt türünün anahtarı.                                        |
| deviceTypeKey                 | Cihaz türünün anahtarı.                                                |
| Kayıtanahtarı      | Kaydın başarı veya başarısızlık durumunu gösteren anahtar.    |
| Kayıt%0 kategori anahtarı  | Kayıt hatası kategorisinin anahtarı (kayıt başarısız olduysa).        |
| Kayıtefailurereasonkey    | Kayıt hatası nedeninin anahtarı (kayıt başarısız olursa).          |
| osVersion                     | Cihazın işletim sistemi sürümü.                               |
| count                         | Yukarıdaki sınıflandırmalarla eşleşen kayıt etkinliklerinin toplam sayısı.  |

## <a name="enrollmenteventstatuses"></a>kayıt \ Menteventdurumlar 
KayıtSayısı **varlığı,** bir cihaz kaydının sonucunu gösterir.

| Özellik                   | Açıklama                                                                       |
|----------------------------|-----------------------------------------------------------------------------------|
| Kayıtanahtarı   | Veri ambarındaki (vekil anahtar) kayıt durumunun benzersiz tanımlayıcısı  |
| KayıtAdı Menteventstatusname  | Kayıt durumunun adı. Aşağıdaki örneklere bakın.                            |

### <a name="example"></a>Örnek

| KayıtAdı Menteventstatusname  | Açıklama                            |
|----------------------------|----------------------------------------|
| Başarılı                    | Başarılı bir cihaz kaydı         |
| Başarısız                     | Hatalı bir cihaz kaydı             |
| Kullanılamaz              | Kayıt durumu kullanılamıyor.  |

## <a name="enrollmentfailurecategories"></a>kayıtkonumunda Mentfailurecategories 
**Kayıt%0 kategori** varlığı, cihaz kaydının neden başarısız olduğunu gösterir. 

| Özellik                       | Açıklama                                                                                 |
|--------------------------------|---------------------------------------------------------------------------------------------|
| Kayıt%0 kategori anahtarı   | Veri ambarındaki (vekil anahtar) kayıt hatası kategorisinin benzersiz tanıtıcısı  |
| kayıtkonumunda Mentfailurecategoryname  | Kayıt hatası kategorisinin adı. Aşağıdaki örneklere bakın.                            |

### <a name="example"></a>Örnek

| kayıtkonumunda Mentfailurecategoryname   | Açıklama                                                                                                   |
|---------------------------------|---------------------------------------------------------------------------------------------------------------|
| Geçerli değil                  | Kayıt hatası kategorisi geçerli değil.                                                            |
| Kullanılamaz                   | Kayıt hatası kategorisi kullanılamıyor.                                                             |
| Bilinmiyor                         | Bilinmeyen hata.                                                                                                |
| Kimlik Doğrulaması                  | Kimlik doğrulaması gerçekleştirilemedi.                                                                                        |
| Yetkilendirme                   | Çağrının kimliği doğrulandı, ancak kaydolma yetkisi yok.                                                         |
| AccountValidation               | Kayıt için Hesap doğrulanamadı. (Hesap engellendi, kayıt etkin değil)                      |
| Kullanıcı doğrulaması                  | Kullanıcı doğrulanamadı. (Kullanıcı yok, Lisans eksik)                                           |
| DeviceNotSupported              | Cihaz mobil cihaz yönetimi için desteklenmiyor.                                                         |
| Inmaintenance                   | Hesap bakımda.                                                                                    |
| Işlemindeki hatalı istek                      | İstemci, hizmet tarafından anlaşılmayan/desteklenmeyen bir istek gönderdi.                                        |
| FeatureNotSupported             | Bu kayıt tarafından kullanılan Özellik (ler) Bu hesap için desteklenmiyor.                                        |
| EnrollmentRestrictionsEnforced  | Yönetici tarafından yapılandırılan kayıt kısıtlamaları bu kaydı engelledi.                                          |
| Clientconnected              | İstemci zaman aşımına uğradı veya kayıt Son Kullanıcı tarafından iptal edildi.                                                        |
| Kullanıcı bırakma                 | Kayıt Son Kullanıcı tarafından bırakıldı. (Son Kullanıcı ekleme başlattı ancak zamanında tamamlanamadı)  |

## <a name="enrollmentfailurereasons"></a>kayıtkullanım Failurereadönemleri  
**Kayıtlımafailurereason** varlığı, belirli bir hata kategorisindeki cihaz kaydı hatasının daha ayrıntılı bir nedenini gösterir.  

| Özellik                     | Açıklama                                                                               |
|------------------------------|-------------------------------------------------------------------------------------------|
| Kayıtefailurereasonkey   | Veri ambarındaki (vekil anahtar) kayıt hatası nedeninin benzersiz tanıtıcısı  |
| Kayıtefailurereasonname  | Kayıt hatası nedeninin adı. Aşağıdaki örneklere bakın.                            |

### <a name="example"></a>Örnek

| Kayıtefailurereasonname      | Açıklama                                                                                                                                                                                            |
|----------------------------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| Geçerli değil                   | Kayıt hatası nedeni geçerli değil.                                                                                                                                                       |
| Kullanılamaz                    | Kayıt hatası nedeni kullanılamıyor.                                                                                                                                                        |
| Bilinmiyor                          | Bilinmeyen hata.                                                                                                                                                                                         |
| Usernotlisanslanmış                  | Kullanıcı Intune 'da bulunamadı veya geçerli bir lisansı yok.                                                                                                                                     |
| Kullanıcı bilinmiyor                      | Kullanıcı Intune tarafından tanınmıyor.                                                                                                                                                                           |
| BulkAlreadyEnrolledDevice        | Bir cihazı yalnızca tek bir Kullanıcı kaydedebilir. Bu cihaz daha önce başka bir kullanıcı tarafından kaydedilmiş.                                                                                                                |
| EnrollmentOnboardingIssue        | Intune mobil cihaz yönetimi (MDM) yetkilisi henüz yapılandırılmadı.                                                                                                                                 |
| AppleChallengeIssue              | İOS Yönetim profili yüklemesi gecikti veya başarısız oldu.                                                                                                                                         |
| AppleOnboardingIssue             | Intune 'a kaydolmak için bir Apple MDM anında iletme sertifikası gerekir.                                                                                                                                       |
| DeviceCap                        | Kullanıcı izin verilen üst sınıra göre daha fazla cihaz kaydetmeyi denedi.                                                                                                                                        |
| Authenticationgereksinimnotmet  | Intune kayıt hizmeti bu isteği yetkilendiremedi.                                                                                                                                            |
| UnsupportedDeviceType            | Bu cihaz, Intune kaydı için en düşük gereksinimleri karşılamıyor.                                                                                                                                  |
| EnrollmentCriteriaNotMet         | Bu cihaz, yapılandırılmış bir kayıt kısıtlama kuralı nedeniyle kayıt yapamadı.                                                                                                                          |
| Bulkdevicenotpreryumura       | Bu cihazın uluslararası mobil ekipman tanımlayıcısı (ıMEı) veya seri numarası bulunamadı.  Bu tanımlayıcı olmadan, cihazlar, şu anda engellenen kişiye ait cihazlar olarak tanınır.  |
| FeatureNotSupported              | Kullanıcı, tüm müşteriler için henüz yayınlanmamış olan veya Intune yapılandırmanızla uyumlu olmayan bir özelliğe erişmeye çalışıyor.                                                            |
| Kullanıcı bırakma                  | Kayıt Son Kullanıcı tarafından bırakıldı. (Son Kullanıcı ekleme başlattı ancak zamanında tamamlanamadı)                                                                                           |
| Apnscercertificate kullanım dışı           | Apple cihazları, zaman aşımına uğradı bir Apple MDM anında iletme sertifikasıyla yönetilemez.                                                                                                                            |

## <a name="intunemanagementextensions"></a>intuneManagementExtensions
**Intunemanagementextension** , gün başına her Windows 10 cihazında **ıntunemanagementextension** sistem durumunu listeler. Son 60 günün verileri alınır.

|       Özellik      |                          Açıklama                          | Örnek |
|---------------------|---------------------------------------------------------------|---------|
| dateKey             | Tarihin benzersiz tanımlayıcısı.                                | 123     |
| tenantKey           | Kiracının benzersiz tanımlayıcısı.                              | 456     |
| deviceKey           | Cihazın benzersiz tanımlayıcısı.                              | 789     |
| extensionVersionKey | IntuneManagementExtension sürümünün benzersiz tanımlayıcısı. | 1       |
| extensionStateKey   | Sistem durumunun benzersiz tanımlayıcısı.                            | 2       |

## <a name="intunemanagementextensionhealthstates"></a>intuneManagementExtensionHealthStates
**Intunemanagemenısionhealthstate** , **ıntunemanagementextension**'ın tüm olası sistem durumlarını listeler.

|      Özellik     |                   Açıklama                  | Örnek |
|-------------------|------------------------------------------------|---------|
| extensionStateKey | Sistem durumunun benzersiz tanımlayıcısı.           | 2       |
| extensionState    | Bir IntuneManagementExtension uzantısının durumu. | Sağlam |

## <a name="intunemanagementextensionversions"></a>intuneManagementExtensionVersions
**Intunemanagemenbir Sionversion** varlığı, **ıntunemanagementextension**tarafından kullanılan tüm sürümleri listeler.

|       Özellik      |                          Açıklama                          | Örnek |
|---------------------|---------------------------------------------------------------|---------|
| extensionVersionKey | IntuneManagementExtension sürümünün benzersiz tanımlayıcısı. | 1       |
| extensionVersion    | 4 basamaklı sürüm numarası.                                   | 1.0.2.0 |

## <a name="mamapplications"></a>MamApplications

**MamApplication** varlığı, Mobil Uygulama Yönetimi (MAM) aracılığıyla yönetilen ancak kuruluşunuza kayıtlı olmayan iş kolu (LOB) uygulamalarını listeler.

| Özellik | Açıklama | Örnek |
|---------|------------|--------|
| mamApplicationKey |MAM uygulamasının benzersiz tanıtıcısı. | 432 |
| mamApplicationName |MAM uygulamasının adı. |MAM uygulaması örnek adı |
| mamApplicationId |MAM uygulamasının uygulama KIMLIĞI. | 123 |
| isDeleted |Bu MAM uygulaması kaydının güncelleştirilip güncelleştirilmediğini gösterir. <br>True- MAM uygulamasının bu tablodaki güncelleştirilmiş alanları içeren yeni bir kaydı var. <br>False- bu MAM uygulaması için en son kayıt. |True/False |
| startDateInclusiveUTC |Bu MAM uygulamasının veri ambarında oluşturulduğu tarih ve UTC diliminde saat. |23/11/2016 00:00:00 |
| deletedDateUTC |IsDeleted değerinin True olarak değiştirildiği tarih ve UTC diliminde saat. |23/11/2016 00:00:00 |
| rowLastModifiedDateTimeUTC |Bu MAM uygulamasının veri ambarında son değiştirildiği tarih ve UTC diliminde saat. |23/11/2016 00:00:00 |


## <a name="mamapplicationinstances"></a>MamApplicationInstances

**MamApplicationInstance** varlığı, Mobil Uygulama Yönetimi (MAM) uygulamalarını kullanıcı ve cihaz başına tekil örnekler olarak listeler. Varlıkta listelenen tüm kullanıcılar ve cihazlar korunur. Örneğin, hepsine en az bir MAM İlkesi atanmıştır.


|          Özellik          |                                                                                                  Açıklama                                                                                                  |               Örnek                |
|----------------------------|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|--------------------------------------|
|   Applicationınstancekey ile   |                                                               Veri ambarındaki MAM uygulaması örneğinin benzersiz tanımlayıcısı - vekil anahtar.                                                                |                 123                  |
|           userId           |                                                                              Bu MAM uygulamasını yükleyen kullanıcının kullanıcı KIMLIĞI.                                                                              | b66bc706-ffff-7437-0340-032819502773 |
|   ApplicationInstanceId    |                                              MAM uygulaması örneğinin benzersiz tanımlayıcısı - ApplicationInstanceKey ile benzer ancak tanımlayıcı, bir doğal anahtardır.                                              | b66bc706-ffff-7437-0340-032819502773 |
| mamApplicationId | Bu mam uygulama örneğinin oluşturulduğu mam uygulamasının uygulama KIMLIĞI.   | 23/11/2016 00:00:00   |
|     applicationVersion     |                                                                                     Bu MAM uygulamasının uygulama sürümü.                                                                                      |                  2                   |
|        createdDate         |                                                                 Bu MAM uygulama örneği kaydının oluşturulduğu tarih. Değer null olabilir.                                                                 |        23/11/2016 00:00:00        |
|          platform          |                                                                          MAM uygulamasının yüklü olduğu cihazın platformu.                                                                           |                  2                   |
|      platformVersion       |                                                                      Bu MAM uygulamasının yüklü olduğu cihazın platform sürümü.                                                                       |                 2.2                  |
|         SDK sürümü         |                                                                            Bu MAM uygulamasını sarmalayan MAM SDK sürümü.                                                                            |                 3.2                  |
| Mamdeviceıd | MAM uygulama örneğinin ilişkilendirildiği cihazın cihaz KIMLIĞI.   | 23/11/2016 00:00:00   |
| mamDeviceType | MAM uygulama örneğinin ilişkilendirildiği cihazın cihaz türü.   | 23/11/2016 00:00:00   |
| Mamaygıtadı | MAM uygulama örneğinin ilişkilendirildiği cihazın cihaz adı.   | 23/11/2016 00:00:00   |
|         isDeleted          | Bu MAM uygulama örneği kaydının güncelleştirilip güncelleştirilmediğini gösterir. <br>True- bu MAM uygulaması örneğinin, bu tablodaki güncelleştirilmiş alanları içeren yeni bir kaydı var. <br>False- bu MAM uygulaması örneği için en son kayıt. |              True/False              |
|   StartDate, Iveutc    |                                                              Bu MAM uygulaması örneğinin, veri ambarında oluşturulduğu tarih ve UTC diliminde saat.                                                               |        23/11/2016 00:00:00        |
|       deletedDateUtc       |                                                                             IsDeleted değerinin True olarak değiştirildiği tarih ve UTC diliminde saat.                                                                              |        23/11/2016 00:00:00        |
| rowLastModifiedDateTimeUtc |                                                           Bu MAM uygulaması örneğinin, veri ambarında son değiştirildiği tarih ve UTC diliminde saat.                                                            |        23/11/2016 00:00:00        |

## <a name="mamcheckins"></a>MamCheckins

**MamCheckin** varlığı, bir Mobil Uygulama Yönetimi (MAM) uygulama örneği Intune Hizmetine iade etme işlemi yaparken toplanan verileri temsil eder. 

> [!Note]  
> Bir uygulama örneği gün içinde birden çok kez iade etme işlemi yaparsa, veri ambarı bunu tek bir iade etme işlemi olarak depolar.

| Özellik | Açıklama | Örnek |
|---------|------------|--------|
| dateKey |MAM uygulamasının iade işleminin, veri ambarına kaydedildiği zamanı belirten tarih anahtarı. | 20160703 |
| Applicationınstancekey ile |Bu MAM uygulamasının iade işlemiyle ilişkili uygulama örneğinin anahtarı. | 123 |
| userKey |Bu MAM uygulamasının iade işlemiyle ilişkili kullanıcı anahtarı. | 4323 |
| mamApplicationKey |MAM uygulama denetimi ile ilişkili uygulamanın uygulama anahtarı. | 432 |
| Devicehealthkey ile |Bu MAM uygulamasının iade işlemiyle ilişkili DeviceHealth için anahtar. | 321 |
| ; platformKey ile |Bu MAM uygulamasının iade işlemiyle ilişkili cihaz platformunu temsil eder. |123 |
| Lastcheckındate |Bu MAM uygulamasının en son iade etme işlemi yaptığı tarih ve saat. Değer null olabilir. |23/11/2016 00:00:00 |

## <a name="mamdevicehealths"></a>MamDeviceHealths

**MamDeviceHealth** varlığı, işletim sistemi kısıtlamaları kaldırılmış olsa bile Mobil Uygulama Yönetimi (MAM) ilkelerinin dağıtıldığı cihazları temsil eder.

| Özellik | Açıklama | Örnek |
|---------|------------|--------|
| Devicehealthkey ile |Cihazın ve cihazla ilişkili sistem durumunun, veri ambarındaki benzersiz tanımlayıcısı - vekil anahtar. |123 |
| deviceHealth |Cihazın ve cihazla ilişkili sistem durumunun benzersiz tanımlayıcısı - DeviceHealthKey ile benzer ancak tanımlayıcı, doğal bir anahtardır. |b66bc706-ffff-7777-0340-032819502773 |
| deviceHealthName |Cihazın durumunu temsil eder. <br>Kullanılamıyor - bu cihaz hakkında bilgi yok. <br>İyi durumda - cihazın işletim sistemi kısıtlamaları kaldırılmamış. <br>İyi durumda değil - cihazın işletim sistemi kısıtlamaları kaldırılmış. |Kullanılamıyor, İyi durumda, İyi durumda değil |
| rowLastModifiedDateTimeUtc |Bu MAM Cihaz Durumunun, veri ambarında son değiştirildiği tarih ve UTC diliminde saat. |23/11/2016 00:00:00 |

## <a name="mamplatforms"></a>MamPlatforms

**MamPlatform** varlığı, Mobil Uygulama Yönetimi (MAM) uygulamasının yüklendiği platform adlarını ve türlerini listeler.


|          Özellik          |                                    Açıklama                                    |                         Örnek                         |
|----------------------------|-----------------------------------------------------------------------------------|---------------------------------------------------------|
|        ; platformKey ile         |     Veri ambarındaki platformun benzersiz tanımlayıcısı - vekil anahtar.      |                           123                           |
|          platform          | Platformun benzersiz tanımlayıcısı; PlatformKey ile benzer ancak doğal bir anahtardır. |                           123                           |
|        platformName        |                                   Platform adı                                   | Kullanılamaz <br>Yok <br>Windows <br>IOS <br>Android. |
| rowLastModifiedDateTimeUtc | Bu platformun veri ambarında son değiştirildiği tarih ve UTC diliminde saat.  |                 23/11/2016 00:00:00                  |

## <a name="managementagenttypes"></a>managementAgentTypes
**managementAgentType** varlığı, bir cihazı yönetmek için kullanılan aracıları temsil eder.

|         Özellik        |                                       Açıklama                                       |
|-------------------------|-----------------------------------------------------------------------------------------|
| Managementagenttypeıd   | Yönetim aracısı türünün benzersiz tanımlayıcısı.                                         |
| managementAgentTypeKey  | Veri ambarındaki yönetim aracısı türünün benzersiz tanımlayıcısı - vekil anahtar. |
| managementAgentTypeName | Cihazı yönetmek için ne tür bir aracı kullanıldığını gösterir.                              |

### <a name="example"></a>Örnek

| ManagementAgentTypeID |                Ad               |                                  Açıklama                                 |
|-----------------------|-----------------------------------|------------------------------------------------------------------------------|
| 1                     | EAS                               | Cihaz, Exchange Active Sync yoluyla yönetiliyor                         |
| 2                     | MDM                               | Cihaz, bir MDM aracısı kullanılarak yönetiliyor                                   |
| 3                     | EasMdm                            | Cihaz, Exchange Active Sync ve bir MDM aracısıyla yönetiliyor        |
| 4                     | IntuneClient                      | Cihaz, Intune bilgisayar aracısı tarafından yönetiliyor                               |
| 5                     | EasIntuneClient                   | Cihaz, Exchange Active Sync ve Intune bilgisayar aracısıyla yönetiliyor |
| 8                     | ConfigManagerClient               | Cihaz, Configuration Manager Aracısı tarafından yönetiliyor     |
| 10                    | ConfigurationManagerClientMdm     | Cihaz, Configuration Manager ve MDM tarafından yönetiliyor.                    |
| 11                    | ConfigurationManagerCLientMdmEas  | Cihaz Configuration Manager, MDM ve Exchange Active Sync tarafından yönetilir.               |
| 16                    | Bilinmiyor                           | Bilinmeyen yönetim aracısı türü                                              |
| 32                    | Jamf                              | Cihaz öznitelikleri Jamf’den getirilir.                               |
| 64                    | GoogleCloudDevicePolicyController |  Cihaz, Google’ın CloudDPC hizmeti tarafından yönetiliyor.                                 |

## <a name="managementstates"></a>managementStates
**ManagementState** varlığı, cihazın durumu hakkında ayrıntılar sağlar. Ayrıntılar; uzak eylemlerin uygulandığı, cihaza jailbreak uygulandığı veya cihazın kökünün belirtildiği durumlarda faydalı olabilir.

|       Özellik      |                                     Açıklama                                    |
|---------------------|------------------------------------------------------------------------------------|
| managementStateID   | Yönetim durumunun benzersiz tanımlayıcısı.                                       |
| managementStateKey  | Veri ambarındaki yönetim durumunun benzersiz tanımlayıcısı - vekil anahtar. |
| managementStateName | Cihaza uygulanan uzak eylemin durumunu gösterir.                 |

### <a name="example"></a>Örnek

| managementStateID |      Ad      |                                                   Açıklama                                                   |
|-------------------|----------------|-----------------------------------------------------------------------------------------------------------------|
| 0                 | Yönetilen        | Hiçbir bekleyen uzak eylem olmadan yönetilir.                                                                       |
| 1                 | RetirePending  | Cihaz için bekleyen bir devre dışı bırakma komutu var.                                                             |
| 2                 | RetireFailed   | Devre dışı bırakma komutu cihazda başarısız oldu.                                                                      |
| 3                 | WipePending    | Cihaz için bekleyen bir silme komutu var.                                                               |
| 4                 | WipeFailed     | Silme komutu cihazda başarısız oldu.                                                                        |
| 5                 | Uygun Değil      | Kötü durumda.                                                                                              |
| 6                 | DeletePending  | Cihaz için bekleyen bir silme komutu var.                                                             |
| 7                 | RetireIssued   | Cihaza bir devre dışı bırakma komutu verildi.                                                               |
| 8                 | WipeIssued     | Bir silme komutu verildi.                                                                               |
| 9                 | WipeCanceled   | Silme komutu iptal edildi.                                                                               |
| 10                | RetireCanceled | Devre dışı bırakma komutu iptal edildi.                                                                             |
| 11                | Bulundu     | Cihaz, Intune tarafından yeni keşfedildi. İlk defa iade edildikten sonra -Yönetiliyor- durumuna geçer. |

## <a name="mobileappinstallstates"></a>mobileAppInstallStates
MobileAppInstallState varlığı, bir mobil uygulama cihaz, kullanıcı veya her ikisini de içeren bir gruba atandıktan sonra uygulamanın yükleme durumunu temsil eder.

|       Özellik      |                        Açıklama                       |
|---------------------|----------------------------------------------------------|
| Appınstallstatekey  | Hesabınız için uygulama yükleme durumunun benzersiz kimliği. |
| Appınstallstate     | Uygulama yükleme durumunun Enum değeri.                     |
| Appınstallstatename | Uygulama yükleme durumunun adı.                           |

## <a name="mobileappinstallstatuscounts"></a>mobileAppInstallStatusCounts
Microsoft Intune yoluyla Mobil Uygulama Yönetimini kullanarak bir hedef cihaz türü için mobil uygulama yükleme durumunu temsil eder.

|      Özellik      |                                                          Açıklama                                                          |
|--------------------|-------------------------------------------------------------------------------------------------------------------------------|
| dateKey            | Uygulama yükleme durumunun kaydedildiği tarihin anahtarı.                                                                     |
| appKey             | AppRevision örneğini tanımlamak için kullanılan mobil uygulamanın anahtarı.                                                          |
| deviceTypeKey      | Mobil Uygulama ile ilişkili Cihaz Türü anahtarı.                                                              |
| Appınstallstatekey | MobileAppInstallState örneğini tanımlamak için kullanılan uygulama yükleme durumunun anahtarı.                                         |
| Raporladı          | Uygulama yükleyicisi, mobil platform veya uygulamanın yüklemesiyle ilgili hizmet tarafından döndürülen hata kodu. |
| count              | Toplam miktar.                                                                                                                  |

## <a name="ownertypes"></a>ownerTypes
**ownerType** varlığı; bir cihazın sahipliğinin şirket, kişisel veya bilinmeyen olduğunu gösterir.

|    Özellik   |                                                                                     Açıklama                                                                                    |           Örnek          |
|---------------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|----------------------------|
| ownerTypeID   | Sahip türünün benzersiz tanımlayıcısı.                                                                                                                                               |                            |
| ownerTypeKey  | Veri ambarındaki sahip türünün benzersiz tanımlayıcısı - vekil anahtar.                                                                                                       |                            |
| ownerTypeName | Cihazların sahip türünü temsil eder: Kurumsal cihaz kuruluşa aittir.  Kişisel - Cihaz kişiye aittir (KCG).   Bilinmiyor - Bu cihazda bilgi yok. | Şirket kişisel bilinmiyor |

> [!Note]  
> `ownerTypeName`Cihazlar Için dinamik gruplar oluştururken AzureAD içindeki filtre için değeri olarak ayarlamanız gerekir `deviceOwnership` `Company` . Daha fazla bilgi için bkz. [Cihazlar Için kurallar](/azure/active-directory/users-groups-roles/groups-dynamic-membership#rules-for-devices). 

## <a name="policies"></a>ilkeler
**İlke** varlığı, cihaz yapılandırma profillerini, uygulama yapılandırma profillerini ve uyumluluk ilkelerini listeler. Kuruluşunuzda bir gruba Mobil Cihaz Yönetimi (MDM) ilkeleri atayabilirsiniz.

|          Özellik          |                                                                       Açıklama                                                                      |                Örnek               |
|----------------------------|--------------------------------------------------------------------------------------------------------------------------------------------------------|--------------------------------------|
| policyKey                  | Veri ambarında ilkeyi temsil eden Benzersiz Anahtar.                                                                                              | 123                                  |
| PolicyId                   | İlkenin veri ambarındaki benzersiz tanımlayıcısı.                                                                                                 | b66bc706-ffff-7437-0340-032819502773 |
| policyName                 | İlkenin Adı.                                                                                                                                    | "Windows 10 Temel"                |
| policyVersion              | Yapılandırmanın Sürümü. İlke düzenlendiğinde veya değiştirildiğinde, daha yeni bir sürüm oluşturulur.                                                             | 1, 2, 3                              |
| isDeleted                  | Bu İlke kaydının güncelleştirilip güncelleştirilmediğini gösterir.  True - İlkenin güncelleştirilmiş alanları içeren yeni bir kaydı var.  False - İlke için en son kayıt. | True/False                           |
| startDateInclusiveUTC      | Bu ilkenin veri ambarında oluşturulma tarihi ve saati (UTC).                                                                              | 23.11.2016 0:00                      |
| deletedDateUTC             | IsDeleted değerinin True olarak değiştirildiği tarih ve UTC diliminde saat.                                                                                                   | 23.11.2016 0:00                      |
| rowLastModifiedDateTimeUTC | Bu ilkenin veri ambarında son değiştirilme tarihi ve saati (UTC).                                                                        | 23.11.2016 0:00                      |

## <a name="policydeviceactivities"></a>policyDeviceActivities
Aşağıdaki tablo; başarılı, beklemede, başarısız veya hata durumundaki cihazların günlük sayısını listeler. Bu sayı, İlke Türü profillerindeki verileri yansıtır. Örneğin, bir cihaz kendisine atanan tüm ilkeler için başarılı durumunda ise ilgili gün için başarılı sayacı bir artar. Cihaza biri başarılı diğeri hata durumunda olmak üzere iki profil atanmışsa varlık, başarılı sayacını artırır ve cihazı hata durumuna geçirir. **policyDeviceActivity** varlığı, son 30 gün içindeki belirli bir gün için kaç cihazın hangi durumda olduğunu listeler.

|  Özellik |                                           Açıklama                                           |        Örnek        |
|-----------|-------------------------------------------------------------------------------------------------|-----------------------|
| dateKey   | Cihaz Yapılandırma Profilinin iade işleminin, veri ambarına kaydedildiği zamanı belirten Tarih Anahtarı. | 20160703              |
| bekleniyor   | Bekleme durumundaki benzersiz cihazların sayısı.                                                    | 123                   |
| başarılı | Başarı durumundaki benzersiz cihazların sayısı.                                                    | 12                    |
| policyKey | İlke Anahtarı, İlke ile birleştirilerek policyName elde edilebilir.                                  | Windows 10 temel |
| error     | Hata durumundaki benzersiz Cihazların sayısı.                                                      | 10                    |
| başarısız    | Başarısız durumundaki benzersiz Cihazların sayısı.                                                     | 2                     |

## <a name="policyplatformtypes"></a>policyPlatformTypes

|        Özellik        |                      Açıklama                      |     Örnek    |
|------------------------|-------------------------------------------------------|----------------|
| policyPlatformTypeKey  | İlke platform türü için benzersiz anahtar.        | 20170519       |
| Policyplatformtypeıd   | İlke platform türü için benzersiz tanımlayıcı. | 1              |
| policyPlatformTypeName | İlke platform türünün adı.              | AndroidForWork |

## <a name="policytypeactivities"></a>policyTypeActivities
**PolicyTypeActivity** varlığı, başarılı, beklemede, başarısız veya hata durumundaki cihazların toplam sayısını listeler. Bu durumları cihazın yapılandırma profiline, uygulama yapılandırma profiline veya uyumluluk ilkesine göre günlük olarak listeler.

|    Özellik   |                                          Açıklama                                          |           Örnek           |
|---------------|-----------------------------------------------------------------------------------------------|-----------------------------|
| dateKey       | Cihaz Yapılandırma Profilinin iade işleminin, veri ambarına kaydedildiği zamanı belirten Tarih Anahtarı. | 20160703                    |
| policyKey     | İlke Anahtarı, İlke ile birleştirilerek policyName elde edilebilir.                                | Windows 10 temel         |
| policyTypeKey | İlke Anahtarı türü, İlke Türü ile birleştirilerek ilke türü adı elde edilebilir.             | Windows 10 Uyumluluk İlkesi |
| bekleniyor       | Bekleme durumundaki benzersiz cihazların sayısı.                                                    | 123                         |
| başarılı     | Başarı durumundaki benzersiz cihazların sayısı.                                                    | 12                          |
| error         | Hata durumundaki benzersiz cihazların sayısı.                                                      | 10                          |
| başarısız        | Başarısız durumundaki benzersiz cihazların sayısı.                                                     | 2                           |

## <a name="policytypes"></a>policyTypes
**PolicyType** varlığı, cihaz yapılandırma profillerini, uygulama yapılandırma profillerini ve Uyumluluk ilkeleri türlerini listeler. Kuruluşunuzda bir gruba Mobil Cihaz Yönetimi (MDM) ilkeleri atayabilirsiniz.

|    Özellik    |                       Açıklama                      |            Örnek            |
|----------------|--------------------------------------------------------|-------------------------------|
| Policytypeıd   | İlkenin kaynak sistemindeki benzersiz tanımlayıcısı.  | 123                           |
| policyTypeKey  | İlkenin veri ambarındaki benzersiz tanımlayıcısı. | 1                             |
| policyTypeName | İlke türünün adı.                               | Windows 10 Uyumluluk ilkesi. |

## <a name="policyuseractivities"></a>policyUserActivities
Aşağıdaki tablo; başarılı, beklemede, başarısız veya hata durumundaki kullanıcıların günlük sayısını listeler. Bu sayı, İlke Türü profillerindeki verileri yansıtır. Örneğin, bir kullanıcı kendisine atanan tüm ilkeler için başarılı durumunda ise ilgili gün için başarılı sayacı bir artar. Bir kullanıcıya biri başarılı diğeri hata durumunda olmak üzere iki profil atanmışsa, kullanıcı hata durumunda olarak değerlendirilir. **PolicyUserActivity** varlığı, son 30 gün içindeki belirli bir gün için kaç kullanıcının hangi durumda olduğunu listeler.

|  Özellik |                                          Açıklama                                          |       Örnek       |
|-----------|-----------------------------------------------------------------------------------------------|---------------------|
| dateKey   | Cihaz Yapılandırma Profilinin iade işleminin, veri ambarına kaydedildiği zamanı belirten Tarih Anahtarı. | 20160703            |
| bekleniyor   | Bekleme durumundaki benzersiz cihazların sayısı.                                                    | 123                 |
| başarılı | Başarı durumundaki benzersiz cihazların sayısı.                                                    | 12                  |
| policyKey | İlke Anahtarı, İlke ile birleştirilerek policyName elde edilebilir.                                | Windows 10 temel |
| error     | Hata durumundaki benzersiz cihazların sayısı.                                                      | 10                  |

## <a name="termsandconditions"></a>termsAndConditions
**termsAndConditions** varlığı, bir Hüküm ve Koşullar (T-C) ilkesinin meta verilerini ve içeriğini temsil eder. T-C ilkelerinin içeriği, kullanıcılara Intune’a ilk kaydolmaya çalıştıklarında ve bir yönetici yeniden kabul gerektirdiğinde içerikte yapılan düzenlemelerden sonra sunulur. Bu ilkeler, yöneticilerin bir kullanıcının Intune’a cihaz kaydetmesi için onaylaması gereken sağlamaları sunmasını sağlar.

|    Özellik        |    Açıklama    |    Örnek        |
|----------------------------------|-----------------------------------------------------------------------------------------------|-----------------------------------------------------------|
|    termsAndConditionsKey    |    ' Usertermsandconditionsaccepler ' koleksiyonundaki bir girdiye karşılık gelen bir anahtar    |    123    |
|    termsAndCondidionsId    |    Bu termsAndConditions girişinin kimliği    |    276edcb7-7440-4339-b6c5-8b6fc556fee6    |
|    termsAndConditionsVersion    |    Bu hüküm ve koşullar girişinin sürümü    |    1    |
|    name    |    Bu termsAndConditions girişinin adı.        |    Intune kullanım koşulları     |
|    açıklama    |    Bu hüküm ve koşulların açıklaması.     |         |
|    başlık    |    Bu hüküm ve koşulların başlığı.     |    Cihaz yönetimi şirket ilkesi        |
|    summaryOfTerms    |    Kullanıcıya verilen koşulların özeti.     |    Hüküm ve koşulları kabul ediyorum.    |
|    termsAndConditionsBodyText    |    Bu hüküm ve koşulların metin gövdesi.       |    *Cihaz şifreleme* 6 basamaklı PIN zorlama    |
|    isDeleted    |    Bu değerin silinip silinmediğine ilişkin True veya False değerleri.     |    Yanlış    |
|    startDateInclusiveUTC    |    Bu hüküm ve koşulların başlama tarihi.     |    23.8.2018 4:01:34 ÖÖ    |
|    endDateEclusiveUTC    |    Bu hüküm ve koşulların bitiş tarihi.     |    31.12.9999 12.00.00 ÖÖ    |

## <a name="userdeviceassociations"></a>userDeviceAssociations
**UserDeviceAssociation** varlığı kuruluşunuzdaki kullanıcı cihaz ilişkilerini içerir.

|        Ad        |                                             Açıklama                                            |     Örnek     |
|--------------------|----------------------------------------------------------------------------------------------------|-----------------|
| userKey            | Kullanıcının veri ambarındaki benzersiz tanımlayıcısı.   (Yedek anahtar).                            | 123             |
| deviceKey          | Cihazın veri ambarındaki benzersiz tanımlayıcısı.                                             | 123             |
| createdDateTimeUTC | Kullanıcı cihaz ilişkisinin oluşturulduğu tarih ve saat. UTC biçimini kullanır.                     | 23.11.2016 0:00 |
| isDeleted          | Kullanıcının cihaz kaydını kaldırdığını ve ilişkinin artık geçerli olmadığını gösterir. | True/False      |
| endedDateTimeUTC   | IsDeleted değerinin True olarak değiştirildiği tarih ve UTC diliminde saat.                                               | 23.6.2017 0:00  |

## <a name="users"></a>kullanıcılar
**user** varlığı, kuruluşunuzda kendisine lisans atanmış olan tüm Azure Active Directory (Azure AD) kullanıcılarını listeler.

**Kullanıcı** varlık koleksiyonu, kullanıcı verilerini içerir. Bu kayıtlar, kullanıcı kaldırıldıysa dahi, veri toplama döneminde kullanıcı durumlarını içerir. Örneğin, bir kullanıcı Intune'a eklenebilir ve son bir ay içerisinde kaldırılabilir. Bu kullanıcı, raporun olduğu saatte bulunmasa da kullanıcı ve durum, önceki ayın verilerinde bulunuyor. Kullanıcının verilerinizdeki varlığının süresini gösterecek bir rapor oluşturabilirsiniz.

|          Özellik          |                                                                                                           Açıklama                                                                                                          |                Örnek               |
|----------------------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|--------------------------------------|
| userKey                    | Veri ambarındaki kullanıcının benzersiz tanımlayıcısı - vekil anahtar.                                                                                                                                                         | 123                                  |
| userId                     | Kullanıcının benzersiz tanımlayıcısı - UserKey’e benzerdir ancak doğal bir anahtardır.                                                                                                                                                    | b66bc706-ffff-7437-0340-032819502773 |
| Kullanıcı e-postası                  | Kullanıcının e-posta adresi.                                                                                                                                                                                                     | John@constoso.com                    |
| userPrincipalName                        | Kullanıcının kullanıcı asıl adı.                                                                                                                                                                                               | John@constoso.com                    |
| displayName                | Kullanıcının görünen adı.                                                                                                                                                                                                      | John                                 |
| ıntunelisanslanmış             | Kullanıcının Intune lisansı olup olmadığını belirtir.                                                                                                                                                                              | True/False                           |
| isDeleted                  | Kullanıcının tüm lisanslarının geçerliliğini yitirip yitirmediğini ve kullanıcının buna bağlı olarak Intune’dan kaldırılıp kaldırılmadığını belirtir. Tek bir kayıt için bu bayrak değişmez. Bunun yerine, yeni bir kullanıcı durumu için yeni bir kayıt oluşturulur. | True/False                           |
| rowLastModifiedDateTimeUTC | Kaydın veri ambarında son değiştirilme tarihi ve saati (UTC)                                                                                                                                                 | 23.11.2016 0:00                      |

## <a name="usertermsandconditionsacceptances"></a>userTermsAndConditionsAcceptances
**userTermsAndConditionsAcceptance** varlığı, bir Hüküm ve Koşullar (T-C) ilkesinin bir kullanıcı tarafından kabul durumunu temsil eder. Kullanıcılar, Şirket Portalı’na erişimlerini koruyabilmek için bu koşulların en güncel sürümünü kabul etmelidir.

|    Özellik    |    Açıklama    |    Örnek    |
|-------------------------------|--------------------------------------------------------------------------------|----------------------------|
|    dateKey    |    ' Tarihlerin ' koleksiyonundaki bir tarih değerlerine karşılık gelen bir anahtar.     |    20180823    |
|    userKey    |    ' Kullanıcılar ' koleksiyonundaki bir kullanıcıya Kullanıcı anahtarı eşleme.     |    20000    |
|    termsAndConditionsKey    |    ' TermsAndConditions ' koleksiyonundaki bir girdiye karşılık gelen bir anahtar    |    1    |
|    acceptedDateTimeUTC    |    Kullanıcının bu hüküm ve koşulları kabul ettiği saat    |    23.8.2018 4:01:34 ÖÖ    |
|    lastModifiedDateTimeUTC    |    Bu girişin son değiştirildiği zaman.     |    23.8.2018 4:01:34 ÖÖ    |

## <a name="vppprogramtypes"></a>vppProgramTypes 
**vppProgramType** varlığı, bir uygulama için olası VPP program türlerini listeler.

|      Özellik      |          Açıklama         |
|--------------------|------------------------------|
| Vppprogramtypeıd   | Tür kimliği.           |
| vppProgramTypeKey  | Anahtar için vekil anahtar. |
| vppProgramTypeName | VPP Program türü.          |

### <a name="example"></a>Örnek

|             VppProgramID             |         Ad        | Açıklama                |
|--------------------------------------|---------------------|----------------------------|
| 3DDA2474-470B-4503-9830-2665C21C1945 | Microsoft           | Microsoft’un VPP programı. |
| 00000000-0000-0000-0000-000000000000 | Henüz Kullanılamıyor | Varsayılan değer, VPP Yok.   |
| B54814E0-68EA-4BA4-8088-B5AAB58E737B | Apple               | Apple’ın VPP programı.     |

## <a name="next-steps"></a>Sonraki adımlar

Intune Veri Ambarı hakkında daha fazla bilgi için bkz. [Veri Ambarı veri modeli](reports-ref-data-model.md).