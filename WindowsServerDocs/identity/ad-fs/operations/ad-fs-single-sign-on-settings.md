---
ms.assetid: 1a443181-7ded-4912-8e40-5aa447faf00c
title: AD FS 2016 シングル サイン オンの設定
description: ''
author: billmath
ms.author: billmath
manager: femila
ms.date: 08/17/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adfs
ms.openlocfilehash: 97e1fa441c5fe4fb7d23743387392732663326de
ms.sourcegitcommit: cd12ace92e7251daaa4e9fabf1d8418632879d38
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/04/2019
ms.locfileid: "66501585"
---
# <a name="ad-fs-single-sign-on-settings"></a>AD FS のシングル サインオンの設定

シングル サインオン (SSO) では、1 回認証を追加の資格情報を入力することがなく複数のリソースにアクセスできます。  この記事では、この動作をカスタマイズするための構成設定と、SSO、既定の AD FS の動作について説明します。  

## <a name="supported-types-of-single-sign-on"></a>サポートされている種類のシングル サインオン

AD FS では、シングル サインオン エクスペリエンスのいくつかの種類をサポートします。  
  
-   **SSO セッション**  
  
     ユーザーが特定のセッション中にアプリケーションを切り替えると、さらにメッセージを排除する認証済みユーザーに対しては、セッションの SSO cookie が書き込まれます。 ただし、特定のセッションが終了した場合、ユーザーが求められることの資格情報。  
  
     AD FS がセッションが設定された SSO クッキーの既定ではユーザーのデバイスが登録されていない場合。 場合は、ブラウザー セッションが終了し、再起動は、このセッションの cookie が削除され、有効でないかを確認します。  
  
-   **永続的な SSO**  
  
     永続的な SSO cookie が有効な限り、ユーザーがアプリケーションを切り替えるときに、画面の指示によりさらに、認証済みユーザーは、永続的な SSO cookie が書き込まれます。 SSO と SSO セッションを永続的な違いは、異なるセッション間で永続的な SSO を管理することができます。  
  
     デバイスが登録されている場合、AD FS は永続的な SSO cookie を設定します。 「サインインしたまま」オプションを選択した場合、AD FS は永続的な SSO cookie 設定もできます。 永続的な SSO cookie が有効かどうかをでない場合は、拒否、削除されます。  
  
-   **アプリケーションの特定の SSO**  
  
     OAuth では、更新トークンは特定のアプリケーションのスコープ内でユーザーの SSO の状態を維持するために使用します。  
  
     AD FS が自分のデバイスを使用している場合、2012R2 の AD FS と AD FS 2016 で 90 日間の最大既定では 7 日をある登録済みデバイスの永続的な SSO cookie 有効期間に基づく更新トークンの有効期限を設定、デバイスが登録されている場合14 日のウィンドウ内の AD FS のリソースにアクセスします。 

場合は、デバイスが登録されていませんが、ユーザーが「サインインしたまま」オプションを選択、更新トークンの有効期限、永続的な SSO cookie の有効期間「サインインしたまま」になります、既定では最大 7 日間の 1 日があります。 それ以外の場合、更新トークンの有効期間 equals セッション SSO cookie の有効期間は既定では 8 時間  
  
 上記のように、登録済みデバイスのユーザーには、永続的な SSO を無効にしない限り、永続的な SSO を常に取得します。 「サインインしたままで」を有効にすると、デバイスの登録解除の永続的な SSO を実現できます (KMSI) 機能です。 
 
 「サインインしたまま」のシナリオで PSSO を有効にする Windows Server 2012 r2 では、これをインストールする必要が[修正プログラム](https://support.microsoft.com/en-us/kb/2958298/)もあるの一部の[Windows RT 8.1、Windows 8.1、および Windows Server 2012 の 2014 年 8 月更新プログラムのロールアップR2](https://support.microsoft.com/en-us/kb/2975719)します。   

タスク | PowerShell | 説明
------------ | ------------- | -------------
永続的な SSO を有効/無効にします。 | ```` Set-AdfsProperties –EnablePersistentSso <Boolean> ````| 永続的な SSO は既定で有効にします。 無効の場合は、PSSO cookie は書き込まれません。
「有効/無効にする"サインインしたまま」 | ```` Set-AdfsProperties –EnableKmsi <Boolean> ```` | 既定では、「サインインしたまま」機能が無効です。 エンドユーザーが AD FS サインイン ページ「サインインしたまま」の選択肢を表示、有効な場合



## <a name="ad-fs-2016---single-sign-on-and-authenticated-devices"></a>AD FS 2016 でのシングル サインオン、認証済みのデバイス
AD FS 2016 は、最大 90 日間に増やすことが、14 日間の期間 (デバイスの使用状況 ウィンドウ) 内で認証を必要とする登録済みのデバイスから要求元を認証するときに、PSSO を変更します。
資格情報を提供する、最初に、後に既定で登録済みデバイスを持つユーザーでシングル サインオンの取得 90 日間の最大期間に 14 日間に少なくとも 1 回を AD FS のリソースにアクセスするデバイスを使用します。  資格情報の提供後 15 日間、待機する場合ユーザーが求められることの資格情報。  

永続的な SSO は既定で有効にします。 無効の場合、PSSO cookie は書き込まれません |。  

``` powershell
Set-AdfsProperties –EnablePersistentSso <Boolean\>
```     
  
デバイスの使用状況 ウィンドウ (既定では 14 日間) は、AD FS プロパティの影響を受ける**DeviceUsageWindowInDays**します。

``` powershell
Set-AdfsProperties -DeviceUsageWindowInDays
```   
AD FS プロパティ、最大 1 つでサインオン期間 (既定では 90 日間) に準拠するもの**PersistentSsoLifetimeMins**します。

``` powershell
Set-AdfsProperties -PersistentSsoLifetimeMins
```    

## <a name="keep-me-signed-in-for-unauthenticated-devices"></a>認証されていないデバイスのサインインを維持します。 
デバイスの登録されていない場合はシングル サインオン期間によって決定されます、**保持 Me 署名で (KMSI)** 機能設定します。  KMSI は、既定では無効になり、KmsiEnabled AD FS プロパティを True に設定して有効にすることができます。

``` powershell
Set-AdfsProperties -EnableKmsi $true  
```    

KMSI を無効になっていると既定シングル サインオン期間は 8 時間です。  これは、SsoLifetime プロパティを使用して構成できます。  プロパティは、既定値は 480 分単位で測定されます。  

``` powershell
Set-AdfsProperties –SsoLifetime <Int32\> 
```   

KMSI を有効になっていると既定シングル サインオン期間は 24 時間です。  これは、KmsiLifetimeMins プロパティを使用して構成できます。  プロパティは、既定値は 1440 分単位で測定されます。

``` powershell
Set-AdfsProperties –KmsiLifetimeMins <Int32\> 
```   

## <a name="multi-factor-authentication-mfa-behavior"></a>多要素認証 (MFA) の動作  
比較的長時間シングル サインオンの提供することで、中に AD FS が求められます追加の認証 (多要素認証) に注意してください前サインオンは、プライマリ資格情報と、MFA ではないに基づいていたが、現在のアクセスを設定するときに。MFA が必要です。  これは、SSO の構成に関係なく。 認証要求を受け取るときに、AD FS が最初に、SSO のコンテキスト (cookie) などがあるかどうかを決定しますうえで、MFA が必要な場合 (場合など、要求が送られてからの外部) SSO コンテキストには、MFA にはが含まれているかどうかを評価すること。  それ以外の場合は、MFA のメッセージが表示されます。  


  
## <a name="psso-revocation"></a>PSSO 失効  
 セキュリティ保護のため、AD FS では、次の条件が満たされたときに事前に発行したすべての永続的な SSO cookie を拒否します。 AD FS を使用した再認証するために、資格情報を提供するユーザーが必要になります。 
  
- ユーザーがパスワードを変更  
  
- AD FS で永続的な SSO の設定は無効です。  
  
- デバイスが紛失または盗難にあった場合、管理者によって無効になっています  
  
- AD FS が登録済みユーザーがユーザーに発行される永続的な SSO cookie を受信するか、またはデバイスがもはやに登録されていません  
  
- AD FS が登録されているユーザーの永続的な SSO cookie を受け取りますが、ユーザーが再登録  
  
- AD FS の受信「サインインしたまま」、「サインアウト」の結果として発行される永続的な SSO cookie で AD FS の設定は無効です  
  
- AD FS が登録されているユーザーに対して発行される永続的な SSO cookie を受け取りますが、認証時にデバイスの証明書が見つからないか、変更されました。  
  
- AD FS の管理者が永続的な SSO の終了時刻を設定します。 この時刻より前に発行されたすべての永続的な SSO cookie が構成されて、AD FS は拒否します  
  
  終了時刻を設定するには、次の PowerShell コマンドレットを実行します。  
  

``` powershell
Set-AdfsProperties -PersistentSsoCutoffTime <DateTime>
```
  
## <a name="enable-psso-for-office-365-users-to-access-sharepoint-online"></a>SharePoint Online へのアクセスに Office 365 ユーザー PSSO を有効にします。  
 PSSO が有効になっているし、AD FS で構成されている、ユーザーが認証された後 AD FS は永続的なクッキーを記述します。 永続的な cookie がまだ有効な場合で、ユーザーが次回、ユーザーは、再認証する資格情報を提供する必要はありません。 Office 365 の追加の認証プロンプトを回避でき、次の 2 つを構成することで SharePoint Online のユーザーが Microsoft Azure AD と SharePoint Online トリガーの永続化する AD FS で規則を要求します。  PSSO SharePoint online へのアクセスに Office 365 ユーザーを有効にするのには、これをインストールする必要があります[修正プログラム](https://support.microsoft.com/en-us/kb/2958298/)もあるの一部の[Windows RT 8.1、Windows 8.1、および Windows Server 2012 R22014年8月更新プログラムのロールアップ](https://support.microsoft.com/en-us/kb/2975719).  
  
 InsideCorporateNetwork クレームを通過する発行変換規則  
  
```  
@RuleTemplate = "PassThroughClaims"  
@RuleName = "Pass through claim - InsideCorporateNetwork"  
c:[Type == "http://schemas.microsoft.com/ws/2012/01/insidecorporatenetwork"]  
=> issue(claim = c);   
A custom Issuance Transform rule to pass through the persistent SSO claim  
@RuleName = "Pass Through Claim - Psso"  
c:[Type == "http://schemas.microsoft.com/2014/03/psso"]  
=> issue(claim = c);  
  
```
  
要約。
<table>
  <tr>
    <th colspan="1">シングル サインオン エクスペリエンス</th>
    <th colspan="3">ADFS 2012 R2 <br> デバイスが登録されているか。</th>
        <th colspan="1"></th>
    <th colspan="3">ADFS 2016 <br> デバイスが登録されているか。</th>
  </tr>

  <tr align="center">
    <th></th>
    <th>使用不可</th>
    <th>KMSI はなし</th>
    <th>使用可能</th>
    <th></th>
    <th>使用不可</th>
    <th>KMSI はなし</th>
    <th>使用可能</th>
  </tr>
 <tr align="center">
    <td>SSO =&gt;更新トークン設定 =&gt;</td>
    <td>8 時間以内</td>
    <td>なし</td>
    <td>なし</td>
    <th></th>
    <td>8 時間以内</td>
    <td>なし</td>
    <td>なし</td>
  </tr>

 <tr align="center">
    <td>PSSO =&gt;更新トークン設定 =&gt;</td>
    <td>なし</td>
    <td>24 時間以内</td>
    <td>7 日間</td>
    <th></th>
    <td>なし</td>
    <td>24 時間以内</td>
    <td>最大 14 日間のウィンドウで 90 日間</td>
  </tr>

 <tr align="center">
    <td>トークンの有効期間</td>
    <td>1 時間</td>
    <td>1 時間</td>
    <td>1 時間</td>
    <th></th>
    <td>1 時間</td>
    <td>1 時間</td>
    <td>1 時間</td>
  </tr>
</table>

**デバイスを登録しますか。** PSSO の取得/永続的な SSO <br>
**デバイスを登録されていませんか。** SSO を取得します。 <br>
**デバイスが登録されていませんが、KMSI でしょうか。** PSSO の取得/永続的な SSO <p>
もし：
 - [x] は、管理者には、KMSI 機能 [AND] が有効に
 - [x] は、ユーザーがフォームのログイン ページに KMSI チェック ボックスをクリックします。
 
**適切な情報:** <br>
持っていないユーザーをフェデレーション、 **LastPasswordChangeTimestamp**セッションの cookie と更新トークンを持つ属性が同期が発行された、 **12 時間の最大年齢値**します。<br>
これは、Azure AD は、古い資格情報が変更されているパスワード) などに関連するトークンを取り消すタイミングを決定できないために発生します。 そのため、Azure AD は、ユーザーと関連付けられているトークンがまだ良好であるかどうかを確認するより頻繁に確認する必要があります。
