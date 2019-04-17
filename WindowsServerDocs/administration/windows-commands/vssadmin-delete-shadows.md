---
title: Vssadmin 削除の影
description: Vssadmin 削除の影] コマンドの説明です。
ms.prod: windows-server-threshold
ms.topic: article
author: JasonGerend
ms.author: jgerend
ms.technology: storage
ms.date: 05/18/2018
ms.localizationpriority: medium
ms.openlocfilehash: 71119174c7fc5929eb4e1982183ba0aed7eb1735
ms.sourcegitcommit: e0479b0114eac7f232e8b1e45eeede96ccd72b26
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/22/2018
ms.locfileid: "2082352"
---
# <a name="vssadmin-delete-shadows"></a>Vssadmin 削除の影

>対象: Windows 10、Windows 8.1、Windows Server 2016、Windows Server 2012 R2、Windows Server 2012、Windows Server 2008 R2、Windows Server 2008

指定したボリュームの影のコピーを削除します。

## <a name="syntax"></a>構文

```PowerShell
vssadmin delete shadows /for=<ForVolumeSpec> [/oldest | /all | /shadow=<ShadowID>] [/quiet]
```

## <a name="parameters"></a>パラメーター

|パラメーター|説明|
|---|---|
|=/\ < 指定せず >|どのボリュームの影のコピーが削除されますかを指定します。|
|古い/|最も古いシャドウ コピーのみを削除します。|
|すべて/|すべての指定された、音量の影のコピーを削除します。|
|[影/= \ < ShadowID >|ShadowID が指定した影のコピーを削除します。 影のコピーの ID を取得するには、するには、 **vssadmin] ボックスの一覧の影**] コマンドを使用します。 シャドウ コピー ID を入力するときに各*X*が 16 進数の文字を表すを次の形式に使用します。<br><br>チームの XXXX-XXXX-で入力して|
|/非表示|コマンドでは実行中のメッセージは表示されないかを指定します。|

## <a name="remarks"></a>注釈

影のコピーは、クライアントがアクセスできる型でのみ削除できます。

## <a name="examples"></a>例

ボリューム C の最も古いシャドウ コピーを削除するには、このコマンドを入力します。

```PowerShell
vssadmin delete shadows /for=c: /oldest
```

## <a name="additional-references"></a>その他の参照

* [コマンドライン構文キー](https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2012-r2-and-2012/cc771080(v%3dws.11))
* [Vssadmin](vssadmin.md)
* [Vssadmin] ボックスの一覧の影](vssadmin-list-shadows.md)