---
title: ライセンス認証エラー コードのトラブルシューティング
description: ライセンス認証エラー コードのトラブルシューティングの方法について説明します
ms.topic: article
ms.date: 03/21/2019
ms.technology: server-general
ms.assetid: ''
author: kaushika-msft
ms.author: kaushika-msft
ms.localizationpriority: medium
ms.openlocfilehash: 076fc3408810ba7b0f51c6a428955f99a66dd394
ms.sourcegitcommit: 3743cf691a984e1d140a04d50924a3a0a19c3e5c
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/17/2019
ms.locfileid: "64880873"
---
# <a name="troubleshooting-activation-error-codes"></a>ライセンス認証エラー コードのトラブルシューティング

**ホーム ユーザー** この記事は、サポート エージェントおよび IT 担当者によって使用されることを目的としています。 Windows ライセンス認証のエラー メッセージについてさらに詳しい情報を探している場合は、次の Microsoft Web サイトにアクセスしてください。

[Windows のライセンス認証エラーに関するヘルプ](https://support.microsoft.com/help/10738/windows-10-get-help-with-activation-errors) 

マルチ ライセンス認証キー (MAK) またはキー管理サービス (KMS) を使用して 1 つ以上の Windows ベースのコンピューターでボリューム ライセンス認証を実行しようとすると、特定のエラー コードを含むエラー メッセージを受け取ります。 この記事では、これらのエラーをトラブルシューティングする方法について説明します。

**エラー コードと説明**

|エラー コード |エラー メッセージ |ライセンス認証の種類 |考えられる原因 |トラブルシューティングの手順 |
|-----------|--------------|----------------|---------------|----------------------|
|    0xC004C001    |    ライセンス認証サーバーで、指定されたプロダクト キーは無効であることが判明しました。    |    MAK    |    無効な MAK が入力されました。    |    キーが Microsoft によって提供された MAK であることを確認してください。 ブロックされているライセンス認証に関する問題については、[マイクロソフト ライセンス認証専用窓口](https://www.microsoft.com/en-us/Licensing/existing-customer/activation-centers)にお問い合わせください。     |
|    0xC004C003     |    ライセンス認証サーバーで、指定されたプロダクト キーがブロックされていることが判明しました。    |    MAK    |    MAK は、ライセンス認証サーバーでブロックされています。    |    [マイクロソフト ライセンス認証専用窓口](https://www.microsoft.com/en-us/Licensing/existing-customer/activation-centers)に問い合わせて、新しい MAK を入手し、システムのインストール/ライセンス認証を行ってください。    |
|    0xC004C008     |    ライセンス認証サーバーで、指定されたプロダクト キーは使用できないことが判明しました。    |    KMS    |    KMS キーがライセンス認証の制限を超えました。    |    KMS ホスト キーは、6 つの異なるコンピューターで最大 10 回までライセンス認証します。 追加ライセンス認証が必要な場合は、[マイクロソフト ライセンス認証専用窓口](https://www.microsoft.com/en-us/Licensing/existing-customer/activation-centers)までお問い合わせください。    |
|    0xC004B100    |    ライセンス認証サーバーで、コンピューターのライセンス認証手続きを完了できなかったことが判明しました。    |    MAK    |    この問題は、MAK がサポートされていない場合に発生することがあります。    |    この問題をトラブルシューティングするには、使用されている MAK が、Microsoft によって提供された MAK であることを確認してください。 MAK が有効かどうかを確認するには、[マイクロソフト ライセンス認証専用窓口](https://www.microsoft.com/en-us/Licensing/existing-customer/activation-centers)にお問い合わせください。    |
|    0xC004C020     |    ライセンス認証サーバーで、マルチ ライセンス認証キーが制限値を超えたことが報告されました。    |    MAK    |    MAK がライセンス認証の制限を超えました。    |    MAK では、その設計によってライセンス認証数が制限されています。   [マイクロソフト ライセンス認証専用窓口](https://www.microsoft.com/en-us/Licensing/existing-customer/activation-centers)にお問い合わせください。    |
|    0xC004C021     |    ライセンス認証サーバーで、マルチ ライセンス認証キーの拡張が制限値を超えたことが報告されました。    |    MAK    |    MAK がライセンス認証の制限を超えました。    |    MAK では、その設計によってライセンス認証数が制限されています。   [マイクロソフト ライセンス認証専用窓口](https://www.microsoft.com/en-us/Licensing/existing-customer/activation-centers)にお問い合わせください。    |
|    0xC004F009     |    The Software Protection Service reported that the grace period expired. (ソフトウェア保護サービスで、猶予期間の期限が切れたことが報告されました。)    |    MAK    |    システムをライセンス認証する前に猶予期間の期限が切れました。 現在、システムは通知状態です。    |    「ユーザー エクスペリエンス」を参照してください。    |
|    0xC004F00F     |    ソフトウェア ライセンス サーバーで、ハードウェア ID バインドが許容範囲のレベルを超えていることが報告されました。    |    MAK/KMS クライアント/KMS ホスト    |    ハードウェアが変更されたか、またはシステムでドライバーが更新されました。    |    MAK:オンラインまたは電話のライセンス認証を使用して、OOT 猶予期間中に再度システムのライセンス認証を行います。      KMS:再起動するか、slmgr.vbs   /ato を実行します。    |
|    0xC004F014     |    The Software Protection Service reported that the product key is not available (ソフトウェア保護サービスで、プロダクト キーは利用可能ではないことが報告されました。)    |    MAK/KMS クライアント    |    プロダクト キーがシステムにインストールされていません。    |    MAK プロダクト キーをインストールするか、またはインストール メディアの \sources\pid.txt にある KMS セットアップ キーをインストールします。    |
|    0xC004F02C     |    The Software Protection Service reported that the format for the offline activation data is incorrect. (ソフトウェア保護サービスで、オフラインのライセンス認証データの形式が正しくないことが報告されました。)    |    MAK/KMS クライアント    |    システムで、電話によるライセンス認証中に入力されたデータが有効ではないことが検出されました。    |    CID が正しく入力されたことを確認します。    |
|    0xC004F035     |    このエラー コードは、"The Software Protection Service reported that the computer could not be activated with a Volume license product key..." (ソフトウェア保護サービスで、ボリューム ライセンス プロダクト キーではコンピューターのライセンス認証の手続きを完了できなかったことが報告されました...) と同じです。このエラー テキストは正しいですが、あいまいです。 このエラーは、Windows の使用条件を満たしているエディションを搭載して出荷されているコンピューターを示すために OEM システムで提供されている Windows マーカーが、このコンピューターの BIOS にないことを示しています。これは、KMS クライアントのライセンス認証の要件です。 エラー: 無効なボリューム ライセンス キー。ライセンス認証をするには、プロダクト キーをマルチ ライセンス認証キー (MAK) または販売キーに変更する必要があります。 You must have a qualifying operating system license AND a Volume license Windows 7 upgrade license, or a full license for Windows 7 from a retail source. (使用条件を満たしているオペレーティング システムのライセンスおよびボリューム ライセンスの Windows 7 アップグレード ライセンスか、または販売元からの Windows 7 完全ライセンスが必要です。) このソフトウェアをこれ以外のどのような状況においてもインストールすることは、契約および該当する著作権に関する法律に違反することになります。    |    KMS クライアント/KMS ホスト    |    Windows 7 ボリューム エディションは、アップグレードのみを対象としてライセンスが供与されています。 使用条件を満たしているオペレーティング システムがインストールされていないコンピューターにボリューム オペレーティング システムをインストールすることはサポートされていません。    |    使用条件を満たしている Microsoft オペレーティング システムのバージョンをインストールしてから、MAK を使ってライセンス認証を行ってください。    |
|    0xC004F038     |    The Software Protection Service reported that the computer could not be activated. (ソフトウェア保護サービスで、コンピューターのライセンス認証ができなかったことが報告されました。) キー管理サービス (KMS) で報告された数が不足しています。 システム管理者に問い合わせてください。    |    KMS クライアント    |    KMS ホストの数が不足しています。 KMS のカウントは、Windows Server の場合は 5 以上、Windows クライアントの場合は 25 以上にする必要があります。    |    KMS クライアントのライセンス認証を行うには、KMS プールにより多くのコンピューターが必要です。 KMS ホストで、Slmgr.vbs /dli を実行して現在のカウントを取得してください。    |
|    0xC004F039     |    The Software Protection Service reported that the computer could not be activated. (ソフトウェア保護サービスで、コンピューターのライセンス認証ができなかったことが報告されました。) キー管理サービス (KMS) が有効になっていません。    |    KMS クライアント    |    このエラーは、KMS 要求に対する応答がない場合に発生します。    |    KMS ホストとクライアント間のネットワーク接続をトラブルシューティングします。 TCP ポート 1688 (既定値) がファイアウォールでブロックされていないこと、またはそれ以外の方法でフィルターされていないことを確認します。    |
|    0xC004F041     |    The Software Protection Service determined that the Key Management Server (KMS) is not activated. (ソフトウェア保護サービスで、キー管理サービス (KMS) がライセンス認証されていないことが判明しました。) KMS をライセンス認証する必要があります。    |    KMS クライアント    |    KMS ホストがライセンス認証されていません。    |    オンライン、電話のいずれかにより KMS ホストをライセンス認証します。    |
|    0xC004F042     |    The Software Protection Service determined that the specified Key Management Service (KMS) cannot be used. (ソフトウェア保護サービスで、指定されたキー管理サービス (KMS) が使用できないことが判明しました。)    |    KMS クライアント    |    KMS クライアントと KMS ホストに不一致があります。    |    このエラーは、クライアント ソフトウェアをライセンス認証できない KMS ホストに KMS クライアントが接続した場合に発生します。 これはたとえば、アプリケーションおよびオペレーティング システムに固有の KMS ホストを含む混在環境でよく見られます。    |
|    0xC004F050     |    The Software Protection Service reported that the product key is invalid. (ソフトウェア保護サービスで、プロダクト キーが無効であることが報告されました。)    |    KMS、KMS クライアント、MAK    |    原因としては、KMS キーの入力ミス、またはオペレーティング システムのリリース版にベータ版のキーを入力したことなどが考えられます。    |    Windows の対応するバージョンに適切な KMS キーをインストールします。 スペルをチェックします。 キーをコピーして貼り付けした場合は、キーで全角ダッシュがダッシュに置き換えられていないかどうかを確認します。    |
|    0xC004F051     |    The Software Protection Service reported that the product key is blocked. (ソフトウェア保護サービスで、プロダクト キーがブロックされていることが報告されました。)    |    MAK/KMS    |    ライセンス認証サーバーのプロダクト キーが Microsoft によってブロックされています。    |    新しい MAK/KMS キーを入手し、システムにインストールして、ライセンス認証します。    |
|    0xC004F064     |    The Software Protection Service reported that the   non-genuine grace period expired. (ソフトウェア保護サービスで、猶予期間の期限 (非正規版) が切れたことが報告されました。)    |    MAK    |    Windows ライセンス認証ツール (WAT) により、システムが正規でないことが判明しました。    |    ボリューム ライセンス認証の操作ガイドを参照してください。    |
|    0xC004F065     |    The Software Protection Service reported that the application is running within the valid non-genuine period. (ソフトウェア保護サービスで、アプリケーションは有効な期間内 (非正規版) で実行されていることが報告されました。)    |    MAK/KMS クライアント    |    Windows ライセンス認証ツールにより、システムは正規でないことが判明しました。 システムは、正規でない猶予期間中も引き続き実行されます。    |    正規のプロダクト キーを入手してインストールし、猶予期間中にシステムのライセンス認証を実行してください。 そうしないと、システムは、猶予期間の終了時に通知状態になります。    |
|    0xC004F06C     |    The Software Protection Service reported that the computer could not be activated. (ソフトウェア保護サービスで、コンピューターをライセンス認証できなかったことが報告されました。) キー管理サービス (KMS) により、要求されたタイムスタンプが無効であることが判明しました。    |    KMS クライアント    |    クライアント コンピューターのシステム時刻と KMS ホストの時刻の差が大きすぎます。    |    時刻の同期は、さまざまな理由でシステムおよびネットワークのセキュリティにとって重要です。 この問題は、KMS と同期するようにクライアントのシステム時刻を変更することにより解決します。 時刻の同期には、ネットワーク タイム プロトコル (NTP) のタイム ソースまたは Active Directory Domain Services を使用することをお勧めします。 この問題では UTP 時刻を使用します。タイム ゾーンの選択には左右されません。    |
|    0x80070005     |    アクセスが拒否されました。 要求された操作には管理者特権が必要です。    |    KMS クライアント/MAK/KMS ホスト    |    ユーザー アカウント制御 (UAC) により、管理者特権でないコマンド プロンプトでライセンス認証処理を実行することは禁止されます。    |    管理者特権のコマンド プロンプトでコマンド slmgr.vbs を実行します。   cmd.exe を右クリックし、[管理者として実行] をクリックします。    |
|    0x8007232A     |    DNS サーバーにエラーが発生しました。    |    KMS ホスト    |    システムにはネットワークまたは DNS の問題があります。    |    ネットワークおよび DNS をトラブルシューティングします。    |
|    0x8007232B     |    DNS 名がありません。    |    KMS クライアント    |    KMS クライアントが DNS で KMS SRV RR を検索できません。 KMS ホストがネットワークに存在しない場合、MAK をインストールする必要があります。    |    KMS ホストがインストールされており、DNS の公開が有効である (既定値) ことを確認します。 DNS が利用不可である場合は、slmgr.vbs /skms <kms_host_name> を使用して KMS クライアントが KMS ホストを指すようにします。オプションで、MAK を取得してインストールしてから、システムのライセンス認証を行います。 最後に、DNS をトラブルシューティングします。    |
|    0x800706BA     |    RPC サーバーが利用できません。    |    KMS クライアント    |    KMS ホストでファイアウォール設定が構成されていないか、または古い DNS SRV レコードです。    |    KMS ホスト コンピューターでキー管理サービスのファイアウォール例外が有効であることを確認します。 SRV レコードで有効な KMS ホストが指定されていることを確認します。 ネットワーク接続をトラブルシューティングします。    |
|    0x8007251D     |    DNS クエリのレコードが見つかりません。    |    KMS クライアント    |    KMS クライアントが DNS で KMS SRV RR を検索できません。    |    ネットワーク接続および DNS のトラブルシューティング    |
|    0xC004F074     |    The Software Protection Service reported that the computer could not be activated. (ソフトウェア保護サービスで、コンピューターのライセンス認証ができなかったことが報告されました。) キー管理サービス (KMS) に接続できませんでした。 詳細については、アプリケーション イベント ログを参照してください。    |    KMS クライアント    |    すべての KMS ホスト システムがエラーを返しました。    |    ライセンス認証の試行に関連する各イベント ID 12288 からのエラーをトラブルシューティングします。    |
|    0x8004FE21     |    このコンピューターは、正規品の Windows を実行していません。    |    MAK/KMS クライアント    |    この問題が発生する原因として、いくつかのことが考えられます。 最も可能性の高い原因として、追加の言語パックのライセンスを供与されていない Windows エディションを実行しているコンピューターに言語パック (MUI) がインストールされていることが考えられます。 (注: これは必ずしも改ざんを示すものではありません。   一部のアプリケーションでは、該当する Windows のエディションでそれらの言語パックがライセンス許諾されていない場合でも、複数言語サポートをインストールできます。)この問題は、追加の機能をインストールできるように Windows がマルウェアによって変更されている場合にも発生することがあります。 また、特定のシステム ファイルが破損している場合にもこの問題が起こることがあります。    |    この問題を解決するには、オペレーティング システムを再インストールする必要があります。    |
|    0x80092328     |    0x80092328 DNS 名がありません。    |    KMS クライアント    |    この問題は、KMS クライアントが DNS で KMS SRV リソース レコードを検出できない場合に発生することがあります。    |    この問題を回避するには、次の Microsoft サポート技術情報の記事の手順に従ってください:929826 Windows Vista Enterprise、Windows Vista Business、Windows 7、または Windows Server 2008 をライセンス認証しようとするとエラー メッセージ "Code 0x8007232b" が表示される    |
|    0x8007007b    |    0x8007007b DNS 名がありません。    |    KMS クライアント    |    この問題は、KMS クライアントが DNS で KMS SRV リソース レコードを検出できない場合に発生することがあります。    |    この問題を回避するには、次の Microsoft サポート技術情報の記事の手順に従ってください:929826 Windows Vista Enterprise、Windows Vista Business、Windows 7、または Windows Server 2008 をライセンス認証しようとするとエラー メッセージ "Code 0x8007232b" が表示される    |
|    0x80070490    |入力したプロダクト キーは使用できませんでした。  プロダクト キーを確認してもう一度やり直してください。 |MAK |この問題は、無効な MAK が入力されたため、または Windows Server 2019 の既知の問題のために発生します。 |この問題を回避するには、コマンド ライン **slmgr -ipk \<5x5 key\>** を使用してコンピューターのライセンス認証を行ってください。|
