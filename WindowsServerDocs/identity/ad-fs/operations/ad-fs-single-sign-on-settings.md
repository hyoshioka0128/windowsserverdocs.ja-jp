---
ms.assetid: 1a443181-7ded-4912-8e40-5aa447faf00c
title: AD FS 2016 シングル サイン オンの設定
author: billmath
ms.author: billmath
manager: femila
ms.date: 08/17/2017
ms.topic: article
ms.prod: windows-server
ms.technology: identity-adfs
ms.openlocfilehash: cdd35ccc7800616f7803937738c942e68bf04c00
ms.sourcegitcommit: 67116322915066b85decb4261d47cedec2cfe12f
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/07/2020
ms.locfileid: "82903439"
---
# <a name="ad-fs-single-sign-on-settings"></a>AD FS のシングルサインオンの設定

シングルサインオン (SSO) を使用すると、ユーザーは1回認証するだけで、追加の資格情報の入力を求められることなく、複数のリソースにアクセスできます。  この記事では、SSO の既定の AD FS 動作、およびこの動作をカスタマイズするための構成設定について説明します。  

## <a name="supported-types-of-single-sign-on"></a>サポートされているシングルサインオンの種類

AD FS は、いくつかの種類のシングルサインオンエクスペリエンスをサポートしています。  
  
-   **セッション SSO**  
  
     セッション SSO cookie は認証されたユーザー向けに記述されており、ユーザーが特定のセッション中にアプリケーションを切り替えると、さらにプロンプトが表示されなくなります。 ただし、特定のセッションが終了した場合、ユーザーは資格情報を再入力するように求められます。  
  
     ユーザーのデバイスが登録されていない場合、既定では、AD FS によってセッション SSO cookie が設定されます。 ブラウザーセッションが終了して再起動された場合、このセッションクッキーは削除され、それ以上有効ではありません。  
  
-   **永続的 SSO**  
  
     永続的 sso cookie は認証されたユーザー用に書き込まれます。これにより、永続的な SSO クッキーが有効である限り、ユーザーがアプリケーションを切り替えるときに、プロンプトが表示されなくなります。 永続 SSO とセッション SSO の違いは、永続 SSO を異なるセッション間で保持できることです。  
  
     デバイスが登録されている場合、AD FS は永続的な SSO cookie を設定します。 また AD FS は、ユーザーが [サインインしたままにする] オプションを選択した場合に、永続的な SSO cookie を設定します。 永続 SSO クッキーが有効でない場合は、拒否および削除されます。  
  
-   **アプリケーション固有の SSO**  
  
     OAuth シナリオでは、更新トークンを使用して、特定のアプリケーションのスコープ内でユーザーの SSO 状態を維持します。  
  
     デバイスが登録されている場合、AD FS は、登録されているデバイスの永続 SSO cookie の有効期間に基づいて更新トークンの有効期限を設定します。これは、AD FS 2012R2 では既定で7日間、AD FS 2016 では最大90日です。ユーザーが14日の期間内に AD FS リソースにアクセスする場合、 

デバイスが登録されておらず、ユーザーが [サインインしたままにする] オプションを選択した場合、更新トークンの有効期限は、"サインインしたままにする" の永続 SSO cookie の有効期間と同じになります。これは、既定では最大7日間になります。 それ以外の場合、更新トークンの有効期間は、既定では8時間のセッション SSO cookie の有効期間と同じになります。  
  
 前述のように、永続的 SSO が無効になっている場合を除き、登録済みデバイスのユーザーは常に永続的 SSO を取得します。 登録されていないデバイスの場合は、"サインインしたままにする" (KMSI) 機能を有効にすることで、永続的 SSO を実現できます。 
 
 Windows Server 2012 R2 では、"サインインしたままにする" シナリオで PSSO を有効にするには、この修正プログラムをインストールする必要があります。この[修正プログラム](https://support.microsoft.com/kb/2958298/)は、 [windows RT 8.1、Windows 8.1、および Windows Server 2012 R2 の年 8 2014 月の更新プログラムのロールアップ](https://support.microsoft.com/kb/2975719)の一部でもあります。   

タスク | PowerShell | 説明
------------ | ------------- | -------------
永続的 SSO の有効化/無効化 | ```` Set-AdfsProperties –EnablePersistentSso <Boolean> ````| 永続的 SSO は既定で有効になっています。 無効になっている場合は、PSSO クッキーは書き込まれません。
[サインインしたままにする] を有効または無効にする | ```` Set-AdfsProperties –EnableKmsi <Boolean> ```` | "サインインしたままにする" 機能は、既定では無効になっています。 有効になっている場合、エンドユーザーは AD FS サインインページで [サインインしたままにする] を選択できます。



## <a name="ad-fs-2016---single-sign-on-and-authenticated-devices"></a>AD FS 2016-シングルサインオンと認証されたデバイス
AD FS 2016 は、要求元が登録されているデバイスから最大90日まで増加し、14日以内に認証が要求される場合、PSSO を変更します ([デバイスの使用状況] ウィンドウ)。
最初に資格情報を入力した後、既定では、登録されたデバイスを持つユーザーは、少なくとも14日ごとに1回以上 AD FS リソースにアクセスするためにデバイスを使用するため、最大90日間のシングルサインオンを利用できます。  資格情報を指定してから15日間待っている場合、ユーザーは資格情報の入力を再度求められます。  

永続的 SSO は既定で有効になっています。 無効になっている場合、PSSO クッキーは書き込まれません |。  

``` powershell
Set-AdfsProperties –EnablePersistentSso <Boolean\>
```     
  
[デバイスの使用量] ウィンドウ (既定では14日) は、AD FS プロパティ**DeviceUsageWindowInDays**によって管理されます。

``` powershell
Set-AdfsProperties -DeviceUsageWindowInDays
```   
シングルサインオンの最大期間 (既定では90日) は AD FS プロパティ**PersistentSsoLifetimeMins**によって管理されます。

``` powershell
Set-AdfsProperties -PersistentSsoLifetimeMins
```    

## <a name="keep-me-signed-in-for-unauthenticated-devices"></a>認証されていないデバイスにサインインしたままにする 
登録されていないデバイスの場合、シングルサインオンの期間は、[サインインした**ままにする (KMSI)** ] 機能の設定によって決まります。  KMSI は既定で無効になっており、AD FS プロパティ KmsiEnabled を True に設定することによって有効にすることができます。

``` powershell
Set-AdfsProperties -EnableKmsi $true  
```    

KMSI を無効にした場合、既定のシングルサインオン期間は8時間です。  これは、プロパティ SsoLifetime を使用して構成できます。  プロパティは分単位で測定されるため、既定値は480です。  

``` powershell
Set-AdfsProperties –SsoLifetime <Int32\> 
```   

KMSI が有効になっている場合、既定のシングルサインオン期間は24時間です。  これは、プロパティ KmsiLifetimeMins を使用して構成できます。  プロパティは分単位で測定されるため、既定値は1440です。

``` powershell
Set-AdfsProperties –KmsiLifetimeMins <Int32\> 
```   

## <a name="multi-factor-authentication-mfa-behavior"></a>Multi-factor authentication (MFA) の動作  
重要なのは、比較的長いシングルサインオンを提供している間、AD FS では、以前のサインオンが MFA ではなくプライマリ資格情報に基づいており、現在のサインオンでは MFA が必要な場合に、追加の認証 (multi-factor authentication) の入力を求められることに注意してください。  これは SSO 構成には関係ありません。 AD FS は、認証要求を受信すると、まず SSO コンテキスト (cookie など) があるかどうかを判断し、MFA が必要な場合 (外部から要求が送信される場合など) は、SSO コンテキストに MFA が含まれているかどうかを評価します。  それ以外の場合は、MFA が要求されます。  


  
## <a name="psso-revocation"></a>PSSO の失効  
 セキュリティを保護するために、次の条件が満たされたときに以前に発行されたすべての永続的な SSO cookie を拒否する AD FS ます。 これには、AD FS での認証を行うために、ユーザーが資格情報を入力する必要があります。 
  
- ユーザーがパスワードを変更する  
  
- 永続 SSO 設定が AD FS で無効になっています  
  
- デバイスが紛失または盗難にあった場合、管理者によって無効にされている  
  
- AD FS は、登録されているユーザーに対して発行された永続的な SSO cookie を受信しますが、ユーザーまたはデバイスは登録されていません  
  
- AD FS は、登録されているユーザーに対して永続的な SSO cookie を受信しますが、ユーザーは再登録します。  
  
- AD FS は、"サインインしたままにする" の結果として発行される永続的な SSO cookie を受信しますが、[サインインしたままにする] 設定は、では無効になってい AD FS  
  
- AD FS は、登録されているユーザーに対して発行された永続的な SSO cookie を受け取りますが、認証時にデバイス証明書が見つからないか変更されています  
  
- AD FS 管理者が永続的 SSO のカットオフ時間を設定しました。 これを構成すると、AD FS は、この時間より前に発行されたすべての永続 SSO cookie を拒否します。  
  
  カットオフ時間を設定するには、次の PowerShell コマンドレットを実行します。  
  

``` powershell
Set-AdfsProperties -PersistentSsoCutoffTime <DateTime>
```
  
## <a name="enable-psso-for-office-365-users-to-access-sharepoint-online"></a>Office 365 ユーザーが SharePoint Online にアクセスできるように PSSO を有効にする  
 PSSO が有効になり AD FS で構成されると、ユーザーが認証された後、AD FS は永続的な cookie を書き込みます。 次回ユーザーがサインインしたときに、永続的な cookie がまだ有効である場合、ユーザーは資格情報を入力して再度認証する必要はありません。 また、Microsoft Azure AD と SharePoint Online で永続化をトリガーするために AD FS で次の2つの要求規則を構成することで、Office 365 および SharePoint Online ユーザーの追加の認証プロンプトを回避することもできます。  Office 365 ユーザーが SharePoint online にアクセスできるようにするには、この修正プログラムをインストールする必要があります。この[修正プログラム](https://support.microsoft.com/kb/2958298/)は、 [windows RT 8.1、Windows 8.1、および Windows Server 2012 R2 の年 8 2014 月の更新プログラムのロールアップ](https://support.microsoft.com/kb/2975719)の一部でもあります。  
  
 InsideCorporateNetwork 要求を通過する発行変換規則  
  
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
  
概要:
<table>
  <tr>
    <th colspan="1">シングルサインオンエクスペリエンス</th>
    <th colspan="3">ADFS 2012 R2 <br> デバイスは登録されていますか?</th>
        <th colspan="1"></th>
    <th colspan="3">ADFS 2016 <br> デバイスは登録されていますか?</th>
  </tr>

  <tr align="center">
    <th></th>
    <th>NO</th>
    <th>いいえ、KMSI</th>
    <th>YES</th>
    <th></th>
    <th>NO</th>
    <th>いいえ、KMSI</th>
    <th>YES</th>
  </tr>
 <tr align="center">
    <td>SSO =&gt;設定更新トークン =&gt;</td>
    <td>8時間</td>
    <td>該当なし</td>
    <td>該当なし</td>
    <th></th>
    <td>8時間</td>
    <td>該当なし</td>
    <td>該当なし</td>
  </tr>

 <tr align="center">
    <td>PSSO =&gt;設定更新トークン =&gt;</td>
    <td>該当なし</td>
    <td>24時間</td>
    <td>7日間</td>
    <th></th>
    <td>該当なし</td>
    <td>24時間</td>
    <td>14日の期間の最大90日</td>
  </tr>

 <tr align="center">
    <td>トークンの有効期間</td>
    <td>1時間</td>
    <td>1時間</td>
    <td>1時間</td>
    <th></th>
    <td>1時間</td>
    <td>1時間</td>
    <td>1時間</td>
  </tr>
</table>

**登録済みのデバイスですか?** PSSO/Persistent SSO を取得する <br>
**登録されていないデバイスですか?** SSO を取得する <br>
**登録されていないデバイスですが、KMSI ですか?** PSSO/Persistent SSO を取得する <p>
もし：
 - [x] 管理者が KMSI 機能を有効にしました [および]
 - [x] ユーザーがフォームログインページで KMSI チェックボックスをクリックします。
 
  
新しい更新トークンの有効性が前のトークンより長い場合にのみ、ADFS は新しい更新トークンを発行します。 トークンの最長有効期間は84日ですが、AD FS 14 日間のスライディングウィンドウでトークンが有効なままになります。 更新トークンが、通常の SSO 時間である8時間有効な場合、新しい更新トークンは発行されません。 
 
 
**次のことをお勧めします。** <br>
**Lastpasswordchangetimestamp**属性が同期されていないフェデレーションユーザーは、**最大有効期間の値が12時間の**セッション cookie と更新トークンを発行します。<br>
これは、古い資格情報 (変更されたパスワードなど) に関連付けられているトークンを取り消すタイミングを Azure AD が判断できないために発生します。 したがって、ユーザーとそれに関連付けられているトークンが良好な状態であることを確認するために、Azure AD を頻繁に確認する必要があります。
