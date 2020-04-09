---
title: mountvol
description: Windows コマンドに関するトピック * * * *-
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: fea8ad4d-f04a-4aaa-a3e5-75931e867b39
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 34a98a273274f7982bfdd970710c04178fed4f5a
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/08/2020
ms.locfileid: "80839385"
---
# <a name="mountvol"></a>mountvol



ボリュームマウントポイントを作成、削除、または一覧表示します。

このコマンドの使用方法の例については、「[例](#BKMK_examples)」を参照してください。

## <a name="syntax"></a>構文

```
mountvol [<Drive>:]<Path VolumeName>
mountvol [<Drive>:]<Path> /d
mountvol [<Drive>:]<Path> /l
mountvol [<Drive>:]<Path> /p
mountvol /r
mountvol [/n | /e]
mountvol <Drive>: /s
```

### <a name="parameters"></a>パラメーター

|パラメーター|説明|
|---------|-----------|
|[\<Drive >:]<Path>|マウントポイントが存在する既存の NTFS ディレクトリを指定します。|
|\<ボリューム >|マウントポイントのターゲットであるボリューム名を指定します。 ボリューム名は次の構文を使用します。 *GUID*はグローバル一意識別子です。</br>`\\\\?\Volume\{GUID}\`</br>かっこ {} は必須です。|
|/d|指定されたフォルダーからボリュームマウントポイントを削除します。|
|/l|指定したフォルダーのマウントされたボリューム名を一覧表示します。|
|/p|指定されたディレクトリからボリュームマウントポイントを削除し、ベーシックボリュームのマウントを解除して、ベーシックボリュームをオフラインにし、unmountable します。 他のプロセスがボリュームを使用している場合、 **mountvol**はボリュームのマウントを解除する前に開いているハンドルを閉じます。|
|/r|システムに存在しないボリュームマウントポイントのディレクトリとレジストリ設定を削除して、システムに戻されたときに、自動的にマウントされず、元のボリュームマウントポイントが割り当てられないようにします。|
|/n|新しいベーシックボリュームの自動マウントを無効にします。 新しいボリュームは、システムに追加されるときに自動的にマウントされません。|
|/e|新しいベーシックボリュームの自動マウントを再び有効にします。|
|/s|指定されたドライブに EFI システムパーティションをマウントします。|
|/?|コマンド プロンプトでヘルプを表示します。|

## <a name="remarks"></a>コメント

-   **Mountvol**を使用すると、ドライブ文字を必要とせずにボリュームをリンクすることができます。
-   **/P**を使用してマウント解除されたボリュームは、ボリュームマウントポイントが作成されるまでマウントされていないボリュームの一覧に表示されます。 ボリュームに複数のマウントポイントがある場合は、 **/d**を使用して、 **/p**を使用する前に追加のマウントポイントを削除します。 ボリュームマウントポイントを割り当てることにより、ベーシックボリュームを再びマウントできるようにすることができます。
-   ハードドライブを再フォーマットまたは交換せずにボリューム領域を拡張する必要がある場合は、別のボリュームにマウントパスを追加することができます。 複数のマウントパスで1つのボリュームを使用する利点は、1つのドライブ文字 (`C:`など) を使用してすべてのローカルボリュームにアクセスできることです。 ローカルボリュームをマウントしてドライブ文字を割り当てることもできますが、どのドライブ文字に対応するかを記憶する必要はありません。

## <a name="examples"></a><a name=BKMK_examples></a>例

マウントポイントを作成するには、次のように入力します。
```
mountvol \sysmount \\?\Volume\{2eca078d-5cbc-43d3-aff8-7e8511f60d0e}\
```

## <a name="additional-references"></a>その他の参照情報

- [コマンド ライン構文の記号](command-line-syntax-key.md)
