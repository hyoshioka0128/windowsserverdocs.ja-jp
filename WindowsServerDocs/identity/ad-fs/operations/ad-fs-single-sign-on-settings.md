---
ms.assetid: 1a443181-7ded-4912-8e40-5aa447faf00c
title: "AD FS 2016 シングル サイン オンの設定"
description: 
author: billmath
ms.author: billmath
manager: femila
ms.date: 08/17/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adfs
ms.openlocfilehash: e8c24399949efc1b8d0b1782e299593c02374c62
ms.sourcegitcommit: db290fa07e9d50686667bfba3969e20377548504
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/12/2017
---
# <a name="ad-fs-single-sign-on-settings"></a>AD FS シングル サイン オン設定

>適用対象: Windows Server 2016、Windows Server 2012 R2

シングル サインオン (SSO) では、1 回を認証し、追加の資格情報を入力することがなく複数のリソースにアクセスすることができます。  この記事では、SSO、だけでなく、この動作をカスタマイズできるようにする構成設定の既定の AD FS の動作について説明します。  

## <a name="supported-types-of-single-sign-on"></a>サポートされている種類のシングル サインオン

AD FS では、シングル サインオン エクスペリエンスのいくつかの種類をサポートします。  
  
-   **セッション SSO**  
  
     ユーザーが特定のセッション中にアプリケーションを切り替えると、さらにメッセージを排除する認証されたユーザーのセッション SSO の Cookie が書き込まれます。 ただし、特定のセッションが終了した場合、求められます証明書をもう一度します。  
  
     AD FS は設定セッション SSO Cookie 既定でユーザーのデバイスが登録されていない場合。 場合は、ブラウザー セッションが終了した、再起動がこのセッションの Cookie が削除されが正しくないかを確認します。  
  
-   **永続的な SSO**  
  
     永続的な SSO Cookie は永続的な SSO の Cookie が有効な場合に限り、ユーザーがアプリケーションを切り替えると、プロンプトが排除さらに、認証済みのユーザーに書き込まれます。 永続的な SSO とセッション SSO の違いは、異なるセッション間で永続的な SSO を維持することができます。  
  
     デバイスが登録されている場合、AD FS は永続的な SSO の Cookie を設定します。 ユーザーが「を手元に記録」オプションを選択した場合、AD FS は永続的な SSO Cookie 設定もできます。 永続的な SSO の Cookie が有効かどうかをでない場合は、拒否された、削除されます。  
  
-   **アプリケーションの特定の SSO**  
  
     シナリオでは、OAuth、更新トークンは特定のアプリケーションのスコープ内にあるユーザーの SSO 状態を維持するために使用されます。  
  
     デバイスが登録されている場合、AD FS は既定では、永続的な SSO Cookie の有効期間は 7 日間、登録済みのデバイスに基づいて更新トークンの有効期限を設定します。 「を手元に記録」オプションを選択した更新トークンの有効期限は同じであれば、永続的な SSO の Cookie の有効期間「状態で保持するログイン me」既定では最大 7 日の 1 日です。 それ以外の場合、更新トークンの有効期間 equals セッション SSO Cookie の有効期間が既定では 8 時間  
  
 前述のように、登録済みのデバイス上のユーザーは永続的な SSO が無効にしない限り、永続的な SSO を常に取得します。 「を保持するログイン me」を有効にすると、デバイスを登録解除の永続的な SSO を実現できます (KMSI) 機能します。 
 
 「を手元に記録」の場合、PSSO を有効にするには、Windows Server 2012 R2 では、これをインストールする必要が[修正プログラム](https://support.microsoft.com/en-us/kb/2958298/)もの一部では、[Windows RT 8.1、Windows 8.1、および Windows Server 2012 R2 の 2014 年 8 月の更新プログラムのロールアップ](https://support.microsoft.com/en-us/kb/2975719)します。   
 
  
## <a name="single-sign-on-and-authenticated-devices"></a>シングル サインオンおよび認証済みのデバイス  
最初に資格情報を提供した後登録されているデバイスと既定のユーザーがシングル サインオンの取得最長 90 日間、14 日間に少なくとも 1 回を AD FS のリソースにアクセスするデバイスを使用して、提供します。  資格情報を提供した後 15 日を待つ、ユーザーはように求められますの資格情報をもう一度。  

永続的な SSO は既定で有効にします。 無効になっている場合、PSSO Cookie は書き込まれません |。  

``` powershell
Set-AdfsProperties –EnablePersistentSso <Boolean\>
```     
  
デバイスの使用状況] (既定では 14 日) は、AD FS プロパティによって左右されます**DeviceUsageWindowInDays**します。

``` powershell
Set-AdfsProperties -DeviceUsageWindowInDays
```   
最大シングル サイン オン期間 (既定では 90 日間) は、AD FS プロパティによって左右されます**PersistentSsoLifetimeMins**します。

``` powershell
Set-AdfsProperties -PersistentSsoLifetimeMins
```    

## <a name="keep-me-signed-in-for-unauthenticated-devices"></a>認証されていないデバイスにサインインしない] します。 
デバイスの登録されていない場合、シングル サインオン期間はによって決まります、**Me ログに記録で (KMSI) 状態で保持する**機能を設定します。  KMSI では、既定では無効になり、KmsiEnabled AD FS プロパティを True に設定が有効にすることができます。

``` powershell
Set-AdfsProperties -EnableKmsi $true  
```    

無効になっている KMSI、既定のシングル サイン オン期間が 8 時間です。  これは、SsoLifetime プロパティを使用して構成できます。  プロパティは、既定値は 480 分単位で計測されます。  

``` powershell
Set-AdfsProperties –SsoLifetime <Int32\> 
```   

有効になっている KMSI で、既定単一サインオン期間は 24 時間です。  これは、KmsiLifetimeMins プロパティを使用して構成できます。  プロパティは、既定値は 1440 分単位で計測されます。

``` powershell
Set-AdfsProperties –KmsiLifetimeMins <Int32\> 
```   

## <a name="multi-factor-authentication-mfa-behavior"></a>多要素認証 (MFA) の動作  
なお、以前サインオンがプライマリ資格情報およびに基づいていない MFA が、現在サインオンするときに MFA が必要ですがシングル サインオンの比較的長い期間は、AD FS を追加の認証 (多要素認証) 要求が提供するために重要です。  これは、SSO の構成に関係なくです。 AD FS、認証要求を受信するが最初に、SSO コンテキスト (Cookie) などがあるかどうかを決定し、MFA が必要な場合 (場合など、要求が送らから外) SSO コンテキストには、MFA が含まれているかどうかは評価します。  ストアド プロシージャを使用していない場合は、MFA のメッセージが表示されます。  


  
## <a name="psso-revocation"></a>PSSO 失効  
 セキュリティを保護するのには、AD FS が以前に、次の条件が満たされたときに発行された任意の永続的な SSO Cookie を拒否します。 AD FS と再び認証するために自分の資格情報を提供するユーザーが必要になります。 
  
-   ユーザー パスワードを変更  
  
-   AD FS で永続的な SSO の設定が無効になっています  
  
-   デバイスが紛失したり盗難されたりした場合、管理者によって無効になっています  
  
-   AD FS が登録されているユーザーがユーザーに対して発行される永続的な SSO の Cookie を受け取るか、デバイスがもはや登録されていません  
  
-   AD FS が登録されたユーザーの永続的な SSO の Cookie を受け取りますが、ユーザーが再登録  
  
-   AD FS 受信「を手元に記録」しますが、「を手元に記録」の結果として発行される永続的な SSO の Cookie の AD FS での設定が無効になっています  
  
-   AD FS が登録されているユーザーに対して発行される永続的な SSO の Cookie を受け取りますが、認証時にデバイスの証明書がないか、変更されました。  
  
-   AD FS 管理者が永続的な SSO の終了時刻を設定します。 これが構成されているときに AD FS はこの時刻より前に発行された任意の永続的な SSO Cookie を拒否します。  
  
 期限の時間を設定するには、次の PowerShell コマンドレットを実行します。  
  

``` powershell
Set-AdfsProperties -PersistentSsoCutoffTime <DateTime>
```
  
## <a name="enable-psso-for-office-365-users-to-access-sharepoint-online"></a>Office 365 ユーザーにアクセスする SharePoint Online PSSO を有効にします。  
 PSSO が有効になっているし、AD FS で構成されている、ユーザーが認証された後 AD FS は永続的な Cookie を記述します。 次回、ユーザーは、永続的な Cookie が有効なままの場合で、ユーザーは再び認証する資格情報を提供する必要はありません。 Office 365 の追加の認証プロンプトも回避でき、次の 2 つを構成して SharePoint Online のユーザーが Microsoft Azure AD と SharePoint Online でトリガーの持続性を AD FS で規則を要求します。  SharePoint をオンラインにアクセスするユーザーを Office 365 の PSSO を有効にするには、このクライアントをインストールする必要があります[修正プログラム](https://support.microsoft.com/en-us/kb/2958298/)もの一部では、[Windows RT 8.1、Windows 8.1、および Windows Server 2012 R2 の 2014 年 8 月の更新プログラムのロールアップ](https://support.microsoft.com/en-us/kb/2975719)します。  
  
 発行変換の規則の InsideCorporateNetwork 要求をパススルーするには  
  
```  
@RuleTemplate = "PassThroughClaims"  
@RuleName = "Pass through claim - InsideCorporateNetwork"  
c:[Type == "https://schemas.microsoft.com/ws/2012/01/insidecorporatenetwork"]  
=> issue(claim = c);   
A custom Issuance Transform rule to pass through the persistent SSO claim  
@RuleName = "Pass Through Claim - Psso"  
c:[Type == "https://schemas.microsoft.com/2014/03/psso"]  
=> issue(claim = c);  
  
```
  
  
    


