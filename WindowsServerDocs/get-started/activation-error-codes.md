---
title: Windows ライセンス認証のエラー コードの解決
description: ライセンス認証エラー コードのトラブルシューティングの方法について説明します
ms.topic: article
ms.date: 9/18/2019
ms.technology: server-general
author: kaushika-msft
ms.author: kaushika-msft; v-tea
ms.localizationpriority: medium
ms.openlocfilehash: 50c50353316db4288f01893125ecd651db63cbb7
ms.sourcegitcommit: 3a3d62f938322849f81ee9ec01186b3e7ab90fe0
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2020
ms.locfileid: "80826355"
---
# <a name="resolve-windows-activation-error-codes"></a>Windows ライセンス認証のエラー コードの解決

> **ホーム ユーザー**  
> この記事は、サポート エージェントおよび IT 担当者によって使用されることを目的としています。 Windows ライセンス認証のエラーメッセージの詳細については、[Windows のライセンス認証エラーに関するヘルプ](https://support.microsoft.com/help/10738/windows-10-get-help-with-activation-errors)を参照してください。  

この記事では、マルチ ライセンス認証キー (MAK) またはキー管理サービス (KMS) を使用して、1 台以上の Windows ベースのコンピューターでボリューム ライセンス認証を実行しようとしたときに発生する可能性があるエラー メッセージに対処するためのトラブルシューティング情報を提供します。 次の表に示すエラー コードを探し、リンクを選択すると、そのエラー コードと解決方法に関する詳細情報が表示されます。

ボリューム ライセンス認証の詳細については、[ボリューム ライセンス認証の計画](https://docs.microsoft.com/windows/deployment/volume-activation/plan-for-volume-activation-client)のページを参照してください。

Windows の現在のバージョンと最新バージョンのボリューム ライセンス認証の詳細については、[ボリュームライセンス認証 [クライアント]](https://docs.microsoft.com/windows/deployment/volume-activation/volume-activation-windows-10) のページを参照してください。

以前のバージョンの Windows でのボリューム ライセンス認証の詳細については、KB 929712 の「 [Windows Vista、Windows Server 2008、Windows Server 2008 R2、および Windows 7 のボリューム アクティベーション情報](https://support.microsoft.com/help/929712/volume-activation-information-for-windows-vista-windows-server-2008-wi)」を参照してください。

## <a name="diagnostic-tool"></a>診断ツール

Microsoft サポート/回復アシスタント (SaRA) を使うと、Windows KMS ライセンス認証のトラブルシューティングが簡単になります。 診断ツールは[こちら](https://aka.ms/SaRA-WindowsActivation)からダウンロードしてください。

このツールでは、Windows のライセンス認証が試行されます。 ライセンス認証のエラー コードが返された場合は、既知のエラー コードに対応する解決策がツールに表示されます。

次のエラー コードがサポートされています。0xC004F038、0xC004F039、0xC004F041、0xC004F074、0xC004C008。

## <a name="summary-of-error-codes"></a>エラー コードの概要

|エラー コード |エラー メッセージ |ライセンス認証の種類&nbsp;|
|-----------|--------------|----------------|
|[0x8004FE21](#0x8004fe21-this-computer-is-not-running-genuine-windows) |このコンピューターは、正規品の Windows を実行していません。  |MAK<br />KMS クライアント |
|[0x80070005](#0x80070005-access-denied) |アクセスが拒否されました。 要求された操作には管理者特権が必要です。 |MAK<br />KMS クライアント<br />KMS ホスト |
|[0x8007007b](#0x8007007b-dns-name-does-not-exist) |0x8007007b DNS 名がありません。 |KMS クライアント |
|[0x80070490](#0x80070490-the-product-key-you-entered-didnt-work) |入力したプロダクト キーは使用できませんでした。 プロダクト キーを確認してもう一度やり直してください。 |MAK |
|[0x800706BA](#0x800706ba-the-rpc-server-is-unavailable) |RPC サーバーが利用できません。 |KMS クライアント |
|[0x8007232A](#0x8007232a-dns-server-failure) |DNS サーバーにエラーが発生しました。  |KMS ホスト  |
|[0x8007232B](#0x8007232b-dns-name-does-not-exist) |DNS 名がありません。 |KMS クライアント |
|[0x8007251D](#0x8007251d-no-records-found-for-dns-query) |DNS クエリのレコードが見つかりません。 |KMS クライアント |
|[0x80092328](#0x80092328-dns-name-does-not-exist) |DNS 名がありません。  |KMS クライアント |
|[0xC004B100](#0xc004b100-the-activation-server-determined-that-the-computer-could-not-be-activated) |ライセンス認証サーバーで、コンピューターのライセンス認証手続きを完了できなかったことが判明しました。 |MAK |
|[0xC004C001](#0xc004c001-the-activation-server-determined-the-specified-product-key-is-invalid) |ライセンス認証サーバーで、指定されたプロダクト キーは無効であることが判明しました。 |MAK|
|[0xC004C003](#0xc004c003-the-activation-server-determined-the-specified-product-key-is-blocked) |ライセンス認証サーバーで、指定されたプロダクト キーがブロックされていることが判明しました。 |MAK |
|[0xC004C008](#0xc004c008-the-activation-server-determined-that-the-specified-product-key-could-not-be-used) |ライセンス認証サーバーで、指定されたプロダクト キーは使用できないことが判明しました。 |KMS |
|[0xC004C020](#0xc004c020-the-activation-server-reported-that-the-multiple-activation-key-has-exceeded-its-limit) |ライセンス認証サーバーで、マルチ ライセンス認証キーが制限値を超えたことが報告されました。 |MAK |
|[0xC004C021](#0xc004c021-the-activation-server-reported-that-the-multiple-activation-key-extension-limit-has-been-exceeded) |ライセンス認証サーバーで、マルチ ライセンス認証キーの拡張が制限値を超えたことが報告されました。 |MAK |
|[0xC004F009](#0xc004f009-the-software-protection-service-reported-that-the-grace-period-expired) |ソフトウェア保護サービスで、猶予期間の期限が切れたことが報告されました。 |MAK |
|[0xC004F00F](#0xc004f00f-the-software-licensing-server-reported-that-the-hardware-id-binding-is-beyond-level-of-tolerance) |ソフトウェア ライセンス サーバーで、ハードウェア ID バインドが許容範囲のレベルを超えていることが報告されました。 |MAK<br />KMS クライアント<br />KMS ホスト |
|[0xC004F014](#0xc004f014-the-software-protection-service-reported-that-the-product-key-is-not-available) |ソフトウェア保護サービスで、プロダクト キーが使用できないことが報告されました。 |MAK<br />KMS クライアント |
|[0xC004F02C](#0xc004f02c-the-software-protection-service-reported-that-the-format-for-the-offline-activation-data-is-incorrect) |ソフトウェア保護サービスで、オフラインのライセンス認証データの形式が正しくないことが報告されました。 |MAK<br />KMS クライアント |
|[0xC004F035](#0xc004f035-invalid-volume-license-key) |ソフトウェア保護サービスで、ボリューム ライセンス プロダクト キーではコンピューターのライセンス認証の手続きを完了できなかったことが報告されました。 |KMS クライアント<br />KMS ホスト |
|[0xC004F038](#0xc004f038-the-count-reported-by-your-key-management-service-kms-is-insufficient) |ソフトウェア保護サービスで、コンピューターをライセンス認証できなかったことが報告されました。 キー管理サービス (KMS) で報告された数が不足しています。 システム管理者に問い合わせてください。 |KMS クライアント |
|[0xC004F039](#0xc004f039-the-key-management-service-kms-is-not-enabled) |ソフトウェア保護サービスで、コンピューターをライセンス認証できなかったことが報告されました。 キー管理サービス (KMS) が有効になっていません。 |KMS クライアント |
|[0xC004F041](#0xc004f041-the-software-protection-service-determined-that-the-key-management-server-kms-is-not-activated) |The Software Protection Service determined that the Key Management Server (KMS) is not activated. (ソフトウェア保護サービスで、キー管理サービス (KMS) がライセンス認証されていないことが判明しました。) KMS をライセンス認証する必要があります。  |KMS クライアント |
|[0xC004F042](#0xc004f042-the-software-protection-service-determined-that-the-specified-key-management-service-kms-cannot-be-used) |ソフトウェア保護サービスで、指定されたキー管理サービス (KMS) が使用できないことが報告されました。 |KMS クライアント |
|[0xC004F050](#0xc004f050-the-software-protection-service-reported-that-the-product-key-is-invalid) |ソフトウェア保護サービスで、プロダクト キーが無効であることが報告されました。 |MAK<br />KMS<br />KMS クライアント |
|[0xC004F051](#0xc004f051-the-software-protection-service-reported-that-the-product-key-is-blocked) |ソフトウェア保護サービスで、プロダクト キーがブロックされたことが報告されました。 |MAK<br />KMS |
|[0xC004F064](#0xc004f064-the-software-protection-service-reported-that-the-non-genuine-grace-period-expired) |The Software Protection Service reported that the non-genuine grace period expired. (ソフトウェア保護サービスで、猶予期間の期限 (非正規版) が切れたことが報告されました。) |MAK |
|[0xC004F065](#0xc004f065-the-software-protection-service-reported-that-the-application-is-running-within-the-valid-non-genuine-period) |The Software Protection Service reported that the application is running within the valid non-genuine period. (ソフトウェア保護サービスで、アプリケーションは有効な期間内 (非正規版) で実行されていることが報告されました。) |MAK<br />KMS クライアント |
|[0xC004F06C](#0xc004f06c-the-request-timestamp-is-invalid) |ソフトウェア保護サービスで、コンピューターをライセンス認証できなかったことが報告されました。 キー管理サービス (KMS) で、要求されたタイムスタンプが無効であることが判明しました。  |KMS クライアント |
|[0xC004F074](#0xc004f074-no-key-management-service-kms-could-be-contacted) |ソフトウェア保護サービスで、コンピューターをライセンス認証できなかったことが報告されました。 キー管理サービス (KMS) に接続できませんでした。 詳細については、アプリケーション イベント ログを参照してください。  |KMS クライアント |

## <a name="causes-and-resolutions"></a>原因と解決策

### <a name="0x8004fe21-this-computer-is-not-running-genuine-windows"></a>0x8004FE21 このコンピューターは、正規品の Windows を実行していません  

#### <a name="possible-cause"></a>考えられる原因

この問題が発生する原因として、いくつかのことが考えられます。 最も可能性の高い原因として、追加の言語パックのライセンスを供与されていない Windows エディションを実行しているコンピューターに言語パック (MUI) がインストールされていることが考えられます。  

> [!NOTE]
> この問題は、必ずしも改ざんを示すものではありません。 一部のアプリケーションでは、そのエディションの Windows にそうした言語パックがライセンス認証されていない場合であっても、多言語サポートをインストールできます。  

この問題は、追加の機能をインストールできるように Windows がマルウェアによって変更されている場合にも発生することがあります。 また、特定のシステム ファイルが破損している場合にもこの問題が起こることがあります。  

#### <a name="resolution"></a>解決方法

この問題を解決するには、オペレーティング システムを再インストールする必要があります。  

### <a name="0x80070005-access-denied"></a>0x80070005 アクセス拒否

このエラー メッセージの全文は次のような内容です。

> アクセスが拒否されました。 要求された操作には管理者特権が必要です。

#### <a name="possible-cause"></a>考えられる原因

ユーザー アカウント制御 (UAC) により、管理者特権でないコマンド プロンプト ウィンドウでライセンス認証処理を実行することは禁止されます。  

#### <a name="resolution"></a>解決方法

管理者特権でのコマンド プロンプトでコマンド **slmgr.vbs** を実行します。 これを行うには、 **[スタート] メニュー**で **cmd.exe** を右クリックし、 **[管理者として実行]** を選択します。  

### <a name="0x8007007b-dns-name-does-not-exist"></a>0x8007007b DNS 名が存在しません

#### <a name="possible-cause"></a>考えられる原因

この問題は、KMS クライアントが DNS で KMS SRV リソース レコードを検出できない場合に発生することがあります。  

#### <a name="resolution"></a>解決方法

このような DNS に関連する問題のトラブルシューティングについては、「[KMS と DNS の問題に関する一般的なトラブルシューティング手順](common-troubleshooting-procedures-kms-dns.md)」を参照してください。  

### <a name="0x80070490-the-product-key-you-entered-didnt-work"></a>0x80070490 入力したプロダクト キーは使用できませんでした

このエラーの全文は次のような内容です。
> 入力したプロダクト キーは使用できませんでした。 プロダクト キーを確認してもう一度やり直してください。  

#### <a name="possible-cause"></a>考えられる原因

この問題は、入力された MAK が無効であるか、Windows Server 2019 の既知の問題が原因で発生します。  

#### <a name="resolution"></a>解決方法

この問題を回避してコンピューターをライセンス認証するには、管理者特権でのコマンド プロンプトで、**slmgr -ipk <5x5 key>** を実行します。

### <a name="0x800706ba-the-rpc-server-is-unavailable"></a>0x800706BA RPC サーバーを利用できません

#### <a name="possible-cause"></a>考えられる原因

KMS ホストでファイアウォール設定が構成されていないか、または古い DNS SRV レコードです。  

#### <a name="resolution"></a>解決方法

KMS ホストで、キー管理サービス (TCP ポート 1688) に対してファイアウォールの例外が有効になっていることを確認します。

DNS SRV レコードが有効な KMS ホストを指していることを確認します。 

ネットワーク接続をトラブルシューティングします。  

このような DNS に関連する問題のトラブルシューティングについては、「[KMS と DNS の問題に関する一般的なトラブルシューティング手順](common-troubleshooting-procedures-kms-dns.md)」を参照してください。  

### <a name="0x8007232a-dns-server-failure"></a>0x8007232A DNS サーバー エラー

#### <a name="possible-cause"></a>考えられる原因

システムにはネットワークまたは DNS の問題があります。

#### <a name="resolution"></a>解決方法

ネットワークおよび DNS をトラブルシューティングします。  

### <a name="0x8007232b-dns-name-does-not-exist"></a>0x8007232B DNS 名が存在しません

#### <a name="possible-cause"></a>考えられる原因

KMS クライアントで、DNS の KMS サーバー リソース レコード (SRV RR) を見つけることができません。  

#### <a name="resolution"></a>解決方法

KMS ホストがインストールされており、DNS の公開が有効である (既定値) ことを確認します。 DNS が利用不可である場合は、**slmgr.vbs /skms <*kms_host_name*>** を使用して KMS クライアントに KMS ホストを指示します。  

KMS ホストがない場合は、MAK を入手してインストールします。 次に、システムをライセンス認証します。

このような DNS に関連する問題のトラブルシューティングについては、「[KMS と DNS の問題に関する一般的なトラブルシューティング手順](common-troubleshooting-procedures-kms-dns.md)」を参照してください。  

### <a name="0x8007251d-no-records-found-for-dns-query"></a>0x8007251D DNS クエリのレコードが見つかりません

#### <a name="possible-cause"></a>考えられる原因

KMS クライアントで、DNS の KMS SRV レコードを見つけることができません。

#### <a name="resolution"></a>解決方法

ネットワーク接続および DNS のトラブルシューティング このような DNS に関連する問題のトラブルシューティング方法については、「[KMS と DNS の問題に関する一般的なトラブルシューティング手順](common-troubleshooting-procedures-kms-dns.md)」を参照してください。  

### <a name="0x80092328-dns-name-does-not-exist"></a>0x80092328 DNS 名が存在しません

#### <a name="possible-cause"></a>考えられる原因

この問題は、KMS クライアントが DNS で KMS SRV リソース レコードを検出できない場合に発生することがあります。

#### <a name="resolution"></a>解決方法

このような DNS に関連する問題のトラブルシューティングについては、「[KMS と DNS の問題に関する一般的なトラブルシューティング手順](common-troubleshooting-procedures-kms-dns.md)」を参照してください。  

### <a name="0xc004b100-the-activation-server-determined-that-the-computer-could-not-be-activated"></a>0xC004B100 ライセンス認証サーバーで、コンピューターのライセンス認証手続きを完了できなかったことが判明しました。

#### <a name="possible-cause"></a>考えられる原因

MAK はサポートされていません。  

#### <a name="resolution"></a>解決方法

この問題を解決するには、使用している MAK が、Microsoft によって提供された MAK であることを確認してください。 MAK が有効かどうかを確認するには、[マイクロソフト ライセンス認証専用窓口](https://www.microsoft.com/Licensing/existing-customer/activation-centers)にお問い合わせください。

### <a name="0xc004c001-the-activation-server-determined-the-specified-product-key-is-invalid"></a>0xC004C001 ライセンス認証サーバーで、指定されたプロダクト キーは無効であることが判明しました。

#### <a name="possible-cause"></a>考えられる原因

入力した MAK が無効です。

#### <a name="resolution"></a>解決方法

キーが Microsoft によって提供された MAK であることを確認してください。 さらにサポートが必要な場合は、[マイクロソフト ライセンス認証専用窓口](https://www.microsoft.com/Licensing/existing-customer/activation-centers)にお問い合わせください。

### <a name="0xc004c003-the-activation-server-determined-the-specified-product-key-is-blocked"></a>0xC004C003 ライセンス認証サーバーで、指定されたプロダクト キーがブロックされていることが判明しました。

#### <a name="possible-cause"></a>考えられる原因

MAK は、ライセンス認証サーバーでブロックされています。

#### <a name="resolution"></a>解決方法

新しい MAK を入手するには、[マイクロソフト ライセンス認証専用窓口](https://www.microsoft.com/Licensing/existing-customer/activation-centers)にお問い合わせください。 新しい MAK を入手したら、もう一度 Windows をインストールし、ライセンス認証してください。  

### <a name="0xc004c008-the-activation-server-determined-that-the-specified-product-key-could-not-be-used"></a>0xC004C008 ライセンス認証サーバーで、指定されたプロダクト キーは使用できないことが判明しました

#### <a name="possible-cause"></a>考えられる原因

KMS キーがライセンス認証の制限を超えました。 1 つの KMS ホスト キーは、最大 6 台の異なるコンピューターで最大 10 回ライセンス認証できます。  

#### <a name="resolution"></a>解決方法

追加のライセンス認証が必要な場合は、[マイクロソフト ライセンス認証専用窓口](https://www.microsoft.com/Licensing/existing-customer/activation-centers)にお問い合わせください。  

### <a name="0xc004c020-the-activation-server-reported-that-the-multiple-activation-key-has-exceeded-its-limit"></a>0xC004C020 ライセンス認証サーバーで、マルチ ライセンス認証キーが制限値を超えたことが報告されました。

#### <a name="possible-cause"></a>考えられる原因

MAK がライセンス認証の制限を超えました。 設計上、MAK のライセンス認証回数には上限があります。

#### <a name="resolution"></a>解決方法

追加のライセンス認証が必要な場合は、[マイクロソフト ライセンス認証専用窓口](https://www.microsoft.com/Licensing/existing-customer/activation-centers)にお問い合わせください。

### <a name="0xc004c021-the-activation-server-reported-that-the-multiple-activation-key-extension-limit-has-been-exceeded"></a>0xC004C021 ライセンス認証サーバーで、マルチ ライセンス認証キーの拡張が制限値を超えたことが報告されました。

#### <a name="possible-cause"></a>考えられる原因

MAK がライセンス認証の制限を超えました。 設計上、MAK のライセンス認証回数には上限があります。

#### <a name="resolution"></a>解決方法

追加のライセンス認証が必要な場合は、[マイクロソフト ライセンス認証専用窓口](https://www.microsoft.com/Licensing/existing-customer/activation-centers)にお問い合わせください。

### <a name="0xc004f009-the-software-protection-service-reported-that-the-grace-period-expired"></a>0xC004F009 ソフトウェア保護サービスで、猶予期間の期限が切れたことが報告されました。

#### <a name="possible-cause"></a>考えられる原因

システムをライセンス認証する前に猶予期間の期限が切れました。 現在、システムは通知状態です。  

#### <a name="resolution"></a>解決方法

サポートが必要な場合は、[マイクロソフト ライセンス認証専用窓口](https://www.microsoft.com/Licensing/existing-customer/activation-centers)にお問い合わせください。

### <a name="0xc004f00f-the-software-licensing-server-reported-that-the-hardware-id-binding-is-beyond-level-of-tolerance"></a>0xC004F00F ソフトウェア ライセンス サーバーで、ハードウェア ID バインドが許容範囲のレベルを超えていることが報告されました。

#### <a name="possible-cause"></a>考えられる原因

ハードウェアが変更されたか、またはシステムでドライバーが更新されました。  

#### <a name="resolution"></a>解決方法

MAK ライセンス認証を使用している場合は、OOT の猶予期間中にオンラインまたは電話によるライセンス認証を使用してシステムのライセンス認証を再実行します。  

KMS ライセンス認証を使用している場合は、Windows を再起動するか、**slmgr.vbs /ato** を実行します。

### <a name="0xc004f014-the-software-protection-service-reported-that-the-product-key-is-not-available"></a>0xC004F014 ソフトウェア保護サービスで、プロダクト キーが使用できないことが報告されました。

#### <a name="possible-cause"></a>考えられる原因

プロダクト キーがシステムにインストールされていません。  

#### <a name="resolution"></a>解決方法

MAK ライセンス認証を使用している場合は、MAK プロダクト キーをインストールします。 

KMS ライセンス認証を使用している場合は、Pid.txt ファイル (インストール メディアの \sources フォルダーにあります) で KMS セットアップ キーを確認します。 キーをインストールします。

### <a name="0xc004f02c-the-software-protection-service-reported-that-the-format-for-the-offline-activation-data-is-incorrect"></a>0xC004F02C ソフトウェア保護サービスで、オフラインのライセンス認証データの形式が正しくないことが報告されました。

#### <a name="possible-cause"></a>考えられる原因

システムで、電話によるライセンス認証の間に入力されたデータが有効ではないことが検出されました。  

#### <a name="resolution"></a>解決方法

CID が正しく入力されたことを確認します。  

### <a name="0xc004f035-invalid-volume-license-key"></a>0xC004F035 無効なボリューム ライセンス キー

このエラー メッセージの全文は次のような内容です。

> エラー: 無効なボリューム ライセンス キー。 ライセンス認証をするには、プロダクト キーをマルチ ライセンス認証キー (MAK) または販売キーに変更する必要があります。 You must have a qualifying operating system license AND a Volume license Windows 7 upgrade license, or a full license for Windows 7 from a retail source. (使用条件を満たしているオペレーティング システムのライセンスおよびボリューム ライセンスの Windows 7 アップグレード ライセンスか、または販売元からの Windows 7 完全ライセンスが必要です。) このソフトウェアをこれ以外のどのような状況においてもインストールすることは、契約および該当する著作権に関する法律に違反することになります。  

このエラー テキストは正しいですが、あいまいです。 このエラーは、Windows の正規のエディションを実行している OEM システムとして認識する Windows マーカーが、コンピューターの BIOS にないことを示しています。 この情報は、KMS クライアントのライセンス認証に必要です。 このコードの具体的な意味: "エラー: 無効なボリューム ライセンス キー"

#### <a name="possible-cause"></a>考えられる原因

Windows 7 ボリューム エディションは、アップグレードのみを対象としてライセンスが供与されています。 Microsoft は、使用条件を満たしているオペレーティング システムがインストールされていないコンピューターにボリューム オペレーティング システムをインストールすることをサポートしていません。  

#### <a name="resolution"></a>解決方法

ライセンス認証をするには、次のいずれかを行う必要があります。

- プロダクト キーをマルチ ライセンス認証キー (MAK) または販売キーに変更します。 You must have a qualifying operating system license AND a Volume license Windows 7 upgrade license, or a full license for Windows 7 from a retail source. (使用条件を満たしているオペレーティング システムのライセンスおよびボリューム ライセンスの Windows 7 アップグレード ライセンスか、または販売元からの Windows 7 完全ライセンスが必要です。)
  > [!NOTE]
  > ライセンス認証をしようとしたときにエラー 0x80072ee2 が発生した場合は、代わりに以下の電話によるライセンス認証方法を使用します。
- 次の手順に従って、電話でライセンス認証を行います。
   1. **slmgr /dti** を実行し、インストール ID の値を記録します。 </li>
   1. 確認 ID を受け取るために、[マイクロソフト ライセンス認証専用窓口](https://www.microsoft.com/Licensing/existing-customer/activation-centers)にお問い合わせいただき、インストール ID をお伝えください。</li>
   1. 確認 ID を使用してライセンス認証をするには、**slmgr /atp &lt;確認 ID&gt;** を実行します。

### <a name="0xc004f038-the-count-reported-by-your-key-management-service-kms-is-insufficient"></a>0xC004F038 キー管理サービス (KMS) で報告された数が不足しています。

このエラー メッセージの全文は次のような内容です。

> ソフトウェア保護サービスで、コンピューターをライセンス認証できなかったことが報告されました。 キー管理サービス (KMS) で報告された数が不足しています。 システム管理者に問い合わせてください。  

#### <a name="possible-cause"></a>考えられる原因

KMS ホストの数が不足しています。 Windows Server の場合、KMS の数は 5 以上である必要があります。 Windows (クライアント) の場合、KMS の数は 25 以上である必要があります。  

#### <a name="resolution"></a>解決方法
KMS を使用して Windows をライセンス認証する前に、KMS プールにコンピューターを追加する必要があります。 KMS ホストの現在の数を確認するには、**Slmgr.vbs /dli** を実行します。  

### <a name="0xc004f039-the-key-management-service-kms-is-not-enabled"></a>0xC004F039 キー管理サービス (KMS) が有効になっていません。

このエラー メッセージの全文は次のような内容です。

> ソフトウェア保護サービスで、コンピューターをライセンス認証できなかったことが報告されました。 キー管理サービス (KMS) が有効になっていません。  

#### <a name="possible-cause"></a>考えられる原因

KMS が KMS 要求に応答しませんでした。

#### <a name="resolution"></a>解決方法

KMS ホストとクライアント間のネットワーク接続をトラブルシューティングします。 TCP ポート 1688 (既定値) がファイアウォールでブロックされていないこと、またはそれ以外の方法でフィルターされていないことを確認します。

### <a name="0xc004f041-the-software-protection-service-determined-that-the-key-management-server-kms-is-not-activated"></a>0xC004F041 The Software Protection Service determined that the Key Management Server (KMS) is not activated (ソフトウェア保護サービスで、キー管理サービス (KMS) がライセンス認証されていないことが判明しました)

このエラー メッセージの全文は次のような内容です。

> The Software Protection Service determined that the Key Management Server (KMS) is not activated. (ソフトウェア保護サービスで、キー管理サービス (KMS) がライセンス認証されていないことが判明しました。) KMS をライセンス認証する必要があります。  

#### <a name="possible-cause"></a>考えられる原因

KMS ホストがライセンス認証されていません。  

#### <a name="resolution"></a>解決方法

オンラインまたは電話によるライセンス認証を使用して、KMS ホストをライセンス認証します。  

### <a name="0xc004f042-the-software-protection-service-determined-that-the-specified-key-management-service-kms-cannot-be-used"></a>0xC004F042 ソフトウェア保護サービスで、指定されたキー管理サービス (KMS) が使用できないことが報告されました

#### <a name="possible-cause"></a>考えられる原因

このエラーは、クライアントソフトウェアをライセンス認証できない KMS ホストに KMS クライアントが接続した場合に発生します。 これはたとえば、アプリケーション固有およびオペレーティング システム固有の KMS ホストを含む混在環境でよく見られます。  

#### <a name="resolution"></a>解決方法

特定の KMS ホストを使用して特定のアプリケーションまたはオペレーティング システムをライセンス認証した場合、KMS クライアントから正しいホストに接続することを確認します。

### <a name="0xc004f050-the-software-protection-service-reported-that-the-product-key-is-invalid"></a>0xC004F050 ソフトウェア保護サービスで、プロダクト キーが無効であることが報告されました

#### <a name="possible-cause"></a>考えられる原因

原因としては、KMS キーの入力ミス、またはオペレーティング システムのリリース版にベータ版のキーを入力したことなどが考えられます。  

#### <a name="resolution"></a>解決方法

Windows の対応する版に適切な KMS キーをインストールします。 スペルをチェックします。 キーをコピーして貼り付ける場合は、キーの全角ダッシュがダッシュに置き換えられていないことを確認します。  

### <a name="0xc004f051-the-software-protection-service-reported-that-the-product-key-is-blocked"></a>0xC004F051 ソフトウェア保護サービスで、プロダクト キーがブロックされたことが報告されました

#### <a name="possible-cause"></a>考えられる原因

ライセンス認証サーバーで、Microsoft がこのプロダクト キーをブロックしたことが判明しました。  

#### <a name="resolution"></a>解決方法

新しい MAK または KMS キーを入手し、システムにインストールして、ライセンス認証します。

### <a name="0xc004f064-the-software-protection-service-reported-that-the-non-genuine-grace-period-expired"></a>0xC004F064 The Software Protection Service reported that the non-genuine grace period expired (ソフトウェア保護サービスで、猶予期間の期限 (非正規版) が切れたことが報告されました)

#### <a name="possible-cause"></a>考えられる原因

Windows ライセンス認証ツール (WAT) で、システムが正規ではないことが判明しました。  

#### <a name="resolution"></a>解決方法

サポートが必要な場合は、[マイクロソフト ライセンス認証専用窓口](https://www.microsoft.com/Licensing/existing-customer/activation-centers)にお問い合わせください。

### <a name="0xc004f065-the-software-protection-service-reported-that-the-application-is-running-within-the-valid-non-genuine-period"></a>0xC004F065 The Software Protection Service reported that the application is running within the valid non-genuine period (ソフトウェア保護サービスで、アプリケーションは有効な期間内 (非正規版) で実行されていることが報告されました)

#### <a name="possible-cause"></a>考えられる原因

Windows ライセンス認証ツールで、システムが正規ではないことが判明しました。 システムは、正規でない猶予期間中も引き続き実行されます。  

#### <a name="resolution"></a>解決方法

正規のプロダクト キーを入手してインストールし、猶予期間中にシステムのライセンス認証を実行してください。 そうしないと、システムは、猶予期間の終了時に通知状態になります。

### <a name="0xc004f06c-the-request-timestamp-is-invalid"></a>0xC004F06C The request timestamp is invalid (要求のタイムスタンプが無効です)

このエラー メッセージの全文は次のような内容です。

> ソフトウェア保護サービスで、コンピューターをライセンス認証できなかったことが報告されました。 キー管理サービス (KMS) で、要求されたタイムスタンプが無効であることが判明しました。  

#### <a name="possible-cause"></a>考えられる原因

クライアント コンピューターのシステム時刻と KMS ホストの時刻の差が大きすぎます。 時刻の同期は、さまざまな理由でシステムおよびネットワークのセキュリティにとって重要です。  

#### <a name="resolution"></a>解決方法

この問題は、KMS ホストと同期するようにクライアントのシステム時刻を変更することにより解決します。 時刻の同期には、ネットワーク タイム プロトコル (NTP) のタイム ソースまたは Active Directory Domain Services を使用することをお勧めします。 この問題には UTP 時間が使用されており、タイム ゾーンの選択には依存していません。  

### <a name="0xc004f074-no-key-management-service-kms-could-be-contacted"></a>0xC004F074 キー管理サービス (KMS) に接続できませんでした

このエラー メッセージの全文は次のような内容です。

> ソフトウェア保護サービスで、コンピューターをライセンス認証できなかったことが報告されました。 キー管理サービス (KMS) に接続できませんでした。 詳細については、アプリケーション イベント ログを参照してください。  

#### <a name="possible-cause"></a>考えられる原因

すべての KMS ホスト システムからエラーが返されました。  

#### <a name="resolution"></a>解決方法

アプリケーション イベント ログで、イベント ID が 12288 で、ライセンス認証の試行に関連付けられている各イベントを特定します。 これらのイベントのエラーを解決します。

DNS に関連する問題のトラブルシューティングについては、「[KMS と DNS の問題に関する一般的なトラブルシューティング手順](common-troubleshooting-procedures-kms-dns.md)」を参照してください。  
