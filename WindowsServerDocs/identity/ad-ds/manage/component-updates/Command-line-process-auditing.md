---
ms.assetid: c8597cc8-bdcb-4e59-a09e-128ef5ebeaf8
title: コマンド ライン プロセスの監査
author: MicrosoftGuyJFlo
ms.author: joflore
manager: mtillman
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server
ms.technology: identity-adds
ms.openlocfilehash: 5ca29f1eef61bd11b2ceede4f335c029412e7331
ms.sourcegitcommit: d5e27c1f2f168a71ae272bebf8f50e1b3ccbcca3
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/23/2020
ms.locfileid: "86966404"
---
# <a name="command-line-process-auditing"></a>コマンド ライン プロセスの監査

>適用対象: Windows Server 2016 の場合は Windows Server 2012 R2

**Author**: Justin 書籍、シニアサポートエスカレーションエンジニア (Windows グループ)  
  
> [!NOTE]  
> この内容は Microsoft カスタマー サポート エンジニアによって作成され、TechNet が通常提供しているトピックよりも詳細な Windows Server 2012 R2 の機能やソリューションの技術的説明を求めている、経験豊かな管理者とシステム設計者を対象としています。 ただし、TechNet と同様の編集過程は実施されていないため、言語によっては通常より洗練されていない文章が見られる場合があります。  
  
## <a name="overview"></a>概要  
  
-   既存のプロセス作成監査イベント ID 4688 に、コマンドラインプロセスの監査情報が含まれるようになりました。  
  
-   また、Applocker イベントログの実行可能ファイルの SHA1/2 ハッシュもログに記録されます。  
  
    -   アプリケーションとサービス Logs\Microsoft\Windows\AppLocker  
  
-   GPO を使用して有効にしますが、既定では無効になっています。  
  
    -   "プロセス作成イベントにコマンドラインを含める"  
  
![コマンドラインによる監査](media/Command-line-process-auditing/GTR_ADDS_Event4688.gif)  
  
**図 SEQ 図 \\ \* アラビア語16イベント4688**  
  
参照 _Ref366427278 \h 図16で更新されたイベント ID 4688 を確認します。  この更新の前に、**プロセスのコマンドライン**の情報はログに記録されません。  このログの追加により、wscript.exe プロセスが開始されただけでなく、VB スクリプトの実行にも使用されていることがわかります。  
  
## <a name="configuration"></a>構成  
この更新プログラムの影響を確認するには、2つのポリシー設定を有効にする必要があります。  
  
### <a name="you-must-have-audit-process-creation-auditing-enabled-to-see-event-id-4688"></a>イベント ID 4688 を確認するには、監査プロセス作成の監査が有効になっている必要があります。  
プロセス作成ポリシーの監査を有効にするには、次のグループポリシーを編集します。  
  
**ポリシーの場所:** コンピューターの構成 > ポリシー > Windows の設定 > セキュリティ設定 > 高度な監査の構成 > 詳細な追跡  
  
**ポリシー名:** プロセス作成の監査  
  
**サポート対象:** Windows 7 以降  
  
**説明/ヘルプ:**  
  
このセキュリティポリシー設定では、プロセスの作成時にオペレーティングシステムが監査イベントを生成するかどうかを決定します ([開始]) と、作成したプログラムまたはユーザーの名前。  
  
これらの監査イベントは、コンピューターがどのように使用されているかを理解し、ユーザーの利用状況を追跡するのに役立ちます。  
  
イベント ボリューム: システムの使用状況に応じて、低から中  
  
**既定値:** 未構成  
  
### <a name="in-order-to-see-the-additions-to-event-id-4688-you-must-enable-the-new-policy-setting-include-command-line-in-process-creation-events"></a>イベント ID 4688 への追加を確認するには、新しいポリシー設定を有効にする必要があります。 [コマンドラインをプロセス作成イベントに含める]  
**テーブル SEQ テーブル \\ \* アラビア19コマンドラインプロセスポリシー設定**  
  
|ポリシーの構成|詳細|  
|------------------------|-----------|  
|**パス**|管理用システム \ システムの監査プロセスの作成|  
|**設定**|**プロセス作成イベントにコマンド ラインを含める**|  
|**既定の設定**|構成されていません (有効ではありません)|  
|**以下でサポートされています。**|?|  
|**説明**|このポリシー設定では、新しいプロセスの作成時にセキュリティ監査イベントのログに記録する情報を決定します。<p>この設定は、プロセス作成の監査ポリシーが有効な場合にのみ適用されます。 このポリシー設定を有効にした場合、このポリシー設定が適用されているワークステーションやサーバーでは、各プロセスのコマンド ライン情報が、プロセス作成の監査イベント 4688 "新しいプロセスの作成" の一部としてテキスト形式でセキュリティ イベント ログに記録されます。<p>このポリシー設定を無効にした場合、または構成しなかった場合、プロセスのコマンド ライン情報はプロセス作成の監査イベントに含まれません。<p>既定: 構成されていません<p>注: このポリシー設定を有効にすると、セキュリティイベントを読み取るアクセス権を持つすべてのユーザーは、正常に作成されたプロセスのコマンドライン引数を読み取ることができます。 コマンド ライン引数には、パスワードやユーザー データなどの機密性の高い情報や個人情報を含めることができます。|  
  
![コマンドラインによる監査](media/Command-line-process-auditing/GTR_ADDS_IncludeCLISetting.gif)  
  
[監査ポリシーの詳細な構成] 設定を使用する場合は、これらの設定が基本の監査ポリシーの設定によって上書きされていないことを確認する必要があります。  設定が上書きされると、イベント4719がログに記録されます。  
  
![コマンドラインによる監査](media/Command-line-process-auditing/GTR_ADDS_Event4719.gif)  
  
すべての基本の監査ポリシーの設定からアプリケーションをブロックして競合を防ぐ方法を、次の手順に示します。  
  
### <a name="to-ensure-that-advanced-audit-policy-configuration-settings-are-not-overwritten"></a>監査ポリシーの詳細な構成の設定が上書きされていないことを確認するには  
![コマンドラインによる監査](media/Command-line-process-auditing/GTR_ADDS_AdvAuditPolicy.gif)  
  
1.  グループポリシー管理コンソールを開きます。  
  
2.  [既定のドメイン ポリシー] を右クリックし、[編集] をクリックします。  
  
3.  [コンピューターの構成]、 [ポリシー]、 [Windows の設定]の順にダブルクリックします。  
  
4.  [セキュリティの設定] をダブルクリックし、[ローカルポリシー] をダブルクリックして、[セキュリティオプション] をクリックします。  
  
5.  [監査: 監査ポリシーのカテゴリ設定を上書きするよう、監査ポリシーのサブカテゴリ設定を強制する (Windows Vista 以降)]をダブルクリックし、 [このポリシーの設定を定義する]をクリックします。  
  
6.  [ 有効] をクリックしてから、[ OK] をクリックします。  
  
## <a name="additional-resources"></a>その他の情報  
[プロセス作成の監査](/previous-versions/windows/it-pro/windows-server-2008-R2-and-2008/dd941613(v=ws.10))  
  
[セキュリティ監査ポリシーのステップ バイ ステップ ガイドの詳細](/previous-versions/windows/it-pro/windows-server-2008-R2-and-2008/dd408940(v=ws.10))  
  
[AppLocker: よく寄せられる質問](/previous-versions/windows/it-pro/windows-server-2008-R2-and-2008/ee619725(v=ws.10))  
  
## <a name="try-this-explore-command-line-process-auditing"></a>試してみよう: コマンドラインプロセスの監査を調べる  
  
1.  **プロセス作成**イベントの監査を有効にし、高度な監査ポリシーの構成が上書きされないようにする  
  
2.  目的のイベントを生成し、スクリプトを実行するスクリプトを作成します。  イベントを観察します。  レッスンでイベントを生成するために使用されるスクリプトは、次のようになります。  
  
    ```  
    mkdir c:\systemfiles\temp\commandandcontrol\zone\fifthward  
    copy \\192.168.1.254\c$\hidden c:\systemfiles\temp\hidden\commandandcontrol\zone\fifthward  
    start C:\systemfiles\temp\hidden\commandandcontrol\zone\fifthward\ntuserrights.vbs  
    del c:\systemfiles\temp\*.* /Q  
    ```  
  
3.  コマンドラインプロセスの監査を有効にする  
  
4.  前と同じスクリプトを実行して、イベントを観察します。  
  
