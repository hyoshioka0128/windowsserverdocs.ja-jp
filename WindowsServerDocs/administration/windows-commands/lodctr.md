---
title: lodctr
description: 'Windows コマンド」のトピック * * *- '
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 5a849abd-6b31-4833-bc8a-306c05eca29a
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 3ea48067bd78d260824da7d091f94957b51b768d
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/17/2019
ms.locfileid: "59852223"
---
# <a name="lodctr"></a>lodctr

>適用先:Windows Server (半期チャネル)、Windows Server 2016、Windows Server 2012 R2、Windows Server 2012

登録またはパフォーマンス カウンターの名前とレジストリの設定をファイルに保存し、信頼されたサービスを指定することができます。
## <a name="syntax"></a>構文
```
lodctr <filename> [/s:<filename>] [/r:<filename>] [/t:<servicename>]
```
### <a name="parameters"></a>パラメーター
|パラメーター|説明|
|-------|--------|
|<filename>|パフォーマンス カウンター名の設定とファイル名の初期化ファイルで提供される説明テキストを登録します。|
|/s:<filename>|保存のパフォーマンス カウンターのレジストリ設定と説明のテキスト ファイルに<filename>します。|
|/r|現在のレジストリ設定とレジストリに関連するパフォーマンスのキャッシュされたファイルからカウンターのレジストリ設定と説明のテキストを復元します。<br /><br />このオプションは、Windows Server 2003 オペレーティング システムでのみ使用できます。|
|/r:<filename>|復元のパフォーマンス カウンターのレジストリ設定と説明のテキスト ファイルから<filename>します。 **警告:** を使用する場合、 **lodctr/r**コマンドをすべてのパフォーマンス カウンターのレジストリ設定を上書きし、説明のテキスト、指定されたファイルで定義されている構成に置き換えることができます。|
|/t:<servicename>|そのサービスを示します<servicename>が信頼されています。|
|/?|コマンド プロンプトにヘルプを表示します。|
## <a name="remarks"></a>注釈
入力する情報にスペースが含まれている場合は、テキストを囲む引用符を使用して (たとえば、"<filename>")。
## <a name="BKMK_Examples"></a>例
現在のパフォーマンスのレジストリ設定を保存し、カウンターの説明のテキスト ファイルに**perf backup1.txt**:
```
lodctr /s:"perf backup1.txt"
```
## <a name="additional-references"></a>その他の参照
-   [コマンドライン構文キー](command-line-syntax-key.md)

