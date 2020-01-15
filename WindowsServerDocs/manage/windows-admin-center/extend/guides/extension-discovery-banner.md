---
title: 拡張機能の検出バナーを有効にする
description: 拡張機能の検出バナーを有効にする
ms.technology: manage
ms.topic: article
author: daniellee-msft
ms.author: jol
ms.date: 06/06/2019
ms.localizationpriority: medium
ms.prod: windows-server
ms.openlocfilehash: d761ba61ae5680373c334889799e82e5d092a0d4
ms.sourcegitcommit: 083ff9bed4867604dfe1cb42914550da05093d25
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/14/2020
ms.locfileid: "75950107"
---
# <a name="enabling-the-extension-discovery-banner"></a>拡張機能の検出バナーを有効にする

>適用対象: Windows Admin Center、Windows Admin Center Preview

Windows 管理センタープレビュー1903で利用可能な新機能は、拡張機能の検出バナーです。 この機能を使用すると、拡張機能でサポートされているサーバーハードウェアの製造元とモデルを宣言できます。また、拡張機能が使用可能なサーバーまたはクラスターにユーザーが接続すると、拡張機能を簡単にインストールするための通知バナーが表示されます。 拡張機能の開発者は拡張機能の可視性を向上させることができ、ユーザーはサーバーの管理機能をさらに簡単に検出できます。

![拡張機能の検出バナー](../../media/extend-guides-extension-discovery-banner/extension-discovery-banner.png)

## <a name="how-the-extension-discovery-banner-works"></a>拡張機能検出バナーの動作

Windows 管理センターが起動されると、登録されている拡張機能フィードに接続され、使用可能な拡張機能パッケージのメタデータがフェッチされます。 その後、ユーザーが Windows 管理センターでサーバーまたはクラスターに接続すると、サーバーハードウェアの製造元とモデルが読み込まれ、概要ツールに表示されます。 現在のサーバーの製造元やモデルがサポートされていることを宣言する拡張機能が見つかった場合は、ユーザーに知らせるバナーを表示します。 [Set up now] \ (今すぐセットアップ \) リンクをクリックすると、ユーザーは拡張機能マネージャーを使用して拡張機能をインストールできるようになります。

## <a name="how-to-implement-the-extension-discovery-banner"></a>拡張機能の検出バナーを実装する方法

Nuspec ファイルの "tags" メタデータは、拡張機能でサポートされているハードウェアの製造元やモデルを宣言するために使用されます。 タグはスペースで区切られ、製造元またはモデルタグのいずれか、またはその両方を追加して、サポートされている製造元やモデルを宣言できます。 タグの形式 ``"[value type]_[value condition]"`` は、[value type] が "Manufacturer" または "Model" (大文字と小文字が区別されます) のいずれかで、[値の条件] は、製造元またはモデル文字列を定義する[Javascript の正規表現](https://developer.mozilla.org/docs/Web/JavaScript/Guide/Regular_Expressions)であり、[値の種類] と [値の条件] はアンダースコアで区切られます。 この文字列は、URI エンコーディングを使用してエンコードされ、nuspec "tags" メタデータ文字列に追加されます。

### <a name="example"></a>例

たとえば、Contoso Inc. という名前の会社のサーバーをサポートする拡張機能を、モデル名 R3xx と R4xx を使用して開発したとします。

1. 製造元のタグが ``"Manufacturer_/Contoso Inc./"``されます。 モデルのタグは ``"Model_/^R[34][0-9]{2}$/"``可能性があります。 一致条件をどの程度厳密に定義するかによって、正規表現を定義するためのさまざまな方法があります。 また、製造元またはモデルタグを複数のタグに分割することもできます。たとえば、モデルタグを ``"Model_/R3../ Model_/R4../"``することもできます。
2. 正規表現をテストするには、web ブラウザーの DevTools コンソールを使用します。 Edge または Chrome で、F12 キーを押して [DevTools] ウィンドウを開き、[コンソール] タブで次のように入力して、Enter キーを押します。

   ```javascript
   var regex = /^R[34][0-9]{2}$/
   ```

   その後、次のように入力して実行すると、' true ' が返されます。

   ```javascript
   regex.test('R300')
   ```

   次のように実行すると、' false ' が返されます。

   ```javascript
   regex.test('R500')
   ```

3. 正規表現を確認したら、次の Javascript メソッドを使用して、DevTools コンソールでもエンコードできます。

   ```javascript
   encodeURI(/^R[34][0-9]{2}$/)
   ```

   Nuspec ファイルに追加するタグ文字列の最終的な形式は次のようになります。

   ```
   <tags>Manufacturer_/Contoso%20Inc./ Model_/%5ER%5B34%5D%5B0-9%5D%7B2%7D$/</tags>
   ```

> [!Tip]
> ハードウェアの製造元には、一部がサポートされていないものの、一部がサポートされている可能性がある非常に広い範囲のモデル名があることを理解しています。 この機能は拡張機能の**検出**を支援することを目的としていますが、すべてのモデルの完全に最新のインベントリである必要はありません。 正規表現は、モデルのサブセットに一致する単純な式として定義できます。 条件に一致しないサーバーモデルに最初に接続した場合、探索バナーが表示されないことがありますが、その場合は、拡張機能を検出してインストールする別のサーバーに接続します。 製造元名にのみ一致する単純な正規表現を定義することも検討してください。 場合によっては、拡張機能によって特定のモデルが実際にサポートされない場合がありますが、[動的ツール表示機能](./dynamic-tool-display.md)を使用して、モデルのサポートを確認し、必要に応じて拡張機能のみを表示したり、すべての機能をサポートしていないモデルの拡張機能を制限したりすることができます。