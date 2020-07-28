---
title: Windows Server Essentials のインストールに関するトラブルシューティング
description: Windows Server Essentials の使用方法について説明します。
ms.date: 10/03/2016
ms.topic: article
ms.assetid: ecf19216-7aac-4aca-839a-342ac28f5329
author: nnamuhcs
ms.author: coreyp
manager: dongill
ms.openlocfilehash: 755b00f9c2593a6923f65437c695dcd6a2de7532
ms.sourcegitcommit: d99bc78524f1ca287b3e8fc06dba3c915a6e7a24
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/27/2020
ms.locfileid: "87180288"
---
# <a name="troubleshoot-windows-server-essentials-installation"></a>Windows Server Essentials のインストールに関するトラブルシューティング

>適用対象: windows Server 2016 Essentials、Windows Server 2012 R2 Essentials、Windows Server 2012 Essentials

このトピックでは、Windows Server Essentials のインストール時に発生する問題のトラブルシューティングについて説明します。 以下の領域に関するガイダンスを示します。


-   [一般的なトラブルシューティング手順](Troubleshoot-Windows-Server-Essentials-installation.md#BKMK_GeneralTroubleshootingSteps)

-   [ドライバーの問題に関するトラブルシューティング](Troubleshoot-Windows-Server-Essentials-installation.md#BKMK_TroubleshootDrivers)

-   [一般的なトラブルシューティング手順](Troubleshoot-Windows-Server-Essentials-installation.md#BKMK_GeneralTroubleshootingSteps)

-   [ドライバーの問題に関するトラブルシューティング](Troubleshoot-Windows-Server-Essentials-installation.md#BKMK_TroubleshootDrivers)


> [!NOTE]
>  Windows Server Essentials コミュニティの最新のトラブルシューティング情報については、 [Windows Server Essentials フォーラム](https://docs.microsoft.com/answers/topics/windows-server-essentials.html/threads)を参照することをお勧めします。 Windows Server Essentials フォーラムは、ヘルプを検索したり、質問したりするために最適な場所です。

##  <a name="general-troubleshooting-steps"></a><a name="BKMK_GeneralTroubleshootingSteps"></a>一般的なトラブルシューティング手順
 Windows Server Essentials のインストールに失敗した場合は、次の手順を実行して、エラーの原因となった問題を特定してください。

> [!IMPORTANT]
>  Windows Server Essentials をインストールするときに、サーバーを手動で再起動しないことが重要です。 サーバーは、セットアップと初期構成中に何度も自動的に再起動されます。 **[サーバーのインストールが正常に行われました]** というメッセージが表示される前にサーバーを手動で再起動すると、インストールが中断され、失敗の原因となる可能性があります。

#### <a name="to-identify-issues-in-a-failed-installation-of-windows-server-essentials"></a>Windows Server Essentials のインストールの失敗に関する問題を特定するには

1.  サーバー ハードウェアが最小ハードウェア要件を満たしていることを確認します。 ハードウェア要件の詳細については、「 [Windows Server Essentials のシステム要件](../get-started/system-requirements.md)」を参照してください。

2.  MSDN から Windows Server Essentials インストール DVD を受け取った場合は、SHA1 の合計を確認して、DVD が有効であることを確認します。 詳細については、「[ファイルチェックサム整合性検証ユーティリティの可用性と説明](https://go.microsoft.com/fwlink/?LinkId=220495)」 (「」を参照してください https://go.microsoft.com/fwlink/?LinkId=220495) 。

3.  サーバーのネットワーク アダプターが、ネットワーク ケーブルでルーターに接続されていることを確認します。

4.  サーバーに複数のネットワーク アダプターがある場合、有効になっているネットワーク アダプターが 1 つだけであることを確かめます。

    > [!IMPORTANT]
    >  Windows Server Essentials をインストールするときに、ネットワークケーブルを切断したり、ルーターを再起動したりしないでください。

5.  [Windows Server Essentials のリリースドキュメント](../get-started/release-notes.md)の「サーバーのインストールと展開」を参照してください。

6.  インストール中にサーバーのセットアップ中にエラーが発生した場合は、サーバー回復 DVD とハードウェアの製造元から提供されている指示に従って、サーバーを工場出荷時の既定の設定に戻します。

##  <a name="troubleshoot-driver-issues"></a><a name="BKMK_TroubleshootDrivers"></a>ドライバーに関する問題のトラブルシューティング
 Windows Server Essentials をインストールするときの最も一般的な問題は、ドライバーを手動でインストールする必要がある記憶域コントローラーです。 Windows には多くの記憶域コントローラー用ドライバーが含まれていますが、特定のハードウェアのドライバーに関しては含まれていない場合があります。

 また、特定のハードウェアに関して、ネットワーク カード ドライバーを手動でインストールしなければならないこともあります。

###  <a name="adding-drivers-for-storage-controllers"></a><a name="BKMK_StorageDrivers"></a>記憶域コントローラーのドライバーを追加しています
 ハードウェアに Windows Server Essentials に含まれていない記憶域ドライバーが必要な場合は、次の情報を使用してセットアップを完了します。

 セットアップ中に次のメッセージが表示される場合、記憶域コントローラー用ドライバーを手動で追加する必要があります。

 **Windows Server セットアップ エラー**

 Windows Server Essentials をホストできるハードディスクドライブが見つかりませんでした。 他の記憶域ドライバーをロードしますか。

 次の手順を使用して、記憶域コントローラー用ドライバーをインストールします。

##### <a name="to-manually-install-a-storage-controller-driver"></a>記憶域コントローラー用ドライバーを手動でインストールするには

1. ご使用の記憶域コントローラー用ドライバーを検索します。 こうしたドライバーはハードウェアの製造元によって提供され、製造元の Web サイトで入手できることもあります。

2. プロッピー ディスクに DRIVERS というフォルダーを作成し、ドライバーをそのフォルダーにコピーします。

3. ドライバーの入ったフロッピー ドライブまたは USB フラッシュ ドライブをコンピューターに接続します。

4. Windows Server Essentials DVD からコンピューターを起動します。

    いずれかの記憶域コントローラードライバーが見つからない場合は、[Windows Server Essentials セットアップエラー] ダイアログボックスが表示されます。

5. [Windows Server Essentials セットアップエラー] ダイアログボックスで、[**はい**] をクリックして追加の記憶域ドライバーを読み込みます。

6. **[ドライバーの inf ファイルを選択してください]** というプロンプトで、プロッピー ディスクまたは USB フラッシュ ドライブの DRIVERS フォルダーにある .inf ファイルにナビゲートし、そのファイル名を右クリックして、**[開く]** をクリックします。 対象のドライバーがロードされます。

   > [!NOTE]
   >  ファイルのロードを試行する前に、ファイル名の拡張子 (.inf) が小文字であることを確認します。 この操作では大文字と小文字が区別され、ファイル名の拡張子が大文字の場合にはドライバー ファイルがロードされません。

7. プロンプトが表示されたら、**[はい]** をクリックして、セットアップのテキスト モードのフェーズで記憶域ドライバーを有効にします。

   セットアップを引き続き続行します。

###  <a name="adding-drivers-for-network-adapters"></a><a name="BKMK_AddingNICdrivers"></a>ネットワークアダプターのドライバーを追加しています
 コンピューター上のネットワークアダプターが Windows Server Essentials でサポートされていない場合、セットアップの完了後にサーバーがネットワークに接続できなくなり、コンピューターをサーバーに接続できなくなります。

 Windows Server Essentials のインストールが終了すると、ネットワークアダプタードライバーが自動的にインストールされなかったかどうかが通知されます。 [コントロール パネル] の **[ネットワーク接続]** を使用して、不足しているネットワーク アダプター ドライバーがあるかどうかを確認することもできます。 サーバー上で対象のネットワーク アダプターに関連したネットワーク接続が表示されない場合、ドライバーをインストールする必要があります。

 いずれかのネットワーク アダプターのサポート対象ドライバーがコンピューターで欠落している場合、適切なネットワーク アダプター ドライバーを手動でインストールしてから、サーバーを再起動しなければなりません。 次の手順に従います。

##### <a name="to-install-a-network-adapter-driver"></a>ネットワーク アダプター ドライバーをインストールするには

1.  ネットワーク アダプターの製造元から、不足しているドライバーを入手します。

2.  製造元のインストールの指示に従ってドライバーをインストールします。

3.  コンピューターを再起動します。

    > [!IMPORTANT]
    >  不足しているネットワークアダプタードライバーをインストールした後にサーバーを再起動しないと、クライアントコンピューターへの Windows Server Essentials コネクタソフトウェアのインストールが失敗する場合があります。
