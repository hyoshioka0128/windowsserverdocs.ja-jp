---
title: reg 復元
description: '* * * * のリファレンストピック'
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: a51f1c0c-969b-4b76-930a-c8bb14dea26e
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 4d490f99f032b38c8bbbe9352b8571b4a85202e1
ms.sourcegitcommit: ab64dc83fca28039416c26226815502d0193500c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/01/2020
ms.locfileid: "82722520"
---
# <a name="reg-restore"></a>reg 復元



書き込みが保存されたサブキーとエントリは、レジストリをバックアップします。



## <a name="syntax"></a>構文

```
Reg restore <KeyName> <FileName>
```

### <a name="parameters"></a>パラメーター

|パラメーター|[説明]|
|---------|-----------|
|\<KeyName>|復元するサブキーの完全なパスを指定します。 復元操作は、ローカル コンピューターでのみ機能します。 られているキー名では、有効なルート キーを含める必要があります。 有効なルート キー: HKLM、HKCU、HKCR、HKU、および HKCC します。|
|\<ファイル名>|レジストリに書き込まれるコンテンツを含むファイルのパスと名前を指定します。 このファイルはで事前に作成する必要があります、 **reg 保存** .hiv 拡張機能を使用して操作します。|
|/?|ヘルプを表示 **reg 復元** コマンド プロンプト。|

## <a name="remarks"></a>Remarks

-   すべてのレジストリ エントリを編集する前に保存された親サブキー、 **reg 保存** 操作します。 復元と元のサブキーの編集に失敗した場合、 **reg 復元** 操作します。
-   次の表に、戻り値の **reg 復元** 操作します。

|値|[説明]|
|-----|-----------|
|0|Success|
|1|障害|

## <a name="examples"></a>例

キー、HKLM\Software\Microsoft\ResKit NTRKBkUp.hiv をという名前のファイルを復元し、キーの既存の内容を上書きする、次のように入力します。
```
REG RESTORE HKLM\Software\Microsoft\ResKit NTRKBkUp.hiv
```

## <a name="additional-references"></a>その他のリファレンス

- [コマンド ライン構文の記号](command-line-syntax-key.md)