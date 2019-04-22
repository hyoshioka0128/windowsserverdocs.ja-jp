---
title: Windows Server バージョン 1803 の新機能
description: コンピューティング、ID、管理、自動化、ネットワーク、セキュリティ、記憶域の新機能について。
ms.prod: windows-server-threshold
ms.technology: server-general
ms.topic: article
author: greg-lindsay
ms.author: greg-lindsay
ms.localizationpriority: high
ms.date: 05/07/2018
ms.openlocfilehash: c4f80b668b91e65b6c8bc528e14f52a1d117a3c9
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/17/2019
ms.locfileid: "59823093"
---
# <a name="whats-new-in-windows-server-version-1803"></a>Windows Server バージョン 1803 の新機能

>適用先:Windows Server (半期チャネル)

<img src="../media/landing-icons/new.png" style='float:left; padding:.5em;' alt="Icon showing a newspaper">&nbsp;ここでは、Windows Server バージョン 1803 の新機能および変更された機能について説明します。 ここに記載されている新機能と変更された機能は、このリリースを使う際に影響が最も大きいと思われるものです。 [Windows Server 半期チャネルの更新プログラム](https://cloudblogs.microsoft.com/windowsserver/2018/03/29/windows-server-semi-annual-channel-update/)に関するページも参照してください。

## <a name="windows-admin-center"></a>Windows Admin Center

Project Honolulu は、**Windows Admin Center** になりました。
<br>&nbsp;
> [!video https://www.youtube.com/embed/WCWxAp27ERk?autoplay=false]

[Windows Admin Center](https://docs.microsoft.com/windows-server/manage/windows-admin-center/overview) は、ローカルとリモート サーバー管理のすべての側面を統合します。 Windows Admin Center は、インターネット接続を必要としない、ローカルに展開されたブラウザー ベースの管理エクスペリエンスです。これにより、Windows Server 展開のあらゆる側面を完全に管理できます。

## <a name="windows-server-release-strategy"></a>Windows Server リリース戦略

Windows Server バージョン 1709 は、半期チャネルの最初のリリースとして 2017 年 9 月にリリースされました。 半期チャネルはリリース間隔が短く、数か月ごとに迅速なイノベーションを必要とするユーザーからのフィードバックに対処しています。 これは、リリース間隔が 2 ～ 3 年おきである長期サービス チャネルを補完するものです。

利用統計情報とフィードバックに基づき、これらのチャネルは次の一般的な戦略に十分に従っていることが実証されています。
- 半期チャネルは、コンテナーやマイクロサービスなどの現在のアプリケーションやイノベーション シナリオに最適です。
- 長期サービス チャネルは、ソフトウェア定義データセンターやハイパーコンバージド インフラストラクチャ (HCI) などのコア インフラストラクチャ シナリオに推奨されるリリースです。 

半期チャネルと長期サービス チャネルの特定のシナリオは次のとおりです。

|   | Long Term Servicing チャネル |  半期チャネル |
| ------------- | ------------- | ------------ |
| 推奨されるシナリオ     | 汎用ファイル サーバー、ファースト パーティおよびサード パーティのワークロード、従来のアプリ、インフラストラクチャの役割、ソフトウェア定義データセンター、およびハイパーコンバージド インフラストラクチャ  | コンテナー化されたアプリケーション、コンテナー ホスト、および迅速なイノベーションを活用するアプリケーション シナリオ |
| 新しいリリース  | 2 ～ 3 年ごと  | 6 か月ごと |
| サポート  | 5 年間のメインストリーム サポート + 5 年間の延長サポート  | 18 か月 |
| エディション  | 利用可能なすべての Windows Server エディション  | Standard エディションと Datacenter エディション |
| 利用できるユーザー  | すべてのチャネルのすべてのユーザー | ソフトウェア アシュアランスとクラウドのユーザーのみ |
| インストール オプション  | Server Core とデスクトップ エクスペリエンス搭載サーバー  | コンテナー ホストとコンテナー イメージ用の Server Core、および Nano Server コンテナー イメージ |

## <a name="application-platform-and-containers"></a>アプリケーション プラットフォームとコンテナー

- Optimization
    - Server Core 基本コンテナー イメージは、Windows Server バージョン 1709 から 30% 減少します。 
    - また、アプリケーションの互換性が向上し、従来のアプリケーションをコンテナー化するのに役立ちます。
    - さまざまな修正や最適化のおかげでコンテナーの起動パフォーマンスおよび実行時パフォーマンスも向上しています。
- コンテナーのネットワーク:Localhost と http プロキシのサポートが追加されたら、およびコンテナーのスケーラビリティとスタートアップ時間が短縮します。
- ツール:ビルドとデバッグ シナリオ用に PowerShell を補完する Curl.exe、Tar.exe、および SSH のサポートが強化されました。

### <a name="server-core-container-image"></a>Server Core コンテナー イメージ

アプリケーションの互換性がより優れた小さい Server Core コンテナーが利用できるようになりました。 詳細情報は、[こちら](https://blogs.technet.microsoft.com/virtualization/2018/01/22/a-smaller-windows-server-core-container-with-better-application-compatibility/)で確認できます。

- 使用されていないオプションの機能と役割が削除されました。 詳細については、[Server Core コンテナーにない役割、役割サービス、および機能](../administration/server-core/server-core-container-removed-roles.md)に関するページを参照してください。
    - ダウンロード サイズが 1.58 GB に縮小されました。これは Windows Server バージョン 1709 から 30% の削減です。
    - ディスク上のサイズが 3.61 GB に縮小されました。これは Windows Server バージョン 1709 から 20% の削減です。
- Nano Server コンテナー イメージは 100MB を下回っています。

### <a name="windows-subsystem-for-linux-wsl"></a>Windows Subsystem for Linux (WSL)

WSL によって、サーバーの管理者は Windows Server の Linux から既存のツールとスクリプトを使用することができます。 [コマンド ラインに関するブログ](https://blogs.msdn.microsoft.com/commandline/tag/wsl/)で紹介された、バックグラウンド タスク、DriveFS、WSLPath などの多くの機能強化は、Windows Server の一部として含まれるようになりました。

### <a name="kubernetes"></a>Kubernetes 

Kubernetes (一般的に K8s と呼ばれます) は、[Cloud Native Computing Foundation](https://www.cncf.io) の管理の下で開発されたコンテナー化されたアプリケーションの展開、スケーリング、管理を自動化するためのオープン ソース システムです。 

Windows Server バージョン 1709 では、ユーザーは次のような Windows ネットワーク機能で Kubernetes を利用することができました。
- ポッドのコンパートメントを共有するには。インフラストラクチャおよび worker ポッドは、ネットワーク コンパートメント (Linux の名前空間に似ています) を共有するようになりました。
- エンドポイントの最適化:コンパートメントの共有に協力してくれたコンテナー サービスは多くの半数以上のエンドポイントを追跡する必要があります。
- データ パスの最適化:カーネル ベースの負荷分散仮想フィルタ リング プラットフォームと、ホストのネットワーク サービスの機能強化を許可します。

Windows Server バージョン 1803 のリリースに伴い、次の Kubernetes リリースでより多くの機能が利用できるようになります。 
- Kubernetes によってオーケストレーションされる Windows コンテナーの[ストレージ プラグイン](https://github.com/Microsoft/K8s-Storage-Plugins)。
- [Project Calico での Tigera](https://cloudblogs.microsoft.com/windowsserver/2017/12/07/securing-modernized-apps-and-simplified-networking-on-windows-with-calico/) との提携などのイニシアティブによるクラウド スケールのネットワーク。
- ポッドごとの複数のコンテナーを含む Hyper-V 分離ポッドのための Windows プラットフォーム サポート。

### <a name="application-compatibility-and-feature-parity-issues-fixed"></a>修正されたアプリケーションの互換性と機能の等価性の問題

- Microsoft Message Queuing (MSMQ) は現在 Server Core コンテナーにインストールされるようになりました。
- ASP.net パフォーマンス カウンターを破損する問題が修正されました。
- コンテナーで実行されているサービスがシャットダウン通知を受信しないという問題が修正されました。
    - 具体的には、通知は、Server Core と Nano Server の両方のコンテナー ベースのイメージ用の CTRL_SHUTDOWN_EVENT に変更されました。 また、通知が Server Core のコンテナー ベースのイメージに拡張され、コンテナーで実行されているすべてのプロセスに影響するようになりました。これには、コンテナーで実行されているサービスへのサービス シャットダウン通知の送信が含まれます。
- 固定データ ドライブが書き込み可能である (FDVDenyWriteAccess) ために BitLocker 保護が必要かどうかを決定するポリシー設定が適用された docker pull および docker load の非互換性が修正されました。 

## <a name="storage"></a>ストレージ

このリリースでは、File Server Resource Manager サービスが、起動時にすべてのボリュームで変更ジャーナル (USN ジャーナルとも呼ばれます) を作成しないようにすることが可能です これにより、各ボリューム上の領域を節約できますが、リアルタイムのファイル分類は無効になります。 詳細については、「[ファイル サーバー リソース マネージャーの概要](https://docs.microsoft.com/windows-server/storage/fsrm/fsrm-overview)」を参照してください。

## <a name="features-added-to-server-core"></a>Server Core に追加された機能

Windows 展開サービス (WDS) の役割のトランスポート サーバーの役割は Server Core に追加されました。

トランスポート サーバーには、WDS のコア ネットワーク部分のみが含まれます。 トランスポート サーバーを使用して、スタンドアロン サーバーからデータ (オペレーティング システム イメージを含む) を送信するマルチキャスト名前空間を作成できます。 また、クライアントが PXE ブートし、独自のカスタム セットアップ アプリケーションをダウンロードできるようにする PXE サーバーを用意する必要がある場合にも使用できます。 これらのシナリオのいずれかを使用する場合は、このオプションを使用する必要があります。

次の Windows PowerShell コマンドを使用して Server Core でトランスポート サーバー サービスを有効にすることができます。

```
Install-WindowsFeature -Name WDS
```

## <a name="see-also"></a>関連項目

[Windows Server のリリース情報](https://docs.microsoft.com/windows-server/get-started/windows-server-release-info)<br>
[新機能については、Windows 10 バージョン 1803 の IT Pro コンテンツです。](https://docs.microsoft.com/windows/whats-new/whats-new-windows-10-version-1803)
