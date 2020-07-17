---
title: manage-bde tpm
description: コンピューターのトラステッドプラットフォームモジュール (TPM) を構成する manage-bde tpm コマンドのリファレンス記事です。
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 11a8530d-edd7-4fe3-ae81-b943766760fe
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: bed203c5de5351162f4c465e43631a4869f0e9a1
ms.sourcegitcommit: 2afed2461574a3f53f84fc9ec28d86df3b335685
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/02/2020
ms.locfileid: "85922190"
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
| -computername | manage-bde.exe が別のコンピューターの BitLocker 保護を変更するために使用されることを指定します。 また、このコマンドの省略版として **-cn**を使用することもできます。 |
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

## <a name="additional-references"></a>その他の参照情報

- [コマンド ライン構文の記号](command-line-syntax-key.md)

- [Windows PowerShell 用の TPM 管理コマンドレット](https://docs.microsoft.com/powershell/module/trustedplatformmodule/)

- [manage-bde コマンド](manage-bde.md)
