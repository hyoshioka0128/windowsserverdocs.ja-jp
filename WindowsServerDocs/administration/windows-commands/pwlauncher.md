---
title: pwlauncher
description: '* * * * のリファレンストピック'
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 0917bb7b-408a-40f7-a1c5-20e94c10d38b
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 0ddda3ab7831643c3c2c096ae87893d97f90155c
ms.sourcegitcommit: ab64dc83fca28039416c26226815502d0193500c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/01/2020
ms.locfileid: "82722753"
---
# <a name="pwlauncher"></a>pwlauncher



Windows To 進むスタートアップオプション (pwlauncher) を有効または無効にします。 **Pwlauncher**コマンドラインツールを使用すると、コンピューターを Windows to 移動ワークスペースで自動的に起動するように構成することができます (1 つが存在する場合)。ただし、ファームウェアを入力したり、スタートアップオプションを変更したりする必要はありません。



## <a name="syntax"></a>構文

```
Pwlauncher {/enable | /disable}
```

### <a name="parameters"></a>パラメーター

|パラメーター|[説明]|
|---------|-----------|
|/enable|Windows To ゴースタートアップオプションを有効にして、コンピューターが現在 USB デバイスから自動的に起動するようにします。|
|/disable|ファームウェアで手動で構成しない限り、Windows To 進むスタートアップオプションを無効にして、コンピューターを USB デバイスから起動できないようにします。|
|/?|コマンド プロンプトにヘルプを表示します。|

## <a name="remarks"></a>Remarks

Windows To ハードルを使用するユーザーにとって最も大きなメリットは、USB からコンピューターを起動することです。 これは、通常、コンピューターが正しく構成されるまで、ファームウェアを入力してさまざまな構成オプションを試すことによって行われます。 これはほとんどのユーザーにとって簡単な作業ではありません。ファームウェアには、不適切に使用した場合にシステムを使用できなくなるオプションが含まれているため、非常に危険です。 この問題を軽減するために、windows 8 以降のオペレーティングシステムには、windows To ゴースタートアップオプションという機能が含まれています。この機能を使用すると、ファームウェアが USB からの起動をサポートしている限り、ファームウェアを入力することなく、USB から起動するようにユーザーのコンピューターを構成できます。 システムが常に USB から起動できるようにするには、まず考慮する必要があることに注意してください。 たとえば、マルウェアを含む USB デバイスが誤ってシステムを危険にさらす可能性がある場合や、複数の USB ドライブが接続され、ブートの競合が発生する場合があります。 このため、既定の構成では、Windows To 進むスタートアップオプションが既定で無効になっています。 また、Windows To ゴースタートアップオプションを構成するには、管理者特権が必要です。 Pwlauncher コマンドラインツールまたは**Windows To ゴースタートアップオプションを変更**するアプリを使用して Windows to 進むスタートアップオプションを有効にすると、コンピューターは起動前にコンピューターに挿入されている任意の USB デバイスから起動しようとします。

## <a name="examples"></a>例

**Pwlauncher**コマンドを使用して、USB からのブートを有効にする方法について説明します。
```
Pwlauncher /enable
```

## <a name="additional-references"></a>その他のリファレンス

- [コマンド ライン構文の記号](command-line-syntax-key.md)