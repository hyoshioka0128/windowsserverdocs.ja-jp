---
ms.assetid: c5eb3fa0-550c-4a2f-a0bc-698b690c4199
title: オンプレミスのデバイス ベースの条件付きアクセスを計画する
description: ''
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adfs
ms.openlocfilehash: 3a78334f64d9e51515757b01f2d788bf87f67a35
ms.sourcegitcommit: cd12ace92e7251daaa4e9fabf1d8418632879d38
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/04/2019
ms.locfileid: "66501610"
---
# <a name="plan-device-based-conditional-access-on-premises"></a>オンプレミスのデバイス ベースの条件付きアクセスを計画する


このドキュメントでは、内部設置型ディレクトリが Azure AD Connect を使用して Azure AD に接続されているハイブリッド シナリオでのデバイスに基づいて条件付きアクセス ポリシーについて説明します。     

## <a name="ad-fs-and-hybrid-conditional-access"></a>AD FS とハイブリッドの条件付きアクセス  

AD FS では、ハイブリッド シナリオで条件付きアクセス ポリシーに内部設置型コンポーネントを提供します。  クラウド リソースへの条件付きアクセスの Azure AD でデバイスを登録するときに Azure AD Connect のデバイスの書き戻しを使用して適用するポリシーを AD FS のオンプレミス機能が利用可能なにあるデバイスの登録情報を使用します。  これにより、内部設置型の両方のアクセス制御ポリシーと、クラウド リソースを一貫した方法があります。  

![条件付きアクセス](media/Plan-Device-based-Conditional-Access-on-Premises/ADFS_ITPRO4.png)  

### <a name="types-of-registered-devices"></a>登録済みデバイスの種類  
Azure AD でデバイス オブジェクトとして表されもオンプレミスの AD FS による条件付きアクセスのために使用するすべての登録済みのデバイスの 3 つの種類があります。  

| |作業を追加または学校のアカウント  |Azure AD への参加  |Windows 10 ドメイン参加    
| --- | --- |--- | --- |
|説明    |  ユーザーは、作業内容を追加または学校のアカウントを BYOD デバイスを対話的にします。  **注:** 職場または学校アカウントは、ワークプ レース ジョイン Windows 8/8.1 で置換を追加       | ユーザーは、その作業の Windows 10 デバイスを Azure AD に参加します。|Windows 10 ドメインに参加したデバイスは、Azure AD に自動的に登録します。|           
|デバイスへのユーザーのログオン     |  職場または学校のアカウントとしての windows ログインはありません。  Microsoft アカウントを使用してログインします。       |   デバイスの登録 (職場または学校) のアカウントとして Windows にログインします。      |     AD のアカウントを使用してログインします。|      
|デバイスの管理方法    |      MDM ポリシー (とその他の Intune 登録)   | MDM ポリシー (とその他の Intune 登録)        |   グループ ポリシー、System Center Configuration Manager (SCCM) |
|Azure AD 信頼の種類|社内参加しています。|Azure AD 参加済み|ドメインに参加する  |     
|W10 設定の場所    | 設定 > アカウント > お客様のアカウント > 職場または学校のアカウントを追加        | 設定 > システム > に関する > Azure AD に参加       |   設定 > システム > に関する > ドメインに参加します。 |       
|IOS および Android デバイスにも使用可能ですか。   |    〇     |       X  |   X   |   

  

デバイスを登録するさまざまな方法の詳細についても参照してください。  
* [Windows 10 デバイスを職場で使用](https://azure.microsoft.com/documentation/articles/active-directory-azureadjoin-windows10-devices/)  
* [作業用に Windows 10 デバイスの設定](https://jairocadena.com/2016/01/18/setting-up-windows-10-devices-for-work-domain-join-azure-ad-join-and-add-work-or-school-account/)  
[Windows 10 Mobile を Azure Active Directory に参加させる](https://technet.microsoft.com/itpro/windows/manage/join-windows-10-mobile-to-azure-active-directory)  

### <a name="how-windows-10-user-and-device-sign-on-is-different-from-previous-versions"></a>Windows 10 のユーザーとデバイスのサインオンが以前のバージョンから別の方法  
Windows 10 およびデバイスの登録と認証の一部の新しい機能がある AD FS 2016 について知っておくべき (特になじみのデバイスの登録と「ワークプ レース ジョイン」以前のリリースである) 場合。  

最初に、Windows 10 および Windows Server 2016 の AD FS でデバイスの登録と認証が不要になったのみに基づいて、X509 ユーザー証明書。  セキュリティを向上させるよりシームレスなユーザー エクスペリエンスを提供する新しいより堅牢なプロトコルがあります。  主な違いは、Windows 10 ドメインに参加すると、Azure AD 参加が、X509 コンピューター証明書と、新しい資格情報は、PRT と呼ばれます。  読み取ることができます [ここ](https://jairocadena.com/2016/01/18/how-domain-join-is-different-in-windows-10-with-azure-ad/) と [ここ](https://jairocadena.com/2016/02/01/azure-ad-join-what-happens-behind-the-scenes/)します。  

Windows 10 および AD FS 2016 の作業について確認を Microsoft Passport を使用してユーザー認証をサポートする第 2 に、 [ここ](https://jairocadena.com/2016/03/09/azure-ad-and-microsoft-passport-for-work-in-windows-10/) と [ここ](https://azure.microsoft.com/documentation/articles/active-directory-azureadjoin-passport-deployment/)します。  

AD FS 2016 では、シームレスなデバイスとユーザー両方 PRT と Passport の資格情報に基づく SSO を提供します。  このドキュメントで手順を使用して、これらの機能を有効にし、処理するを確認できます。  

### <a name="device-access-control-policies"></a>デバイスのアクセス制御ポリシー  
デバイスなどの単純な AD FS アクセス制御のルールで使用できます。  

- 登録済みのデバイスからのみアクセスを許可します。   
- デバイスが登録されていない場合は、多要素認証を必要と  

これらのルールは、ネットワーク アクセスの場所などの豊富な条件付きアクセス ポリシーを作成する、多要素認証などの他の要因に結合できます。  


- 特定のグループまたはグループのメンバーを除き、企業ネットワークの外部からアクセスする登録されていないデバイスの多要素認証を要求します。  

Ad FS 2016 でこれらのポリシーを構成しても、特定のデバイスの信頼レベルを要求するには、具体的には: か **認証**, 、**管理**, 、または **準拠**します。  

AD FS の構成の詳細については、アクセス制御ポリシーは、「 [AD FS でのアクセス制御ポリシー](../../ad-fs/operations/Access-Control-Policies-in-AD-FS.md)します。  

#### <a name="authenticated-devices"></a>認証済みのデバイス  
認証済みのデバイスは、登録されているデバイス (Intune およびサード パーティの mdm で有効 for Windows 10、Android と iOS のみの Intune) MDM に登録していないですです。   

認証済みのデバイスがある、 **isManaged** AD FS 要求の値を持つ **FALSE**します。 (一方、登録されていないデバイスが不足してこの要求います)。認証済みのデバイス (と登録されているすべてのデバイス) がわかっています AD FS 要求の値を持つ **TRUE**します。  

#### <a name="managed-devices"></a>管理対象のデバイス:   

管理対象デバイスは、MDM. に登録されている登録済みのデバイス  

管理対象デバイスが isManaged AD FS クレームの値が **TRUE**します。  

#### <a name="devices-compliant-with-mdm-or-group-policies"></a>(MDM またはグループ ポリシー) に準拠したデバイス  
対応のデバイスはのみに登録されていない MDM が MDM ポリシーに準拠して、登録済みのデバイスです。 (対応情報は、MDM とおよび Azure AD に書き込まれます)。  

準拠デバイスでは、 **isCompliant** AD FS 要求の値を持つ **TRUE**します。    

AD FS 2016 デバイスと条件付きアクセスの信頼性情報の一覧については、次を参照してください。 [参照](#reference)します。  


## <a name="reference"></a>リファレンス  
#### <a name="complete-list-of-new-ad-fs-2016-and-device-claims"></a>新しい AD FS 2016 とデバイスの要求の完全なリスト  

* https://schemas.microsoft.com/ws/2014/01/identity/claims/anchorclaimtype  
* http://schemas.xmlsoap.org/ws/2005/05/identity/claims/implicitupn  
* https://schemas.microsoft.com/2014/03/psso  
* https://schemas.microsoft.com/2015/09/prt  
* http://schemas.xmlsoap.org/ws/2005/05/identity/claims/upn  
* https://schemas.microsoft.com/ws/2008/06/identity/claims/primarygroupsid  
* https://schemas.microsoft.com/ws/2008/06/identity/claims/primarysid  
* http://schemas.xmlsoap.org/ws/2005/05/identity/claims/name  
* https://schemas.microsoft.com/ws/2008/06/identity/claims/windowsaccountname  
* https://schemas.microsoft.com/ws/2008/06/identity/claims/groupsid  
* https://schemas.microsoft.com/2012/01/devicecontext/claims/registrationid  
* https://schemas.microsoft.com/2012/01/devicecontext/claims/displayname  
* https://schemas.microsoft.com/2012/01/devicecontext/claims/identifier  
* https://schemas.microsoft.com/2012/01/devicecontext/claims/ostype  
* https://schemas.microsoft.com/2012/01/devicecontext/claims/osversion  
* https://schemas.microsoft.com/2012/01/devicecontext/claims/ismanaged  
* https://schemas.microsoft.com/2012/01/devicecontext/claims/isregistereduser  
* https://schemas.microsoft.com/2014/02/devicecontext/claims/isknown  
* https://schemas.microsoft.com/2014/02/deviceusagetime  
* https://schemas.microsoft.com/2014/09/devicecontext/claims/iscompliant  
* https://schemas.microsoft.com/2014/09/devicecontext/claims/trusttype  
* https://schemas.microsoft.com/claims/authnmethodsreferences  
* https://schemas.microsoft.com/2012/01/requestcontext/claims/x-ms-client-user-agent  
* https://schemas.microsoft.com/2012/01/requestcontext/claims/x-ms-endpoint-absolute-path  
* https://schemas.microsoft.com/ws/2012/01/insidecorporatenetwork  
* https://schemas.microsoft.com/2012/01/requestcontext/claims/client-request-id  
* https://schemas.microsoft.com/2012/01/requestcontext/claims/relyingpartytrustid  
* https://schemas.microsoft.com/2012/01/requestcontext/claims/x-ms-client-ip  
* https://schemas.microsoft.com/2014/09/requestcontext/claims/userip  
* https://schemas.microsoft.com/ws/2008/06/identity/claims/authenticationmethod  
