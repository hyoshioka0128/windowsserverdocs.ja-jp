---
title: winsat の mfmedia
description: Winsat のリファレンス。メディアファンデーション framework を使用したビデオデコード (再生) のパフォーマンスを測定します。
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 09a3b3dd-f746-4e6e-b684-76a9bde0c78d
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 3a03304f4df27dc7fdf9bb0af5e2f4d6f2b9c98d
ms.sourcegitcommit: ab64dc83fca28039416c26226815502d0193500c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/01/2020
ms.locfileid: "82720663"
---
# <a name="winsat-mfmedia"></a>winsat の mfmedia



メディアファンデーション framework を使用したビデオデコード (再生) のパフォーマンスを測定します。



## <a name="syntax"></a>構文

```
winsat mfmedia <parameters>
```

### <a name="parameters"></a>パラメーター

|パラメーター|説明|
|----------|-----------|
|-入力\<ファイル名>|必須: 再生またはエンコードするビデオクリップを含むファイルを指定します。 このファイルは、メディアファンデーションで表示できる任意の形式にすることができます。|
|-dumpgraph|評価を開始する前に、フィルターグラフを GraphEdit と互換性のあるファイルに保存するように指定します。|
|-ns|フィルターグラフを入力ファイルの通常の再生速度で実行するように指定します。 既定では、フィルターグラフは可能な限り高速に実行され、プレゼンテーション時間は無視されます。|
|-play|デコードモードで評価を実行し、既定の DirectSound デバイスを使用して指定された**入力**ファイルで、指定されたオーディオコンテンツを再生します。 既定では、オーディオ再生は無効になっています。|
|-nopmp|評価中にメディアファンデーション保護されたメディアパイプライン (MFPMP) プロセスを使用しないでください。|
|-pmp|評価中は常に、MFPMP プロセスを使用してください。</br>注: **-pmp**または **-nopmp**が指定されていない場合は、必要な場合にのみ、mfpmp が使用されます。|
|-v|状態と進行状況の情報を含む詳細出力を STDOUT に送信します。 すべてのエラーは、コマンドウィンドウにも書き込まれます。|
|-xml \<ファイル名>|評価の出力を指定した XML ファイルとして保存します。 指定したファイルが存在する場合は上書きされます。|
|-idiskinfo|物理ボリュームと論理ディスクに関する情報を、XML 出力の** \<systemconfig>** セクションの一部として保存します。|
|-iguid|XML 出力ファイルにグローバル一意識別子 (GUID) を作成します。|
|-メモメモのテキスト|XML 出力ファイルの** \<note>** セクションにメモテキストを追加します。|
|-icn|XML 出力ファイルにローカルコンピューター名を含めます。|
|-eef|XML 出力ファイルに追加のシステム情報を列挙します。|

## <a name="examples"></a>例

- C:\windows が Windows フォルダーの場所であるコンピューター上で、メディアファンデーション保護されたメディアパイプライン (MFPMP) を使用せずに、 **winsat の正式**な評価中に使用される入力ファイルで評価を実行する場合は。  
  ```
  winsat mfmedia -input c:\windows\performance\winsat\winsat.wmv -nopmp
  ```

## <a name="remarks"></a>Remarks

-   **Winsat**を使用するには、ローカルの Administrators グループのメンバーシップ、またはそれと同等のメンバーシップが最低限必要です。 コマンドは、管理者特権でのコマンドプロンプトウィンドウから実行する必要があります。
-   管理者特権でのコマンドプロンプトウィンドウを開くには、[**スタート**]、[**アクセサリ**] の順にクリックし、[**コマンドプロンプト**] を右クリックして、[**管理者として実行**] をクリックします。

## <a name="additional-references"></a>その他のリファレンス

