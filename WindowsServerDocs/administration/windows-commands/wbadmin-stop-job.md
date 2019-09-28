---
title: wbadmin 停止ジョブ
description: 'Windows コマンドに関するトピック * * * *- '
ms.custom: na
ms.prod: windows-server
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 3b83b398-39c7-4410-bf17-5c1fb1a4f46d
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 671ab48722970af214a040d8ca7fea807a525698
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/27/2019
ms.locfileid: "71362211"
---
# <a name="wbadmin-stop-job"></a>wbadmin 停止ジョブ



現在実行中のバックアップまたは回復操作をキャンセルします。 取り消された操作は再開できません。最初から取り消されたバックアップまたは回復操作を再実行する必要があります。

このサブコマンドを使用してバックアップまたは回復操作を停止するには、 **Backup Operators**グループまたは**Administrators**グループのメンバーであるか、適切な権限が委任されている必要があります。 さらに、実行する必要があります **wbadmin** 管理者特権でコマンド プロンプトからです。 (管理者特権でのコマンドプロンプトを開くには、 **[コマンドプロンプト]** を右クリックし、 **[管理者として実行]** をクリックします)。

## <a name="syntax"></a>構文

```
wbadmin stop job
[-quiet]
```

## <a name="parameters"></a>パラメーター

|パラメーター|説明|
|---------|-----------|
|-通知の停止|ユーザーにプロンプトを表示せずにサブコマンドを実行します。|

#### <a name="additional-references"></a>その他の参照情報

-   [コマンド ライン構文の記号](command-line-syntax-key.md)
-   [Wbadmin](wbadmin.md)