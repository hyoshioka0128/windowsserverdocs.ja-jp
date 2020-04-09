---
title: reg unload
description: Windows コマンドに関するトピック * * * *-
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 1d07791d-ca27-454e-9797-27d7e84c5048
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: e5fd1436ed1122a09eea11d358a3711aedddf2c1
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/08/2020
ms.locfileid: "80836275"
---
# <a name="reg-unload"></a>reg unload



レジストリを使用して既に読み込まれているセクションを削除、 **reg ロード** 操作します。

このコマンドを使用する方法の例については、[例](#BKMK_examples)を参照してください。

## <a name="syntax"></a>構文

```
reg unload <KeyName>
```

### <a name="parameters"></a>パラメーター

|パラメーター|説明|
|---------|-----------|
|\<KeyName >|アンロードするサブキーの完全なパスを指定します。 リモートコンピューターを指定する場合は、コンピューター名 (\\\\ComputerName\) を*KeyName*の一部として指定します。 \\\\ComputerName \ を省略すると、操作は既定でローカルコンピューターに設定されます。 *KeyName* 有効なルート キーを含める必要があります。 ローカル コンピューターの有効なルート キーは、HKLM、HKCU、HKCR、HKU、および HKCC です。 リモート コンピューターが指定されている場合は、有効なルート キーは HKLM および HKU です。|
|/?|ヘルプを表示 **reg アンロード** コマンド プロンプト。|

## <a name="remarks"></a>コメント

次の表に、戻り値の **reg アンロード** オプション。

|値|説明|
|-----|-----------|
|0|成功|
|1|失敗|

## <a name="examples"></a><a name=BKMK_examples></a>例

TempHive ファイル HKLM ハイブをアンロードするには、次のように入力します。
```
REG UNLOAD HKLM\TempHive
```

> [!CAUTION]
> 代替手段があるない場合は、直接、レジストリを編集しないでください。 レジストリエディターでは、標準のセーフガードがバイパスされるため、パフォーマンスを低下させたり、システムに損害を与えたり、Windows の再インストールが必要になることもあります。 ほとんどのレジストリ設定は、コントロールパネルまたは Microsoft 管理コンソール (MMC) のプログラムを使用して、安全に変更できます。 レジストリを直接編集する必要がある場合は、最初にバックアップします。

## <a name="additional-references"></a>その他の参照情報

- [コマンド ライン構文の記号](command-line-syntax-key.md)