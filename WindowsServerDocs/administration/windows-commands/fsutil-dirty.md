---
ms.assetid: 385a2a7c-d6bd-4f11-9c18-fca0413f9e97
title: Fsutil ダーティ
ms.prod: windows-server
manager: dmoss
ms.author: toklima
author: toklima
ms.technology: storage
audience: IT Pro
ms.topic: article
ms.date: 10/16/2017
ms.openlocfilehash: 3b35938c21180199aabb74431d20a31167aea706
ms.sourcegitcommit: ab64dc83fca28039416c26226815502d0193500c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/01/2020
ms.locfileid: "82725536"
---
# <a name="fsutil-dirty"></a>Fsutil ダーティ
> 適用対象: Windows Server (半期チャネル)、Windows Server 2019、Windows Server 2016、Windows 10、Windows Server 2012 R2、Windows 8.1、Windows Server 2012、Windows 8、Windows Server 2008 R2、Windows 7

ボリュームのダーティビットを照会または設定します。 ボリュームのダーティビットが設定されている場合、 **autochk**は、次回コンピューターを再起動したときに、ボリュームにエラーがないかどうかを自動的にチェックします。



## <a name="syntax"></a>構文

```
fsutil dirty {query | set} <VolumePath>
```

### <a name="parameters"></a>パラメーター

|   パラメーター   |                                                 [説明]                                                  |
|---------------|--------------------------------------------------------------------------------------------------------------|
|     query     |                                  指定されたボリュームのダーティビットを照会します。                                   |
|      set      |                                    指定されたボリュームのダーティビットを設定します。                                    |
| \<VolumePath> | ドライブ名の後にコロンまたは GUID を指定します。次の形式で指定します:**ボリューム {**<em>guid</em>**}**。 |

## <a name="remarks"></a>Remarks

-   ボリュームのダーティビットは、ファイルシステムが不整合な状態にある可能性があることを示します。 次の理由により、ダーティビットを設定できます。

    -   ボリュームがオンラインであり、未処理の変更があります。

    -   変更がディスクにコミットされる前に、ボリュームに変更が加えられ、コンピューターがシャットダウンされました。

    -   ボリュームで破損が検出されました。

-   コンピューターの再起動時にダーティビットが設定されている場合、 **chkdsk**を実行してファイルシステムの整合性を検証し、ボリュームに関する問題を修正します。

## <a name="examples"></a><a name="BKMK_examples"></a>例
ドライブ C のダーティビットに対してクエリを実行するには、次のように入力します。

```
fsutil dirty query c:
```

-   ボリュームがダーティの場合、次の出力が表示されます。

    `Volume C: is dirty`

-   ボリュームがダーティでない場合は、次の出力が表示されます。

    `Volume C: is not dirty`

ドライブ C にダーティビットを設定するには、次のように入力します。

```
fsutil dirty set C:
```

## <a name="additional-references"></a>その他のリファレンス
- [コマンド ライン構文の記号](command-line-syntax-key.md)

[Fsutil](Fsutil.md)


