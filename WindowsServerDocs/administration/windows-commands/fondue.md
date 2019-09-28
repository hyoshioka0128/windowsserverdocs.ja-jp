---
title: fondue
description: 'Windows コマンドに関するトピック * * * *- '
ms.custom: na
ms.prod: windows-server
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: fc4467f6-ddbb-4d6d-b51e-5a50a957b8c0
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: d75d2d9fb57f8888cfc5bf50e2f7796aefc66102
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/27/2019
ms.locfileid: "71377092"
---
# <a name="fondue"></a>fondue

>適用先:Windows Server (半期チャネル)、Windows Server 2016、Windows Server 2012 R2、Windows Server 2012

Windows Update またはグループポリシーによって指定された別のソースから必要なファイルをダウンロードして、Windows のオプション機能を有効にします。 機能のマニフェストファイルは、Windows イメージに既にインストールされている必要があります。 
## <a name="syntax"></a>構文
```
fondue.exe /enable-feature:<feature_name> [/caller-name:<program_name>] [/hide-ux:{all | rebootRequest}]
```
### <a name="parameters"></a>パラメーター

|              パラメーター              |                                                                                                                                                                     説明                                                                                                                                                                     |
|-------------------------------------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
|  /enable-feature: <*feature_name*>   |                                                                               有効にする Windows オプション機能の名前を指定します。 有効にできる機能は、コマンドラインごとに1つだけです。 複数の機能を有効にするには、各機能に対して、"/" を使用します。                                                                                |
|    /callname: <*program_name*>    |                                                                                 スクリプトまたはバッチファイルから小文字の .exe を呼び出すときに、プログラム名またはプロセス名を指定します。 このオプションを使用すると、エラーが発生した場合にプログラム名を SQM レポートに追加できます。                                                                                 |
| /hideux: {all &#124; rebootRequest} | **[すべて]** を使用して、Windows Update にアクセスするための進行状況とアクセス許可要求を含むすべてのメッセージをユーザーに非表示にします。 アクセス許可が必要な場合、操作は失敗します。<br /><br />**RebootRequest**を使用して、コンピューターを再起動するアクセス許可を求めるユーザーメッセージのみを非表示にします。 このオプションは、再起動要求を制御するスクリプトがある場合に使用します。 |

## <a name="BKMK_Examples"></a>例
Microsoft .NET Framework 3.5 を有効にするには、次のように入力します。
```
fondue.exe /enable-feature:NETFX3
```
Microsoft .NET Framework 3.5 を有効にするには、プログラム名を SQM レポートに追加し、ユーザーにメッセージを表示しないようにするには、次のように入力します。
```
fondue.exe /enable-feature:NETFX3 /caller-name:Admin.bat /hide-ux:all
```
## <a name="additional-references"></a>その他の参照情報
- [コマンド ライン構文の記号](command-line-syntax-key.md)
  ## <a name="see-also"></a>関連項目
  [Microsoft .NET Framework 3.5 の展開に関する考慮事項](https://go.microsoft.com/fwlink/?LinkId=248869)
