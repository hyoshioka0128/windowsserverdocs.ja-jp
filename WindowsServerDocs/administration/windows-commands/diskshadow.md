---
title: Diskshadow (英語の可能性あり)
description: ボリュームシャドウコピーサービス (VSS) によって提供される機能を公開するツールである、Diskshadow コマンドのリファレンス記事です。
ms.topic: article
ms.assetid: e962537d-b759-4368-b6f1-e8391cf7b221
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 3170cde50208eb54d1657ceee0c409d76ed3b806
ms.sourcegitcommit: 53d526bfeddb89d28af44210a23ba417f6ce0ecf
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/06/2020
ms.locfileid: "87890801"
---
# <a name="diskshadow"></a>Diskshadow (英語の可能性あり)

> 適用対象: Windows Server (半期チャネル)、Windows Server 2019、Windows Server 2016、Windows Server 2012 R2、Windows Server 2012

Diskshadow.exe は、ボリュームシャドウコピーサービス (VSS) によって提供される機能を公開するツールです。 既定では、Diskshadow は、Diskraid や Diskpart と同様の対話型のコマンドインタープリターを使用します。 Diskshadow には、スクリプト可能なモードも含まれています。

> [!NOTE]
> Diskshadow を実行するには、ローカルの Administrators グループのメンバーシップ、またはそれと同等のメンバーシップが最低限必要です。

## <a name="syntax"></a>構文

対話モードの場合は、コマンドプロンプトで次のように入力して、Diskshadow コマンドインタープリターを開始します。

```
diskshadow
```

スクリプトモードの場合は、次のように入力します。 *script.txt*は、Diskshadow コマンドを含むスクリプトファイルです。

```
diskshadow -s script.txt
```

### <a name="parameters"></a>パラメーター

Diskshadow コマンドインタープリターで、またはスクリプトファイルを使用して、次のコマンドを実行できます。 シャドウコピーを作成するには、少なくとも**追加**と**作成**のみが必要です。 ただし、これによってコンテキストとオプションの設定がなくなりされ、コピーバックアップが作成され、バックアップ実行スクリプトを使用せずにシャドウコピーが作成されます。

| command | 説明 |
| --------- | ----------- |
| [set コマンド](set_2.md) | シャドウコピーを作成するためのコンテキスト、オプション、詳細モード、およびメタデータファイルを設定します。 |
| [メタデータの読み込みコマンド](load-metadata.md) | 転送可能なシャドウコピーをインポートする前に、または復元の場合にライターメタデータを読み込む前に、メタデータ .cab ファイルを読み込みます。 |
| [writer コマンド](writer.md) | ライターまたはコンポーネントが含まれていること、または backup または restore プロシージャからライターまたはコンポーネントが除外されていることを確認します。 |
| [コマンドの追加](add.md) | シャドウコピーするボリュームのセットにボリュームを追加するか、エイリアス環境に別名を追加します。 |
| [create コマンド](create.md) | 現在のコンテキストとオプションの設定を使用して、シャドウコピーの作成プロセスを開始します。 |
| [exec コマンド](exec.md) | ローカルコンピューター上のファイルを実行します。 |
| [バックアップの開始コマンド](begin-backup.md) | 完全バックアップセッションを開始します。 |
| [バックアップの終了コマンド](end-backup.md) | 完全バックアップセッションを終了し、必要に応じて、適切なライター状態の**backupcomplete**イベントを発行します。 |
| [restore コマンドの開始](begin-restore.md) | 復元セッションを開始し、関連するライターに**復元前**イベントを発行します。 |
| [復元コマンドの終了](end-restore.md) | 復元セッションを終了し、関連するライターに**postrestore**イベントを発行します。 |
| [reset コマンド](reset.md) | Diskshadow を既定の状態にリセットします。 |
| [list コマンド](list.md) | システム上にあるライター、シャドウコピー、または現在登録されているシャドウコピープロバイダーの一覧を表示します。 |
| [shadows コマンドの削除](delete-shadows.md) | シャドウコピーを削除します。 |
| [import コマンド](import.md) | 読み込まれたメタデータファイルからシステムに転送可能なシャドウコピーをインポートします。 |
| [mask コマンド](mask.md) | **インポート**コマンドを使用してインポートされたハードウェアシャドウコピーを削除します。 |
| [コマンドの公開](expose.md) | は、ドライブ文字、共有、またはマウントポイントとして、永続的なシャドウコピーを公開します。 |
| [コマンドを公開しません](unexpose.md) | [**公開**] コマンドを使用して公開されたシャドウコピーを公開しません。 |
| [break コマンド](break_2.md) | VSS からシャドウコピーボリュームの関連付けを解除します。 |
| [revert コマンド](revert.md) | 指定したシャドウ コピーにボリュームを元に戻します。 |
| [exit コマンド](exit.md) | コマンドインタープリターまたはスクリプトを終了します。 |

## <a name="examples"></a>例

これは、バックアップ用にシャドウコピーを作成するコマンドのシーケンスの例です。 このファイルは、スクリプトである dsh として保存し、を使用して実行でき `diskshadow /s script.dsh` ます。

次のように想定します。

- C: diskshadowdata という名前の既存のディレクトリがあり \\ ます。

- システムボリュームは C: で、データボリュームは "d" です。

- C: diskshadowdata に backupscript .cmd ファイルがあり \\ ます。

- Backupscript. .cmd ファイルは、バックアップドライブに shadow data p: および q: のコピーを実行します。

これらのコマンドは手動で入力するか、スクリプト化することができます。

```
#Diskshadow script file
set context persistent nowriters
set metadata c:\diskshadowdata\example.cab
set verbose on
begin backup
add volume c: alias systemvolumeshadow
add volume d: alias datavolumeshadow

create

expose %systemvolumeshadow% p:
expose %datavolumeshadow% q:
exec c:\diskshadowdata\backupscript.cmd
end backup
#End of script
```

## <a name="additional-references"></a>その他の参照情報

- [コマンド ライン構文の記号](command-line-syntax-key.md)
