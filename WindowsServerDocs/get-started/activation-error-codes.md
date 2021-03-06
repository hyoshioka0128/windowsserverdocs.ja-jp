---
title: ライセンス認証エラー コードのトラブルシューティング
description: ライセンス認証エラー コードのトラブルシューティングを行う方法について説明します
ms.topic: article
ms.date: 03/21/2019
ms.technology: server-general
ms.assetid: ''
author: kaushika-msft
ms.author: kaushika-msft
ms.localizationpriority: medium
ms.openlocfilehash: 076fc3408810ba7b0f51c6a428955f99a66dd394
ms.sourcegitcommit: 7478dd3959d893bd42620e30e3b56f35407f1dec
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/29/2019
ms.locfileid: "64880873"
---
# <a name="troubleshooting-activation-error-codes"></a>ライセンス認証エラー コードのトラブルシューティング

**ホーム ユーザー**この記事では、サポート担当者および IT プロフェッショナルで使用するためです。 Windows ライセンス認証のエラー メッセージに関する詳細については、探している場合は、次の Microsoft web サイトに移動します。

[Windows ライセンス認証エラーに関するヘルプします。](https://support.microsoft.com/help/10738/windows-10-get-help-with-activation-errors) 

マルチ ライセンス認証キー (MAK) またはキー管理サービス (KMS) を使用して、1 つまたは複数の Windows ベースのコンピューター上でボリューム ライセンス認証を実行するときは、特定のエラー コードが含まれているエラー メッセージが表示されます。 この記事では、これらのエラーをトラブルシューティングする方法について説明します。

**エラー コードと説明**

|エラー コード |エラー メッセージ |ライセンス認証の種類 |考えられる原因 |トラブルシューティングの手順 |
|-----------|--------------|----------------|---------------|----------------------|
|    0xC004C001    |    ライセンス認証サーバーの決定、指定されたプロダクト キーが無効です。    |    MAK    |    無効な MAK が入力されました。    |    キーが Microsoft によって提供された MAK であることを確認します。 ブロックされている、アクティブ化に関する問題は、連絡先をご覧ください、 [Microsoft ライセンスのライセンス認証センター。](https://www.microsoft.com/en-us/Licensing/existing-customer/activation-centers)     |
|    0xC004C003     |    指定されたプロダクト キーがブロックされているライセンス認証サーバーの決定    |    MAK    |    MAK は、ライセンス認証サーバーでブロックされています。    |    連絡先は。[Microsoft ライセンスのライセンス認証センター](https://www.microsoft.com/en-us/Licensing/existing-customer/activation-centers)新しい MAK を入手して、システムのインストール/ライセンス認証します。    |
|    0xC004C008     |    ライセンス認証サーバーには、指定されたプロダクト キーが使用しないことが決定されます。    |    KMS    |    KMS キーがライセンス認証の制限を超えました。    |    KMS ホスト キーがアクティブ化最大 10 回 6 つの異なるコンピューター上。 複数のアクティブ化が必要な場合にお問い合わせください。、 [Microsoft ライセンスのライセンス認証センター](https://www.microsoft.com/en-us/Licensing/existing-customer/activation-centers)します。    |
|    0xC004B100    |    ライセンス認証サーバーには、コンピューターがアクティブにしないことが決定されます。    |    MAK    |    この問題は、MAK は、サポートされていない場合に発生する可能性があります。    |    この問題をトラブルシューティングするために使用される MAK が Microsoft によって提供された MAK であることを確認します。 MAK が有効であることを確認するには、次にお問い合わせください。 します。[Microsoft ライセンスのライセンス認証センター](https://www.microsoft.com/en-us/Licensing/existing-customer/activation-centers)します。    |
|    0xC004C020     |    ライセンス認証サーバーでは、複数のライセンス認証キーが限界を超えていることを報告します。    |    MAK    |    MAK がライセンス認証の制限を超えました。    |    MAK では、その設計によってライセンス認証数が制限されています。   連絡先、 [Microsoft ライセンスのライセンス認証センター](https://www.microsoft.com/en-us/Licensing/existing-customer/activation-centers)します。    |
|    0xC004C021     |    ライセンス認証サーバーでは、マルチ ライセンス認証キーの拡張機能の制限を超えたことを報告します。    |    MAK    |    MAK がライセンス認証の制限を超えました。    |    MAK では、その設計によってライセンス認証数が制限されています。   連絡先、 [Microsoft ライセンスのライセンス認証センター](https://www.microsoft.com/en-us/Licensing/existing-customer/activation-centers)    |
|    0xC004F009     |    ソフトウェア保護サービスでは、猶予期間が期限切れを報告します。    |    MAK    |    猶予期間には、システムがアクティブ化する前に有効期限が切れました。 現在、システムは通知状態です。    |    「ユーザー エクスペリエンス」を参照してください。    |
|    0xC004F00F     |    ソフトウェアのライセンス サーバーは、トレランスのレベルを超えて、ハードウェア ID バインドを報告します。    |    MAK/KMS クライアント/KMS ホスト    |    ハードウェアが変更されたか、ドライバーがシステムに更新されました。    |    MAK:オンラインを使用して行う猶予期間中に、システムを再アクティブ化または電話のアクティブ化します。      KMS:再起動、または slmgr.vbs/ato を実行します。    |
|    0xC004F014     |    ソフトウェア保護サービスは、プロダクト キーが使用できないことを報告    |    MAK/KMS クライアント    |    プロダクト キーがシステムにインストールされていません。    |    MAK プロダクト キーでは、インストールまたは \sources\pid.txt インストール メディアにある KMS セットアップ キーをインストールします。    |
|    0xC004F02C     |    ソフトウェア保護サービスでは、オフラインのライセンス認証データの形式が正しいことを報告します。    |    MAK/KMS クライアント    |    システムは、電話によるライセンス認証中に入力されたデータが無効であるが検出されました。    |    CID が正しく入力されたことを確認します。    |
|    0xC004F035     |    このエラー コードは、「ソフトウェア保護サービスが報告、コンピューターがボリューム ライセンス プロダクト キー でアクティブ化されませんでした」と同じです。エラー テキストは正しいがあいまいです。 このエラーを条件に一致するエディションの Windows で、KMS クライアントのライセンス認証の要件は、出荷するコンピューターを示すために、OEM システムで提供される – BIOS に Windows マーカーがコンピューターに存在しないことを示します。 エラー: をアクティブ化する無効なボリューム ライセンス キーの順序、マルティプル アクティベーション キー (MAK) または製品版の有効なキーに、プロダクト キーを変更する必要があります。 評価する必要がありますオペレーティング システムのライセンスと、ボリューム小売ソースから Windows 7、Windows 7 のアップグレード ライセンス、または完全なライセンスをライセンスします。 本ソフトウェアの他のインストールは、アグリーメントと適用可能な著作権に関する法律の違反です。    |    KMS クライアント/KMS ホスト    |    Windows 7 ボリューム エディションの場合はライセンスにアップグレードのみを取得します。 インストールされている条件を満たすオペレーティング システムがないコンピューターでボリュームのオペレーティング システムをインストールすることはサポートされません。    |    Microsoft のオペレーティング システムの資格を満たすバージョンをインストールし、MAK を使用して、アクティブ化します。    |
|    0xC004F038     |    ソフトウェア保護サービスでは、コンピューターが認証されませんでしたを報告します。 キー管理サービス (KMS) によって報告された数が十分ではありません。 システム管理者に問い合わせてください。    |    KMS クライアント    |    KMS ホストの数が不足しています。 KMS 数は、Windows Server で 5 以上または Windows クライアントの 25 である必要があります。    |    KMS クライアントがアクティブ化する、KMS プールより多くのコンピューターが必要です。 KMS ホストで現在の数を取得する Slmgr.vbs/dli」と入力を実行します。    |
|    0xC004F039     |    ソフトウェア保護サービスでは、コンピューターが認証されませんでしたを報告します。 キー管理サービス (KMS) が有効になっていません。    |    KMS クライアント    |    このエラーは、KMS 要求が応答しないときに発生します。    |    KMS ホストとクライアント間のネットワーク接続のトラブルシューティングを行います。 TCP ポート 1688 (既定値) のファイアウォールでブロックまたはそれ以外の場合にフィルター処理されていないことを確認してください。    |
|    0xC004F041     |    ソフトウェア保護サービスでは、キー管理サーバー (KMS) がアクティブにしないことを決定します。 KMS をライセンス認証する必要があります。    |    KMS クライアント    |    KMS ホストがライセンス認証されていません。    |    KMS ホストのいずれかのオンラインまたは電話でライセンス認証を有効にします。    |
|    0xC004F042     |    ソフトウェア保護サービスには、指定したキー管理サービス (KMS) を使用できないことが決定されます。    |    KMS クライアント    |    KMS クライアントと KMS ホストに不一致があります。    |    このエラーは、KMS クライアントが、クライアント ソフトウェアをアクティブにすることはできません、KMS ホストに接続するときに発生します。 たとえば、アプリケーションとオペレーティング システムに固有の KMS ホストを含む混在環境で一般的なことができます。    |
|    0xC004F050     |    ソフトウェア保護サービスでは、プロダクト キーが無効であるを報告します。    |    KMS、KMS クライアント、MAK    |    これは、またはオペレーティング システムのリリース版にベータ版のキーを入力して、KMS キーの入力ミスによって発生することができます。    |    Windows の対応するバージョンに適切な KMS キーをインストールします。 スペルをチェックします。 場合は、キーをコピーして、貼り付けることを確認します em dash がないされてダッシュに置き換えられてキー。    |
|    0xC004F051     |    ソフトウェア保護サービスでは、プロダクト キーがブロックされていることを報告します。    |    MAK/KMS    |    ライセンス認証サーバーのプロダクト キーは、Microsoft によってブロックされます。    |    新しい MAK/KMS キーを取得、システムにインストールおよびアクティブ化します。    |
|    0xC004F064     |    ソフトウェア保護サービスでは、非正規品の猶予期間が期限切れを報告します。    |    MAK    |    Windows ライセンス認証ツール (WAT) は、システムが正規と判断されました。    |    ボリューム ライセンス認証運用ガイドを参照してください。    |
|    0xC004F065     |    ソフトウェア保護サービスでは、アプリケーションが有効な非正規の期間内で実行されていることを報告します。    |    MAK/KMS クライアント    |    Windows ライセンス認証ツールは、システムが正規品であることに決めました。 システムは、非正規品の猶予期間中に実行し続けます。    |    取得して、正規のプロダクト キーをインストールし、猶予期間中、システムをアクティブ化します。 それ以外の場合、システムが、猶予期間の最後に、通知の状態に変わります。    |
|    0xC004F06C     |    ソフトウェア保護サービスでは、コンピューターが認証されませんでしたを報告します。 要求のタイムスタンプが無効であるキー管理サービス (KMS) が決定されます。    |    KMS クライアント    |    クライアント コンピューターのシステム時刻は、KMS ホスト上の時刻とは大きく異なります。    |    時刻の同期は、さまざまな理由からシステムとネットワークのセキュリティに重要です。 KMS と同期するクライアントのシステム時刻を変更することで、この問題を解決します。 ネットワーク タイム プロトコル (NTP) タイム ソースまたは時刻の同期、Active Directory Domain Services を使用することをお勧めします。 この問題は UTP 時刻を使用しはタイム ゾーンの選択に依存しません。    |
|    0x80070005     |    アクセスが拒否されました。 要求されたアクションには、高度な特権が必要です。    |    KMS クライアント/MAK/KMS ホスト    |    ユーザー アカウント制御 (UAC) は、アクティブ化プロセスが非管理者特権でコマンド プロンプトで実行されていることを禁止します。    |    管理者特権のコマンド プロンプトでコマンド slmgr.vbs を実行します。   cmd.exe を右クリックし、[管理者として実行] をクリックします。    |
|    0x8007232A     |    DNS サーバーにエラーが発生しました。    |    KMS ホスト    |    システムにはネットワークまたは DNS の問題があります。    |    ネットワークおよび DNS をトラブルシューティングします。    |
|    0x8007232B     |    DNS 名がありません。    |    KMS クライアント    |    KMS クライアントが DNS で KMS SRV RR を検索できません。 KMS ホストがネットワーク上に存在しない場合、MAK をインストールする必要があります。    |    確認 KMS ホストがインストールされていることと、DNS 発行は、(既定値) を有効にします。 DNS が使用できない場合は、slmgr.vbs/skms < kms_host_name > を使用して KMS ホストに KMS クライアントをポイントします。必要に応じてを入手して; MAK のインストール次に、システムを有効にします。 最後に、DNS をトラブルシューティングします。    |
|    0x800706BA     |    RPC サーバーを利用できません。    |    KMS クライアント    |    KMS ホストでは、ファイアウォールの設定が構成されていないか、DNS SRV レコードが古い。    |    KMS ホスト コンピューターのキー管理サービスのファイアウォールの例外が有効になっていることを確認します。 SRV レコードが指す有効な KMS ホストを確認します。 ネットワーク接続をトラブルシューティングします。    |
|    0x8007251D     |    レコードの DNS クエリが見つかりません。    |    KMS クライアント    |    KMS クライアントが DNS で KMS SRV RR を検索できません。    |    ネットワーク接続および DNS のトラブルシューティング    |
|    0xC004F074     |    ソフトウェア保護サービスでは、コンピューターが認証されませんでしたを報告します。 キー管理サービス (KMS) を接続ありませんでした。 詳細については、アプリケーション イベント ログを参照してください。    |    KMS クライアント    |    すべての KMS ホスト システムには、エラーが返されます。    |    各イベント ID 12288 のライセンス認証の試行に関連付けられているからのエラーのトラブルシューティングを行います。    |
|    0x8004FE21     |    このコンピューターには、正規の Windows が実行されていません。    |    MAK/KMS クライアント    |    この問題は、いくつかの理由の発生する可能性があります。 最も可能性の高い理由は、言語パック (MUI) を追加の言語パックに許可されていない Windows エディションを実行しているコンピューターにインストールされていることです。 (これは必ずしもの改ざんを示す値に注意してください。   一部のアプリケーション インストールできます多言語のサポートでも Windows のエディションは、これらの言語パックのライセンスがありません。)この問題は、Windows がインストールされる機能の追加を許可するマルウェアによって変更された場合にも発生する可能性があります。 この問題は、特定のシステム ファイルが破損している場合にも発生する可能性があります。    |    この問題を解決するには、オペレーティング システムを再インストールする必要があります。    |
|    0x80092328     |    0x80092328 DNS 名が存在しません。    |    KMS クライアント    |    この問題は、KMS クライアントが見つからない場合、KMS SRV リソース レコードを DNS に発生する可能性があります。    |    この問題を回避するには、次のマイクロソフト サポート技術情報記事の手順に従います。929826 エラー メッセージを Windows Vista Enterprise、Windows Vista Business、Windows 7、または Windows Server 2008 をアクティブ化しようとするとします。「コード 0x8007232b」    |
|    0x8007007b    |    0x8007007b DNS 名が存在しません。    |    KMS クライアント    |    この問題は、KMS クライアントが見つからない場合、KMS SRV リソース レコードを DNS に発生する可能性があります。    |    この問題を回避するには、次のマイクロソフト サポート技術情報記事の手順に従います。929826 エラー メッセージを Windows Vista Enterprise、Windows Vista Business、Windows 7、または Windows Server 2008 をアクティブ化しようとするとします。「コード 0x8007232b」    |
|    0x80070490    |入力したプロダクト キーは動作しませんでした。  プロダクト キーを確認し、もう一度やり直してまたは、別のアカウントを入力します。 |MAK |この問題は、無効な MAK が入力されたため、または Windows Server 2019 で既知の問題により発生します。 |この問題を回避するには、コマンドラインを使用してコンピューターをライセンス認証**slmgr ipk \<5 x 5 のキー\>**|
