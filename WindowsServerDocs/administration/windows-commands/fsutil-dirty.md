---
title: fsutil dirty
description: ボリュームのダーティビットを照会または設定する fsutil dirty コマンドの参照記事。
ms.prod: windows-server
manager: dmoss
ms.author: toklima
author: toklima
ms.technology: storage
ms.assetid: 385a2a7c-d6bd-4f11-9c18-fca0413f9e97
ms.topic: article
ms.date: 10/16/2017
ms.openlocfilehash: cb133dc9f9f19a948eb88d24935fac27f2a5e4a3
ms.sourcegitcommit: 145cf75f89f4e7460e737861b7407b5cee7c6645
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/29/2020
ms.locfileid: "87409733"
---
# <a name="fsutil-dirty"></a>fsutil dirty

> 適用対象: Windows Server (半期チャネル)、Windows Server 2019、Windows Server 2016、Windows 10、Windows Server 2012 R2、Windows 8.1、Windows Server 2012、Windows 8

ボリュームのダーティビットを照会または設定します。 ボリュームのダーティビットが設定されている場合、 **autochk**は、次回コンピューターを再起動したときに、ボリュームにエラーがないかどうかを自動的にチェックします。

## <a name="syntax"></a>構文

```
fsutil dirty {query | set} <volumepath>
```

### <a name="parameters"></a>パラメーター

| パラメーター | 説明 |
| --------- | ----------- |
| query | 指定されたボリュームのダーティビットを照会します。 |
| set | 指定されたボリュームのダーティビットを設定します。 |
| `<volumepath>` | ドライブ名の後にコロンまたは GUID を指定します。次の形式で指定し `volume{GUID}` ます。 |

#### <a name="remarks"></a>解説

- ボリュームのダーティビットは、ファイルシステムが不整合な状態にある可能性があることを示します。 次の理由により、ダーティビットを設定できます。

    - ボリュームがオンラインであり、未処理の変更があります。

    - 変更がディスクにコミットされる前に、ボリュームに変更が加えられ、コンピューターがシャットダウンされました。

    - ボリュームで破損が検出されました。

- コンピューターの再起動時にダーティビットが設定されている場合、 **chkdsk**を実行してファイルシステムの整合性を検証し、ボリュームに関する問題を修正します。

### <a name="examples"></a>例

ドライブ C のダーティビットに対してクエリを実行するには、次のように入力します。

```
fsutil dirty query c:
```

- ボリュームがダーティの場合、次の出力が表示されます。`Volume C: is dirty`

- ボリュームがダーティでない場合は、次の出力が表示されます。`Volume C: is not dirty`

ドライブ C にダーティビットを設定するには、次のように入力します。

```
fsutil dirty set C:
```

## <a name="additional-references"></a>その他のリファレンス

- [コマンド ライン構文の記号](command-line-syntax-key.md)

- [fsutil](fsutil.md)
