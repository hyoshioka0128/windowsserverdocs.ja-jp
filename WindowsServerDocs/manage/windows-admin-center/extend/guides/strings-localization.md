---
title: 文字列と Windows Admin Center でローカライズ
description: ため Windows Admin Center SDK (Project Honolulu) で、文字列のローカライズの準備について説明します
ms.technology: manage
ms.topic: article
author: nwashburn-ms
ms.author: niwashbu
ms.date: 06/18/2018
ms.localizationpriority: medium
ms.prod: windows-server-threshold
ms.openlocfilehash: f0671160bd790d80e35f6d6c1586a07969939070
ms.sourcegitcommit: f1edfc6525e09dd116b106293f9260123a94de0c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/12/2019
ms.locfileid: "9296734"
---
# 文字列と Windows Admin Center でローカライズ #

>適用対象: Windows Admin Center、Windows Admin Center Preview

文字列とローカライズについて説明して Windows Admin Center の拡張 SDK をより詳細なみましょう。

プレゼンテーション層を利用することで/src/resources/strings - strings.resjson ファイルの上に描画されるすべての文字列のローカライズを有効にするには、既に設定されています。 拡張機能を新しい文字列を追加する必要がある場合は、新しいエントリとしてこの resjson ファイルに追加しています。 既存の構造はこの形式に従います。

``` ts
"<YourExtensionName>_<Component>_<Accessor>": "Your string value goes here.",
```

文字列の任意の形式を使用できますが、生成プロセス (、resjson を受け取り、使用可能な TypeScript クラスを出力するプロセス) がピリオド (.) にアンダー スコア (_) を変換することに注意してください。

たとえば、このエントリします。
``` ts
"HelloWorld_cim_title": "CIM Component",
```
次のアクセサー構造が生成されます。
``` ts
MsftSme.resourcesStrings<Strings>().HelloWorld.cim.title;
```

## ローカライズのための他の言語を追加します。 ## 

他の言語にローカライズ、strings.resjson ファイルは、各言語用に作成する必要があります。 これらのファイルが内の場所をする必要がある```\loc\output\{!ExtensionName}\{!LanguageFolder}\strings.resjson```します。 対応するフォルダーで使用できる言語は次のとおりです。

| 言語      | フォルダー      |
| ------------- |-------------|
| Čeština | cs-CZ |
| Deutsch | de-DE |
| 英語 | ja-JP |
| としてスペイン語 | es-ES |
| Français | fr-FR | 
| Magyar | hu-HU | 
| 語 | it-IT |
| 日本語 | ja-JP | 
| 한국어 | ko-KR | 
| 語 | nl-NL |
| Polski | pl-PL |
| Português (Brasil) | pt-BR |
| Português (ポルトガル) | pt-PT |
| РУССКИЙ | ru-RU |
| Svenska | sv-SE |
| Türkçe    | tr-TR |
| 中文(简体) | zh-CN |
| 中文(繁體) | zh-TW |
> [!NOTE]
> ファイル構造のニーズがローカライズされた/出力の別の内側の場合は、' 生成 resjson-json-ローカライズ '、gulpfile.js で公開されている gulp タスクの localeOffset を調整する必要があります。 このオフセットは strings.resjson ファイルの検索を開始する必要がありますが、ローカライズされたフォルダーから深い方法です。

各 strings.resjson ファイルは、このガイドの上部にある上述したものと同じ方法でフォーマットされます。 

たとえば、としてスペイン語にローカライズ含める含めるでは、このエントリ```\loc\output\HelloWorld\es-ES\strings.resjson```: 
```json
"HelloWorld_cim_title": "CIM Componente",
```
いつでも、ローカライズされた文字列を追加した、gulp 生成する必要があります表示するためにもう一度実行します。 次のコマンドを実行します。
``` cmd
gulp generate 
```

文字列が生成されたことを確認する] に移動```\src\app\assets\strings\{!LanguageFolder}\strings.resjson```します。 このファイルで、新しく追加されたエントリが表示されます。
できるようになりました Windows Admin Center で言語のオプションを切り替えた場合は、拡張機能内のローカライズされた文字列を表示することはできます。 
