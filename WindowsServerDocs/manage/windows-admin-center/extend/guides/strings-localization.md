---
title: Windows 管理センターでの文字列とローカライズ
description: Windows 管理センター SDK (Project ホノルル) で、ローカライズ可能な文字列を取得する方法について説明します。
ms.topic: article
author: nwashburn-ms
ms.author: niwashbu
ms.date: 06/18/2018
ms.localizationpriority: medium
ms.openlocfilehash: 565e4da69466549538c380457269304c7f1cdd5a
ms.sourcegitcommit: dfa48f77b751dbc34409aced628eb2f17c912f08
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/07/2020
ms.locfileid: "87944922"
---
# <a name="strings-and-localization-in-windows-admin-center"></a>Windows 管理センターでの文字列とローカライズ #

>適用先:Windows Admin Center、Windows Admin Center Preview

Windows 管理センターの拡張機能 SDK についてさらに詳しく説明し、文字列とローカライズについて説明します。

プレゼンテーション層に表示されるすべての文字列のローカライズを有効にするには、/src/resources/strings の下にある文字列の resjson ファイルを使用します。これは既に設定されています。 拡張機能に新しい文字列を追加する必要がある場合は、新しいエントリとしてこの resjson ファイルに追加します。 既存の構造は、次の形式に従います。

``` ts
"<YourExtensionName>_<Component>_<Accessor>": "Your string value goes here.",
```

文字列には任意の形式を使用できますが、生成プロセス (resjson を取得し、使用可能な TypeScript クラスを出力するプロセス) は、アンダースコア (_) をピリオド (.) に変換することに注意してください。

たとえば、次のエントリがあるとします。
``` ts
"HelloWorld_cim_title": "CIM Component",
```
では、次のアクセサー構造が生成されます。
``` ts
MsftSme.resourcesStrings<Strings>().HelloWorld.cim.title;
```

## <a name="add-other-languages-for-localization"></a>ローカリゼーション用の他の言語を追加する ##

他の言語にローカライズする場合は、各言語に対して文字列. resjson ファイルを作成する必要があります。 これらのファイルは、に配置する必要があり ```\loc\output\{!ExtensionName}\{!LanguageFolder}\strings.resjson``` ます。 対応するフォルダーで使用できる言語は次のとおりです。

| Language      | フォルダー      |
| ------------- |-------------|
| Čeština | cs-CZ |
| Deutsch | de-DE |
| 英語 | ja-JP |
| Español | es-ES |
| Français | fr-FR |
| Magyar | hu-HU |
| Italiano | it-IT |
| Japanese | ja-JP |
| 한국어 | ko-KR |
| Nederlands | nl-NL |
| Polski | pl-PL |
| Português (Brasil) | pt-BR |
| Português (Portugal) | pt-PT |
| Русский | ru-RU |
| Svenska | sv-SE |
| Türkçe    | tr-TR |
| 中文 (简体) | zh-CN |
| 中文 (繁體) | zh-TW |
> [!NOTE]
> ファイル構造のニーズが loc/output の中で異なる場合は、gulpfile.js にある gulp タスクの localeOffset を調整する必要があります。これは、このような場合に発生します。 このオフセットは、文字列の検索を開始する loc フォルダーの深さです。 resjson ファイル。

各文字列. resjson ファイルは、このガイドの冒頭で説明したのと同じ方法で書式設定されます。

たとえば、スペイン語のローカライズを含めるには、次のエントリをに追加し ```\loc\output\HelloWorld\es-ES\strings.resjson``` ます。
```json
"HelloWorld_cim_title": "CIM Componente",
```
ローカライズされた文字列を追加した場合は、gulp の生成を再度実行して、表示されるようにする必要があります。 次のコマンドを実行します。
``` cmd
gulp generate
```

文字列が生成されたことを確認するには、に移動 ```\src\app\assets\strings\{!LanguageFolder}\strings.resjson``` します。 新しく追加されたエントリがこのファイルに表示されます。
Windows 管理センターで言語オプションを切り替えると、ローカライズされた文字列が拡張機能に表示されるようになります。
