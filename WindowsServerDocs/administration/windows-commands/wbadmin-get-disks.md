---
title: wbadmin のディスクの取得
description: Wbadmin get disks の Windows コマンドに関するトピック。ローカルコンピューターで現在オンラインになっている内部ディスクと外部ディスクの一覧が表示されます。
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 320edef1-df11-446b-a183-9f81811ef938
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 0243edce77febddccc3497df34685113f2a1b48f
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/08/2020
ms.locfileid: "80829765"
---
# <a name="wbadmin-get-disks"></a>wbadmin のディスクの取得



ローカルコンピューターで現在オンラインになっている内部ディスクと外部ディスクの一覧を表示します。

このサブコマンドを使用してオンラインになっているディスクを一覧表示するには、 **Backup Operators**グループまたは**Administrators**グループのメンバーであるか、適切なアクセス許可が委任されている必要があります。 さらに、実行する必要があります **wbadmin** 管理者特権でコマンド プロンプトからです。 (管理者特権でのコマンドプロンプトを開くには、 **[コマンドプロンプト]** を右クリックし、 **[管理者として実行]** をクリックします)。

## <a name="syntax"></a>構文

```
wbadmin get disks
```

### <a name="parameters"></a>パラメーター

このサブコマンドにはパラメーターがありません。

## <a name="additional-references"></a>その他の参照情報

-   - [コマンド ライン構文の記号](command-line-syntax-key.md)
-   [Wbadmin](wbadmin.md)
-   [WBDisk](https://technet.microsoft.com/library/jj902446.aspx)コマンドレット