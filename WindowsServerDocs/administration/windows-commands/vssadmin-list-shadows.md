---
title: Vssadmin] ボックスの一覧の影
description: コマンドをシャドウ vssadmin リストの説明しています。
ms.prod: windows-server-threshold
ms.topic: article
author: JasonGerend
ms.author: jgerend
ms.technology: storage
ms.date: 05/18/2018
ms.localizationpriority: medium
ms.openlocfilehash: 07da36da1473563c3236a4fafc3ceae06259981a
ms.sourcegitcommit: e0479b0114eac7f232e8b1e45eeede96ccd72b26
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/22/2018
ms.locfileid: "2082443"
---
# <a name="vssadmin-list-shadows"></a>Vssadmin] ボックスの一覧の影

>対象: Windows 10、Windows 8.1、Windows Server 2016、Windows Server 2012 R2、Windows Server 2012、Windows Server 2008 R2、Windows Server 2008

指定したボリュームのすべての既存シャドウ コピーを一覧表示します。 パラメーターを指定せずには、このコマンドを使用する場合は、**影コピーの設定**で指定された順序でコンピューターのすべてのボリューム シャドウ コピーが表示されます。

## <a name="syntax"></a>構文

```PowerShell
vssadmin list shadows [/for=<ForVolumeSpec>] [/shadow=<ShadowID>]
```

## <a name="parameters"></a>パラメーター

|パラメーター|説明|
|---|---|
|=/\ < 指定せず >|影のコピーが表示されますボリュームを指定します。|
|[影/= \ < ShadowID >|ShadowID が指定した影のコピーを一覧表示します。 影のコピーの ID を取得するには、するには、 **vssadmin] ボックスの一覧の影**] コマンドを使用します。 シャドウ コピー ID を入力するときに各*X*が 16 進数の文字を表すを次の形式に使用します。<br><br>チームの XXXX-XXXX-で入力して|

## <a name="additional-references"></a>その他の参照

* [コマンドライン構文キー](https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2012-r2-and-2012/cc771080(v%3dws.11))
* [Vssadmin](vssadmin.md)