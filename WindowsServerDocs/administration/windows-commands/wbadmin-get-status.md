---
title: wbadmin の状態の取得
description: 現在実行中のバックアップまたは回復操作の状態を報告する wbadmin get status のリファレンストピックです。
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 2911b944-7b95-46aa-8c1e-1d55a2fcc94c
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 0e41c54b9f916f0032a4976cdfa6d3ca101fb744
ms.sourcegitcommit: 4f407b82435afe3111c215510b0ef797863f9cb4
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/24/2020
ms.locfileid: "83821192"
---
# <a name="wbadmin-get-status"></a>wbadmin の状態の取得



現在実行中のバックアップまたは回復操作の状態を報告します。

このサブコマンドを使用するには、 **Backup Operators**グループまたは**Administrators**グループのメンバであるか、適切な権限が委任されている必要があります。 さらに、実行する必要があります **wbadmin** 管理者特権でコマンド プロンプトからです。 (管理者特権でのコマンドプロンプトを開くには、[**コマンドプロンプト**] を右クリックし、[**管理者として実行**] をクリックします)。

## <a name="syntax"></a>構文

```
wbadmin get status
```

### <a name="parameters"></a>パラメーター

このサブコマンドにはパラメーターがありません。

## <a name="remarks"></a>注釈

-   このサブコマンドは、現在のバックアップまたは回復操作が完了するまで停止しません。コマンドウィンドウを閉じた場合でも、サブコマンドは引き続き実行されます。
-   現在のバックアップまたは回復操作を停止する場合は、 **wbadmin stop job**サブコマンドを使用します。

## <a name="additional-references"></a>その他のリファレンス

- [コマンド ライン構文の記号](command-line-syntax-key.md)
-   [Wbadmin](wbadmin.md)
-   [WBJob](https://technet.microsoft.com/library/jj902426.aspx)コマンドレット