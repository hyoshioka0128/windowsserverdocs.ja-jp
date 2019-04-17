---
title: ルート ナビゲーション動作の変更
description: Windows Admin Center SDK (Project Honolulu) のソリューション拡張機能の開発 - ルート ナビゲーションの動作の変更
ms.technology: manage
ms.topic: article
author: nwashburn-ms
ms.author: niwashbu
ms.date: 08/07/2018
ms.localizationpriority: medium
ms.prod: windows-server-threshold
ms.openlocfilehash: 4a5cba228aa3a0afed99c0d853c3720a5b46f650
ms.sourcegitcommit: 546229d6b5fa7e16f725c6c35f4dcc272711b811
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/18/2018
ms.locfileid: "4905042"
---
# ソリューション拡張機能のルート ナビゲーションの動作を変更します。

>適用対象: Windows Admin Center、Windows Admin Center Preview

このガイドでは、別の接続のリストの動作を使用して、ソリューションのルートのナビゲーションの動作を変更する方法とツールの一覧を表示または非表示する方法説明します。

## ルートのナビゲーションの動作を変更します。

{拡張ルート} \src で manifest.json ファイルを開き、プロパティ"rootNavigationBehavior"を検索します。 このプロパティは、2 つの有効な値:「接続」または「パス」。 「接続」の動作は、ドキュメントの後半で詳しく説明します。

### として、rootNavigationBehavior パスの設定

値を設定```rootNavigationBehavior```に```path```を削除して、```requirements```プロパティ、および leave、```path```空の文字列プロパティ。 ソリューション拡張機能を構築する最小限必要な構成が完了しました。 ファイルを保存および gulp build]-> [gulp サービスを提供すると、ツール、およびし側拡張機能に読み込む、ローカルの Windows Admin Center の拡張機能です。

有効なマニフェスト エントリ ポイントの配列は、このようになります。
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

このような構造を使って構築されたツール、読み込むには、接続が必須ではないか、ノード接続機能を必要はありませんが、します。

### RootNavigationBehavior として接続の設定

設定すると、```rootNavigationBehavior```プロパティを```connections```、Windows Admin Center のシェルの通知は、接続するか、接続されているノード (常には、いくつかの種類のサーバー) があると、接続の状態を確認します。 これによりが 2 ステップで接続を検証します。 1) Windows Admin Center しようとするための資格情報 (リモート PowerShell セッションを確立)、ノードにログインして、2)、ノードが接続可能な状態である場合の識別に提供する PowerShell スクリプトを実行します。

接続と有効なソリューションの定義は、次のようになります。

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

RootNavigationBehavior が「接続」に設定されている場合、マニフェストでの接続の定義を作成することが必要です。 ここでは、「ヘッダー」プロパティ (ユーザーがメニューから選択すると、ソリューションのヘッダーに表示に使用されます)、connectionTypes 配列、(これを指定する connectionTypes は、ソリューションで使われます。 詳細については、ときドキュメント。)。

## 有効にして、[ツール] メニューを無効にします。 ##

定義のソリューションで利用可能な別のプロパティは、「ツール」プロパティです。 これにより、読み込まれるツールと、[ツール] メニューを表示するかどうかが決まります。 有効にすると、Windows Admin Center は、左側にある [ツール] メニューをレンダリングします。 DefaultTool で必須では、適切なリソースを読み込むためには、マニフェストにツールのエントリ ポイントを追加することです。 "DefaultTool"の値は、マニフェストで定義されているツールの"name"プロパティである必要があります。
