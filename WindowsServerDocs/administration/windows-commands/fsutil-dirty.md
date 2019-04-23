---
ms.assetid: 385a2a7c-d6bd-4f11-9c18-fca0413f9e97
title: ダーティ fsutil
ms.prod: windows-server-threshold
manager: dmoss
ms.author: toklima
author: toklima
ms.technology: storage
audience: IT Pro
ms.topic: article
ms.date: 10/16/2017
ms.openlocfilehash: c308b0497a5a39a25384b22441b733143df8727b
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/17/2019
ms.locfileid: "59852133"
---
# <a name="fsutil-dirty"></a>ダーティ fsutil
>適用先:Windows Server (半期チャネル)、Windows Server 2016、Windows 10、Windows Server 2012 R2、Windows 8.1、Windows Server 2012、Windows 8、Windows Server 2008 R2、Windows 7

クエリまたはボリュームの不良ビットを設定します。 ボリュームがダーティの場合は、ビットが設定、 **autochk**コンピューターが再起動したときに、ボリュームのエラーを自動的にチェックします。

このコマンドを使用する方法の例については、[例](#BKMK_examples)を参照してください。

## <a name="syntax"></a>構文

```
fsutil dirty {query | set} <VolumePath>
```

## <a name="parameters"></a>パラメーター

|パラメーター|説明|
|-------------|---------------|
|クエリ (query)|指定したボリュームの不良ビットを照会します。|
|セット (set)|指定したボリュームの不良ビットを設定します。|
|\<VolumePath >|次の形式でコロンまたは GUID が続く、ドライブ名を指定します。**ボリューム {0}***GUID***}** します。|

## <a name="remarks"></a>注釈

-   ボリュームの不良ビットは、一貫性のない状態で、ファイル システムがありますを示します。 不良ビットを設定できます。

    -   ボリュームがオンラインであり、未処理の変更。

    -   ボリュームに変更を行ったし、しますが、ディスクにコミットする前に、コンピューターがシャット ダウンします。

    -   ボリュームの破損が検出されました。

-   コンピューターを再起動すると、不良ビットが設定されている場合**chkdsk**実行ボリュームに関する問題を解決しようとして、ファイル システムの整合性を確認します。

## <a name="BKMK_examples"></a>例
ドライブ C 上の不良ビットをクエリするには、次のように入力します。

```
fsutil dirty query c:
```

-   ボリュームがダーティの場合は、次の出力が表示されます。

    `Volume C: is dirty`

-   ボリュームがダーティでない場合は、次の出力が表示されます。

    `Volume C: is not dirty`

ドライブ C 上の不良ビットを設定するに次のように入力します。

```
fsutil dirty set C:
```

#### <a name="additional-references"></a>その他の参照情報
[コマンドライン構文キー](Command-Line-Syntax-Key.md)

[Fsutil](Fsutil.md)


