---
title: ルート ナビゲーション動作の変更
description: ソリューションの拡張機能 Windows Admin Center SDK (プロジェクト ホノルル) の開発 - ルート ナビゲーションの動作を変更します。
ms.technology: manage
ms.topic: article
author: nwashburn-ms
ms.author: niwashbu
ms.date: 08/07/2018
ms.localizationpriority: medium
ms.prod: windows-server-threshold
ms.openlocfilehash: 4a5cba228aa3a0afed99c0d853c3720a5b46f650
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/17/2019
ms.locfileid: "59861733"
---
# <a name="modify-root-navigation-behavior-for-a-solution-extension"></a>ソリューションの拡張機能のルートのナビゲーション動作を変更します。

>適用先:Windows Admin Center、Windows Admin Center プレビュー

このガイドでは、別の接続の一覧の動作をソリューションのルートのナビゲーション動作を変更する方法とツールの一覧を表示または非表示する方法について説明します。

## <a name="modifying-root-navigation-behavior"></a>ルートのナビゲーション動作を変更します。

{0} 拡張機能ルート} \src で manifest.json ファイルを開き、"rootNavigationBehavior"プロパティが見つかりません。 このプロパティは、2 つの有効な値:「接続」または"path"。 「接続」の動作は、ドキュメントの後半で説明します。

### <a name="setting-path-as-a-rootnavigationbehavior"></a>RootNavigationBehavior として設定パス

値を設定```rootNavigationBehavior```に```path```、し、削除、```requirements```プロパティ、およびままにしてください、```path```として空の文字列プロパティ。 ソリューションの拡張機能を構築する最低限必要な構成を完了しました。 ファイルを保存し、gulp のビルド]-> [するとして gulp の機能とツール、およびし側拡張機能を読み込むローカル Windows Admin Center の拡張機能にします。

有効なマニフェストのエントリ ポイントの配列のようになります。
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

このような構造に組み込まれているツールを読み込むには、必須ではない接続ではノードの接続機能にもありません。

### <a name="setting-connections-as-a-rootnavigationbehavior"></a>接続を rootNavigationBehavior として設定

設定すると、```rootNavigationBehavior```プロパティを```connections```、Windows Admin Center シェルの通知は、接続されているノード (常に何らかの種類のサーバーの場合) に接続することがある接続の状態を確認します。 これにより、2 つの手順には接続を確認しています。 1) Windows Admin Center は (リモートの PowerShell セッションの確立)、用の資格情報を持つノードにログインを試行しようと、2) ノードが接続可能な状態である場合を識別するために指定した PowerShell スクリプトが実行されます。

接続の定義が有効なソリューションは、次のようになります。

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

RootNavigationBehavior が「接続」に設定されている場合は、マニフェスト内の接続の定義をビルドする必要があります。 これは"header"プロパティを (ユーザーがメニューから選択すると、ソリューションのヘッダーの表示に使用されます)、(これは指定する connectionTypes はソリューションで使用 connectionTypes 配列が含まれます。 します。 詳細については、するときのドキュメントです。)。

## <a name="enabling-and-disabling-the-tools-menu"></a>有効にして、[ツール] メニューを無効化 ##

ソリューションの定義で使用できる別のプロパティは、"tools"プロパティです。 これは、ツールに読み込まれると、[ツール] メニューを表示するかどうかに影響します。 有効な場合、Windows Admin Center は左側にある [ツール] メニューに表示されます。 DefaultTool、必要なは、適切なリソースを読み込むためには、マニフェストに、ツールのエントリ ポイントを追加することです。 "DefaultTool"の値は、マニフェストで定義されているツールの"name"プロパティである必要があります。
