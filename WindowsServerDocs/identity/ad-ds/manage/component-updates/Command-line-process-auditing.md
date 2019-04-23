---
ms.assetid: c8597cc8-bdcb-4e59-a09e-128ef5ebeaf8
title: コマンド ライン プロセスの監査
description: ''
author: MicrosoftGuyJFlo
ms.author: joflore
manager: mtillman
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adds
ms.openlocfilehash: 66ae6992775319cf614b0cb4c21f864150746687
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/17/2019
ms.locfileid: "59859553"
---
# <a name="command-line-process-auditing"></a>コマンド ライン プロセスの監査

>適用先:Windows Server 2016、Windows Server 2012 R2

**作成者**:Justin Turner、シニア サポート エスカレーション エンジニア、Windows グループ  
  
> [!NOTE]  
> この内容は Microsoft カスタマー サポート エンジニアによって作成され、TechNet が通常提供しているトピックよりも詳細な Windows Server 2012 R2 の機能やソリューションの技術的説明を求めている、経験豊かな管理者とシステム設計者を対象としています。 ただし、TechNet と同様の編集過程は実施されていないため、言語によっては通常より洗練されていない文章が見られる場合があります。  
  
## <a name="overview"></a>概要  
  
-   既存のプロセス作成監査イベント 4688 の ID には、今すぐコマンド ライン プロセスの監査情報が含まれます。  
  
-   Applocker イベント ログに実行可能ファイルの SHA1/2 のハッシュもログには  
  
    -   アプリケーションとサービス Logs\Microsoft\Windows\AppLocker  
  
-   GPO を使用して有効にしたが、既定で無効になっています  
  
    -   「プロセス作成イベントにコマンドラインを含める」  
  
![コマンドラインの監査](media/Command-line-process-auditing/GTR_ADDS_Event4688.gif)  
  
**図 SEQ 図\\\*アラビア 16 イベント 4688**  
  
REF _Ref366427278 \h 図 16 で更新されるイベント ID 4688 を確認します。  この更新プログラムの前の情報のいずれも**プロセス コマンド ライン**ログに記録を取得します。  この追加のログ記録のためだけでなく、wscript.exe プロセスの開始が、VB スクリプトを実行するために使用もが今すぐ確認できます。  
  
## <a name="configuration"></a>構成  
この更新プログラムの効果を確認するには、2 つのポリシー設定を有効にする必要があります。  
  
### <a name="you-must-have-audit-process-creation-auditing-enabled-to-see-event-id-4688"></a>プロセス作成の監査のイベント ID 4688 の参照を有効になっている監査が必要です。  
プロセス作成の監査ポリシーを有効にするには、次のグループ ポリシーを編集します。  
  
**ポリシーの場所:** コンピューターの構成 > ポリシー > Windows の設定 > セキュリティ設定 > 監査の構成の詳細 > 追跡の詳細  
  
**ポリシー名:** プロセス作成の監査  
  
**サポートされています。** Windows 7 以降  
  
**説明/ヘルプ:**  
  
このセキュリティ ポリシーの設定は、オペレーティング システムがプロセスには (開始) が作成されると、監査イベントと、プログラムまたは作成したユーザーの名前を生成するかどうかを判断します。  
  
これらのイベントの監査、コンピューターの使用方法を理解するのに役立つとユーザーの利用状況を追跡するためにします。  
  
イベント ボリューム:低 ~ 中、システムの使用状況に応じて  
  
**既定値:** 未構成  
  
### <a name="in-order-to-see-the-additions-to-event-id-4688-you-must-enable-the-new-policy-setting-include-command-line-in-process-creation-events"></a>イベント ID 4688 への追加を確認するためには、新しいポリシー設定を有効にする必要があります。プロセス作成イベントにコマンド ラインを含める  
**SEQ テーブル\\\*アラビア語の 19 コマンド ライン プロセスのポリシー設定**  
  
|ポリシーの構成|詳細|  
|------------------------|-----------|  
|**[パス]**|管理 Templates\System\Audit プロセスの作成|  
|**設定**|**プロセス作成イベントにコマンドラインを含める**|  
|**既定の設定**|未構成 (無効)|  
|**サポートされています。**|?|  
|**説明**|このポリシー設定では、新しいプロセスの作成時にセキュリティ監査イベントのログに記録する情報を決定します。<br /><br />この設定は、プロセス作成の監査ポリシーが有効な場合にのみ適用されます。 このポリシー設定を有効にした場合、このポリシー設定が適用されているワークステーションやサーバーでは、各プロセスのコマンド ライン情報が、プロセス作成の監査イベント 4688 "新しいプロセスの作成" の一部としてテキスト形式でセキュリティ イベント ログに記録されます。<br /><br />このポリシー設定を無効にした場合、または構成しなかった場合、プロセスのコマンド ライン情報はプロセス作成の監査イベントに含まれません。<br /><br />既定:未構成<br /><br />注:このポリシー設定を有効にすると、いずれかのコマンドライン引数を正常に読み取られたことが、セキュリティ イベントの読み取りアクセス権を持つすべてのユーザーは、プロセスを作成します。 コマンド ライン引数には、パスワードやユーザー データなどの機密性の高い情報や個人情報を含めることができます。|  
  
![コマンドラインの監査](media/Command-line-process-auditing/GTR_ADDS_IncludeCLISetting.gif)  
  
高度な監査ポリシーの構成設定を使用する場合は、これらの設定が、基本的な監査ポリシーの設定によって上書きされないことを確認する必要があります。  設定が上書きされると、4719 イベントが記録されます。  
  
![コマンドラインの監査](media/Command-line-process-auditing/GTR_ADDS_Event4719.gif)  
  
すべての基本の監査ポリシーの設定からアプリケーションをブロックして競合を防ぐ方法を、次の手順に示します。  
  
### <a name="to-ensure-that-advanced-audit-policy-configuration-settings-are-not-overwritten"></a>監査ポリシーの詳細な構成の設定が上書きされていないことを確認するには  
![コマンドラインの監査](media/Command-line-process-auditing/GTR_ADDS_AdvAuditPolicy.gif)  
  
1.  グループ ポリシー管理コンソールを開く  
  
2.  既定のドメイン ポリシーを右クリックし、[編集] をクリックします。  
  
3.  コンピューターの構成をダブルクリックし、[ポリシー] をダブルクリックし、[Windows 設定] をダブルクリックします。  
  
4.  セキュリティ設定 をダブルクリック、ローカル ポリシー をダブルクリックし、セキュリティ オプション をクリックします。  
  
5.  監査をダブルクリックします。強制的に監査ポリシー サブカテゴリ設定 (Windows Vista またはそれ以降) を監査ポリシー カテゴリの設定をオーバーライドし、このポリシー設定を定義する順にクリックします。  
  
6.  有効 をクリックし、ok をクリックします。  
  
## <a name="additional-resources"></a>その他のリソース  
[プロセス作成の監査](https://technet.microsoft.com/library/dd941613(v=WS.10).aspx)  
  
[セキュリティ監査ポリシーのステップ バイ ステップ ガイドの詳細](https://technet.microsoft.com/library/dd408940(v=WS.10).aspx)  
  
[AppLocker:よく寄せられる質問](https://technet.microsoft.com/library/ee619725(v=ws.10).aspx)  
  
## <a name="try-this-explore-command-line-process-auditing"></a>これを試してください。コマンド ライン プロセスの監査を詳細します。  
  
1.  有効にする**プロセス作成の監査**イベント、高度な監査ポリシーの構成が上書きされないように、  
  
2.  関心のある一部のイベントを生成し、スクリプトを実行するスクリプトを作成します。  イベントを確認します。  次のように、レッスンでは、イベントを生成するためのスクリプト。  
  
    ```  
    mkdir c:\systemfiles\temp\commandandcontrol\zone\fifthward  
    copy \\192.168.1.254\c$\hidden c:\systemfiles\temp\hidden\commandandcontrol\zone\fifthward  
    start C:\systemfiles\temp\hidden\commandandcontrol\zone\fifthward\ntuserrights.vbs  
    del c:\systemfiles\temp\*.* /Q  
    ```  
  
3.  コマンド ライン プロセスの監査を有効にします。  
  
4.  以前と同じスクリプトを実行し、イベントを確認します  
  


