---
title: wbadmin のバックアップの無効化
description: 'Windows コマンドに関するトピック * * * *- '
ms.custom: na
ms.prod: windows-server
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 5176cbd9-0696-4b3f-9c35-272dd84f7898
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 405bbb3c07206032f1a9e3039c563e7c842e362e
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/27/2019
ms.locfileid: "71362493"
---
# <a name="wbadmin-disable-backup"></a>wbadmin のバックアップの無効化



既存のスケジュールされた毎日のバックアップの実行を停止します。

スケジュールされた毎日のバックアップを無効にするには、 **Administrators**グループのメンバーであるか、適切な権限が委任されている必要があります。 さらに、実行する必要があります **wbadmin** 管理者特権でコマンド プロンプトからです。 (管理者特権でのコマンドプロンプトを開くには、 **[コマンドプロンプト]** を右クリックし、 **[管理者として実行]** をクリックします)。

## <a name="syntax"></a>構文

```
wbadmin disable backup
[-quiet]
```

## <a name="parameters"></a>パラメーター

|パラメーター|説明|
|---------|-----------|
|-通知の停止|ユーザーにプロンプトを表示せずにサブコマンドを実行します。|

#### <a name="additional-references"></a>その他の参照情報

-   [コマンド ライン構文の記号](command-line-syntax-key.md)
-   [Wbadmin](wbadmin.md)