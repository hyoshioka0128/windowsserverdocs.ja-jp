---
title: reg 読み込み
description: '* * * * のリファレンストピック'
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 3b0b2b1b-f510-4108-9e9d-7057e924aa6e
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 2523876e2ea2305ede3289226c934c9352825ba9
ms.sourcegitcommit: ab64dc83fca28039416c26226815502d0193500c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/01/2020
ms.locfileid: "82722537"
---
# <a name="reg-load"></a>reg 読み込み



書き込みは、サブキーと別のサブキーにエントリをレジストリに保存します。 トラブルシューティングまたはレジストリ エントリを編集するために使用される一時ファイルで使用するためのものです。



## <a name="syntax"></a>構文

```
reg load KeyName FileName
```

### <a name="parameters"></a>パラメーター

|パラメーター|[説明]|
|---------|-----------|
|\<KeyName>|読み込むサブキーの完全なパスを指定します。 リモートコンピューターを指定する場合は、コンピューター名を*KeyName*の\\ \\一部\)として ComputerName という形式で指定します。 ComputerName \\ \\\ を省略すると、操作は既定でローカルコンピューターに設定されます。 *KeyName* 有効なルート キーを含める必要があります。 ローカル コンピューターの有効なルート キー: HKLM、HKCU、HKCR、HKU、および HKCC します。 有効なルート キーは、リモート コンピューターが指定されている場合: HKLM および HKU します。|
|\<ファイル名>|読み込むファイルのパスと名前を指定します。 使用してこのファイルを事前に作成する必要があります、 **reg 保存** 操作と .hiv 拡張子です。|
|/?|ヘルプを表示 **reg ロード** コマンド プロンプト。|

## <a name="remarks"></a>Remarks

次の表に、戻り値の **reg ロード** 操作します。

|値|[説明]|
|-----|-----------|
|0|Success|
|1|障害|

## <a name="examples"></a>例

キー HKLM\TempHive に TempHive.hiv をという名前のファイルを読み込むには、次のように入力します。
```
REG LOAD HKLM\TempHive TempHive.hiv
```

## <a name="additional-references"></a>その他のリファレンス

- [コマンド ライン構文の記号](command-line-syntax-key.md)