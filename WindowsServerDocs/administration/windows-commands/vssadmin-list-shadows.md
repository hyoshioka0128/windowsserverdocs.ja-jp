---
title: Vssadmin 一覧の影
description: Vssadmin リストの説明では、コマンドをシャドウします。
ms.prod: windows-server-threshold
ms.topic: article
author: JasonGerend
ms.author: jgerend
ms.technology: storage
ms.date: 05/18/2018
ms.localizationpriority: medium
ms.openlocfilehash: 3601986a51e8c5b362a28c686ed132eda8e4b640
ms.sourcegitcommit: 2977c707a299929c6ab0d1e0adab2e1c644b8306
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/24/2019
ms.locfileid: "63706562"
---
# <a name="vssadmin-list-shadows"></a>Vssadmin 一覧の影

>適用対象:Windows 10、Windows 8.1、Windows Server 2016、Windows Server 2012 R2、Windows Server 2012、Windows Server 2008 R2、Windows Server 2008

指定されたボリュームの既存のシャドウ コピーをすべて一覧表示します。 指定された順序でコンピューターのすべてのボリューム シャドウ コピーが表示されますパラメーターを指定せずには、このコマンドを使用する場合**シャドウ コピー セット**します。

## <a name="syntax"></a>構文

```PowerShell
vssadmin list shadows [/for=<ForVolumeSpec>] [/shadow=<ShadowID>]
```

## <a name="parameters"></a>パラメーター

|パラメーター|説明|
|---|---|
|/=\<指定せず >|ボリューム シャドウ コピーは、対象として表示されますを指定します。|
|/shadow=\<ShadowID>|ShadowID で指定されたシャドウ コピーを一覧表示します。 シャドウ コピー ID を取得する、 **vssadmin 一覧 shadows**コマンド。 次の形式を使用して、シャドウ コピー ID を入力するときに、各*X* 16 進数の文字を表します。<br><br>XXXXXXXX-XXXX-XXXX-XXXX-XXXXXXXXXXXX|

## <a name="additional-references"></a>その他の参照情報

* [コマンドライン構文キー](https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2012-r2-and-2012/cc771080(v%3dws.11))
* [vssadmin](vssadmin.md)