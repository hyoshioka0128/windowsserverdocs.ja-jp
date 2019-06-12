---
title: 拡張機能の検出のバナーを有効にします。
description: 拡張機能の検出のバナーを有効にします。
ms.technology: manage
ms.topic: article
author: daniellee-msft
ms.author: jol
ms.date: 06/06/2019
ms.localizationpriority: medium
ms.prod: windows-server-threshold
ms.openlocfilehash: fafc16d6acae3c5a7a58a379d2f88998b8e98c3d
ms.sourcegitcommit: 6ef4986391607bb28593852d06cc6645e548a4b3
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/07/2019
ms.locfileid: "66811882"
---
# <a name="enabling-the-extension-discovery-banner"></a>拡張機能の検出のバナーを有効にします。

>適用先:Windows Admin Center、Windows Admin Center プレビュー

Windows Admin Center プレビュー 1903 年の新機能では、拡張機能の検出バナーです。 この機能により、サーバー ハードウェアの製造元とモデルがサポートを宣言する拡張機能と拡張機能を簡単にインストールするユーザーは、サーバーまたは拡張機能の使用可能なクラスターに接続すると通知バナーが表示されます。 拡張機能の開発者がその拡張機能の可視性を取得できなくなり、ユーザーは、サーバーの管理機能を簡単に検出できます。

![拡張機能の検出のバナー](../../media/extend-guides-extension-discovery-banner/extension-discovery-banner.png)

## <a name="how-the-extension-discovery-banner-works"></a>拡張機能の検出バナーのしくみ

Windows Admin Center を起動するが登録されている拡張フィードに接続され、使用可能な拡張機能パッケージのメタデータを取得します。 ユーザーは、サーバーまたは Windows Admin Center でのクラスターに接続するときは、概要ツールに表示するには、サーバー ハードウェアの製造元とモデルを読んだします。 現在のサーバーの製造元やモデルをサポートしていることを宣言する拡張機能、見つかった場合ユーザーに通知するバナーが表示されます。 「今すぐセットアップ」リンクをクリックしてになります、ユーザーに拡張機能マネージャーが、拡張機能をインストールすることができます。

## <a name="how-to-implement-the-extension-discovery-banner"></a>拡張機能の検出のバナーを実装する方法

.Nuspec ファイルで"tags"のメタデータは、どのハードウェアの製造元を宣言するために使用または、拡張機能のサポートをモデル化します。 タグはスペースで区切られます、か、製造元またはモデルのタグまたはその両方をサポートされている製造元やモデルの宣言を追加することができます。 タグの書式は``"[value type]_[value condition]"``[値の型] が「製造元」または「モデル」(大文字小文字を区別) のいずれかには、[値の条件] が、 [Javascript の正規表現](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Guide/Regular_Expressions)製造元またはモデルの文字列と [値の種類] を定義して [条件の値] は、アンダー スコアで区切られます。 この文字列は、エンコードと .nuspec"tags"のメタデータの文字列に追加の URI を使用してエンコードされます。

### <a name="example"></a>例

たとえば、Contoso, Inc. のモデルという会社からサーバーをサポートする拡張機能を開発して R3xx と R4xx の名前します。

1. 製造元のタグになります``"Manufacturer_/Contoso Inc./"``します。 モデルのタグは、``"Model_/^R[34][0-9]{2}$/"``します。 どの程度厳密に一致する条件を定義する、によって、正規表現を定義するさまざまな方法があります。 複数のタグに、製造元またはモデルのタグを分割することも、たとえば、モデルのタグもは``"Model_/R3../ Model_/R4../"``します。
2. Web ブラウザーの DevTools コンソールを使用して正規表現をテストできます。 Edge または Chrome では、DevTools ウィンドウを開く f12 キーを押すし、コンソール タブで、入力ヒットし、次を入力してください。

   ```javascript
   var regex = /^R[34][0-9]{2}$/
   ```

   その後、入力、次を実行すると、'true' を返します。

   ```javascript
   regex.test('R300')
   ```

   次を実行すると、'false' 返すとします。

   ```javascript
   regex.test('R500')
   ```

3. 正規表現を確認した後 DevTools コンソールも、エンコード、次の Javascript メソッドを使用できます。

   ```javascript
   encodeURI(/^R[34][0-9]{2}$/)
   ```

   最終的な .nuspec ファイルに追加するタグの文字列の形式は次のようになります。

   ```
   <tags>Manufacturer_/Contoso%20Inc./ Model_/%5ER%5B34%5D%5B0-9%5D%7B2%7D$/</tags>
   ```

> [!Tip]
> ハードウェアの製造元のモデル名のうちいくつかサポートされる可能性がいくつかは非常に広い範囲であることに認識しています。 支援するものではこの機能に注意してください、**検出**拡張機能が、すべてのモデルの完全に最新のインベントリを使用することはありません。 モデルのサブセットに一致する単純な式を指定するように正規表現を定義できます。 最初の条件と一致しませんサーバー モデルに接続している場合、ユーザーはバナーが検出を表示しない可能性がありますが、遅かれ早かれしは検出し、拡張機能をインストールする別のサーバーに接続します。 製造元の名前とのみ一致する単純な正規表現を定義することも検討できます。 場合によっては、拡張機能は実際に対応していない特定のモデルが使用することができます、[動的なツールの表示機能](./dynamic-tool-display.md)モデルのサポートを確認し、該当する場合に、拡張機能のみを表示するカスタム PowerShell スクリプトを定義するか、すべての機能をサポートしていないモデルの拡張機能に限定の機能を提供します。