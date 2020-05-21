---
title: Vssadmin リストの影
description: Vssadmin list shadows コマンドの説明です。
ms.prod: windows-server
ms.topic: article
author: JasonGerend
ms.author: jgerend
ms.technology: storage
ms.date: 05/18/2018
ms.localizationpriority: medium
ms.openlocfilehash: 38eda178b6c9e34fec1d63ed6c59f01023b859c4
ms.sourcegitcommit: bf887504703337f8ad685d778124f65fe8c3dc13
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/16/2020
ms.locfileid: "83436677"
---
# <a name="vssadmin-list-shadows"></a>Vssadmin リストの影

> 適用対象: Windows 10、Windows 8.1、Windows Server 2016、Windows Server 2012 R2、Windows Server 2012、Windows Server 2008 R2、Windows Server 2008

指定したボリュームの既存のシャドウコピーをすべて一覧表示します。 パラメーターを指定せずにこのコマンドを使用すると、コンピューター上のすべてのボリュームシャドウコピーが、**シャドウコピーセット**によって指定された順序で表示されます。

## <a name="syntax"></a>構文

```PowerShell
vssadmin list shadows [/for=<ForVolumeSpec>] [/shadow=<ShadowID>]
```

### <a name="parameters"></a>パラメーター

|パラメーター|説明|
|---|---|
|/for = \< ForVolumeSpec>|シャドウコピーが表示されるボリュームを指定します。|
|/shadow = \< ShadowID>|ShadowID によって指定されたシャドウコピーの一覧を表示します。 シャドウコピー ID を取得するには、 **vssadmin list shadows**コマンドを使用します。 シャドウコピー ID を入力するときは、次の形式を使用します。各*X*は16進文字を表します。<br><br>XXXXXXXX-XXXX-XXXX-XXXX-XXXXXXXXXXXX-XXXX-XXXX-XXXXXXXX-XXXX-XXXX-XXXX-XXXXXXXXXXXX|

## <a name="additional-references"></a>その他のリファレンス

* [コマンドライン構文のキー](https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2012-r2-and-2012/cc771080(v%3dws.11))
* [Vssadmin](vssadmin.md)