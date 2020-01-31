---
ms.assetid: ed3206b4-bbfc-4bc7-a43c-981b0544a50d
title: Active Directory フェデレーションサービス (AD FS) に必要な更新プログラム (AD FS)
description: ''
author: billmath
ms.author: billmath
manager: femila
ms.date: 3/29/2019
ms.topic: article
ms.prod: windows-server
ms.technology: identity-adfs
ms.openlocfilehash: b50b1b7b43002c91ee849f352e255f520f6d96f0
ms.sourcegitcommit: 07c9d4ea72528401314e2789e3bc2e688fc96001
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/29/2020
ms.locfileid: "76822735"
---
# <a name="required-updates-for-active-directory-federation-services-ad-fs-and-web-application-proxy-wap"></a>Active Directory フェデレーションサービス (AD FS) (AD FS) と Web アプリケーションプロキシ (WAP) に必要な更新

2016年10月の時点で、Windows Server のすべてのコンポーネントに対するすべての更新プログラムは、Windows Update (WU) を介してのみリリースされます。  修正プログラムや個別のダウンロードはありません。
これは、Windows Server 2016、Windows Server 2012 R2、Windows Server 2012、および Windows Server 2008 R2 SP1 に適用されます。

このページには、AD FS と WAP に関連する特定のロールアップパッケージと、AD FS および WAP に推奨される修正プログラムの更新プログラムの履歴リストが一覧表示されます。

## <a name="updates-for-ad-fs-and-wap-in-windows-server-2016"></a>Windows Server 2016 での AD FS と WAP の更新プログラム
Windows Server 2016 の更新プログラムは、Windows Update によって毎月配信され、累積されます。 次に示す更新パッケージは、すべての AD FS および WAP 2016 サーバーで推奨されており、以前に必要なすべての更新と最新の修正が含まれています。

|KB# |説明|リリース日
|----- | ----- |-----
|[4534271](https://support.microsoft.com/help/4534271/windows-10-update-kb4534271) | Google Chrome のリリース80では、新しい[SameSite](https://www.chromestatus.com/feature/5088147346030592) cookie ポリシーが既定でサポートされているため AD FS chrome エラーが発生する可能性があります。 詳細については、[こちら](https://docs.microsoft.com/office365/troubleshoot/miscellaneous/chrome-behavior-affects-applications)を参照してください。 |2020年1月|
|[CVE-2019-1126](https://portal.msrc.microsoft.com/security-guidance/advisory/CVE-2019-1126) | このセキュリティ更新プログラムは、Active Directory フェデレーションサービス (AD FS) (AD FS) の脆弱性に対処します。これにより、攻撃者がエクストラネットロックアウトポリシーをバイパスできる可能性があります。 |2019年7月|
|[4489889 (OS ビルド 14393.2879)](https://support.microsoft.com/help/4489889/windows-10-update-kb4489889) | 重複証明書利用者信頼が AD FS 管理コンソールに表示される Active Directory フェデレーションサービス (AD FS) (AD FS) の問題に対処します。 これは、AD FS 管理コンソールを使用して証明書利用者信頼を作成または表示する場合に発生します。</br></br> AD FS 2016 でエクストラネットのスマートロックアウト (ESL) が有効になっている間に発生する、高 Active Directory フェデレーションサービス (AD FS) (ADFS) Web アプリケーションプロキシ (WAP) の待機時間の問題 (10,000 ミリ秒) に対処します。 このセキュリティ更新プログラムは、 [CVE-2018-16794](https://nvd.nist.gov/vuln/detail/CVE-2018-16794)で説明されている脆弱性に対処します。 |2019 年 3 月|
|[4487006 (OS ビルド 14393.2828)](https://support.microsoft.com/help/4487006/windows-10-update-kb4487006) | PowerShell または Active Directory フェデレーションサービス (AD FS) (AD FS) 管理コンソールを使用しているときに、証明書利用者信頼の更新が失敗する原因となる問題に対処します。 この問題は、複数の PassiveRequestorEndpoint を発行するオンラインメタデータ URL を使用するように証明書利用者信頼を構成すると発生します。 "MSIS7615: 証明書利用者信頼に指定された信頼されたエンドポイントは、その証明書利用者信頼に対して一意である必要があります。" というエラーが発生します。  </br></br>Azure のパスワード保護ポリシーにより、外部の複雑さのパスワード変更に関する特定のエラーメッセージを表示する問題に対処します。 |2019 年 2 月|
|[4462928 (OS ビルド 14393.2580)](https://support.microsoft.com/help/4462928/windows-10-update-kb4462928)|Active Directory フェデレーションサービス (AD FS) (ADFS) エクストラネットスマートロックアウト (ESL) と代替ログイン ID 間の相互運用の問題に対処します。 代替ログイン ID が有効になっている場合、AD FS Powershell コマンドレットを呼び出し、AdfsAccountActivity と AdfsAccountLockout を呼び出して、"アカウントが見つかりません" エラーを返します。 AdfsAccountActivity が呼び出されると、既存のエントリを編集する代わりに新しいエントリが追加されます。|2018 年 10 月|
|[4343884 (OS ビルド 14393.2457)](https://support.microsoft.com/help/4343884/windows-10-update-kb4343884)|カスタムカルチャ定義を使用するモバイルデバイスで Multi-Factor Authentication が正しく機能しない Active Directory フェデレーションサービス (AD FS) (AD FS) の問題に対処します。 </br></br>Windows Hello for Business の問題に対処します。この問題は、新規ユーザーの登録で大幅な遅延 (15 秒) が発生します。 この問題は、ハードウェアセキュリティモジュールを使用して ADFS 登録機関 (RA) 証明書を格納している場合に発生します。|2018 年 8 月|
|[4338822 (OS ビルド 14393.2395)](https://support.microsoft.com/help/4338822/windows-10-update-kb4338822)|AD FS 管理コンソールを作成またはコンソールから証明書利用者信頼を表示するときに重複する証明書利用者信頼を示しています。 AD FS では問題に対処します。</br></br>Windows Hello for Business が失敗すると、ADFS で問題に対処します。 問題は、2 つのクレーム プロバイダーがある場合に発生します。 PIN の登録が失敗し、"400 内部サーバーエラー: デバイス識別子を取得できません。" というメッセージが表示されます。</br></br> 終了しない非アクティブな接続に関連する WAP 問題に対処します。 これにより、システム リソースのリーク (メモリ リークなど)、WAP サービスが応答しなくです。 ユーザー別のログイン オプションを選択できないようにする AD FS 問題に対処します。 これには、ユーザーが証明書ベースの認証を使用してログインする選択が構成されていないときに発生します。 これは、ユーザーが証明書ベースの認証を選択すると、別のログイン オプションを選択してから再試行してくださいにも発生します。 この場合、ブラウザーを閉じるまでには、ユーザー名は証明書ベースの認証ページにリダイレクトします。|2018 年 7 月|
|[4103720 (OS ビルド 14393.2273)](https://support.microsoft.com/help/4103720/windows-10-update-kb4103720)|PreventTokenReplays が有効になっている場合に、SAML 証明書利用者への IdP によって開始されたログインが失敗するようにする ADFS の問題に対処します。 </br></br>OAUTH がデバイスまたはブラウザーアプリケーションから認証されるときに発生する ADFS の問題に対処します。 ユーザーパスワードの変更によってエラーが生成され、ユーザーはログインするためにアプリまたはブラウザーを終了する必要があります。 </br></br>UTC + 1 以上 (ヨーロッパおよびアジア) でエクストラネットのスマートロックアウトを有効にできなかった問題に対処します。 さらに、通常のエクストラネットロックアウトは、次のエラーで失敗します。 AdfsAccountActivity: UTC に変換されたときに MinValue より小さい datetime 値を JSON にシリアル化することはできません。</br></br>アドレス、ADFS Windows Hello for ビジネスの問題で新しいユーザーが自分の PIN をプロビジョニングできませんにない。 このエラーは、MFA プロバイダーが構成されていない場合に発生します。|2018 年 5 月|
|[4093120 (OS ビルド 14393.2214)](https://support.microsoft.com/help/4093120/windows-10-update-kb4093120)| 未処理の更新トークンの検証の問題を解決します。 次のエラーが生成されます: "MSIS9312: 無効な OAuth 更新トークンを受信しました。 '... OAuth。 更新トークンは、トークンで許可されている時間よりも前に受信されました。 " |2018 年 4 月|
|[4077525 (OS ビルド 14393.2097)](https://support.microsoft.com/help/4077525/windows-10-update-kb4077525)|ADFS ファームに Windows Internal Database (WID) を使用する少なくとも2台のサーバーがある場合に HTTP 500 エラーが発生する問題に対処します。 このシナリオでは、Web アプリケーションプロキシ (WAP) サーバー上の HTTP 基本事前認証が、一部のユーザーの認証に失敗します。 このエラーが発生すると、WAP イベントログに Microsoft Windows Web アプリケーションプロキシの警告イベント ID 13039 が表示されることがあります。 この説明は、"Web アプリケーションプロキシがユーザーを認証できませんでした。 事前認証は、"リッチクライアント用 ADFS" です。 指定されたユーザーには、指定された証明書利用者へのアクセスが許可されていません。 ターゲット証明書利用者または WAP 証明書利用者の承認規則を変更する必要があります。 "</br></br>認証時に AD FS が prompt = login を無視できなくなる問題を解決します。 パスワード認証が使用されないシナリオをサポートするために、無効なオプションが追加されました。 詳細については、Windows Server 2016 RTM での認証時に "prompt = login" パラメーターを無視する AD FS を参照してください。</br></br>認証オプションとして証明書を選択する承認された顧客 (および証明書利用者) が接続できない AD FS の問題に対処します。 Windows 統合認証 (WIA) が有効になっていて、要求で WIA を実行できる場合、prompt = login を使用するとエラーが発生します。</br></br>Id プロバイダー (IDP) が OAuth グループ内の証明書利用者 (RP) に関連付けられている場合に、AD FS によってホーム領域検出 (HRD) ページが正しく表示されない問題に対処します。 OAuth グループの RP に複数の IDPs が関連付けられていない限り、ユーザーは HRD ページを表示しません。 代わりに、ユーザーは、認証のために関連付けられている IDP に直接アクセスします。|2018 年 2 月|
|[4041688 (OS ビルド 14393.1794)](https://support.microsoft.com/kb/4041688)|この修正は、間違ったキャッシュ動作が原因で AD 機関の要求が間違った Id プロバイダーに断続的にリダイレクトされる問題に対処します。 これにより、Multi-factor Authentication などの認証機能が有効になります。 </br></br>AAD Connect Health が混合 WS2012R2 と WS2016 ADFS ファームで適切な忠実性 (詳細な監査を使用) によってレポート ADFS サーバーの正常性をレポートする機能を追加しました。</br></br>2012 R2 ADFS ファームを ADFS 2016 にアップグレードするときに、多くの証明書利用者信頼があるときに、ファームの動作レベルを上げる powershell コマンドレットがタイムアウトして失敗する問題を修正しました。</br></br>AD FS が、他のセキュリティトークンサーバー (STS) への要求のフェデレーション中に wct パラメーター値を変更することによって認証エラーが発生する問題に対処しました。|2017 年 10 月|
|[4038801 (OS ビルド 14393.1737)](https://support.microsoft.com/kb/4038801)|フェデレーション LDPs を使用した OIDC ログアウトのサポートが追加されました。 これにより、LDP とのフェデレーションがある1台のデバイスに複数のユーザーが連続してログインしている "キオスクシナリオ" が可能になります。</br></br>CEP/CES ベースの証明書が gMSA アカウントで使用できない WinHello の問題を修正した。</br></br>外部キーが原因で、Windows Server 2016 ADFS サーバーの Windows Internal Database (WID) が一部の設定を同期できない問題を修正します。たとえば、外部キーが原因で、Windows Server ADFS サーバーの ApplicationGroupId 列などの一部の設定が同期されない場合があります。制約. このような同期エラーが発生すると、プライマリサーバーとセカンダリ ADFS サーバー間で異なる要求、要求プロバイダー、およびアプリケーションエクスペリエンスが発生する可能性があります。 また、WID プライマリロールがセカンダリノードに移動された場合、アプリケーショングループは ADFS 管理 UX で管理できなくなります。</br></br>この更新プログラムは、カスタムカルチャ定義を使用するモバイルデバイスで Multi-factor Authentication が正しく機能しない問題を修正します。|2017 年 9 月|
|[4034661 (OS ビルド 14393.1613)](https://support.microsoft.com/kb/4034661)|"成功の監査" と "失敗の監査" を有効にした後でも、ADFS 4.0 \ Windows Server 2016 RS1 ADFS サーバーのセキュリティイベントログに、呼び出し元の IP アドレスが nog 411 で記録される問題を修正します。</br></br>この修正は、ADFX サーバーが HTTP プロキシを使用するように構成されている場合の Azure Multi-factor Authentication (MFA) の問題に対処します。</br></br>"期限切れまたは失効した証明書を ADFS プロキシサーバーに提示しても、ユーザーにエラーが返されないという問題に対処しました。"|2017 年 8 月|
|[4034658 (OS ビルド 14393.1593)](https://support.microsoft.com/kb/4034658)|オンプレミスのデプロイで Windows Hello For Business 用の MFA 証明書の登録をサポートするために 2016年の AD FS サーバーを修正します。|2017 年 8 月|
|[4025334 (OS ビルド 14393.1532)](https://support.microsoft.com/kb/4025334)|PkeyAuth 要求に正しくないデータが含まれている場合に、PkeyAuth token handler が認証に失敗する問題に対処しました。 認証は、デバイス認証を実行しなくても続行されます。|2017 年 7 月|
|[4022723 (OS ビルド 14393.1378)](https://support.microsoft.com/kb/4022723)|[Web アプリケーションプロキシ]DisableHttpOnlyCookieProtection 構成プロパティの値は、2012R2/2016 混合デプロイの WAP 2016 では選択されません </br></br>[Web アプリケーションプロキシ]EAS 事前認証シナリオの AD FS からユーザーアクセストークンを取得できません。</br></br>AD FS 2016: WSFED サインアウトしたときに例外が発生する|2017 年 6 月
|[3213986](https://support.microsoft.com/kb/3213986)|X64 ベースシステム用 Windows Server 2016 の累積的な更新プログラム (KB3213986)| 2017 年 1 月

## <a name="updates-for-ad-fs-and-wap-in-windows-server-2012-r2"></a>Windows Server 2012 R2 での AD FS と WAP の更新プログラム
Windows Server 2012 R2 の Active Directory フェデレーションサービス (AD FS) (AD FS) でリリースされた修正プログラムと更新プログラムのロールアップの一覧を次に示します。

|KB# |説明|リリース日
|----- | ----- |-----
|[4534309](https://support.microsoft.com/help/4534309/windows-8-1-kb4534309)| Google Chrome のリリース80では、新しい[SameSite](https://www.chromestatus.com/feature/5088147346030592) cookie ポリシーが既定でサポートされているため AD FS chrome エラーが発生する可能性があります。 詳細については、[こちら](https://docs.microsoft.com/office365/troubleshoot/miscellaneous/chrome-behavior-affects-applications)を参照してください。 |2020年1月
|[4507448](https://support.microsoft.com/help/4507448/windows-8-1-update-kb4507448)| このセキュリティ更新プログラムは、Active Directory フェデレーションサービス (AD FS) (AD FS) の脆弱性に対処します。これにより、攻撃者がエクストラネットロックアウトポリシーをバイパスできる可能性があります。 |2019年7月
|[4041685](https://support.microsoft.com/kb/4041685)|要求ヘッダーの MSISConext クッキーが最終的にヘッダーサイズの制限をオーバーフローし、HTTP 状態コード400の "Bad Request-Header 長すぎます" で失敗する可能性がある AD FS の問題に対処します。</br></br>認証時に ADFS が "prompt = login" を無視できなくなる問題を修正しました。 非パスワード認証が使用される復元シナリオに "Disabled" オプションが追加されました。|更新プログラムのロールアップの2017年10月のプレビュー
|[4019217](https://support.microsoft.com/kb/4019217)|サーバー 2012 R2 AD FS サーバーを使用しているときに、トークンブローカーを使用しているワークフォルダークライアントが機能しない|2017年5月の更新プログラムのロールアップ
|[4015550](https://support.microsoft.com/kb/4015550)|外部ユーザーを認証せず、AD FS WAP が要求をランダムに転送できない AD FS の問題を修正した|2017年4月の更新プログラムのロールアップ
|[4015547](https://support.microsoft.com/kb/4015547)|外部ユーザーを認証せず、AD FS WAP が要求をランダムに転送できない AD FS の問題を修正した|2017年4月のセキュリティ更新プログラム
|[4012216](https://support.microsoft.com/kb/4009970)|MS17-019 このセキュリティ更新プログラムは、Active Directory フェデレーションサービス (AD FS) (ADFS) の脆弱性を解決します。 攻撃者が特別に細工された要求を AD FS サーバーに送信すると、脆弱性によって情報漏えいが発生する可能性があります。これにより、攻撃者はターゲットシステムに関する機密情報を読み取ることができます。|2017年3月の更新プログラムのロールアップ
|[3179574](https://support.microsoft.com/kb/3179574)|エクストラネットパスワード更新 AD FS の問題を修正した。 |2016年8月の更新プログラムのロールアップ
|[3172614](https://support.microsoft.com/kb/3172614)|Prompt = ログイン[サポート](https://technet.microsoft.com/windows-server-docs/identity/ad-fs/overview/ad-fs-faq#BKMK_7)を導入し、AD FS 管理コンソールと Always requireauthentication 設定の問題を修正しました。 |2016年7月の更新プログラムのロールアップ
|[3163306](https://support.microsoft.com/kb/3163306)|Active Directory フェデレーションサービス (AD FS) (AD FS) 3.0 は、接続文字列で Secure Sockets Layer (SSL) ポート636または3269を使用するように構成されているライトウェイトディレクトリアクセスプロトコル (LDAP) 属性ストアに接続できません。 |2016年6月の更新プログラムのロールアップ
|[3148533](https://support.microsoft.com/kb/3148533)|Windows Server 2012 R2 の ADFS プロキシを介して MFA フォールバック認証が失敗する |2016 年 5 月
|[3134787](https://support.microsoft.com/kb/3134787)|AD FS ログには、Windows Server 2012 R2 のアカウントロックアウトシナリオのクライアント IP アドレスが含まれていません。 |2016 年 2 月
|[3134222](https://support.microsoft.com/kb/3134222)|MS16-020: サービス拒否に対処するための Active Directory フェデレーションサービス (AD FS) のセキュリティ更新プログラム: 2016 年2月9日|2016 年 2 月
|[3105881](https://support.microsoft.com/kb/3105881)|Windows Server 2012 R2 ベースの AD FS サーバーでデバイス認証が有効になっていると、アプリケーションにアクセスできない|2015 年 10 月
|[3092003](https://support.microsoft.com/kb/3092003)|ユーザーが Windows Server 2012 R2 で MFA を使用すると、ページの読み込みが繰り返し、認証が失敗する AD FS|2015 年 8 月
|[3080778](https://support.microsoft.com/kb/3080778)|Windows Server 2012 R2 で MFA アダプターが例外をスローすると AD FS が OnError を呼び出さない|2015 年 7 月
|[3075610](https://support.microsoft.com/kb/3075610)|Windows Server 2012 R2 で要求プロバイダーを追加または削除した後、セカンダリ AD FS サーバーで信頼関係が失われる|2015 年 7 月
|[3070080](https://support.microsoft.com/kb/3070080)|ホーム領域の検出は、要求に対応していない証明書利用者信頼に対して正しく機能していません|2015 年 6 月
|[3052122](https://support.microsoft.com/kb/3052122)|更新により、Windows Server 2012 R2 の AD FS トークンに複合 ID 要求のサポートが追加されます。|5月2015
|[3045711](https://support.microsoft.com/kb/3045711)|MS15-040: Active Directory フェデレーションサービス (AD FS) の脆弱性により、情報漏えいが起こる|2015年4月
|[3042127](https://support.microsoft.com/kb/3042127)|Windows Server 2012 R2 で WAP を介して共有メールボックスを開いたときに "HTTP 400-Bad Request" エラーが発生する|2015 年 3 月
|[3042121](https://support.microsoft.com/kb/3042121)|Windows Server 2012 R2 の Web アプリケーションプロキシ認証トークンの AD FS トークン再生保護|2015 年 3 月
|[3035025](https://support.microsoft.com/kb/3035025)|Windows Server 2012 R2 で登録されているデバイスをユーザーが使用する必要がないように、パスワード更新機能の修正プログラム|2015 年 1 月
|[3033917](https://support.microsoft.com/kb/3033917)|AD FS は、Windows Server 2012 R2 の SAML 応答を処理できません|2015 年 1 月
|[3025080](https://support.microsoft.com/kb/3025080)|Windows Server 2012 R2 の Web アプリケーションプロキシを使用して Office ファイルを保存しようとすると操作が失敗する|2015 年 1 月
|[3025078](https://support.microsoft.com/kb/3025078)|間違ったユーザー名を使用して Windows Server 2012 R2 にログオンすると、ユーザー名の入力を求められません。|2015 年 1 月
|[3020813](https://support.microsoft.com/kb/3020813)|Windows Server 2012 R2 で web アプリケーションを実行すると、認証を求めるメッセージが表示され AD FS|2015 年 1 月
|[3020773](https://support.microsoft.com/kb/3020773)|Windows Server 2012 R2 でデバイス登録サービスを最初に展開した後のタイムアウトエラー|2015 年 1 月
|[3018886](https://support.microsoft.com/kb/3018886)|イントラネットから Windows Server 2012 R2 AD FS サーバーにアクセスすると、ユーザー名とパスワードを2回入力するように求められます。|2015 年 1 月
|[3013769](https://support.microsoft.com/kb/3013769)|Windows Server 2012 R2 更新プログラムのロールアップ|2014 年 12 月
|[3000850](https://support.microsoft.com/kb/3000850)|Windows Server 2012 R2 更新プログラムのロールアップ|2014 年 11 月
|[2975719](https://support.microsoft.com/kb/2975719)|Windows Server 2012 R2 更新プログラムのロールアップ|2014 年 8 月
|[2967917](https://support.microsoft.com/kb/2967917)|Windows Server 2012 R2 更新プログラムのロールアップ|2014 年 7 月
|[2962409](https://support.microsoft.com/kb/2962409)|Windows Server 2012 R2 更新プログラムのロールアップ|2014 年 6 月
|[2955164](https://support.microsoft.com/kb/2955164)|Windows Server 2012 R2 更新プログラムのロールアップ|5月2014
|[2919355](https://support.microsoft.com/kb/2919355)|Windows Server 2012 R2 更新プログラムのロールアップ|2014 年 4 月

## <a name="updates-for-ad-fs-in-windows-server-2012-ad-fs-21-and-ad-fs-20"></a>Windows Server 2012 での AD FS の更新 (AD FS 2.1) と AD FS 2.0
AD FS 2.0 および2.1 用にリリースされている修正プログラムおよび更新プログラムのロールアップの一覧を次に示します。

|KB# |説明|リリース日|適用先:
|----- | ----- |-----|-----
|[3197878](https://support.microsoft.com/kb/3197878)|Windows Server 2012 でプロキシによる認証に失敗する (これは修正プログラム3094446の一般リリースです)|2016年11月の品質ロールアップ|AD FS 2.1
|[3197869](https://support.microsoft.com/kb/3197869)|Windows Server 2008 R2 SP1 でプロキシによる認証に失敗する (これは修正プログラム3094446の一般リリースです)|2016年11月の品質ロールアップ|AD FS 2.0
|[3094446](https://support.microsoft.com/kb/3094446)|Windows Server 2012 または Windows Server 2008 R2 SP1 でプロキシによる認証に失敗する|2015 年 9 月|AD FS 2.0 および2.1
|[3070078](https://support.microsoft.com/kb/3070078)|Windows Server 2012 の暗号化証明書に対して認証する場合、AD FS 2.1 は例外をスローします。|2015 年 7 月|AD FS 2.1
|[3062577](https://support.microsoft.com/kb/3062577)|MS15-062: Active Directory フェデレーションサービスの脆弱性により、特権が昇格される|2015 年 6 月|AD FS 2.0/2.1
|[3003381](https://support.microsoft.com/kb/3003381)|MS14-077: Active Directory フェデレーションサービス (AD FS) の脆弱性により、情報が漏えいする可能性があります: 2015 年4月14日|2014 年 11 月|AD FS 2.0/2.1
|[2987843](https://support.microsoft.com/kb/2987843)|Windows Server 2012 で多くのユーザーが web アプリケーションにログオンすると AD FS フェデレーションサーバーのメモリ使用量が増加し続ける|2014 年 7 月|AD FS 2.1
|[2957619](https://support.microsoft.com/kb/2957619)|委任されたトークンの AD FS に対する要求が行われると、AD FS の証明書利用者信頼が停止します。|5月2014|AD FS 2.1
|[2926658](https://support.microsoft.com/kb/2926658)|SQL アクセス許可がない場合、ADFS SQL ファームの配置が失敗する|2014 年 10 月|AD FS 2.1
|[2896713](https://support.microsoft.com/kb/2896713)または[2989956](https://support.microsoft.com/kb/2989956)|AD FS サーバーにセキュリティ更新プログラム2843638をインストールした後で、いくつかの問題を修正するための更新プログラムを利用できます。|2013年11月</br></br>2014年9月|AD FS 2.0/2.1
|[2877424](https://support.microsoft.com/kb/2877424)|更新プログラムでは、AD FS 2.1 ファーム内の複数の証明書利用者信頼に対して1つの証明書を使用できます。|2013 年 10 月|AD FS 2.1
|[2873168](https://support.microsoft.com/kb/2873168)|修正: サードパーティの CSP と HSM を使用し、Windows Server 2008 R2 Service Pack 1 の AD FS 2.0 の更新プログラムのロールアップ3で要求プロバイダー信頼を構成すると、エラーが発生します。|2013年9月|AD FS 2.0
|[2861090](https://support.microsoft.com/kb/2861090)|暗号化証明書のサブジェクト名にコンマがあると、Windows Server 2008 R2 SP1 で例外が発生する|2013 年 8 月|AD FS 2.0
|[2843639](https://support.microsoft.com/kb/2843639)|保護Active Directory フェデレーションサービス (AD FS) の脆弱性により、情報漏えいが起こる|2013年11月|AD FS 2.1
|[2843638](https://support.microsoft.com/kb/2843638)|MS13-066: Active Directory フェデレーションサービス (AD FS) 2.0 のセキュリティ更新プログラムの説明: 2013 年8月13日|2013 年 8 月|AD FS 2.0
|[2827748](https://support.microsoft.com/kb/2827748)|Federationmetadata.xml ファイルには、Windows Server 2012 の WS-TRUST および WS-FEDERATION エンドポイントの MEX エンドポイント情報が含まれていません|5月2013|AD FS 2.1
|[2790338](https://support.microsoft.com/kb/2790338)|Active Directory フェデレーションサービス (AD FS) (AD FS) 2.0 の更新プログラムのロールアップ3の説明|2013 年 3 月|AD FS 2.0
