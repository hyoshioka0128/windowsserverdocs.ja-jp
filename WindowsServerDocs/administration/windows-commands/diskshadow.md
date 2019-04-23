---
title: diskshadow
description: 'Windows コマンド」のトピック * * *- '
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: e962537d-b759-4368-b6f1-e8391cf7b221
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: b2c5648235a1c856c6aef09621e2381e74d08d70
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/17/2019
ms.locfileid: "59869183"
---
# <a name="diskshadow"></a>diskshadow

>適用先:Windows Server (半期チャネル)、Windows Server 2016、Windows Server 2012 R2、Windows Server 2012

diskshadow.exe はボリューム シャドウ コピー サービスによって提供される機能を公開するツール\(VSS\)します。 既定では、diskshadow は diskraid または DiskPart に似た対話型コマンド インタープリターを使用します。 diskshadow には、スクリプト可能なモードも含まれています。  
  
> [!NOTE]  
> ローカルの Administrators グループ、またはそれと同等のメンバーシップは、diskshadow の実行に必要な最小値です。  
  
diskshadow のコマンドを使用する方法の例については、次を参照してください。[例](#BKMK_examples)します。  
  
## <a name="syntax"></a>構文  
対話型モードの場合は、diskshadow コマンド インタープリターを開始するコマンド プロンプトで、次を入力します。  
  
```  
diskshadow  
```  
  
スクリプト モードの場合、以下の入力場所*script.txt* diskshadow のコマンドを含むスクリプト ファイルには。  
  
```  
diskshadow -s script.txt  
```  
  
## <a name="diskshadow-commands"></a>diskshadow コマンド  
またはスクリプト ファイルを diskshadow コマンド インタープリターでは、次のコマンドを実行できます。  
  
|パラメーター|説明|  
|-------|--------|  
|[set_2](set_2.md)|コンテキスト、オプション、詳細出力モード、およびシャドウ コピーを作成するためのメタデータ ファイルを設定します。|  
|[復元をシミュレートします](simulate-restore.md)|発行することがなく、コンピューター上の復元のセッション内のライターをテスト **復元前** または **PostRestore** ライターへのイベントです。|  
|[メタデータを読み込み](load-metadata.md)|移動可能なシャドウ コピーをインポートする前に、メタデータの .cab ファイルの読み込みまたは復元の場合、ライター メタデータを読み込みます。|  
|[ライター](writer.md)|ライターまたはコンポーネントが含まれるか、バックアップまたは復元の手順からライターまたはコンポーネントを除外することを確認します。|  
|[add_1](add_1.md)|シャドウ コピー、ボリュームのセットにボリュームを追加するか、別名環境にエイリアスを追加します。|  
|[create_1](create_1.md)|現在のコンテキストとオプションの設定を使用して、シャドウ コピーの作成プロセスを開始します。|  
|[exec](exec.md)|ローカル コンピューター上のファイルを実行します。|  
|[バックアップを開始します。](begin-backup.md)|完全バックアップのセッションを開始します。|  
|[末尾のバックアップ](end-backup.md)|完全バックアップのセッションとの問題を終了、 **Backupcomplete**イベントが必要な場合は、適切なライターの状態。|  
|[復元を開始します。](begin-restore.md)|復元セッションとの問題を開始、**復元前**イベントに関連するライター。|  
|[最後の復元](end-restore.md)|復元セッションとの問題を終了、 **PostRestore**イベントに関連するライター。|  
|[reset](reset.md)|diskshadow を既定の状態にリセットします。|  
|[list](list.md)|ライター、シャドウ コピー、または現在登録されているシャドウ コピー プロバイダーは、システム上にあるを一覧表示します。|  
|[影を削除します。](delete-shadows.md)|シャドウ コピーを削除します。|  
|[import](import.md)|システムに読み込まれたメタデータ ファイルからの移植可能なシャドウ コピーをインポートします。|  
|[マスク](mask.md)|使用してインポートされたハードウェアのシャドウ コピーを削除、**インポート**コマンド。|  
|[expose](expose.md)|ドライブ文字、共有、またはマウント ポイントとして永続的なシャドウ コピーを公開します。|  
|[unexpose](unexpose.md)|使用して公開されたシャドウ コピーを unexposes、**公開**コマンド。|  
|[break_2](break_2.md)|Vss シャドウ コピー ボリュームの関連付けを解除します。|  
|[元に戻す](revert.md)|指定したシャドウ コピーにボリュームを元に戻します。|  
|[exit_1](exit_1.md)|diskshadow を終了します。|  
  
## <a name="remarks"></a>注釈  
  
-   少なくとものみ**追加**と**作成**シャドウ コピーを作成するために必要な。 ただし、コンテキストとオプションの設定を申し立ててはこれ、バックアップのコピーになります、バックアップの実行スクリプトなしでのみシャドウ コピーが作成されます。  
  
## <a name="BKMK_examples"></a>例  
これは、バックアップ シャドウ コピーを作成するコマンドのシーケンスの例です。 Script.dsh、としてファイルに保存され diskshadow を使用して実行するには、その\/s script.dsh  
  
次のものとします。  
  
-   C: と呼ばれる既存のディレクトリがある\\diskshadowdata します。  
  
-   システム ボリュームが c: とデータ量は d: です。  
  
-   C: backupscript.cmd ファイルがある\\diskshadowdata します。  
  
-   Backupscript.cmd ファイルでは、シャドウ データ p: とに、バックアップ ドライブ q: のコピーを実行します。  
  
これらのコマンドを手動で入力するか、スクリプト化。  
  
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
  
#### <a name="additional-references"></a>その他の参照  
[コマンドライン構文キー](command-line-syntax-key.md)  
  

