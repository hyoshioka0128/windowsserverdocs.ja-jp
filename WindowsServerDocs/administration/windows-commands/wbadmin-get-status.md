---
title: wbadmin get 状態
description: 'Windows コマンド」のトピック * * *- '
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 2911b944-7b95-46aa-8c1e-1d55a2fcc94c
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 35fd640aa56bca7c5f5d6f3901fe095d0b8a73cc
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/17/2019
ms.locfileid: "59863413"
---
# <a name="wbadmin-get-status"></a>wbadmin get 状態



現在実行中のバックアップや回復操作の状態を報告します。

このサブコマンドを使用する、 **Backup Operators**グループまたは**管理者**グループ、またはをされている必要が適切なアクセス許可を委任します。 さらに、実行する必要があります **wbadmin** 管理者特権でコマンド プロンプトからです。 (を開き、管理者特権でコマンド プロンプトを右クリック**コマンド プロンプト**、 をクリックし、**管理者として実行**)。

## <a name="syntax"></a>構文

```
wbadmin get status
```

## <a name="parameters"></a>パラメーター

このサブコマンドには、パラメーターがありません。

## <a name="remarks"></a>注釈

-   このサブコマンドは、現在のバックアップまで停止しませんまたは回復操作が完了したら、コマンド ウィンドウを閉じた場合でもを実行し、サブコマンドを続けます。
-   現在のバックアップまたは復旧操作を停止する場合を使用して、 **wbadmin の停止ジョブ**サブコマンドします。

#### <a name="additional-references"></a>その他の参照情報

-   [コマンドライン構文キー](command-line-syntax-key.md)
-   [Wbadmin](wbadmin.md)
-   [Get WBJob](https://technet.microsoft.com/library/jj902426.aspx)コマンドレット