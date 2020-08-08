---
title: ルート ナビゲーション動作の変更
description: ソリューション拡張機能の開発 Windows 管理センター SDK (Project ホノルル)-ルートナビゲーション動作の変更
ms.topic: article
author: nwashburn-ms
ms.author: niwashbu
ms.date: 08/07/2018
ms.localizationpriority: medium
ms.openlocfilehash: bc7ef3c25c41abd6c7b91e37cecca017664ee223
ms.sourcegitcommit: dfa48f77b751dbc34409aced628eb2f17c912f08
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/07/2020
ms.locfileid: "87944943"
---
# <a name="modify-root-navigation-behavior-for-a-solution-extension"></a>ソリューション拡張機能のルートナビゲーション動作を変更する

>適用先:Windows Admin Center、Windows Admin Center Preview

このガイドでは、ソリューションのルートナビゲーション動作を変更して、さまざまな接続リストの動作を設定する方法と、ツールの一覧を表示または非表示にする方法について説明します。

## <a name="modifying-root-navigation-behavior"></a>ルートナビゲーション動作の変更

{Extension root} \ src のファイルで manifest.jsを開き、プロパティ "rootNavigationBehavior" を見つけます。 このプロパティには、"connections" または "path" という2つの有効な値があります。 "接続" の動作については、ドキュメントの後半で詳しく説明します。

### <a name="setting-path-as-a-rootnavigationbehavior"></a>RootNavigationBehavior としてのパスの設定

の値をに設定し、 ```rootNavigationBehavior``` ```path``` プロパティを削除して、プロパティを ```requirements``` 空の文字列のままにし ```path``` ます。 ソリューション拡張機能をビルドするために必要な最小限の構成が完了しました。 ファイルを保存し、> gulp gulp をツールと同じように保存して、拡張機能をローカルの Windows 管理センターの拡張機能にサイドロードします。

有効なマニフェスト entryPoints 配列は次のようになります。
```
    "entryPoints": [
        {
          "entryPointType": "solution",
          "name": "main",
          "urlName": "testsln",
          "displayName": "resources:strings:displayName",
          "description": "resources:strings:description",
          "icon": "sme-icon:icon-win-powerShell",
          "path": "",
          "rootNavigationBehavior": "path"
        }
    ],
```

この種類の構造で構築されたツールでは、読み込みに接続する必要はありませんが、ノード接続機能は使用できません。

### <a name="setting-connections-as-a-rootnavigationbehavior"></a>RootNavigationBehavior としての接続の設定

プロパティをに設定すると、接続する必要がある接続された ```rootNavigationBehavior``` ```connections``` ノード (常に何らかの種類のサーバー) が存在することを Windows 管理センターシェルに通知し、接続の状態を確認します。 これにより、接続を確認する手順が2つあります。 1) Windows 管理センターは、(リモート PowerShell セッションを確立するために) 資格情報を使用してノードにログインしようとします。 2) 指定した PowerShell スクリプトを実行して、ノードが接続可能な状態であるかどうかを識別します。

接続を含む有効なソリューション定義は次のようになります。

``` json
        {
          "entryPointType": "solution",
          "name": "example",
          "urlName": "solutionexample",
          "displayName": "resources:strings:displayName",
          "description": "resources:strings:description",
          "icon": "sme-icon:icon-win-powerShell",
          "rootNavigationBehavior": "connections",
          "connections": {
            "header": "resources:strings:connectionsListHeader",
            "connectionTypes": [
                "msft.sme.connection-type.example"
                ]
            },
            "tools": {
                "enabled": false,
                "defaultTool": "solution"
            }
        },
```

RootNavigationBehavior が "connections" に設定されている場合は、マニフェスト内の接続定義を構築する必要があります。 これには、"header" プロパティ (ユーザーがメニューから選択したときにソリューションヘッダーに表示される)、connectionTypes 配列 (ソリューションで使用される connectionTypes が指定されます) が含まれます。 詳細については、connectionProvider のドキュメントを参照してください。)

## <a name="enabling-and-disabling-the-tools-menu"></a>[ツール] メニューの有効化と無効化 ##

ソリューション定義で使用できるもう1つのプロパティは、"tools" プロパティです。 これにより、[ツール] メニューが表示されているかどうか、および読み込まれるツールが決まります。 有効にすると、Windows 管理センターで左側の [ツール] メニューが表示されます。 DefaultTool では、適切なリソースを読み込むために、マニフェストにツールのエントリポイントを追加する必要があります。 "DefaultTool" の値は、マニフェストで定義されているツールの "name" プロパティである必要があります。
