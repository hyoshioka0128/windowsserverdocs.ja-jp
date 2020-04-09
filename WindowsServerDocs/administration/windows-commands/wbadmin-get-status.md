---
title: wbadmin の状態の取得
description: Wbadmin get status の Windows コマンドに関するトピック。現在実行中のバックアップまたは回復操作の状態を報告します。
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 2911b944-7b95-46aa-8c1e-1d55a2fcc94c
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: f8ebf1a078632f78dc8d58c232550345f0de78f2
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/08/2020
ms.locfileid: "80829745"
---
# <a name="wbadmin-get-status"></a>wbadmin の状態の取得



現在実行中のバックアップまたは回復操作の状態を報告します。

このサブコマンドを使用するには、 **Backup Operators**グループまたは**Administrators**グループのメンバであるか、適切な権限が委任されている必要があります。 さらに、実行する必要があります **wbadmin** 管理者特権でコマンド プロンプトからです。 (管理者特権でのコマンドプロンプトを開くには、 **[コマンドプロンプト]** を右クリックし、 **[管理者として実行]** をクリックします)。

## <a name="syntax"></a>構文

```
wbadmin get status
```

### <a name="parameters"></a>パラメーター

このサブコマンドにはパラメーターがありません。

## <a name="remarks"></a>コメント

-   このサブコマンドは、現在のバックアップまたは回復操作が完了するまで停止しません。コマンドウィンドウを閉じた場合でも、サブコマンドは引き続き実行されます。
-   現在のバックアップまたは回復操作を停止する場合は、 **wbadmin stop job**サブコマンドを使用します。

## <a name="additional-references"></a>その他の参照情報

-   - [コマンド ライン構文の記号](command-line-syntax-key.md)
-   [Wbadmin](wbadmin.md)
-   [WBJob](https://technet.microsoft.com/library/jj902426.aspx)コマンドレット