---
title: Windows Server Essentials のインストールに関するトラブルシューティング
description: Windows Server Essentials を使用する方法について説明します
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
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/17/2019
ms.locfileid: "59862023"
---
# <a name="troubleshoot-windows-server-essentials-installation"></a>Windows Server Essentials のインストールに関するトラブルシューティング

>適用先:Windows Server 2016 Essentials、Windows Server 2012 R2 Essentials、Windows Server 2012 Essentials

このトピックでは、Windows Server Essentials をインストールするときに発生する問題のトラブルシューティングを提供します。 以下の領域に関するガイダンスを示します。  
  

-   [一般的なトラブルシューティング手順](Troubleshoot-Windows-Server-Essentials-installation.md#BKMK_GeneralTroubleshootingSteps)  
  
-   [ドライバーの問題をトラブルシューティングします。](Troubleshoot-Windows-Server-Essentials-installation.md#BKMK_TroubleshootDrivers)  

-   [一般的なトラブルシューティング手順](Troubleshoot-Windows-Server-Essentials-installation.md#BKMK_GeneralTroubleshootingSteps)  
  
-   [ドライバーの問題をトラブルシューティングします。](Troubleshoot-Windows-Server-Essentials-installation.md#BKMK_TroubleshootDrivers)  

  
> [!NOTE]
>  Windows Server Essentials コミュニティの最新のトラブルシューティング情報について、お勧めしますをご覧ください、 [Windows Server Essentials フォーラム](https://social.technet.microsoft.com/Forums/winserveressentials/threads)します。 Windows Server Essentials フォーラムは、ヘルプを検索したり、質問したりするために最適な場所です。  
  
##  <a name="BKMK_GeneralTroubleshootingSteps"></a> 一般的なトラブルシューティング手順  
 Windows Server Essentials のインストールに失敗した場合は、エラーの原因となった問題を識別できるように次の手順を実行します。  
  
> [!IMPORTANT]
>  手動で再起動しないサーバー Windows Server Essentials をインストールするときに重要です。 サーバーは、セットアップと初期構成中に何度も自動的に再起動されます。 **[サーバーのインストールが正常に行われました]** というメッセージが表示される前にサーバーを手動で再起動すると、インストールが中断され、失敗の原因となる可能性があります。  
  
#### <a name="to-identify-issues-in-a-failed-installation-of-windows-server-essentials"></a>Windows Server Essentials のインストールが失敗した問題を識別するには  
  
1.  サーバー ハードウェアが最小ハードウェア要件を満たしていることを確認します。 ハードウェア要件については、次を参照してください。 [Windows Server Essentials のシステム要件](../get-started/system-requirements.md)します。  
  
2.  MSDN から Windows Server Essentials のインストール DVD を受信する場合は、DVD が、sha1、有効であることを確認します。 詳細については、次を参照してください。[ファイル チェックサム整合性検証ユーティリティの可用性と説明](https://go.microsoft.com/fwlink/?LinkId=220495)(https://go.microsoft.com/fwlink/?LinkId=220495)します。  
  
3.  サーバーのネットワーク アダプターが、ネットワーク ケーブルでルーターに接続されていることを確認します。  
  
4.  サーバーに複数のネットワーク アダプターがある場合、有効になっているネットワーク アダプターが 1 つだけであることを確かめます。  
  
    > [!IMPORTANT]
    >  ネットワーク ケーブル、Windows Server Essentials をインストールするときに、ルーターを再起動したりしないでください。  
  
5.  「サーバーのインストールと展開」を確認[Windows Server Essentials のリリース ドキュメント](../get-started/release-notes.md)  
  
6.  エラー メッセージを受信する場合のインストール中に、サーバーのセットアップでサーバーを出荷時の設定に復元するサーバー リカバリ DVD とハードウェアの製造元の指示を使用中にエラーが発生しました。  
  
##  <a name="BKMK_TroubleshootDrivers"></a> ドライバーの問題をトラブルシューティングします。  
 Windows Server Essentials をインストールするときに、最も一般的な問題は、ドライバーを手動でインストールする必要がある記憶域コント ローラーです。 Windows には多くの記憶域コントローラー用ドライバーが含まれていますが、特定のハードウェアのドライバーに関しては含まれていない場合があります。  
  
 また、特定のハードウェアに関して、ネットワーク カード ドライバーを手動でインストールしなければならないこともあります。  
  
###  <a name="BKMK_StorageDrivers"></a> 記憶域コント ローラー用ドライバーを追加  
 ハードウェアには、Windows Server Essentials に含まれていない記憶装置ドライバーが必要とする場合は、次の情報を使用して、セットアップを完了します。  
  
 セットアップ中に次のメッセージが表示される場合、記憶域コントローラー用ドライバーを手動で追加する必要があります。  
  
 **Windows Server のセットアップ エラー**  
  
 Windows Server Essentials をホストできるハード ディスクのドライブが見つかりませんでした。 他の記憶域ドライバーをロードしますか。  
  
 次の手順を使用して、記憶域コントローラー用ドライバーをインストールします。  
  
##### <a name="to-manually-install-a-storage-controller-driver"></a>記憶域コントローラー用ドライバーを手動でインストールするには  
  
1.  ご使用の記憶域コントローラー用ドライバーを検索します。 こうしたドライバーはハードウェアの製造元によって提供され、製造元の Web サイトで入手できることもあります。  
  
2.  プロッピー ディスクに DRIVERS というフォルダーを作成し、ドライバーをそのフォルダーにコピーします。  
  
3.  ドライバーの入ったフロッピー ドライブまたは USB フラッシュ ドライブをコンピューターに接続します。  
  
4.  Windows Server Essentials の DVD からコンピューターを起動します。  
  
     すべての記憶域コント ローラー ドライバーが不足している場合は、Windows Server Essentials のセットアップ エラー ダイアログ ボックスが表示されます。  
  
5.  Windows Server Essentials のセットアップ エラー] ダイアログ ボックスで、[**はい**に追加の記憶域ドライバーをロードします。  
  
6.  **[ドライバーの inf ファイルを選択してください]** というプロンプトで、プロッピー ディスクまたは USB フラッシュ ドライブの DRIVERS フォルダーにある .inf ファイルにナビゲートし、そのファイル名を右クリックして、**[開く]** をクリックします。 対象のドライバーがロードされます。  
  
    > [!NOTE]
    >  ファイルのロードを試行する前に、ファイル名の拡張子 (.inf) が小文字であることを確認します。 この操作では大文字と小文字が区別され、ファイル名の拡張子が大文字の場合にはドライバー ファイルがロードされません。  
  
7.  プロンプトが表示されたら、**[はい]** をクリックして、セットアップのテキスト モードのフェーズで記憶域ドライバーを有効にします。  
  
 セットアップを引き続き続行します。  
  
###  <a name="BKMK_AddingNICdrivers"></a> ネットワーク アダプターのドライバーを追加します。  
 コンピューター上のネットワーク アダプターが Windows Server Essentials でサポートされていない場合、サーバーが接続されていないネットワーク セットアップが完了し、コンピューター、サーバーに接続することができなきます。  
  
 Windows Server Essentials のインストールの最後で、ネットワーク アダプター ドライバーが自動的にインストールされていない場合に通知されます。 [コントロール パネル] の **[ネットワーク接続]** を使用して、不足しているネットワーク アダプター ドライバーがあるかどうかを確認することもできます。 サーバー上で対象のネットワーク アダプターに関連したネットワーク接続が表示されない場合、ドライバーをインストールする必要があります。  
  
 いずれかのネットワーク アダプターのサポート対象ドライバーがコンピューターで欠落している場合、適切なネットワーク アダプター ドライバーを手動でインストールしてから、サーバーを再起動しなければなりません。 次の手順を実行します。  
  
##### <a name="to-install-a-network-adapter-driver"></a>ネットワーク アダプター ドライバーをインストールするには  
  
1.  ネットワーク アダプターの製造元から、不足しているドライバーを入手します。  
  
2.  製造元のインストールの指示に従ってドライバーをインストールします。  
  
3.  コンピューターを再起動します。  
  
    > [!IMPORTANT]
    >  不足しているネットワーク アダプター ドライバーをインストールした後に、サーバーを再起動しないと、クライアント コンピューターに Windows Server Essentials コネクタ ソフトウェアのインストールが失敗する可能性があります。
