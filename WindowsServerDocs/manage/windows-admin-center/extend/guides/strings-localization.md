---
title: Windows 管理センターでの文字列とローカライズ
description: Windows 管理センター SDK (Project ホノルル) で、ローカライズ可能な文字列を取得する方法について説明します。
ms.technology: manage
ms.topic: article
author: nwashburn-ms
ms.author: niwashbu
ms.date: 06/18/2018
ms.localizationpriority: medium
ms.prod: windows-server
ms.openlocfilehash: 61289ae175ca8b906386cff9e36f5023ea28d051
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/27/2019
ms.locfileid: "71385239"
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

他の言語にローカライズする場合は、各言語に対して文字列. resjson ファイルを作成する必要があります。 これらのファイルは、に```\loc\output\{!ExtensionName}\{!LanguageFolder}\strings.resjson```配置する必要があります。 対応するフォルダーで使用できる言語は次のとおりです。

| [言語]      | フォルダー      |
| ------------- |-------------|
| Čeština | cs-CZ |
| Deutsch | de-DE |
| 英語 | en-US |
| Español | es-ES |
| Français | fr-FR | 
| Magyar | hu-HU | 
| Italiano | it-IT |
| 日本語 | ja-JP | 
| 한국어 | ko-KR | 
| Nederlands | nl-NL |
| Polski | pl-PL |
| Português (Brasil) | pt-BR |
| Português (Portugal) | pt-PT |
| ロシア語 | ru-RU |
| Svenska | sv-SE |
| Türkçe    | tr-TR |
| 中文 (简体) | zh-CN |
| 中文 (繁體) | zh-TW |
> [!NOTE]
> ファイル構造のニーズが loc/output 内で異なる場合は、gulpfile にある gulp タスクの localeOffset を調整する必要があります。これは、にあります。 このオフセットは、文字列の検索を開始する loc フォルダーの深さです。 resjson ファイル。

各文字列. resjson ファイルは、このガイドの冒頭で説明したのと同じ方法で書式設定されます。 

たとえば、スペイン語のローカライズを含めるには、次のエントリ```\loc\output\HelloWorld\es-ES\strings.resjson```をに追加します。 
```json
"HelloWorld_cim_title": "CIM Componente",
```
ローカライズされた文字列を追加した場合は、gulp の生成を再度実行して、表示されるようにする必要があります。 次のコマンドを実行します。
``` cmd
gulp generate 
```

文字列が生成されたことを確認する```\src\app\assets\strings\{!LanguageFolder}\strings.resjson```には、に移動します。 新しく追加されたエントリがこのファイルに表示されます。
Windows 管理センターで言語オプションを切り替えると、ローカライズされた文字列が拡張機能に表示されるようになります。 
