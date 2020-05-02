---
title: time
description: システム時刻を設定および表示する方法について説明します。
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 1276a257-7283-41da-ae80-fb4cfb311f9d
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: e27b260bdaa8896ad3cf0ad58294467bbb63e1c2
ms.sourcegitcommit: ab64dc83fca28039416c26226815502d0193500c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/01/2020
ms.locfileid: "82721364"
---
# <a name="time"></a>time



表示またはシステム時刻を設定します。 パラメーターを指定せずに使用する場合 **時間** 現在のシステム時刻が表示され、新しい時間を入力するように求められます。



## <a name="syntax"></a>構文

```
time [/t | [<HH>[:<MM>[:<SS>]] [am|pm]]]
```

### <a name="parameters"></a>パラメーター

|パラメーター|[説明]|
|---------|-----------|
|\<HH> [:\<MM> [:\<SS> [。\<NN>]]] [am\|pm]|システム時刻を指定された、新しい時間に設定 *HH* (必要)、時間単位で *MM* 分単位で、 *SS* の秒数。 *NN* の秒を指定するために使用できます。 場合 **いる** または **pm** が指定されていない **時間** 既定で 24 時間制を使用します。|
|/t|ときに、新しいメッセージを表示せずには、現在の時刻を表示します。|
|/?|コマンド プロンプトにヘルプを表示します。|

## <a name="remarks"></a>Remarks

-   現在の時刻を変更するには、管理者の資格情報が必要です。
-   値を区切る必要があります *HH*, 、*MM*, 、および *SS* コロン (::)。 *SS* と *NN* ピリオド (.) で区切る必要があります。
-   有効な *HH* 値は 0 ~ 24 です。
-   有効な *MM* と *SS* 値は 0 ~ 59 です。

## <a name="examples"></a><a name="BKMK_examples"></a>例

コマンド拡張機能が有効になっている場合は、現在のシステム時刻を表示するを入力します。
```
time /t
```
現在のシステム時刻を午後 5 時 30 分に変更するには、次のいずれかを入力します。
```
time 17:30:00
time 5:30 pm
```
新しい時間を入力するプロンプトが後に現在のシステム時刻を表示するには、次のように入力します。
```
The current time is: 17:33:31.35
Enter the new time:
```
現在の時刻を保持し、コマンド プロンプトに戻り、ENTER キーを押します。 現在の時刻を変更するには、新しい時間を入力し、ENTER キーを押します。

## <a name="additional-references"></a>その他のリファレンス

- [コマンド ライン構文の記号](command-line-syntax-key.md)