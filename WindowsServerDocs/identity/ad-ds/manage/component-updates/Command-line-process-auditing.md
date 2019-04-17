---
ms.assetid: c8597cc8-bdcb-4e59-a09e-128ef5ebeaf8
title: "コマンド ライン プロセスの監査"
description: 
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adds
ms.openlocfilehash: 61e7a5ca2b9c00c9976e6032bb10adb1974020b0
ms.sourcegitcommit: db290fa07e9d50686667bfba3969e20377548504
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/12/2017
---
# <a name="command-line-process-auditing"></a>コマンド ライン プロセスの監査

>適用対象: Windows Server 2016、Windows Server 2012 R2

**作成者**: Windows グループに Justin チューナー シニア サポート エスカレーション エンジニア  
  
> [!NOTE]  
> このコンテンツが、Microsoft カスタマー サポート エンジニアによって書き込まれるあり、経験豊富な管理者と TechNet の通常のトピックよりも機能と Windows Server 2012 R2 で解決策の詳細な技術的説明を求めているシステム アーキテクトです。 ただし、実施されていません、同様の編集過程のため、TechNet の「新機能が見つかった通常より洗練されて、言語によってように見える場合があります。  
  
## <a name="overview"></a>概要  
  
-   既存のプロセスの作成監査イベント 4688 の ID が、コマンド ライン プロセスの監査情報が含まれますようになりました。  
  
-   Applocker イベント ログで、実行可能ファイルの SHA1/2 ハッシュは記録も  
  
    -   アプリケーションとサービス Logs\Microsoft\Windows\AppLocker  
  
-   GPO を使用して有効にするが、既定で無効になっています  
  
    -   「プロセス作成イベントにコマンド ラインを含める」  
  
![コマンド ラインの監査](media/Command-line-process-auditing/GTR_ADDS_Event4688.gif)  
  
**図 SEQ Figure \\\ * ARABIC 16 イベント 4688**  
  
REF _Ref366427278 \h 図 16 で更新されたイベント 4688 の ID を確認します。  これ以前の情報を更新**プロセスのコマンド ライン**ログに記録を取得します。  この追加のログのためことがわかることだけでなく、wscript.exe プロセス開始しましたが、[VB スクリプトを実行するために使用したもします。  
  
## <a name="configuration"></a>構成  
この更新プログラムの影響を表示するには、2 つのポリシー設定を有効にする必要があります。  
  
### <a name="you-must-have-audit-process-creation-auditing-enabled-to-see-event-id-4688"></a>プロセス作成の監査の監査イベント 4688 の ID を表示するを有効にする必要があります。  
プロセス作成の監査ポリシーを有効にするには、次のグループ ポリシーを編集します。  
  
**ポリシーの場所:**コンピューターの構成 > ポリシー > Windows の設定 > セキュリティの設定 > 高度な監査の構成 > 詳細な追跡  
  
**ポリシー名:**プロセス作成の監査  
  
**サポートされている:** Windows 7 以降  
  
**説明/ヘルプ:**  
  
このセキュリティ ポリシー設定では、オペレーティング システムは監査イベント (開始)、プロセスの作成時と、プログラムまたはそれを作成したユーザーの名前を生成するかどうかを決定します。  
  
これらの監査イベント コンピューターの使用方法を理解するのに役立つとユーザーのアクティビティを追跡します。  
  
イベント ボリューム: システムの使用状況に応じて、[中] に低  
  
**既定値:**構成されていません。  
  
### <a name="in-order-to-see-the-additions-to-event-id-4688-you-must-enable-the-new-policy-setting-include-command-line-in-process-creation-events"></a>イベント ID 4688 に追加されたものを表示するには、するために、新しいポリシー設定を有効にする必要がありますプロセス作成イベントにコマンド ラインを含める。  
**SEQ テーブル \\\ * ARABIC 19 コマンド ライン プロセスのポリシー設定**  
  
|ポリシーの構成|詳細|  
|------------------------|-----------|  
|**パス**|管理 Templates\System\Audit プロセスの作成|  
|**設定**|**プロセス作成イベントにコマンド ラインを含める**|  
|**既定の設定**|未構成 (有効になっていない)|  
|**サポートされています。**|?|  
|**説明**|このポリシー設定では、どのような情報が、新しいプロセスが作成されたときに、セキュリティ監査イベントの記録を決定します。<br /><br />この設定は、プロセス作成の監査ポリシーが有効な場合にのみ適用されます。 プロセス作成の監査イベント 4688 の一部として、セキュリティ イベント ログにプレーン テキストですべてのプロセスのコマンド ライン情報が記録されますこのポリシー設定を有効にした場合「新しいプロセスが作成されて、」このポリシー設定が適用されているワークステーションとサーバーで。<br /><br />無効にするか、またはこのポリシー設定を構成しなかった場合、プロセスのコマンド ライン情報はプロセス作成の監査イベントには含まれません。<br /><br />既定値: 未構成<br /><br />注: このポリシー設定が有効になっているときに、セキュリティ イベントはいずれかのコマンド ライン引数を正常に読み取りできる読み取りアクセス権を持つ任意のユーザー プロセスを作成します。 コマンド ライン引数は、パスワードやユーザー データなどの機密情報やプライベートの情報を含めることができます。|  
  
![コマンド ラインの監査](media/Command-line-process-auditing/GTR_ADDS_IncludeCLISetting.gif)  
  
高度な監査ポリシーの構成設定を使用する場合は、基本の監査ポリシーの設定によって、これらの設定が上書きされないことを確認する必要があります。  イベント 4719 が、設定が上書きされるときに記録されます。  
  
![コマンド ラインの監査](media/Command-line-process-auditing/GTR_ADDS_Event4719.gif)  
  
次の手順では、すべての基本の監査ポリシー設定の適用をブロックすることによって競合を回避する方法を示します。  
  
### <a name="to-ensure-that-advanced-audit-policy-configuration-settings-are-not-overwritten"></a>高度な監査ポリシーの構成設定が上書きされないことを確認するには  
![コマンド ラインの監査](media/Command-line-process-auditing/GTR_ADDS_AdvAuditPolicy.gif)  
  
1.  グループ ポリシー管理コンソールを開く  
  
2.  既定のドメイン ポリシーを右クリックし、[編集] をクリックします。  
  
3.  コンピューターの構成をダブルクリックし、[ポリシー] をダブルクリックし、[Windows の設定] をダブルクリックします。  
  
4.  セキュリティ設定をダブルクリックして、[ローカル ポリシー] をダブルクリックし、[セキュリティ オプション] をクリックします。  
  
5.  監査をダブルクリックします。監査ポリシー サブカテゴリを強制 (Windows Vista またはそれ以降) を監査ポリシー カテゴリの設定を上書きし、[このポリシー設定を定義する] をクリックします。  
  
6.  有効] をクリックし、[OK] をクリックします。  
  
## <a name="additional-resources"></a>その他のリソース  
[プロセス作成の監査](https://technet.microsoft.com/library/dd941613(v=WS.10).aspx)  
  
[セキュリティ監査ポリシーを高度な Step-by-Step Guide](https://technet.microsoft.com/library/dd408940(v=WS.10).aspx)  
  
[AppLocker: よく寄せられる質問](https://technet.microsoft.com/library/ee619725(v=ws.10).aspx)  
  
## <a name="try-this-explore-command-line-process-auditing"></a>コマンド ライン プロセスの監査を確認してください。  
  
1.  有効にする**プロセス作成の監査**イベントし、高度な監査ポリシーの構成が上書きされないことを確認  
  
2.  関心のある一部のイベントを生成するスクリプトを実行するスクリプトを作成します。  イベントを確認します。  次のように、スクリプトのレッスンのイベントを生成するために使用します。  
  
    ```  
    mkdir c:\systemfiles\temp\commandandcontrol\zone\fifthward  
    copy \\192.168.1.254\c$\hidden c:\systemfiles\temp\hidden\commandandcontrol\zone\fifthward  
    start C:\systemfiles\temp\hidden\commandandcontrol\zone\fifthward\ntuserrights.vbs  
    del c:\systemfiles\temp\*.* /Q  
    ```  
  
3.  コマンド ライン プロセスの監査を有効にします。  
  
4.  同じスクリプトを実行してイベント  
  


