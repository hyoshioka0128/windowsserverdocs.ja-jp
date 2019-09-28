---
title: Get AllMulticastTransmissions コマンドを使用してください。
description: 'Windows コマンドに関するトピック * * * *- '
ms.custom: na
ms.prod: windows-server
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 95b8fb79-7a8a-4f0c-88f4-92bc1111c67f
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 644684ffb356ef07120bc391e3d3da2daf768eaf
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/27/2019
ms.locfileid: "71363342"
---
# <a name="using-the-get-allmulticasttransmissions-command"></a>Get AllMulticastTransmissions コマンドを使用してください。

>適用先:Windows Server (半期チャネル)、Windows Server 2016、Windows Server 2012 R2、Windows Server 2012

サーバー上のすべてのマルチキャスト転送に関する情報を表示します。
## <a name="syntax"></a>構文
Windows Server 2008 の場合:
```
wdsutil /Get-AllMulticastTransmissions [/Server:<Server name>] [/Show:Clients] [/ExcludedeletePending]
```
Windows Server 2008 R2 の場合:
```
wdsutil /Get-AllMulticastTransmissions [/Server:<Server name>] [/Show:{Boot | Install | All}] [/details:Clients]  [/ExcludedeletePending]
```
## <a name="parameters"></a>パラメーター

|        パラメーター        |                                                                                                                                                                                                                                                                   説明                                                                                                                                                                                                                                                                    |
|-------------------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| [/Server:<Server name>] |                                                                                                                                                                                 サーバーの名前を指定します。 NetBIOS 名または完全修飾ドメイン名 (FQDN) のいずれかを指定できます。 サーバー名が指定されていない場合は、ローカルのサーバーが使用されます。                                                                                                                                                                                  |
|         [/Show]         | **Windows Server 2008**<br /><br />/Show:Clients - マルチキャスト転送に接続されているクライアント コンピューターに関する情報を表示します。<br /><br />**Windows Server 2008 R2**<br /><br />表示: {ブートと #124 文字です。インストールと #124 文字です。すべて} - 返すイメージの種類。                                **ブート** ブート イメージの転送のみを返します。                                  **インストール** インストールのイメージ転送のみを返します。 **すべて** 両方のイメージの種類を返します。 |
|                         |                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                  |
|    詳細: クライアント     |                                                                                                                                                                                              Windows Server 2008 R2 のみサポートされます。 存在する場合、送信に接続されているクライアントが表示されます。                                                                                                                                                                                               |
| [/Excludedeletepending] |                                                                                                                                                                                                                                              一覧から任意の非アクティブ化された転送を除外します。                                                                                                                                                                                                                                               |

## <a name="BKMK_examples"></a>例
すべての転送に関する情報を表示するには、次のように入力します。
- Windows Server 2008: `wdsutil /Get-AllMulticastTransmissions`
- Windows Server 2008 R2:非アクティブ化される送信を除くすべての転送に関する情報を表示するには、次のように入力します: 0 @no__t
- Windows Server 2008: `wdsutil /Get-AllMulticastTransmissions /Server:MyWDSServer /Show:Clients /ExcludedeletePending`
- Windows Server 2008 R2: `wdsutil /Get-AllMulticastTransmissions /Server:MyWDSServer /Show:All /details:Clients /ExcludedeletePending`
  #### <a name="additional-references"></a>その他の参照情報
  [コマンドライン構文のポイント](command-line-syntax-key.md)
  [/get-multicasttransmission コマンドを使用して](using-the-get-multicasttransmission-command.md)
  [MulticastTransmission 新しいコマンドを使用して](using-the-new-multicasttransmission-command.md)
  [/remove-multicasttransmission コマンドを使用して](using-the-remove-multicasttransmission-command.md)
  [サブコマンド:/start-multicasttransmission](subcommand-start-multicasttransmission.md)
