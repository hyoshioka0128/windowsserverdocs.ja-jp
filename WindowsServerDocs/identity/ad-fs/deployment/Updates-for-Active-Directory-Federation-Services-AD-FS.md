---
ms.assetid: ed3206b4-bbfc-4bc7-a43c-981b0544a50d
title: "Active Directory フェデレーション サービス (AD FS) に必要な更新プログラム"
description: 
author: billmath
ms.author: billmath
manager: femila
ms.date: 11/28/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adfs
ms.openlocfilehash: 434bf65c9f5ec977318b5efcdeebd19a5f1ed475
ms.sourcegitcommit: db290fa07e9d50686667bfba3969e20377548504
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/12/2017
---
# <a name="required-updates-for-active-directory-federation-services-ad-fs-and-web-application-proxy-wap"></a>Active Directory フェデレーション サービス (AD FS) と Web アプリケーション プロキシ (WAP) を必要な更新プログラム

>適用対象: Windows Server 2016、Windows Server 2012 R2、Windows Server 2012、Windows Server 2008 R2 SP1

2016 年 10 月の時点で Windows Server のすべてのコンポーネントをすべての更新プログラムにのみ使用して Windows Update (WU) がリリースされます。  ない他の修正プログラムまたは個別のダウンロード パッケージがあります。
これは、Windows Server 2016、Windows Server 2012 R2、Windows Server 2012 および Windows Server 2008 R2 SP1 に適用されます。

このページには、AD FS と WAP、AD FS と WAP 推奨修正プログラムの更新の履歴の一覧に対して特定の関心のあるプログラムのロールアップ パッケージが一覧表示します。

## <a name="updates-for-ad-fs-and-wap-in-windows-server-2016"></a>AD FS と WAP Windows Server 2016 での更新プログラム
Windows Server 2016 の更新プログラムは、毎月 Windows Update を通じて配信されは累積的です。 以下の更新パッケージのすべての AD FS と WAP 2016 サーバーをお勧めをすべて以前に必要な更新プログラムだけでなく、最新の修正プログラムが含まれています。

|KB # |説明|リリース日
|----- | ----- |-----
|[4041688 (OS Build 14393.1794)](https://support.microsoft.com/kb/4041688)|This fix addresses an issue that intermittently misdirects AD Authority requests to the wrong Identity Provider because of incorrect caching behavior. This can effect authentication features like Multi Factor Authentication. </br></br>Added the ability for AAD Connect Health to report ADFS server health with correct fidelity (using verbose auditing) on mixed WS2012R2 and WS2016 ADFS farms.</br></br>Fixed a problem where during upgrade of 2012 R2 ADFS farm to ADFS 2016, the powershell cmdlet to raise the farm behavior level fails with a timeout when there are many relying party trusts.</br></br>Addressed an issue where AD FS causes authentication failures by modifying the wct parameter value while federating the requests to other Security Token Server (STS).|October 2017|
|[4038801 (OS Build 14393.1737)](https://support.microsoft.com/kb/4038801)|Support added for OIDC logout using federated LDPs. This will allow "Kiosk Scenarios" where multiple users might be serially logged into a single device where there is federation with an LDP.</br></br>Fixed a WinHello issue where CEP/CES based certificates don't work with gMSA accounts.</br></br>Fixes a problem where the Windows Internal Database (WID) on Windows Server 2016 ADFS servers fails to sync some settings, such as the ApplicationGroupId columns from IdentityServerPolicy.Scopes and IdentityServerPolicy.Clients tables)  due to a foreign key constraint. Such sync failures can cause different claim, claim provider and application experiences between primary to secondary ADFS servers. Also, if the WID primary role is moved to a secondary node, application groups will no longer be manageable in the ADFS management UX.</br></br>This update fixes an issues where Multi Factor Authentication does not work correctly with Mobile devices that use custom culture definitions|September 2017|
|[4034661 (OS Build 14393.1613)](https://support.microsoft.com/kb/4034661)|Fixes a problem where the caller IP address is nog logged by 411 events in the Security Event log of ADFS 4.0 \ Windows Server 2016 RS1 ADFS servers even after enabling “success audits” and “failure audits”.</br></br>This fix addresses an issue with Azure Multi Factor Authentication (MFA) when an ADFX server is configured to use an HTTP Proxy.</br></br>"Addressed an issue where presenting an expired or revoked certificate to the ADFS Proxy server does not return an error to the user."|August 2017|
|[4034658 (OS Build 14393.1593)](https://support.microsoft.com/kb/4034658)|Fix for 2016 AD FS server in order to support MFA certificate enrollment for Windows Hello For Business for on prem deployments|August 2017| 
|[4025334 (OS Build 14393.1532)](https://support.microsoft.com/kb/4025334)|Addressed an issue where the PkeyAuth token handler could fail an authentication if the pkeyauth request contains incorrect data. The authentication should still continue without performing device authentication|July 2017|
|[4022723 (OS Build 14393.1378)](https://support.microsoft.com/kb/4022723)|[Web Application Proxy] Value of DisableHttpOnlyCookieProtection configuration property is not picked up by WAP 2016 in 2012R2/2016 mixed deployment </br></br>[Web Application Proxy] Unable to obtain user access token from AD FS in EAS Pre-auth scenarios.</br></br>AD FS 2016 : WSFED sign-out leads to an exception|2017 年 6 月 
|[3213986](https://support.microsoft.com/kb/3213986)|(KB3213986) x64 ベース システム用 Windows Server 2016 の累積的な更新プログラム| 2017 年 1 月

## <a name="updates-for-ad-fs-and-wap-in-windows-server-2012-r2"></a>AD FS と WAP Windows Server 2012 R2 での更新プログラム
Active Directory フェデレーション サービス (AD FS) 用の Windows Server 2012 R2 でリリースされた修正プログラムおよび更新プログラムのロールアップの一覧を次に示します。

|KB # |説明|リリース日
|----- | ----- |-----
|[4041685](https://support.microsoft.com/kb/4041685)|Addressed an AD FS issue where MSISConext cookies in request headers can eventually overflow the headers size limit and cause failure to authenticate with HTTP status code 400 “Bad Request - Header Too Long".</br></br>Fixed a problem where ADFS can no longer ignore "prompt=login" during authentication. A "Disabled" option was added to restore scenarios where non-password authentication is used.|October 2017 Preview of Update Rollup|
|[4019217](https://support.microsoft.com/kb/4019217)|Work Folders clients using token broker do not work when using a Server 2012 R2 AD FS Server|May 2017 Preview Update Rollup| 
|[4015550](https://support.microsoft.com/kb/4015550)|Fixed an issue with AD FS not authenticating External users and AD FS WAP randomly failing to forward request|April 2017 Update Rollup| 
|[4015547](https://support.microsoft.com/kb/4015547)|Fixed an issue with AD FS not authenticating External users and AD FS WAP randomly failing to forward request|April 2017 Security Update| 
|[4012216](https://support.microsoft.com/kb/4009970)|MS17-019 This security update resolves a vulnerability in Active Directory Federation Services (ADFS). The vulnerability could allow information disclosure if an attacker sends a specially crafted request to an AD FS server, allowing the attacker to read sensitive information about the target system.|March 2017 Update Rollup| 
|[3179574](https://support.microsoft.com/kb/3179574)|AD FS のエクストラネットのパスワードを更新問題を修正しました。 |2016 年 8 月の更新プログラムのロールアップ
|[3172614](https://support.microsoft.com/kb/3172614)|導入されたプロンプト = ログイン[サポート](https://technet.microsoft.com/en-us/windows-server-docs/identity/ad-fs/overview/ad-fs-faq#BKMK_7)、AD FS 管理コンソールと AlwaysRequireAuthentication 設定問題を修正しました。 |2016 年 7 月更新プログラムのロールアップ
|[3163306](https://support.microsoft.com/kb/3163306)|Active Directory フェデレーション サービス (AD FS) 3.0 は 636 または 3269 接続文字列で Secure Sockets Layer (SSL) ポートを使用するように構成されているライトウェイト ディレクトリ アクセス プロトコル (LDAP) 属性ストアに接続できません。 |2016 年 6 月の更新プログラムのロールアップ
|[3148533](https://support.microsoft.com/kb/3148533)|Windows Server 2012 R2 で ad FS プロキシを介して MFA 代替の認証が失敗します。 |2016 年 5 月
|[3134787](https://support.microsoft.com/kb/3134787)|AD FS ログにはアカウント ロックアウトのシナリオでは、Windows Server 2012 R2 のクライアントの IP アドレスが含まれていません。 |2016 年 2 月
|[3134222](https://support.microsoft.com/kb/3134222)|MS16 020: セキュリティの更新を Active Directory フェデレーション サービスのアドレスにサービス拒否: 2016 年 2 月 9 日|2016 年 2 月
|[3105881](https://support.microsoft.com/kb/3105881)|Windows Server 2012 R2 ベースの AD FS サーバーでデバイス認証が有効にするとアプリケーションにアクセスできません。|2015 年 10 月
|[3092003](https://support.microsoft.com/kb/3092003)|繰り返しページが読み込まれ、ユーザーは、Windows Server 2012 R2 AD FS で MFA を使用するときに認証が失敗しました。|2015 年 8 月
|[3080778](https://support.microsoft.com/kb/3080778)|AD FS が呼び出されませんエラー時 MFA アダプターは、Windows Server 2012 R2 で例外をスロー|2015 年 7 月
|[3075610](https://support.microsoft.com/kb/3075610)|追加するか、または Windows Server 2012 R2 での要求プロバイダーを削除した後、セカンダリの AD FS サーバー上の信頼関係が失われる|2015 年 7 月
|[3070080](https://support.microsoft.com/kb/3070080)|ホーム領域検出の信頼性情報の非対応 Relying Party Trust に対して正しく動作していません|2015 年 6 月
|[3052122](https://support.microsoft.com/kb/3052122)|Windows Server 2012 R2 で AD FS トークンで複合 ID のクレームのサポートを追加する更新プログラム|May 2015
|[3045711](https://support.microsoft.com/kb/3045711)|MS15 040: Active Directory フェデレーション サービスの脆弱性により情報漏えい|2015 年 4 月
|[3042127](https://support.microsoft.com/kb/3042127)|"HTTP 400 - 要求が正しくありません"Windows Server 2012 R2 で WAP によって共有されているメールボックスを開くときのエラー|March 2015
|[3042121](https://support.microsoft.com/kb/3042121)|Windows Server 2012 R2 での Web アプリケーション プロキシの認証トークンを AD FS トークン リプレイの保護|March 2015
|[3035025](https://support.microsoft.com/kb/3035025)|パスワード更新用の修正プログラム機能できるように、ユーザーが Windows Server 2012 R2 で登録されたデバイスを使用する必要はありません。|2015 年 1 月
|[3033917](https://support.microsoft.com/kb/3033917)|AD FS は Windows Server 2012 R2 で SAML 応答を処理できません。|2015 年 1 月
|[3025080](https://support.microsoft.com/kb/3025080)|Windows Server 2012 R2 で Web アプリケーション プロキシ経由 Office ファイルを保存しようとすると、操作が失敗します。|2015 年 1 月
|[3025078](https://support.microsoft.com/kb/3025078)|要求されないユーザー名をもう一度、不適切なユーザー名を使用して、Windows Server 2012 R2 にログオンするときに|2015 年 1 月
|[3020813](https://support.microsoft.com/kb/3020813)|Windows Server 2012 R2 AD FS で web アプリケーションを実行するときに認証を求められました。|2015 年 1 月
|[3020773](https://support.microsoft.com/kb/3020773)|Windows Server 2012 R2 でのデバイス登録サービスの初期展開後にタイムアウト エラー|2015 年 1 月
|[3018886](https://support.microsoft.com/kb/3018886)|されたら、ユーザー名とパスワードを 2 回イントラネットから Windows Server 2012 R2 AD FS サーバーにアクセスするときに|2015 年 1 月
|[3013769](https://support.microsoft.com/kb/3013769)|Windows Server 2012 R2 更新プログラム ロールアップ|年 12 月 2014
|[3000850](https://support.microsoft.com/kb/3000850)|Windows Server 2012 R2 更新プログラム ロールアップ|2014 年 11 月
|[2975719](https://support.microsoft.com/kb/2975719)|Windows Server 2012 R2 更新プログラム ロールアップ|2014 年 8 月
|[2967917](https://support.microsoft.com/kb/2967917)|Windows Server 2012 R2 更新プログラム ロールアップ|July 2014
|[2962409](https://support.microsoft.com/kb/2962409)|Windows Server 2012 R2 更新プログラム ロールアップ|2014 年 6 月
|[2955164](https://support.microsoft.com/kb/2955164)|Windows Server 2012 R2 更新プログラム ロールアップ|2014 年 5 月
|[2919355](https://support.microsoft.com/kb/2919355)|Windows Server 2012 R2 更新プログラム ロールアップ|2014 年 4 月

## <a name="updates-for-ad-fs-in-windows-server-2012-ad-fs-21-and-ad-fs-20"></a>更新プログラムの AD FS では、Windows Server 2012 (AD FS 2.1) と AD FS 2.0
AD FS 2.0 および 2.1 のリリースされている修正プログラムおよび更新プログラムのロールアップの一覧を次に示します。

|KB # |説明|リリース日|適用対象します。
|----- | ----- |-----|-----
|[3197878](https://support.microsoft.com/kb/3197878)|(これは、全般的な 3094446 修正プログラムのリリースです)、Windows Server 2012 でプロキシを使用した認証が失敗します。|2016 年 11 月の品質ロールアップ|AD FS 2.1
|[3197869](https://support.microsoft.com/kb/3197869)|Windows Server 2008 R2 SP1 (これは 3094446 修正プログラムの全般的なリリース) でプロキシ経由の認証が失敗しました。|2016 年 11 月の品質ロールアップ|AD FS 2.0
|[3094446](https://support.microsoft.com/kb/3094446)|Windows Server 2012 または Windows Server 2008 R2 SP1 でプロキシを使用した認証が失敗します。|September 2015|AD FS 2.0 および 2.1
|[3070078](https://support.microsoft.com/kb/3070078)|Windows Server 2012 で暗号化証明書に対して認証するときに、AD FS 2.1 が例外をスローします。|2015 年 7 月|AD FS 2.1
|[3062577](https://support.microsoft.com/kb/3062577)|MS15 062: Active Directory フェデレーション サービスの脆弱性により、特権の昇格|2015 年 6 月|AD FS 2.0 2.1/
|[3003381](https://support.microsoft.com/kb/3003381)|MS14 077: Active Directory フェデレーション サービスの脆弱性により情報の漏洩: 2015 年 4 月 14 日|2014 年 11 月|AD FS 2.0 2.1/
|[2987843](https://support.microsoft.com/kb/2987843)|Windows Server 2012 での web アプリケーションに多くのユーザーのログオンと AD FS フェデレーション サーバーのメモリ使用量が増加し続ける|July 2014|AD FS 2.1
|[2957619](https://support.microsoft.com/kb/2957619)|AD FS の委任トークンを要求が行われたときに、証明書利用者信頼の AD fs が停止しました|2014 年 5 月|AD FS 2.1
|[2926658](https://support.microsoft.com/kb/2926658)|SQL のアクセス許可があるない場合、ADFS SQL ファームの展開が失敗します。|October 2014|AD FS 2.1
|[2896713](https://support.microsoft.com/kb/2896713) or [2989956](https://support.microsoft.com/kb/2989956)|AD FS サーバーで 2843638 のセキュリティ更新プログラムをインストールした後は、いくつかの問題を解決する更新プログラムがあります。|2013 年 11 月</br></br>September 2014|AD FS 2.0 2.1/
|[2877424](https://support.microsoft.com/kb/2877424)|更新プログラムでは、複数証明書利用者信頼、AD FS で 2.1 ファーム用に 1 つの証明書を使用することができます。|2013 年 10 月|AD FS 2.1
|[2873168](https://support.microsoft.com/kb/2873168)|修正: サード パーティ製の CSP と HSM を使用して Windows Server 2008 R2 Service Pack 1 での AD FS 2.0 の更新プログラムのロールアップ 3 内の要求プロバイダー信頼を構成すると、エラーが発生しました。|9 月 2013|AD FS 2.0
|[2861090](https://support.microsoft.com/kb/2861090)|暗号化証明書のサブジェクト名の先頭に Windows Server 2008 R2 SP1 で例外が発生しました。|2013 年 8 月|AD FS 2.0
|[2843639](https://support.microsoft.com/kb/2843639)|[セキュリティ]Active Directory フェデレーション サービスの脆弱性により情報漏えい|2013 年 11 月|AD FS 2.1
|[2843638](https://support.microsoft.com/kb/2843638)|Active Directory フェデレーション サービス 2.0 用セキュリティ更新プログラムの MS13 066: の説明: 2013 年 8 月 13 日|2013 年 8 月|AD FS 2.0
|[2827748](https://support.microsoft.com/kb/2827748)|Federationmetadata.xml ファイル情報がない、MEX エンドポイントの Windows Server 2012 で、Ws-trust、Ws-federation エンドポイント|2013 年 5 月|AD FS 2.1
|[2790338](https://support.microsoft.com/kb/2790338)|Active Directory フェデレーション サービス (AD FS) の更新プログラムのロールアップ 3 の説明 2.0|2013 年 3 月|AD FS 2.0




