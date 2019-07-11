---
ms.assetid: ed3206b4-bbfc-4bc7-a43c-981b0544a50d
title: Active Directory フェデレーション サービス (AD FS) の必要な更新プログラム
description: ''
author: billmath
ms.author: billmath
manager: femila
ms.date: 3/29/2019
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adfs
ms.openlocfilehash: 2336847825cfb3f232674a1e39d3bab7953a32c0
ms.sourcegitcommit: be243a92f09048ca80f85d71555ea6ee3751d712
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/11/2019
ms.locfileid: "67792298"
---
# <a name="required-updates-for-active-directory-federation-services-ad-fs-and-web-application-proxy-wap"></a>Active Directory フェデレーション サービス (AD FS) と Web アプリケーション プロキシ (WAP) の必要な更新プログラム


2016 年 10 月の時点で Windows Server のすべてのコンポーネントに対するすべての更新にのみ Windows Update (WU) 経由で、解放されます。  ない他の修正プログラムまたは個別のダウンロード パッケージがあります。
これは、Windows Server 2016、Windows Server 2012 R2、Windows Server 2012 および Windows Server 2008 R2 SP1 に適用されます。

このページは、AD FS と WAP では、AD FS と WAP の推奨される修正プログラムの更新の履歴一覧の特定の関心のあるプログラムのロールアップ パッケージを一覧表示します。

## <a name="updates-for-ad-fs-and-wap-in-windows-server-2016"></a>AD FS と WAP で Windows Server 2016 の更新プログラム
Windows Server 2016 の更新プログラムは毎月 Windows Update 経由で配信され、は累積されます。 以下に示す更新プログラム パッケージは、すべての AD FS と WAP 2016 サーバーの推奨がおよび、以前に必要なすべての更新プログラムと最新の修正プログラムが含まれています。

|KB # |説明|リリース日
|----- | ----- |-----
|[CVE-2019-1126](https://portal.msrc.microsoft.com/security-guidance/advisory/CVE-2019-1126) | このセキュリティ更新プログラムは、攻撃者がエクストラネットのロックアウト ポリシーをバイパスする Active の Directory フェデレーション サービス (AD FS) の脆弱性に対処します。 |2019 年の 7 月|
|[4489889 (OS ビルド 14393.2879)](https://support.microsoft.com/help/4489889/windows-10-update-kb4489889) | 重複している信頼、AD FS 管理コンソールに表示される証明書利用者を原因となる Active の Directory フェデレーション サービス (AD FS) で発生する問題に対処します。 これは、証明書利用者信頼、AD FS 管理コンソールを使用して作成または表示するときに発生します。 |3 月 2019|
|[4487006 (OS ビルド 14393.2828)](https://support.microsoft.com/help/4487006/windows-10-update-kb4487006) | 証明書利用者信頼を PowerShell または Active Directory フェデレーション サービス (AD FS) の管理コンソールを使用するときに更新プログラムが問題に対処します。 この問題は、1 つ以上の PassiveRequestorEndpoint を発行するオンラインのメタデータ URL を使用するを証明書利用者信頼を構成する場合に発生します。 エラーは、"MSIS7615:A relying party trust で指定された信頼できるエンドポイントする必要がありますで一意であるその証明書利用者信頼のためです。"  </br></br>Azure パスワード保護ポリシーのために複雑さの外部パスワード変更の特定のエラー メッセージを表示する問題に対処します。 |2019 年 2 月|
|[4462928 (OS ビルド 14393.2580)](https://support.microsoft.com/help/4462928/windows-10-update-kb4462928)|Active Directory フェデレーション サービス (ADFS) エクストラネット スマート ロックアウト (ESL) と代替ログイン ID の間の相互運用の問題に対処します。 代替ログイン ID が有効な場合は、AD FS Powershell コマンドレット、Get AdfsAccountActivity とリセット AdfsAccountLockout、戻り値の「アカウントが見つかりません」エラーを呼び出します。 セット AdfsAccountActivity が呼び出されると、既存のものを編集する代わりに新しいエントリが追加されます。|2018 年 10 月|
|[4343884 (OS ビルド 14393.2457)](https://support.microsoft.com/en-us/help/4343884/windows-10-update-kb4343884)|Multi-factor Authentication が機能しないという正しくモバイル デバイスのカスタム定義を使用すると、Active Directory フェデレーション サービス (AD FS) の問題に対処します。 </br></br>Windows hello for Business の新しいユーザー登録で大幅な遅延 (15 秒) が発生する問題に対処します。 この問題は、ハードウェア セキュリティ モジュールを使用して、ADFS 登録機関 (RA) 証明書を格納するときに発生します。|2018 年 8 月|
|[4338822 (OS ビルド 14393.2395)](https://support.microsoft.com/help/4338822/windows-10-update-kb4338822)|AD FS 管理コンソールを作成またはコンソールから証明書利用者信頼を表示するときに重複する証明書利用者信頼を示しています。 AD FS では問題に対処します。</br></br>Windows Hello for Business が失敗すると、ADFS で問題に対処します。 問題は、2 つのクレーム プロバイダーがある場合に発生します。 PIN の登録は失敗し、"400 の内部サーバー エラー。デバイスの識別子を取得できません。"</br></br> 終了しない非アクティブな接続に関連する WAP 問題に対処します。 これにより、システム リソースのリーク (メモリ リークなど)、WAP サービスが応答しなくです。 ユーザー別のログイン オプションを選択できないようにする AD FS 問題に対処します。 これには、ユーザーが証明書ベースの認証を使用してログインする選択が構成されていないときに発生します。 これは、ユーザーが証明書ベースの認証を選択すると、別のログイン オプションを選択してから再試行してくださいにも発生します。 この場合、ブラウザーを閉じるまでには、ユーザー名は証明書ベースの認証ページにリダイレクトします。|2018 年 7 月|
|[4103720 (OS ビルド 14393.2273)](https://support.microsoft.com/help/4103720/windows-10-update-kb4103720)|SAML 証明書利用者 PreventTokenReplays を有効にするときに、IdP によって開始されたログインが原因で ADFS を使用した問題に対処します。 </br></br>デバイスまたはブラウザー アプリケーションからの OAUTH 認証するときに発生する ADFS 問題に対処します。 ユーザー パスワードの変更は、エラーを生成し、アプリケーションまたはログインにブラウザーを終了する必要があります。 </br></br>場所 (utc) +1 エクストラネットのスマート ロックアウトと高い (ヨーロッパおよびアジア) を有効にする動作しなかった問題に対処します。 さらに、次のエラーで失敗する通常のエクストラネット ロックアウトが発生します。Get AdfsAccountActivity:DateTime.MaxValue より大きいか UTC に変換するときに DateTime.MinValue より小さい DateTime 値は、JSON にシリアル化することはできません。</br></br>アドレス、ADFS Windows Hello for ビジネスの問題で新しいユーザーが自分の PIN をプロビジョニングできませんにない。 これには、MFA プロバイダーが構成されていないときに発生します。|2018 年 5 月|
|[4093120 (OS ビルド 14393.2214)](https://support.microsoft.com/help/4093120/windows-10-update-kb4093120)| ハンドルされていない更新トークンの検証の問題に対処します。 次のエラーが生成されます。"Microsoft.IdentityServer.Web.Protocols.OAuth.Exceptions.OAuthInvalidRefreshTokenException:MSIS9312:無効な OAuth 更新トークンを受信します。 更新トークンが受信したトークンで許容時間よりも前です。" |2018 年 4 月|
|[4077525 (OS ビルド 14393.2097)](https://support.microsoft.com/help/4077525/windows-10-update-kb4077525)|:ADFS ファームがある Windows Internal Database (WID) を使用して、少なくとも 2 つのサーバーと HTTP 500 エラーが発生する問題に対処します。 このシナリオで Web アプリケーション プロキシ (WAP) サーバー上の HTTP 基本の事前認証は一部のユーザーの認証に失敗します。 エラーが発生する場合は、警告、WAP のイベント ログでイベント ID 13039 Microsoft Windows Web アプリケーション プロキシも表示があります。 説明の読み取り、"Web アプリケーション プロキシは、ユーザーの認証に失敗しました。 事前認証は、' リッチ クライアントの ADFS ' です。 特定のユーザーは、指定された証明書利用者にアクセスする権限がありません。 ターゲット証明書利用者または WAP 証明書利用者の承認規則に必要な変更です。"</br></br>プロンプトが AD FS に無視できなく問題に対処認証時にログインを = です。 によって、パスワード認証を使用しないシナリオをサポートするために、無効になっているオプションが追加されました。 詳細については、AD FS Windows Server 2016 RTM で、認証時に「prompt = login」パラメーターを無視するを参照してください。</br></br>承認されている AD FS で問題を解決するお客様 (および証明書利用者) 証明書を選択するように、認証オプションは接続に失敗します。 プロンプトを使用する場合に、障害が発生したログインを = Windows 統合認証 (WIA) が有効になっていて、要求は、WIA を行うことができます。</br></br>AD FS 表示されます、ホーム領域検出 (HRD) ページ id プロバイダー (IDP) は、OAuth グループで証明書利用者 (RP) と関連付けられているときに問題に対処します。 複数の Idp が OAuth グループで RP に関連付けられている場合を除き、ユーザーは表示されません HRD ページ。 代わりに、ユーザーが認証に関連付けられている IDP に直接移動します。|2018 年 2 月|
|[4041688 (OS ビルド 14393.1794)](https://support.microsoft.com/kb/4041688)|この修正プログラムは、不適切なキャッシュ動作のために、不適切な Id プロバイダーに要求を AD 機関を断続的に間違った宛先問題に対処します。 これにより、多要素認証などの認証機能が影響することができます。 </br></br>AAD Connect Health の機能が (詳細な監査を使用した) 正しいに忠実混合 WS2012R2 および WS2016 ADFS ファームで ADFS サーバーの正常性レポートに追加。</br></br>ファーム動作レベルを上げるための powershell コマンドレットは、2012年のアップグレード中に R2 の ad FS ファームを ADFS 2016 問題を修正、多くの証明書利用者信頼がある場合にタイムアウトで失敗します。</br></br>AD FS が要求するその他のセキュリティ トークン サーバー (STS) をフェデレーションしているときに、wct パラメーターの値を変更することで認証エラーを発生する問題に対処します。|2017 年 10 月|
|[4038801 (OS ビルド 14393.1737)](https://support.microsoft.com/kb/4038801)|LDPs フェデレーションを使用して、OIDC ログアウトの追加をサポートします。 これにより、「キオスク シナリオ」、複数のユーザーが直列に記録される 1 つのデバイスが、LDP とのフェデレーション。</br></br>GMSA アカウントで CEP/CES ベースの証明書の問題は動作しない WinHello を修正しました。</br></br>IdentityServerPolicy.Scopes IdentityServerPolicy.Clients テーブルから ApplicationGroupId 列など、一部の設定を同期する Windows Server 2016 の ad FS サーバーで Windows Internal Database (WID) が失敗する問題を修正) により、外部キー制約です。 このような同期エラーは、さまざまな要求が発生する、プライマリからセカンダリへの ADFS サーバー間でのプロバイダーとアプリケーションのエクスペリエンスを要求できます。 また、WID の主な役割はセカンダリ ノードに移動する場合のアプリケーション グループしなくなる ADFS 管理エクスペリエンスで管理しやすい</br></br>この更新プログラムは多要素認証が機能しないという正しくモバイル デバイスのカスタム定義を使用すると、問題を修正します。|2017 年 9 月|
|[4034661 (OS ビルド 14393.1613)](https://support.microsoft.com/kb/4034661)|呼び出し元の IP アドレスが ADFS 4.0 のセキュリティ イベント ログに 411 イベントによってログに記録 nog が問題を修正 \「成功の監査」と「失敗の監査」を有効にした後にも Windows Server 2016 RS1 ADFS サーバー。</br></br>この修正プログラムが Azure 多要素認証 (MFA) と、問題を解決するは、ADFX サーバーは HTTP プロキシを使用するように構成します。</br></br>「を ADFS プロキシ サーバーに有効期限が切れたか、失効した証明書を表示するエラーは返されませんをユーザーに、問題に対処します。」|2017 年 8 月|
|[4034658 (OS ビルド 14393.1593)](https://support.microsoft.com/kb/4034658)|オンプレミスのデプロイで Windows Hello For Business 用の MFA 証明書の登録をサポートするために 2016年の AD FS サーバーを修正します。|2017 年 8 月|
|[4025334 (OS ビルド 14393.1532)](https://support.microsoft.com/kb/4025334)|Pkeyauth 要求には、不適切なデータが含まれている場合に、PkeyAuth トークン ハンドラーで、認証に失敗が問題に対処します。 デバイス認証を実行せず、認証が引き続き必要があります。|2017 年 7 月|
|[4022723 (OS ビルド 14393.1378)](https://support.microsoft.com/kb/4022723)|[Web アプリケーション プロキシ]DisableHttpOnlyCookieProtection 構成プロパティの値は取得されません WAP 2016 2012R2/2016 混合展開で </br></br>[Web アプリケーション プロキシ]EAS の事前認証シナリオで AD FS からのユーザー アクセス トークンを取得できませんでした。</br></br>AD FS 2016 :サインアウト WSFED が例外を発生します。|2017 年 6 月
|[3213986](https://support.microsoft.com/kb/3213986)|X64 ベース システム (KB3213986) の Windows Server 2016 の累積更新プログラム| 2017 年 1 月

## <a name="updates-for-ad-fs-and-wap-in-windows-server-2012-r2"></a>AD FS と WAP で Windows Server 2012 R2 更新プログラム
Windows Server 2012 R2 で Active Directory フェデレーション サービス (AD FS) 用にリリースされた修正プログラムと更新プログラムのロールアップの一覧を以下に示します。

|KB # |説明|リリース日
|----- | ----- |-----
|[4507448](https://support.microsoft.com/help/4507448/windows-8-1-update-kb4507448)| このセキュリティ更新プログラムは、攻撃者がエクストラネットのロックアウト ポリシーをバイパスする Active の Directory フェデレーション サービス (AD FS) の脆弱性に対処します。 |2019 年の 7 月
|[4041685](https://support.microsoft.com/kb/4041685)|AD FS 要求ヘッダーで MSISConext cookie できます最終的にヘッダー サイズの上限をオーバーフロー、問題の認証に失敗する HTTP ステータス コード 400 でアドレス指定された「不適切な要求-ヘッダー長すぎます」。</br></br>ADFS が無視できなく「prompt = login」認証中に問題を修正しました。 [無効] オプションは、パスワード以外の認証が使用されているシナリオの復元に追加されました。|2017 年 10 月プレビューの更新プログラムのロールアップ
|[4019217](https://support.microsoft.com/kb/4019217)|ワーク フォルダー サーバー 2012 R2 AD FS サーバーを使用する場合、トークン ブローカーを使用してクライアントが動作しません。|2017 年 5 月プレビューの更新プログラムのロールアップ
|[4015550](https://support.microsoft.com/kb/4015550)|AD FS の外部ユーザーと要求を転送するようにランダムに失敗している AD FS WAP を認証できない問題を修正しました|2017 年 4 月の更新プログラムのロールアップ
|[4015547](https://support.microsoft.com/kb/4015547)|AD FS の外部ユーザーと要求を転送するようにランダムに失敗している AD FS WAP を認証できない問題を修正しました|2017 年 4 月のセキュリティ更新プログラム
|[4012216](https://support.microsoft.com/kb/4009970)|MS17 019 このセキュリティ更新プログラムは、Active Directory フェデレーション サービス (ADFS) で脆弱性を解決します。 この脆弱性により、攻撃者は、ターゲット システムに関する機密情報を読み取る、攻撃者の AD FS サーバーに特別に作成された要求を送信する場合、情報漏えいでした。|2017 年 3 月更新プログラムのロールアップ
|[3179574](https://support.microsoft.com/kb/3179574)|AD FS エクストラネットのパスワードの更新プログラムで問題を修正しました。 |2016 年 8 月更新プログラムのロールアップ
|[3172614](https://support.microsoft.com/kb/3172614)|プロンプトが導入されたログインを =[サポート](https://technet.microsoft.com/windows-server-docs/identity/ad-fs/overview/ad-fs-faq#BKMK_7)、AlwaysRequireAuthentication 設定と AD FS 管理コンソールで問題を修正しました。 |2016 年 7 月更新プログラムのロールアップ
|[3163306](https://support.microsoft.com/kb/3163306)|Active Directory フェデレーション サービス (AD FS) 3.0 は、Secure Sockets Layer (SSL) ポート 636 または 3269 で接続文字列を使用して構成されているライトウェイト ディレクトリ アクセス プロトコル (LDAP) 属性ストアに接続できません。 |2016 年 6 月の更新プログラムのロールアップ
|[3148533](https://support.microsoft.com/kb/3148533)|Windows Server 2012 R2 で ADFS プロキシを介して MFA のフォールバック認証に失敗しました。 |2016 年 5 月
|[3134787](https://support.microsoft.com/kb/3134787)|AD FS ログにアカウント ロックアウトのシナリオでは、Windows Server 2012 R2 のクライアント IP アドレスが含まれていません。 |2016 年 2 月
|[3134222](https://support.microsoft.com/kb/3134222)|MS16 020:セキュリティの更新は、Active Directory フェデレーション サービスのアドレス型サービス拒否:2016 年 2 月 9 日|2016 年 2 月
|[3105881](https://support.microsoft.com/kb/3105881)|Windows Server 2012 R2 ベースの AD FS サーバーでデバイス認証が有効になっているときにアプリケーションにアクセスできません。|2015 年 10 月
|[3092003](https://support.microsoft.com/kb/3092003)|ページが繰り返し読み込まれ、ユーザーは、Windows Server 2012 R2 AD FS で MFA を使用する際に認証が失敗しました。|2015 年 8 月
|[3080778](https://support.microsoft.com/kb/3080778)|AD FS が呼び出されません OnError MFA アダプターは、Windows Server 2012 R2 で例外をスローします|2015 年 7 月
|[3075610](https://support.microsoft.com/kb/3075610)|追加、または Windows Server 2012 R2 でのクレーム プロバイダーを削除した後、セカンダリの AD FS サーバー上の信頼関係が失われる|2015 年 7 月
|[3070080](https://support.microsoft.com/kb/3070080)|ホーム領域検出の信頼性情報の非対応 Relying Party Trust の正常に動作しません。|2015 年 6 月
|[3052122](https://support.microsoft.com/kb/3052122)|更新プログラムは、Windows Server 2012 R2 で AD FS のトークンで複合 ID のクレームのサポートを追加します|2015 年 5 月
|[3045711](https://support.microsoft.com/kb/3045711)|MS15 040:Active Directory フェデレーション サービスの脆弱性により、情報漏えいが起こる|2015 年 4 月
|[3042127](https://support.microsoft.com/kb/3042127)|"HTTP 400 - Bad Request"Windows Server 2012 R2 の WAP での共有メールボックスを開くとエラー|2015 年 3 月
|[3042121](https://support.microsoft.com/kb/3042121)|Windows Server 2012 R2 での Web アプリケーション プロキシの認証トークンを AD FS トークン リプレイ保護|2015 年 3 月
|[3035025](https://support.microsoft.com/kb/3035025)|パスワードの更新の修正プログラムは機能するため、ユーザーが Windows Server 2012 R2 で登録されたデバイスを使用する必要はありません。|2015 年 1 月
|[3033917](https://support.microsoft.com/kb/3033917)|AD FS は Windows Server 2012 R2 での SAML 応答を処理できません。|2015 年 1 月
|[3025080](https://support.microsoft.com/kb/3025080)|Windows Server 2012 R2 で Web アプリケーション プロキシ経由の Office ファイルを保存しようとすると、操作が失敗しました。|2015 年 1 月
|[3025078](https://support.microsoft.com/kb/3025078)|されたらユーザー名をもう一度、誤ったユーザー名を使用して、Windows Server 2012 R2 へのログオンにする|2015 年 1 月
|[3020813](https://support.microsoft.com/kb/3020813)|Windows Server 2012 R2 AD FS で web アプリケーションを実行するときに認証を求められました。|2015 年 1 月
|[3020773](https://support.microsoft.com/kb/3020773)|Windows Server 2012 R2 でのデバイス登録サービスの初期デプロイ後にタイムアウト エラー|2015 年 1 月
|[3018886](https://support.microsoft.com/kb/3018886)|されたら、ユーザー名とパスワードを 2 回のイントラネットから Windows Server 2012 R2 AD FS サーバーにアクセスするときに|2015 年 1 月
|[3013769](https://support.microsoft.com/kb/3013769)|Windows Server 2012 R2 Update Roll アップ|2014 年 12 月
|[3000850](https://support.microsoft.com/kb/3000850)|Windows Server 2012 R2 Update Roll アップ|2014 年 11 月
|[2975719](https://support.microsoft.com/kb/2975719)|Windows Server 2012 R2 Update Roll アップ|2014 年 8 月
|[2967917](https://support.microsoft.com/kb/2967917)|Windows Server 2012 R2 Update Roll アップ|2014 年 7 月
|[2962409](https://support.microsoft.com/kb/2962409)|Windows Server 2012 R2 Update Roll アップ|2014 年 6 月
|[2955164](https://support.microsoft.com/kb/2955164)|Windows Server 2012 R2 Update Roll アップ|2014 年 5 月
|[2919355](https://support.microsoft.com/kb/2919355)|Windows Server 2012 R2 Update Roll アップ|2014 年 4 月

## <a name="updates-for-ad-fs-in-windows-server-2012-ad-fs-21-and-ad-fs-20"></a>更新プログラムの AD FS では、Windows Server 2012 (AD FS 2.1) と AD FS 2.0
AD FS 2.0 および 2.1 用にリリースされた修正プログラムと更新プログラムのロールアップの一覧を以下に示します。

|KB # |説明|リリース日|適用先:
|----- | ----- |-----|-----
|[3197878](https://support.microsoft.com/kb/3197878)|(これは 3094446 の修正プログラムの一般向けリリース)、Windows Server 2012 でプロキシ経由の認証に失敗しました。|2016 年 11 月品質ロールアップ|AD FS 2.1
|[3197869](https://support.microsoft.com/kb/3197869)|Windows Server 2008 R2 SP1 (これは 3094446 の修正プログラムの一般向けリリース) でプロキシ経由の認証に失敗しました。|2016 年 11 月品質ロールアップ|AD FS 2.0
|[3094446](https://support.microsoft.com/kb/3094446)|Windows Server 2012 または Windows Server 2008 R2 SP1 でプロキシ経由の認証に失敗しました。|2015 年 9 月|AD FS 2.0 および 2.1
|[3070078](https://support.microsoft.com/kb/3070078)|AD FS 2.1 は、Windows Server 2012 での暗号化証明書に対して認証を行うときに例外をスローします|2015 年 7 月|AD FS 2.1
|[3062577](https://support.microsoft.com/kb/3062577)|MS15 062:Active Directory フェデレーション サービスの脆弱性により、特権が昇格されます。|2015 年 6 月|AD FS 2.0 / 2.1
|[3003381](https://support.microsoft.com/kb/3003381)|MS14 077:Active Directory フェデレーション サービスの脆弱性により、情報漏えい。2015 年 4 月 14 日|2014 年 11 月|AD FS 2.0 / 2.1
|[2987843](https://support.microsoft.com/kb/2987843)|多くのユーザーが Windows Server 2012 で web アプリケーションをログオン時に AD FS フェデレーション サーバーのメモリ使用量が増加し続ける|2014 年 7 月|AD FS 2.1
|[2957619](https://support.microsoft.com/kb/2957619)|委任されたトークンの AD fs の要求が行われたときに、AD FS での証明書利用者信頼が停止しました|2014 年 5 月|AD FS 2.1
|[2926658](https://support.microsoft.com/kb/2926658)|SQL アクセス許可があるない場合、ADFS SQL ファームの展開が失敗します。|2014 年 10 月|AD FS 2.1
|[2896713](https://support.microsoft.com/kb/2896713)または[2989956](https://support.microsoft.com/kb/2989956)|AD FS サーバーに 2843638 のセキュリティ更新プログラムをインストールした後、いくつかの問題を修正する更新プログラムがあります。|2013 年 11 月</br></br>2014 年 9 月|AD FS 2.0 / 2.1
|[2877424](https://support.microsoft.com/kb/2877424)|Update 2.1 のファーム、AD FS で複数の利用者の信頼の 1 つの証明書を使用できます。|2013 年 10 月|AD FS 2.1
|[2873168](https://support.microsoft.com/kb/2873168)|修正:エラーは、サード パーティ製の CSP と HSM を使用し、Windows Server 2008 R2 Service Pack 1 での AD FS 2.0 の更新プログラム ロールアップ 3 での要求プロバイダー信頼を構成するときに発生します。|2013 年 9 月|AD FS 2.0
|[2861090](https://support.microsoft.com/kb/2861090)|暗号化証明書のサブジェクト名にコンマ、Windows Server 2008 R2 SP1 で例外が発生します。|2013 年 8 月|AD FS 2.0
|[2843639](https://support.microsoft.com/kb/2843639)|[セキュリティ]Active Directory フェデレーション サービスの脆弱性により、情報漏えいが起こる|2013 年 11 月|AD FS 2.1
|[2843638](https://support.microsoft.com/kb/2843638)|MS13 066:Active Directory フェデレーション サービス 2.0 のセキュリティ更新プログラムの説明です。2013 年 8 月 13 日|2013 年 8 月|AD FS 2.0
|[2827748](https://support.microsoft.com/kb/2827748)|Federationmetadata.xml ファイルでは、Windows Server 2012 で Ws-trust および Ws-federation エンドポイントの MEX エンドポイントの情報は含まれません|2013 年 5 月|AD FS 2.1
|[2790338](https://support.microsoft.com/kb/2790338)|Active Directory フェデレーション サービス (AD FS) の更新プログラムのロールアップ 3 の説明 2.0|2013 年 3 月|AD FS 2.0
