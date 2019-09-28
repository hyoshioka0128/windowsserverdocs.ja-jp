---
title: pwlauncher
description: 'Windows コマンドに関するトピック * * * *- '
ms.custom: na
ms.prod: windows-server
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
ms.openlocfilehash: 4cf65643e0c5a4b28e06619a8156792b6e5456ea
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/27/2019
ms.locfileid: "71371967"
---
# <a name="pwlauncher"></a>pwlauncher



Windows To 進むスタートアップオプション (pwlauncher) を有効または無効にします。 **Pwlauncher**コマンドラインツールを使用すると、コンピューターを Windows to 移動ワークスペースで自動的に起動するように構成することができます (1 つが存在する場合)。ただし、ファームウェアを入力したり、スタートアップオプションを変更したりする必要はありません。

このコマンドを使用する方法の例については、[例](#BKMK_examples)を参照してください。

## <a name="syntax"></a>構文

```
Pwlauncher {/enable | /disable}
```

## <a name="parameters"></a>パラメーター

|パラメーター|説明|
|---------|-----------|
|/enable|Windows To ゴースタートアップオプションを有効にして、コンピューターが現在 USB デバイスから自動的に起動するようにします。|
|/disable|ファームウェアで手動で構成しない限り、Windows To 進むスタートアップオプションを無効にして、コンピューターを USB デバイスから起動できないようにします。|
|/?|コマンド プロンプトにヘルプを表示します。|

## <a name="remarks"></a>コメント

Windows To ハードルを使用するユーザーにとって最も大きなメリットは、USB からコンピューターを起動することです。 これは、通常、コンピューターが正しく構成されるまで、ファームウェアを入力してさまざまな構成オプションを試すことによって行われます。 これはほとんどのユーザーにとって簡単な作業ではありません。ファームウェアには、不適切に使用した場合にシステムを使用できなくなるオプションが含まれているため、非常に危険です。 この問題を軽減するために、Windows 8 以降のオペレーティングシステムには、"Windows To 進むスタートアップオプション" という機能が含まれています。これにより、ユーザーは、ファームウェアを入力することなく、Windows 内から USB から起動するようにコンピューターを構成できます。ファームウェアは、USB からの起動をサポートしています。 システムが常に USB から起動できるようにするには、まず考慮する必要があることに注意してください。 たとえば、マルウェアを含む USB デバイスが誤ってシステムを危険にさらす可能性がある場合や、複数の USB ドライブが接続され、ブートの競合が発生する場合があります。 このため、既定の構成では、Windows To 進むスタートアップオプションが既定で無効になっています。 また、Windows To ゴースタートアップオプションを構成するには、管理者特権が必要です。 Pwlauncher コマンドラインツールまたは**Windows To ゴースタートアップオプションを変更**するアプリを使用して Windows to 進むスタートアップオプションを有効にすると、コンピューターは起動前にコンピューターに挿入されている任意の USB デバイスから起動しようとします。

## <a name="BKMK_examples"></a>例

次の例では、 **pwlauncher**コマンドを使用して、USB からのブートを有効にする方法を示します。
```
Pwlauncher /enable
```

#### <a name="additional-references"></a>その他の参照情報

[コマンド ライン構文の記号](command-line-syntax-key.md)