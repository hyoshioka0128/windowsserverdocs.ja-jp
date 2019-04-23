---
title: 拡張機能で PowerShell を使用する
description: Windows Admin Center SDK (プロジェクト ホノルル) 拡張機能で PowerShell を使用します。
ms.technology: manage
ms.topic: article
author: nwashburn-ms
ms.author: niwashbu
ms.date: 06/18/2018
ms.localizationpriority: medium
ms.prod: windows-server-threshold
ms.openlocfilehash: ae5004104150c510a56c06161c9280e029968298
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/17/2019
ms.locfileid: "59867603"
---
# <a name="using-powershell-in-your-extension"></a>拡張機能で PowerShell を使用する #

>適用先:Windows Admin Center、Windows Admin Center プレビュー

Windows Admin Center の拡張機能 SDK にさらに深くしましょう: 拡張機能への PowerShell コマンドを追加する方法について説明します。

## <a name="powershell-in-typescript"></a>TypeScript での PowerShell ##

Gulp のビルド プロセスには、すべて".ps1"は「/src/リソース/スクリプト」フォルダーに配置され、「src/生成」フォルダーの下の「powershell スクリプト」クラスを作成する場合に生成する手順があります。

>[!NOTE] 
> "Powershell scripts.ts"も"strings.ts"ファイルを手動で更新はありません。 [次へ] の生成に対して行った変更が上書きされます。

### <a name="adding-your-own-powershell-script"></a>独自の PowerShell スクリプトを追加します。 ##

詳細については、独自の PowerShell スクリプトをすぐに追加する方法を追加します。

### <a name="managing-powershell-sessions"></a>PowerShell セッションの管理 ###

Windows Admin Center での PowerShell を使用しているときにセッションは、スクリプトの実行プロセスの必要なコンポーネントです。 リモートの管理対象サーバーでスクリプトを実行するには、PowerShell 実行空間を使用します。 Windows Admin Center は、の有効期間を管理し、シーケンシャル スクリプトの実行の実行空間を再利用を有効にする PowerShellSession オブジェクト内の実行空間の作成と管理をラップします。

すべてのコンポーネントは、3 つのオプションを使用して、AppContextService クラスによって作成されるセッション オブジェクトへの参照を作成する必要があります。
<!-- I don't 100% get this part - it looks like you're adding 3 arguments - nodeName, <session key>, and <PowerShellSessionRequestOptions>. I got that from looking at the examples, not the text. We need to rework those paras explaining. -->
``` ts
this.psSession = this.appContextService.powerShell.createSession(this.appContextService.activeConnection.nodeName);
```

CreateSession メソッドに、ノードの名前を指定して、新しい PowerShell セッションが作成、使用、および PowerShell 呼び出しの完了時にすぐに破棄します。 この機能は、1 回限りの呼び出しが繰り返し使用されるパフォーマンスに影響することができます。 セッションは作成するには約 1 秒、速度低下を招くので継続的にセッションをリサイクルします。

``` ts
this.psSession = this.appContextService.powerShell.createSession(this.appContextService.activeConnection.nodeName, '<session key>');
```

最初の省略可能なパラメーターは、\<セッション キー\>パラメーター。 これには、検索して (つまり Component2 がその同じセッションを使用して Component1"SME ROCKS、"キーを使用してセッションを作成できます) のコンポーネントでも、再利用が可能なキー付きのセッションが作成されます。  

``` ts
this.psSession = this.appContextService.powerShell.createSession(this.appContextService.activeConnection.nodeName, '<session key>', <PowerShellSessionRequestOptions>);
```
<!-- The second optional parameter is \<PowerShellSessionRequestOptions\> that does ... ? -->
### <a name="common-patterns"></a>一般的なパターン ###

ほとんどの場合、キー付きのセッションを作成、 **ngOnInit**メソッド、および内のイメージの dispose、 **ngOnDestroy**します。 コンポーネントがコンポーネント間で共有されていない、基になるセッション内の複数の PowerShell スクリプトがある場合、このパターンに従います。

最良の結果をサービスではなく、コンポーネントの内部で管理されるセッションの作成 - その有効期間を維持するかどうかを確認し、クリーンアップを適切に管理することができます。