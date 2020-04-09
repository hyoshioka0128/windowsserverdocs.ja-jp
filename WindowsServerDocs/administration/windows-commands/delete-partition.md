---
title: delete partition
description: パーティションの削除に関する Windows コマンドのトピック。フォーカスのあるパーティションを削除します。
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 65752312-cb16-46f6-870f-1b95c507b101
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: a24c18cf98f2899fbb57f1f5f2d2776824d637b7
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/08/2020
ms.locfileid: "80846575"
---
# <a name="delete-partition"></a>delete partition

フォーカスがあるパーティションを削除します。

## <a name="syntax"></a>構文

```
delete partition [noerr] [override]
```

### <a name="parameters"></a>パラメーター

|パラメーター|説明|
|---------|-----------|
|override|パーティションの種類にかかわらず、DiskPart ですべてのパーティションを削除できるようにします。 通常、DiskPart では既知のデータパーティションのみを削除できます。|
|noerr|スクリプト専用です。 エラーが発生しても、エラーが発生しなかったかのように DiskPart はコマンドの処理を続けます。 このパラメーターは、エラー発生すると、DiskPart はエラー コードを生成して終了します。|

## <a name="remarks"></a>コメント

> [!CAUTION]
> ダイナミックディスク上のパーティションを削除すると、ディスク上のすべてのダイナミックボリュームが削除されるため、データが破棄され、ディスクが破損状態のままになります。 ダイナミックボリュームを削除するには、代わりに **[ボリュームの削除]** コマンドを常に使用します。 パーティションはダイナミックディスクから削除できますが、作成することはできません。 たとえば、ダイナミック GPT ディスクで認識されない GUID パーティション テーブル (GPT) パーティションを削除することはできます。 このようなパーティションを削除しても、結果として得られる空き領域が使用できなくなることはありません。 このコマンドは、DiskPart の**clean**コマンドを使用できない緊急の状況で、破損したオフラインダイナミックディスク上の領域を再利用できるようにするためのものです。
> -   システムパーティション、ブートパーティション、またはアクティブなページングファイルやクラッシュダンプ情報が含まれているパーティションを削除することはできません。
> -   この操作を正常に実行するには、パーティションを選択する必要があります。 **[パーティションの選択**] コマンドを使用してパーティションを選択し、それにフォーカスを移動します。

## <a name="examples"></a><a name=BKMK_examples></a>例

フォーカスのあるパーティションを削除するには、次のように入力します。
```
delete partition
```

## <a name="additional-references"></a>その他の参照情報

- [コマンド ライン構文の記号](command-line-syntax-key.md)

