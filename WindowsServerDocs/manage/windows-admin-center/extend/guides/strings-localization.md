---
title: 文字列と Windows Admin Center でのローカライズ
description: Windows Admin Center SDK (プロジェクト ホノルル) でのローカライズ可能、文字列の取得について説明します
ms.technology: manage
ms.topic: article
author: nwashburn-ms
ms.author: niwashbu
ms.date: 06/18/2018
ms.localizationpriority: medium
ms.prod: windows-server-threshold
ms.openlocfilehash: fb328f86c98141a5a2a1c4fd05ec1d4c96a7bc5f
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/17/2019
ms.locfileid: "59845403"
---
# <a name="strings-and-localization-in-windows-admin-center"></a>文字列と Windows Admin Center でのローカライズ #

>適用先:Windows Admin Center、Windows Admin Center プレビュー

文字列とローカライズについて説明を Windows Admin Center の拡張機能 SDK をさらに深くしましょう。

プレゼンテーション層、活用/src/resources/strings - strings.resjson ファイル上に描画されるすべての文字列のローカライズを有効にするには、既に設定されます。 新しい文字列、拡張機能を追加する必要がある場合は、新しいエントリとしてこの resjson ファイルに追加、します。 既存の構造では、この形式に従います。

``` ts
"<YourExtensionName>_<Component>_<Accessor>": "Your string value goes here.",
```

の文字列たい任意の形式を使用できますが、生成処理 (、resjson を受け取り、使用可能な TypeScript クラスを出力するプロセス) がピリオド (.) にアンダー スコア (_) を変換することに注意してください。

たとえば、このエントリ。
``` ts
"HelloWorld_cim_title": "CIM Component",
```
次のアクセサー構造が生成されます。
``` ts
MsftSme.resourcesStrings<Strings>().HelloWorld.cim.title;
```
