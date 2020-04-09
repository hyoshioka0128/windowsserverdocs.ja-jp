---
title: diskshadow
description: Diskshadow の Windows コマンドに関するトピック。これは、ボリュームシャドウコピーサービス (VSS) によって提供される機能を公開するツールです。
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: e962537d-b759-4368-b6f1-e8391cf7b221
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 5ded552394b7cf6001929ad4a639e89a660bb09c
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/08/2020
ms.locfileid: "80845395"
---
# <a name="diskshadow"></a>diskshadow

>適用対象: Windows Server (半期チャネル)、Windows Server 2016、Windows Server 2012 R2、Windows Server 2012

diskshadow は、ボリュームシャドウコピーサービス (VSS) によって提供される機能を公開するツールです。 既定では、diskshadow は、diskraid や DiskPart と同様の対話型のコマンドインタープリターを使用します。 diskshadow には、スクリプト可能なモードも含まれています。  
  
> [!NOTE]  
> Diskshadow を実行するには、ローカルの Administrators グループのメンバーシップ、またはそれと同等のメンバーシップが最低限必要です。  
  
Diskshadow コマンドの使用方法の例については、「[例](#BKMK_examples)」を参照してください。  
  
## <a name="syntax"></a>構文  
対話モードの場合は、コマンドプロンプトで次のように入力して、diskshadow コマンドインタープリターを開始します。  
  
```  
diskshadow  
```  
  
スクリプトモードで、次のように入力し*ます。* ここで、test.txt は、diskshadow コマンドを含むスクリプトファイルです。  
  
```  
diskshadow -s script.txt  
```  
  
## <a name="diskshadow-commands"></a>diskshadow コマンド  
Diskshadow コマンドインタープリターで、またはスクリプトファイルを使用して、次のコマンドを実行できます。  
  
|パラメーター|説明|  
|-------|--------|  
|[set_2](set_2.md)|シャドウコピーを作成するためのコンテキスト、オプション、詳細モード、およびメタデータファイルを設定します。|  
|[復元のシミュレーション](simulate-restore.md)|発行することがなく、コンピューター上の復元のセッション内のライターをテスト **復元前** または **PostRestore** ライターへのイベントです。|  
|[メタデータの読み込み](load-metadata.md)|転送可能なシャドウコピーをインポートする前に、または復元の場合にライターメタデータを読み込む前に、メタデータ .cab ファイルを読み込みます。|  
|[ライター](writer.md)|ライターまたはコンポーネントが含まれていること、または backup または restore プロシージャからライターまたはコンポーネントが除外されていることを確認します。|  
|[add](add.md)|シャドウコピーするボリュームのセットにボリュームを追加するか、エイリアス環境に別名を追加します。|  
|[create_1](create_1.md)|現在のコンテキストとオプションの設定を使用して、シャドウコピーの作成プロセスを開始します。|  
|[実行](exec.md)|ローカルコンピューター上のファイルを実行します。|  
|[バックアップの開始](begin-backup.md)|完全バックアップセッションを開始します。|  
|[バックアップの終了](end-backup.md)|完全バックアップセッションを終了し、必要に応じて、適切なライター状態の**Backupcomplete**イベントを発行します。|  
|[復元の開始](begin-restore.md)|復元セッションを開始し、関連するライターに**復元前**イベントを発行します。|  
|[復元の終了](end-restore.md)|復元セッションを終了し、関連するライターに**postrestore**イベントを発行します。|  
|[reset](reset.md)|diskshadow を既定の状態にリセットします。|  
|[表](list.md)|システム上にあるライター、シャドウコピー、または現在登録されているシャドウコピープロバイダーの一覧を表示します。|  
|[影の削除](delete-shadows.md)|シャドウコピーを削除します。|  
|[インポート](import.md)|読み込まれたメタデータファイルからシステムに転送可能なシャドウコピーをインポートします。|  
|[隠す](mask.md)|**インポート**コマンドを使用してインポートされたハードウェアシャドウコピーを削除します。|  
|[さらす](expose.md)|は、ドライブ文字、共有、またはマウントポイントとして、永続的なシャドウコピーを公開します。|  
|[を非公開](unexpose.md)|**[公開]** コマンドを使用して公開されたシャドウコピーを公開しません。|  
|[break_2](break_2.md)|VSS からシャドウコピーボリュームの関連付けを解除します。|  
|[反転](revert.md)|指定したシャドウコピーにボリュームを戻します。|  
|[exit_1](exit_1.md)|diskshadow を終了します。|  
  
## <a name="remarks"></a>コメント  
  
-   シャドウコピーを作成するには、少なくとも**追加**と**作成**のみが必要です。 ただし、これによってコンテキストとオプションの設定がプランされ、コピーバックアップが作成されます。バックアップ実行スクリプトを使用しない場合にのみ、シャドウコピーが作成されます。  
  
## <a name="examples"></a><a name=BKMK_examples></a>例  
これは、バックアップ用にシャドウコピーを作成するコマンドのシーケンスの例です。 これは、スクリプトとしてファイルに保存し、diskshadow \/s スクリプトを使用して実行できます。  
  
次のように想定します。  
  
-   C:\\diskshadowdata という名前の既存のディレクトリがあります。  
  
-   システムボリュームは C: で、データボリュームは "d" です。  
  
-   C:\\diskshadowdata に backupscript .cmd ファイルがあります。  
  
-   Backupscript. .cmd ファイルは、バックアップドライブに shadow data p: および q: のコピーを実行します。  
  
これらのコマンドは手動で入力するか、スクリプト化することができます。  
  
```  
#diskshadow script file  
set context persistent nowriters  
set metadata c:\diskshadowdata\example.cab  
set verbose on  
begin backup  
add volume c: alias Systemvolumeshadow  
add volume d: alias Datavolumeshadow  
  
create  
  
expose %Systemvolumeshadow% p:  
expose %Datavolumeshadow% q:  
exec c:\diskshadowdata\backupscript.cmd  
end backup  
#End of script  
```  
  
## <a name="additional-references"></a>その他の参照情報  
- [コマンド ライン構文の記号](command-line-syntax-key.md)  
  

