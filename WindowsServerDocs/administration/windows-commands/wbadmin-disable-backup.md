---
title: wbadmin のバックアップの無効化
description: Wbadmin disable backup の Windows コマンドに関するトピックでは、スケジュールされた既存の毎日のバックアップの実行を停止します。
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 5176cbd9-0696-4b3f-9c35-272dd84f7898
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: e2fb3d22fc3857cce191ee11381ae6e7e6ac1175
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/08/2020
ms.locfileid: "80829855"
---
# <a name="wbadmin-disable-backup"></a>wbadmin のバックアップの無効化



既存のスケジュールされた毎日のバックアップの実行を停止します。

スケジュールされた毎日のバックアップを無効にするには、 **Administrators**グループのメンバーであるか、適切な権限が委任されている必要があります。 さらに、実行する必要があります **wbadmin** 管理者特権でコマンド プロンプトからです。 (管理者特権でのコマンドプロンプトを開くには、 **[コマンドプロンプト]** を右クリックし、 **[管理者として実行]** をクリックします)。

## <a name="syntax"></a>構文

```
wbadmin disable backup
[-quiet]
```

### <a name="parameters"></a>パラメーター

|パラメーター|説明|
|---------|-----------|
|-quiet|ユーザーにプロンプトを表示せずにサブコマンドを実行します。|

## <a name="additional-references"></a>その他の参照情報

-   - [コマンド ライン構文の記号](command-line-syntax-key.md)
-   [Wbadmin](wbadmin.md)