---
title: Reg アンロード
description: 'Windows コマンド」のトピック * * *- '
ms.custom: na
ms.prod: windows-server-threshold
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
ms.openlocfilehash: aaa7d7a9fa82db2968d988e3b7b3fb8275a72337
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/17/2019
ms.locfileid: "59834983"
---
# <a name="reg-unload"></a>Reg アンロード



レジストリを使用して既に読み込まれているセクションを削除、 **reg ロード** 操作します。

このコマンドを使用する方法の例については、[例](#BKMK_examples)を参照してください。

## <a name="syntax"></a>構文

```
reg unload <KeyName>
```

## <a name="parameters"></a>パラメーター

|パラメーター|説明|
|---------|-----------|
|\<キー名 >|アンロードするサブキーの完全なパスを指定します。 リモート コンピューターに指定する場合、コンピューター名を含める (形式の\\ \\ComputerName\)の一部として、 *KeyName*します。 省略すると\\ \\ComputerName\ によりローカル コンピューターに既定値に操作します。 *KeyName* 有効なルート キーを含める必要があります。 ローカル コンピューターの有効なルート キーは、HKLM、HKCU、HKCR、HKU、および HKCC です。 リモート コンピューターが指定されている場合は、有効なルート キーは HKLM および HKU です。|
|/?|ヘルプを表示 **reg アンロード** コマンド プロンプト。|

## <a name="remarks"></a>注釈

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
> 代替手段があるない場合は、直接、レジストリを編集しないでください。 レジストリ エディターは、標準の保護をバイパスする、設定にパフォーマンスが低下することができます、システムの破損やでも Windows を再インストールする必要があります。 ほとんどのレジストリ設定は、コントロール パネルまたは Microsoft 管理コンソール (MMC) では、プログラムを使用して安全に変更できます。 レジストリを直接編集する必要がある場合は、最初にバックアップします。

#### <a name="additional-references"></a>その他の参照情報

[コマンドライン構文キー](command-line-syntax-key.md)