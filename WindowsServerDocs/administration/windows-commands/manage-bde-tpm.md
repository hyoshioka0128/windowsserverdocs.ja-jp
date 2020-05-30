---
title: manage-bde tpm
description: コンピューターのトラステッドプラットフォームモジュール (TPM) を構成する manage-bde tpm コマンドのリファレンストピックです。
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 11a8530d-edd7-4fe3-ae81-b943766760fe
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 3aa597dbd871c64efc7e718ef70ed0c69b256ab9
ms.sourcegitcommit: 29bc8740e5a8b1ba8f73b10ba4d08afdf07438b0
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/30/2020
ms.locfileid: "84222145"
---
# <a name="manage-bde-tpm"></a>manage-bde tpm

> 適用対象: Windows Server (半期チャネル)、Windows Server 2019、Windows Server 2016、Windows Server 2012 R2、Windows Server 2012

コンピューターのトラステッド プラットフォーム モジュール (TPM) を構成します。

## <a name="syntax"></a>構文

```
manage-bde -tpm [-turnon] [-takeownership <ownerpassword>] [-computername <name>] [{-?|/?}] [{-help|-h}]
```

### <a name="parameters"></a>パラメーター

| パラメーター | 説明 |
| --------- | ----------- |
| -オン | 有効にして、TPM は、TPM 所有者パスワードを設定することができます。 使用することも **-t** としてこのコマンドの簡易版です。 |
| -takeownership | 所有者パスワードを設定して、TPM の所有権を取得します。 使用することも **-o** としてこのコマンドの簡易版です。 |
| `<ownerpassword>` | 指定した TPM 所有者パスワードを表します。 |
| -computername | Manage-bde.exe を使用して、別のコンピューター上の BitLocker 保護を変更することを指定します。 また、このコマンドの省略版として **-cn**を使用することもできます。 |
| `<name>` | BitLocker による保護を変更するコンピューターの名前を表します。 指定できる値には、コンピューターの NetBIOS 名とコンピューターの IP アドレスが含まれます。 |
| -? または /? | コマンドプロンプトで簡単なヘルプを表示します。 |
| -help または-h | 表示は、コマンド プロンプトでヘルプを完了します。 |

### <a name="examples"></a>例

TPM をオンにするには、次のように入力します。

```
manage-bde  tpm -turnon
```

TPM の所有権を取得し、所有者パスワードをに設定するには *0wnerP@ss* 、次のように入力します。

```
manage-bde  tpm  takeownership 0wnerP@ss
```

## <a name="additional-references"></a>その他のリファレンス

- [コマンド ライン構文の記号](command-line-syntax-key.md)

- [Windows PowerShell 用の TPM 管理コマンドレット](https://docs.microsoft.com/powershell/module/trustedplatformmodule/)

- [manage-bde コマンド](manage-bde.md)
