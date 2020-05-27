---
title: manage-bde tpm
description: '* * * * のリファレンストピック'
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 11a8530d-edd7-4fe3-ae81-b943766760fe
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: c93a80a076b34ad4e7340387b098042b58103ae8
ms.sourcegitcommit: 4f407b82435afe3111c215510b0ef797863f9cb4
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/24/2020
ms.locfileid: "83820759"
---
# <a name="manage-bde-tpm"></a>manage-bde: tpm

> 適用対象: Windows Server (半期チャネル)、Windows Server 2019、Windows Server 2016、Windows Server 2012 R2、Windows Server 2012
>
> [!IMPORTANT]
> このコマンドは、Windows 8、Windows Server 2012 またはそれ以降のオペレーティング システムを実行しているコンピュータでの使用はサポートされていません。 これらのコンピューターを使用することができます、 [Windows PowerShell 用の TPM 管理コマンドレット](https://docs.microsoft.com/powershell/module/trustedplatformmodule/)します。
> Windows 7 または Windows Server 2008 を実行しているコンピューターでこのコマンドを使用している場合は、このコマンドを使用してコンピューターのトラステッドプラットフォームモジュール (TPM) を構成することもできます。
> ## <a name="syntax"></a>構文
> ```
> manage-bde -tpm [-turnon] [-takeownership <OwnerPassword>] [-computername <Name>] [{-?|/?}] [{-help|-h}]
> ```
> #### <a name="parameters"></a>パラメーター
>
> |    パラメーター    |                                                                              説明                                                                               |
> |-----------------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
> |     -オン     |              有効にして、TPM は、TPM 所有者パスワードを設定することができます。 使用することも **-t** としてこのコマンドの簡易版です。              |
> | -takeownership  |                      所有者パスワードを設定して、TPM の所有権を取得します。 使用することも **-o** としてこのコマンドの簡易版です。                       |
> | <OwnerPassword> |                                                      指定した TPM 所有者パスワードを表します。                                                       |
> |  -computername  | Manage-bde.exe を使用して、別のコンピューター上の BitLocker 保護を変更することを指定します。 また、このコマンドの省略版として **-cn**を使用することもできます。 |
> |     <Name>      |    BitLocker による保護を変更するコンピューターの名前を表します。 指定できる値には、コンピューターの NetBIOS 名とコンピューターの IP アドレスが含まれます。     |
> |    -? または /?     |                                                               コマンドプロンプトで簡単なヘルプを表示します。                                                               |
> |   -help または-h   |                                                             コマンドプロンプトで完全なヘルプを表示します。                                                              |
>
> ## <a name="examples"></a>例
> **-Tpm**コマンドを使用して tpm を有効にする方法を説明します。
> ```
> manage-bde  tpm -turnon
> ```
> **Tpm コマンドを**使用して tpm の所有権を取得し、所有者パスワードをに設定する方法を示し 0wnerP@ss ます。
> ```
> manage-bde  tpm  takeownership 0wnerP@ss
> ```
> ## <a name="additional-references"></a>その他のリファレンス
> - [コマンド ライン構文の記号](command-line-syntax-key.md)
> -   [manage-bde](manage-bde.md)
