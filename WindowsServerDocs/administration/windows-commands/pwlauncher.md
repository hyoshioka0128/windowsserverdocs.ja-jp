---
title: pwlauncher
description: 'Windows コマンド」のトピック * * *- '
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 0917bb7b-408a-40f7-a1c5-20e94c10d38b
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 8ec9748056b296bb0c74250b36c762fb86fa90ad
ms.sourcegitcommit: 08eba714d3ceb5f2dfb5486d6b990da1aa4dcbdd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/14/2019
ms.locfileid: "65564649"
---
# <a name="pwlauncher"></a>pwlauncher



有効または、Windows To Go スタートアップ オプション (pwlauncher) を無効にします。 **Pwlauncher**コマンド ライン ツールを使用する、Windows To Go ワークスペースを自動的に起動するコンピューターを構成できます (と仮定すると 1 つが存在する) のファームウェアを入力するか、スタートアップ オプションを変更する必要がなくなります。

このコマンドを使用する方法の例については、[例](#BKMK_examples)を参照してください。

## <a name="syntax"></a>構文

```
Pwlauncher {/enable | /disable}
```

## <a name="parameters"></a>パラメーター

|パラメーター|説明|
|---------|-----------|
|/enable|コンピューターが存在する場合は、USB デバイスから自動的に起動されるように Windows To Go スタートアップ オプションを使用にします。|
|/disable|Windows To Go スタートアップ オプションを無効にファームウェアに手動で構成されていない場合、コンピューターで USB デバイスから起動できることはできません。|
|/?|コマンド プロンプトにヘルプを表示します。|

## <a name="remarks"></a>注釈

Windows To Go を使用しようとしているユーザーの最大の障壁が USB からブートするコンピューターを取得しています。 これは従来、ファームウェアを入力し、コンピューターが正しく構成されるまで、さまざまな構成オプションをしようとして行います。 これはほとんどのユーザーに対して単純な作業でないし、は非常に危険なファームウェアには、レンダリング システムが正しく使用されている場合に使用できないオプションが含まれています。 以降のオペレーティング システムが「Windows To Go スタートアップ オプション」と呼ばれる機能を含む Windows 8and、この問題を軽減するために Windows 内から USB からブートするには、そのコンピューターを構成するユーザーを可能に-これまでに限り、ファームウェアを入力しなくても、ファームウェアでは、USB からブートをサポートします。 最初に、常に USB からブートするシステムを有効にするとがへの影響を考慮する必要があります。 たとえば、マルウェアを含む USB デバイスは、システムを侵害する誤って起動でしたまたはブートの競合が発生する、複数の USB ドライブにプラグインできるようにします。 このため、既定の構成は、Windows To Go スタートアップ オプション既定で無効になっています。 さらに、Windows To Go スタートアップ オプションを構成するのには、管理者特権が必要です。 Pwlauncher コマンド ライン ツールを使用して、Windows To Go スタートアップ オプションを有効にしたかどうか、または**変更 Windows To Go スタートアップ オプション**アプリは前に、コンピューターに挿入する任意の USB デバイスからブートするコンピューターを試みます開始します。

## <a name="BKMK_examples"></a>例

次の例を使用する方法を示しています、 **pwlauncher** USB からブートを有効にするコマンド。
```
Pwlauncher /enable
```

#### <a name="additional-references"></a>その他の参照情報

[コマンド ライン構文の記号](command-line-syntax-key.md)