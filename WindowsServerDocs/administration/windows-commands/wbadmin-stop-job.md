---
title: wbadmin 停止ジョブ
description: Wbadmin stop job の Windows コマンドに関するトピック。現在実行中のバックアップまたは回復操作をキャンセルします。 取り消された操作は再開できません。最初から取り消されたバックアップまたは回復操作を再実行する必要があります。
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 3b83b398-39c7-4410-bf17-5c1fb1a4f46d
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 4a00b4a93e0aaa954f8f07adae825a4f582c5581
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/08/2020
ms.locfileid: "80829485"
---
# <a name="wbadmin-stop-job"></a>wbadmin 停止ジョブ



現在実行中のバックアップまたは回復操作をキャンセルします。 取り消された操作は再開できません。最初から取り消されたバックアップまたは回復操作を再実行する必要があります。

このサブコマンドを使用してバックアップまたは回復操作を停止するには、 **Backup Operators**グループまたは**Administrators**グループのメンバーであるか、適切な権限が委任されている必要があります。 さらに、実行する必要があります **wbadmin** 管理者特権でコマンド プロンプトからです。 (管理者特権でのコマンドプロンプトを開くには、 **[コマンドプロンプト]** を右クリックし、 **[管理者として実行]** をクリックします)。

## <a name="syntax"></a>構文

```
wbadmin stop job
[-quiet]
```

### <a name="parameters"></a>パラメーター

|パラメーター|説明|
|---------|-----------|
|-quiet|ユーザーにプロンプトを表示せずにサブコマンドを実行します。|

## <a name="additional-references"></a>その他の参照情報

-   - [コマンド ライン構文の記号](command-line-syntax-key.md)
-   [Wbadmin](wbadmin.md)