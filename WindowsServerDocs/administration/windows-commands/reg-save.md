---
title: reg 保存
description: '* * * * のリファレンストピック'
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: b326482b-c8af-467d-a20c-0481eeda3d5c
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 1dd3e932e67df7eb972bd625ecec24f986cf3f3d
ms.sourcegitcommit: ab64dc83fca28039416c26226815502d0193500c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/01/2020
ms.locfileid: "82722510"
---
# <a name="reg-save"></a>reg 保存



指定したファイルで指定されたサブキー、エントリ、およびレジストリの値のコピーを保存します。



## <a name="syntax"></a>構文

```
reg save <KeyName> <FileName> [/y]
```

### <a name="parameters"></a>パラメーター

|パラメーター|[説明]|
|---------|-----------|
|\<KeyName>|サブキーの完全なパスを指定します。 リモートコンピューターを指定する場合は、コンピューター名を*KeyName*の\\ \\一部\)として ComputerName という形式で指定します。 ComputerName \\ \\\ を省略すると、操作は既定でローカルコンピューターに設定されます。 *KeyName* 有効なルート キーを含める必要があります。 ローカル コンピューターの有効なルート キー: HKLM、HKCU、HKCR、HKU、および HKCC します。 有効なルート キーは、リモート コンピューターが指定されている場合: HKLM および HKU します。|
|\<ファイル名>|作成されるファイルのパスと名前を指定します。 パスが指定されていない場合は、現在のパスが使用されます。|
|/y|名前の既存のファイルを上書き *FileName* 確認を求めずにします。|
|/?|ヘルプを表示 **reg 保存** コマンド プロンプト。|

## <a name="remarks-optional-section"></a>\<省略可能なセクション>

-   次の表に、戻り値の **reg 保存** 操作します。

|値|[説明]|
|-----|-----------|
|0|Success|
|1|障害|
-   すべてのレジストリ エントリを編集する前に保存された親サブキー、 **reg 保存** 操作します。 復元と元のサブキーの編集に失敗した場合、 **reg 復元** 操作します。

## <a name="examples"></a>例

現在のフォルダーに hive MyApp AppBkUp.hiv という名前のファイルを保存するには、次のように入力します。
```
REG SAVE HKLM\Software\MyCo\MyApp AppBkUp.hiv
```

## <a name="additional-references"></a>その他のリファレンス

- [コマンド ライン構文の記号](command-line-syntax-key.md)