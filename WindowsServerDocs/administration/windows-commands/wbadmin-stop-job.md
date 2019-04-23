---
title: wbadmin の停止ジョブ
description: 'Windows コマンド」のトピック * * *- '
ms.custom: na
ms.prod: windows-server-threshold
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
ms.openlocfilehash: 7a9e71fe2e4883c52c2418e21fc8764fd14e6c81
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/17/2019
ms.locfileid: "59889723"
---
# <a name="wbadmin-stop-job"></a>wbadmin の停止ジョブ



現在実行中のバックアップや回復操作をキャンセルします。 取り消された操作を再開できません-先頭から取り消されたバックアップや回復操作を再実行する必要があります。

このサブコマンドでバックアップや回復操作を停止するには、メンバーである、 **Backup Operators**グループまたは**管理者**グループ、またはをされている必要が適切な権限が委任します。 さらに、実行する必要があります **wbadmin** 管理者特権でコマンド プロンプトからです。 (を開き、管理者特権でコマンド プロンプトを右クリック**コマンド プロンプト**し**管理者として実行**)。

## <a name="syntax"></a>構文

```
wbadmin stop job
[-quiet]
```

## <a name="parameters"></a>パラメーター

|パラメーター|説明|
|---------|-----------|
|-通知の停止|ユーザーにプロンプトなしで、サブコマンドを実行します。|

#### <a name="additional-references"></a>その他の参照情報

-   [コマンドライン構文キー](command-line-syntax-key.md)
-   [Wbadmin](wbadmin.md)