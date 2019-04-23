---
title: winsat mfmedia
description: Windows コマンド
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 09a3b3dd-f746-4e6e-b684-76a9bde0c78d
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 69ce4fac127a6af8a94f3800d62c45989cf7020b
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/17/2019
ms.locfileid: "59845433"
---
# <a name="winsat-mfmedia"></a>winsat mfmedia



ビデオのデコード (再生) メディア ファンデーション フレームワークを使用してパフォーマンスを測定します。

このコマンドを使用する方法の例については、[例](#BKMK_examples)を参照してください。

## <a name="syntax"></a>構文

```
winsat mfmedia <parameters>
```

## <a name="parameters"></a>パラメーター

|パラメーター|説明|
|----------|-----------|
|-入力\<ファイル名 >|［必須］:ビデオ クリップを再生またはエンコードを含むファイルを指定します。 メディア ファンデーションによってレンダリングできる任意の形式で、ファイルができます。|
|-dumpgraph|評価の開始前に、フィルター グラフが GraphEdit と互換性のあるファイルに保存されることを指定します。|
|ns|入力ファイルの標準の再生速度でフィルター グラフを実行するかを指定します。 既定では、フィルターのグラフはプレゼンテーション時間を無視して、できるだけ速く実行されます。|
|-再生|実行での評価モードとプレイのいずれかの指定で指定されたファイルのオーディオのコンテンツのデコード **-入力**既定 DirectSound デバイスを使用します。 既定では、オーディオ再生は無効です。|
|-nopmp|Media Foundation 保護されたメディア パイプライン (MFPMP) を使用しないで、評価時に処理します。|
|-pmp|必ず、MFPMP の使用、評価時に処理します。</br>注:場合 **- pmp**または **- nopmp**が指定されていない、MFPMP は必要な場合にのみ使用されます。|
|-v|状態と進行状況の情報を含む、STDOUT に詳細な出力を送信します。 すべてのエラーは、コマンド ウィンドウにも書き込まれます。|
|xml\<ファイル名 >|評価の出力は、指定した XML ファイルとして保存します。 指定したファイルが存在する場合は上書きされます。|
|-idiskinfo|一部として物理ボリュームと論理ディスクに関する情報を保存、  **\<SystemConfig >** XML 出力にセクション。|
|-iguid|XML 出力ファイルのグローバル一意識別子 (GUID) を作成します。|
|-「メモのテキスト」に注意してください|注意のテキストを追加、 **\<注 >** XML 出力ファイルのセクション。|
|これによって icn-|XML 出力ファイルには、ローカル コンピューター名を含めます。|
|-eef|XML 出力ファイルに追加のシステム情報を列挙します。|

## <a name="BKMK_examples"></a>例

-   次の例では、評価を実行中で使用される入力ファイルを使用して、**正式な winsat** Media Foundation 保護されたメディア パイプライン (MFPMP)、c:\windows の場所のコンピューターに採用することなしの評価Windows のフォルダーです。  
    ```
    winsat mfmedia -input c:\windows\performance\winsat\winsat.wmv -nopmp
    ```

## <a name="remarks"></a>注釈

-   ローカルの Administrators グループ、またはそれと同等のメンバーシップが使用するために必要な最低限**winsat**します。 コマンドは、管理者特権でコマンド プロンプト ウィンドウから実行する必要があります。
-   管理者特権でコマンド プロンプト ウィンドウを開くには、次のようにクリックします**開始**、 をクリック**アクセサリ**、を右クリック**コマンド プロンプト**、 をクリック**を管理者として実行。**.

#### <a name="additional-references"></a>その他の参照情報

