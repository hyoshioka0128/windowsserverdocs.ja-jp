---
title: "Windows Server Essentials のインストールをトラブルシューティングします。"
description: "Windows Server Essentials を使用する方法について説明します。"
ms.custom: na
ms.date: 10/03/2016
ms.prod: windows-server-2016-essentials
ms.reviewer: na
ms.suite: na
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: ecf19216-7aac-4aca-839a-342ac28f5329
author: nnamuhcs
ms.author: coreyp
manager: dongill
ms.openlocfilehash: 293b392203269a65efffcefb3744bedc659f71c9
ms.sourcegitcommit: db290fa07e9d50686667bfba3969e20377548504
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/12/2017
---
# <a name="troubleshoot-windows-server-essentials-installation"></a>Windows Server Essentials のインストールをトラブルシューティングします。

>Windows Server 2016 Essentials、Windows Server 2012 R2 Essentials での Windows Server 2012 Essentials を適用対象:

このトピックでは、Windows Server Essentials をインストールするときに発生する問題のトラブルシューティングを提供します。 次の領域におけるガイダンスを示します。  
  

-   [一般的なトラブルシューティング手順](Troubleshoot-Windows-Server-Essentials-installation.md#BKMK_GeneralTroubleshootingSteps)  
  
-   [ドライバーの問題をトラブルシューティングします。](Troubleshoot-Windows-Server-Essentials-installation.md#BKMK_TroubleshootDrivers)  

-   [一般的なトラブルシューティング手順](Troubleshoot-Windows-Server-Essentials-installation.md#BKMK_GeneralTroubleshootingSteps)  
  
-   [ドライバーの問題をトラブルシューティングします。](Troubleshoot-Windows-Server-Essentials-installation.md#BKMK_TroubleshootDrivers)  

  
> [!NOTE]
>  Windows Server Essentials コミュニティから最新のトラブルシューティング情報について、ことをお勧めを参照する、[Windows Server Essentials フォーラム](https://social.technet.microsoft.com/Forums/winserveressentials/threads)します。 Windows Server Essentials フォーラムは、ヘルプについては、検索するか、質問をお勧めします。  
  
##  <a name="BKMK_GeneralTroubleshootingSteps"></a>一般的なトラブルシューティング手順  
 Windows Server Essentials のインストールに失敗した場合、エラーの原因となった問題を特定するために次の手順を実行します。  
  
> [!IMPORTANT]
>  ない手動でサーバーを再起動する Windows Server Essentials のインストール中に重要です。 サーバーが自動的に再起動数回セットアップと初期構成中にします。 確認した場合は、サーバーを再起動する前に手動で、**サーバーのインストールが成功した**メッセージは、インストールが中断およびが失敗する原因となったいる可能性があります。  
  
#### <a name="to-identify-issues-in-a-failed-installation-of-windows-server-essentials"></a>Windows Server Essentials のインストールに失敗の問題を特定するには  
  
1.  サーバー ハードウェアが最小要件を満たしていることを確認します。 ハードウェア要件については、次を参照してください。[Windows Server Essentials のシステム要件](../get-started/system-requirements.md)します。  
  
2.  MSDN の Windows Server Essentials のインストール DVD を受け取っている場合は、DVD が有効では、SHA1 のチェックサムをチェックして、確認します。 詳細については、次を参照してください。[ファイル チェックサム整合性検証ユーティリティの可用性と説明](https://go.microsoft.com/fwlink/?LinkId=220495)(https://go.microsoft.com/fwlink/?LinkId=220495)。  
  
3.  サーバー上のネットワーク アダプターが、ネットワーク ケーブルでルーターに接続されていることを確認します。  
  
4.  サーバーに 1 つ以上のネットワーク アダプターがある場合は、その 1 つのみのネットワーク アダプターが有効になっていることを確認します。  
  
    > [!IMPORTANT]
    >  ネットワーク ケーブルを切断し、Windows Server Essentials のインストール中に、ルーターを再起動したりしないでください。  
  
5.  「サーバーのインストールとデプロイメント」を参照[Windows Server Essentials のリリースのドキュメント](../get-started/release-notes.md)  
  
6.  エラー メッセージを受け取った場合のインストール中に、サーバーのセットアップを工場出荷時の既定の設定に、サーバーを復元して、ハードウェアの製造元によって提供されるについては、サーバー回復 DVD を使用中にエラーが発生しました。  
  
##  <a name="BKMK_TroubleshootDrivers"></a>ドライバーの問題をトラブルシューティングします。  
 Windows Server Essentials をインストールするときに、最も一般的な問題は、ドライバーを手動でインストールする必要がある記憶域コントローラーです。 Windows には、多くの記憶域コントローラー用ドライバーが含まれていますが、これが、特定のハードウェアのドライバーは含まれません。  
  
 特定のハードウェア、ネットワーク カード ドライバーを手動でインストールする必要もあります。  
  
###  <a name="BKMK_StorageDrivers"></a>記憶域コントローラー用ドライバーを追加します。  
 ハードウェアは、Windows Server Essentials に含まれていない記憶域ドライバーを必要とする場合は、セットアップを完了する、次の情報を使用します。  
  
 セットアップ中に、次のメッセージが表示された場合は、記憶域コントローラー用ドライバーを手動で追加する必要があります。  
  
 **Windows Server セットアップ エラー**  
  
 Windows Server Essentials をホストできるハード ディスクが見つかりませんでした。 追加の記憶域ドライバーをロードしますか?  
  
 記憶域コントローラー ドライバーをインストールするのにには、次の手順を使用します。  
  
##### <a name="to-manually-install-a-storage-controller-driver"></a>記憶域コントローラー ドライバーを手動でインストールするには  
  
1.  記憶域コントローラー用ドライバーを検索します。 これらはハードウェアの製造元によって提供され、製造元の Web サイトで利用可能な場合があります。  
  
2.  フロッピー ディスクに DRIVERS というフォルダーを作成または USB フラッシュ ドライブ、およびフォルダーにドライバーをコピーします。  
  
3.  コンピューターにドライバーを USB フラッシュ ドライブ、フロッピー ドライブを接続します。  
  
4.  Windows Server Essentials DVD からコンピューターを起動します。  
  
     すべての記憶域コントローラー用ドライバーが不足している場合は、Windows Server Essentials のセットアップ エラー] ダイアログ ボックスが表示されます。  
  
5.  Windows Server Essentials のセットアップ エラー] ダイアログ ボックスで、[**はい**に追加の記憶域ドライバーをロードします。  
  
6.  **ドライバーの inf ファイルを選択してください**プロンプト、ドライバー フォルダーで、プロッピー ディスクまたは USB フラッシュ ドライブ上の .inf ファイルに移動、ファイルを選択、ファイル名を右クリックし] をクリックして**開く**します。 これには、ドライバーが読み込まれます。  
  
    > [!NOTE]
    >  ファイルを読み込む前に、ファイル名拡張子 (.inf) が小文字であることを確認します。 この操作は、大文字と小文字が区別し、ファイル名拡張子がある大文字の場合、ドライバー ファイルは読み込まれません。  
  
7.  プロンプトで、をクリックして**はい**セットアップのテキスト モードのフェーズ中に、記憶域ドライバーを利用できるようにします。  
  
 セットアップを引き続き続行します。  
  
###  <a name="BKMK_AddingNICdrivers"></a>ネットワーク アダプターのドライバーを追加します。  
 場合は、コンピューター上のネットワーク アダプターは、Windows Server Essentials でサポートされていない、サーバーが接続されていないネットワーク セットアップが完了したら、し、コンピューター、サーバーに接続することはできません。  
  
 、、Windows Server Essentials のインストールの最後に、ネットワーク アダプター ドライバーが自動的にインストールされていない場合に通知されます。 使用することも**のネットワーク接続**コントロール パネルの [不足しているネットワーク アダプター ドライバーを確認します。 サーバー上のネットワーク アダプターに関連付けられているネットワーク接続が表示されない場合は、ドライバーをインストールする必要があります。  
  
 サポートされている任意のネットワーク アダプターのドライバーが足りない場合は、適切なネットワーク アダプター ドライバーを手動でインストールしてから、サーバーを再起動する必要があります。 次の手順に従います。  
  
##### <a name="to-install-a-network-adapter-driver"></a>ネットワーク アダプター ドライバーをインストールするには  
  
1.  ネットワーク アダプターの製造元から不足しているドライバーを取得します。  
  
2.  製造元の指示をに従ってインストール ドライバーをインストールします。  
  
3.  コンピューターを再起動します。  
  
    > [!IMPORTANT]
    >  不足しているネットワーク アダプター ドライバーをインストールした後に、サーバーを再起動しないと、クライアント コンピューターで Windows Server Essentials コネクタ ソフトウェアのインストールが失敗する可能性があります。
