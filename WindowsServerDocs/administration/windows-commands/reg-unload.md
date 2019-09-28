---
title: reg アンロード
description: 'Windows コマンドに関するトピック * * * *- '
ms.custom: na
ms.prod: windows-server
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 1d07791d-ca27-454e-9797-27d7e84c5048
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 32df397b597291269dcfb1449d00e86b2f4f5836
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/27/2019
ms.locfileid: "71384623"
---
# <a name="reg-unload"></a>reg アンロード



レジストリを使用して既に読み込まれているセクションを削除、 **reg ロード** 操作します。

このコマンドを使用する方法の例については、[例](#BKMK_examples)を参照してください。

## <a name="syntax"></a>構文

```
reg unload <KeyName>
```

## <a name="parameters"></a>パラメーター

|パラメーター|説明|
|---------|-----------|
|\<KeyName >|アンロードするサブキーの完全なパスを指定します。 リモートコンピューターを指定する場合は、コンピューター名を、 *KeyName*の一部として \\ @ No__t-1 computername @ no__t の形式で指定します。 @No__t-0 @ no__t-1 Computername \ を省略すると、操作は既定でローカルコンピューターに設定されます。 *KeyName* 有効なルート キーを含める必要があります。 ローカル コンピューターの有効なルート キーは、HKLM、HKCU、HKCR、HKU、および HKCC です。 リモート コンピューターが指定されている場合は、有効なルート キーは HKLM および HKU です。|
|/?|ヘルプを表示 **reg アンロード** コマンド プロンプト。|

## <a name="remarks"></a>コメント

次の表に、戻り値の **reg アンロード** オプション。

|値|説明|
|-----|-----------|
|0|成功|
|1|失敗|

## <a name="BKMK_examples"></a>例

TempHive ファイル HKLM ハイブをアンロードするには、次のように入力します。
```
REG UNLOAD HKLM\TempHive
```

> [!CAUTION]
> 代替手段があるない場合は、直接、レジストリを編集しないでください。 レジストリエディターでは、標準のセーフガードがバイパスされるため、パフォーマンスを低下させたり、システムに損害を与えたり、Windows の再インストールが必要になることもあります。 ほとんどのレジストリ設定は、コントロールパネルまたは Microsoft 管理コンソール (MMC) のプログラムを使用して、安全に変更できます。 レジストリを直接編集する必要がある場合は、最初にバックアップします。

#### <a name="additional-references"></a>その他の参照情報

[コマンド ライン構文の記号](command-line-syntax-key.md)