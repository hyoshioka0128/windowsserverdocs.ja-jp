---
title: manage-bde tpm
description: Windows コマンドに関するトピック * * * *-
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 11a8530d-edd7-4fe3-ae81-b943766760fe
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: b6495bfbfedea7219ae175145f72fc12314ce7ae
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/08/2020
ms.locfileid: "80839765"
---
# <a name="manage-bde-tpm"></a>manage-bde: tpm

> 適用対象: Windows Server (半期チャネル)、Windows Server 2016、Windows Server 2012 R2、Windows Server 2012
> 
> [!IMPORTANT]
> このコマンドは、Windows 8、Windows Server 2012 またはそれ以降のオペレーティング システムを実行しているコンピュータでの使用はサポートされていません。 これらのコンピューターを使用することができます、 [Windows PowerShell 用の TPM 管理コマンドレット](https://docs.microsoft.com/powershell/module/trustedplatformmodule/)します。
> Windows 7 または Windows Server 2008 を実行しているコンピューターでこのコマンドを使用している場合は、このコマンドを使用してコンピューターのトラステッドプラットフォームモジュール (TPM) を構成することもできます。 このコマンドの使用方法の例については、次を参照してください。 [例](#BKMK_Examples)します。
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
> ## <a name="examples"></a><a name=BKMK_Examples></a>例
> 使用して、次の例に示す、 **- tpm** コマンドを TPM をオンにします。
> ```
> manage-bde  tpm -turnon
> ```
> 次の例では、 **tpm**コマンドを使用して tpm の所有権を取得し、所有者パスワードを 0wnerP@ssに設定しています。
> ```
> manage-bde  tpm  takeownership 0wnerP@ss
> ```
> ## <a name="additional-references"></a>その他の参照情報
> -   - [コマンド ライン構文の記号](command-line-syntax-key.md)
> -   [manage-bde](manage-bde.md)
