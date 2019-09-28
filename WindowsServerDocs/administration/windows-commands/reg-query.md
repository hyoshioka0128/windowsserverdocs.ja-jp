---
title: reg クエリ
description: 'Windows コマンドに関するトピック * * * *- '
ms.custom: na
ms.prod: windows-server
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 0e6a0d7c-ed9b-4318-833d-33f265a81f39
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: d2f616fb33974df4327c7b2536b3143b75d116be
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/27/2019
ms.locfileid: "71371720"
---
# <a name="reg-query"></a>reg クエリ



次の層のサブキーと、レジストリで指定したサブキーの下にあるエントリの一覧を返します。

このコマンドを使用する方法の例については、[例](#BKMK_examples)を参照してください。

## <a name="syntax"></a>構文

```
reg query <KeyName> [{/v <ValueName> | /ve}] [/s] [/se <Separator>] [/f <Data>] [{/k | /d}] [/c] [/e] [/t <Type>] [/z]
```

## <a name="parameters"></a>パラメーター

|パラメーター|説明|
|---------|-----------|
|\<KeyName >|サブキーの完全なパスを指定します。 リモートコンピューターを指定する場合は、コンピューター名を、 *KeyName*の一部として \\ @ No__t-1 computername @ no__t の形式で指定します。 @No__t-0 @ no__t-1 Computername \ を省略すると、操作は既定でローカルコンピューターに設定されます。 *KeyName* 有効なルート キーを含める必要があります。 ローカルコンピューターの有効なルートキーは次のとおりです。HKLM、HKCU、HKCR、HKU、および HKCC。 リモートコンピューターが指定されている場合、有効なルートキーは次のとおりです。HKLM と HKU。|
|/v \<ValueName >|照会するレジストリ値の名前を指定します。 すべての値の名前を省略すると、 *KeyName* が返されます。 *ValueName* このパラメーターは省略可能な場合は、 **/f** オプションも使用します。|
|/ve|値の名前が空のクエリを実行します。|
|/s|すべてのサブキーと値の名前を再帰的にクエリを指定します。|
|/se \<Separator >|REG_MULTI_SZ 値名の種類で検索する 1 つの値の区切り記号を指定します。 場合 *区切り* が指定されていない **\0** を使用します。|
|/f @no__t 0Data >|データを検索するパターンを指定します。 文字列にスペースが含まれている場合は、二重引用符を使用します。 指定しない場合、ワイルドカード **&#42;** () が検索パターンとして使用されます。|
|/k|キー名のみで検索を指定します。|
|/d|データのみで検索するよう指定します。|
|/c|クエリを大文字小文字を区別することを示します。 既定では、クエリでは大文字小文字が区別されません。|
|/e|完全一致のみを返すように指定します。 既定では、すべての一致が返されます。|
|/t \<Type >|検索するレジストリの種類を指定します。 有効なデータ型は、次のとおりです。REG_SZ、REG_MULTI_SZ、REG_EXPAND_SZ、REG_DWORD、REG_BINARY、REG_NONE。 指定されていない場合は、すべての型が検索されます。|
|/z|レジストリの型に対応する数値を検索結果に含めるように指定します。|
|/?|ヘルプを表示 **reg クエリ** コマンド プロンプト。|

## <a name="remarks-optional-section"></a>解説 \<optional section >

次の表に、戻り値の **reg クエリ** 操作します。

|値|説明|
|-----|-----------|
|0|成功|
|1|失敗|

## <a name="BKMK_examples"></a>例

名前値のバージョンの値を HKLM\Software\Microsoft\ResKit キーを表示するには、次のように入力します。
```
REG QUERY HKLM\Software\Microsoft\ResKit /v Version
```
ABC という名前のリモート コンピューター上のすべてのサブキーと HKLM\Software\Microsoft\ResKit\Nt\Setup キーの値を表示するに次のように入力します。
```
REG QUERY \\ABC\HKLM\Software\Microsoft\ResKit\Nt\Setup /s
```
すべてのサブキーとを REG_MULTI_SZ を使用して型の値を表示する **#** の区切り記号として入力します。
```
REG QUERY HKLM\Software\Microsoft\ResKit\Nt\Setup /se #
```
キーを表示するには、値と完全一致と大文字小文字を区別のデータと一致するシステムのデータ種類が REG_SZ の HKLM ルートの下。
```
REG QUERY HKLM /f SYSTEM /t REG_SZ /c /e
```
キー、値、および一致するデータを表示する **0F** データのデータの HKCU ルート キーの下に「REG_BINARY」と入力します。
```
REG QUERY HKCU /f 0F /d /t REG_BINARY
```
値と値の名前は hklm \software の下にある null (既定値) のデータを表示するには、次のように入力します。
```
REG QUERY HKLM\SOFTWARE /ve
```

#### <a name="additional-references"></a>その他の参照情報

[コマンド ライン構文の記号](command-line-syntax-key.md)