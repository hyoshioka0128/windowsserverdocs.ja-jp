---
title: manage-bde tpm
description: 'Windows コマンド」のトピック * * *- '
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 11a8530d-edd7-4fe3-ae81-b943766760fe
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: f2b8390d49257c3c6acd9ed4fd45773e5a65aac4
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/17/2019
ms.locfileid: "59840583"
---
# <a name="manage-bde-tpm"></a>manage-bde: tpm

>適用先:Windows Server (半期チャネル)、Windows Server 2016、Windows Server 2012 R2、Windows Server 2012

> [!IMPORTANT]
> このコマンドは、Windows 8、Windows Server 2012 またはそれ以降のオペレーティング システムを実行しているコンピュータでの使用はサポートされていません。 これらのコンピューターを使用することができます、 [Windows PowerShell 用の TPM 管理コマンドレット](https://technet.microsoft.com/library/jj603116.aspx)します。
Windows 7 または Windows Server 2008 を実行しているコンピューターでこのコマンドを使用する場合は、コンピューターのトラステッド プラットフォーム モジュール (TPM) このコマンドを使用して引き続き構成できます。 このコマンドの使用方法の例については、次を参照してください。 [例](#BKMK_Examples)します。
## <a name="syntax"></a>構文
```
manage-bde -tpm [-turnon] [-takeownership <OwnerPassword>] [-computername <Name>] [{-?|/?}] [{-help|-h}]
```
### <a name="parameters"></a>パラメーター
|パラメーター|説明|
|-------|--------|
|-オン|有効にして、TPM は、TPM 所有者パスワードを設定することができます。 使用することも **-t** としてこのコマンドの簡易版です。|
|-takeownership|所有者パスワードを設定して、TPM の所有権を取得します。 使用することも **-o** としてこのコマンドの簡易版です。|
|<OwnerPassword>|指定した TPM 所有者パスワードを表します。|
|-computername|別のコンピューターに bitlocker による保護の変更に使用する、bde.exe を指定します。 使用することも **- cn**としてこのコマンドの簡易版です。|
|<Name>|BitLocker による保護を変更するコンピューターの名前を表します。 指定できる値には、コンピューターの NetBIOS 名とコンピューターの IP アドレスが含まれます。|
|-? または /?|コマンド プロンプトでヘルプの簡単なが表示されます。|
|--help または-h|コマンド プロンプトでヘルプを完了しますが表示されます。|
## <a name="BKMK_Examples"></a>例
使用して、次の例に示す、 **- tpm** コマンドを TPM をオンにします。
```
manage-bde  tpm -turnon
```
次の例を使用して、* * * * tpm コマンドを TPM の所有権を取得し、所有者パスワードを設定0wnerP@ssします。
```
manage-bde  tpm  takeownership 0wnerP@ss
```
## <a name="additional-references"></a>その他の参照
-   [コマンドライン構文キー](command-line-syntax-key.md)
-   [manage-bde](manage-bde.md)
