---
title: fsutil dirty
description: ボリュームのダーティビットを照会または設定する fsutil dirty コマンドの参照記事。
manager: dmoss
ms.author: toklima
author: toklima
ms.assetid: 385a2a7c-d6bd-4f11-9c18-fca0413f9e97
ms.topic: article
ms.date: 10/16/2017
ms.openlocfilehash: 00fd11e577957e45bb8b2491b54cf1548effedc3
ms.sourcegitcommit: 53d526bfeddb89d28af44210a23ba417f6ce0ecf
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/06/2020
ms.locfileid: "87890002"
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

#### <a name="remarks"></a>Remarks

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

## <a name="additional-references"></a>その他の参照情報

- [コマンド ライン構文の記号](command-line-syntax-key.md)

- [fsutil](fsutil.md)
