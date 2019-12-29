---
title: prncnfg
description: Prncfg コマンドを使用してプリンターを構成する方法について説明します。
ms.custom: na
ms.prod: windows-server
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 38a4e8fa-3122-495b-a125-35b926bc6415
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 07/11/2018
ms.openlocfilehash: 5cbbf82e832c50d168e0bef06b2b7c3022dd90e8
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/27/2019
ms.locfileid: "71372140"
---
# <a name="prncnfg"></a>prncnfg

>適用対象: Windows Server (半期チャネル)、Windows Server 2016、Windows Server 2012 R2、Windows Server 2012

プリンターに関する構成情報を表示または構成します。

## <a name="syntax"></a>構文
```
cscript Prncnfg {-g | -t | -x | -?} [-S <ServerName>] [-P <printerName>] [-z <NewprinterName>] [-u <UserName>] [-w <Password>] [-r <PortName>] [-l <Location>] [-h <Sharename>] [-m <Comment>] [-f <SeparatorFileName>] [-y <Datatype>] [-st <starttime>] [-ut <Untiltime>] [-i <DefaultPriority>] [-o <Priority>] [<+|->shared] [<+|->direct] [<+|->hidden] [<+|->published] [<+|->rawonly] [<+|->queued] [<+|->enablebidi] [<+|->keepprintedjobs] [<+|->workoffline] [<+|->enabledevq] [<+|->docompletefirst]
```

## <a name="parameters"></a>パラメーター
|パラメーター|説明|
|-------|--------|
|-g|プリンターに関する構成情報を表示します。|
|-t|プリンターを構成します。|
|-x|プリンターの名前を変更します。|
|-S \<ServerName\>|管理するプリンターをホストするリモート コンピューターの名前を指定します。 コンピューターを指定しないと、ローカル コンピューターが使用されます。|
|-P \<printerName\>|管理するプリンターの名前を指定します。 必須。|
|-z \<NewprinterName\>|新しいプリンター名を指定します。 必要があります、 **-x** と **-p** パラメーター。|
|-u \<UserName\>-w \<パスワード\>|管理するプリンターをホストするコンピューターに接続するアクセス許可を持つアカウントを指定します。 ターゲット コンピューターのローカル Administrators グループのすべてのメンバーにこれらのアクセス許可があるが、アクセス許可は、他のユーザーに与えることもできます。 アカウントを指定しない場合は、コマンドを実行するこれらのアクセス許可を持つアカウントでログオンする必要があります。|
|-r \<PortName\>|プリンターが接続されているポートを指定します。 パラレル ポートまたはシリアル ポートの場合は、(LPT1 や COM1 など) のポートの ID を使用します。 TCP/IP ポートである場合は、ポートを追加したときに指定したポート名を使用します。|
|-l \<の場所\>|"コピールーム" などのプリンターの場所を指定します。|
|-h \<Sharename\>|プリンターの共有名を指定します。|
|-m \<コメント\>|プリンターのコメントの文字列を指定します。|
|-f \<SeparatorFileName\>|区切りページに表示されるテキストを含むファイルを指定します。|
|-y \<Datatype\>|プリンターが受け入れることができるデータ型を指定します。|
|-st \<starttime\>|可用性に制限は、プリンターを構成します。 プリンターが使用可能な時刻を指定します。 利用できない場合、プリンターにドキュメントを送信する場合、ドキュメントの保持 (スプール)、プリンターが使用可能になるまでです。 時刻は、24 時間制を指定する必要があります。 たとえば、午後 11時 00分を指定する次のように入力します。 **2300**します。|
|-ut \<Endtime\>|可用性に制限は、プリンターを構成します。 プリンターが存在しない時刻を指定します。 利用できない場合、プリンターにドキュメントを送信する場合、ドキュメントの保持 (スプール)、プリンターが使用可能になるまでです。 時刻は、24 時間制を指定する必要があります。 たとえば、午後 11時 00分を指定する次のように入力します。 **2300**します。|
|-o \<優先度\>|スプーラが印刷キューに印刷ジョブをルーティングに使用する優先順位を指定します。 優先順位の高い印刷キューでは、優先度の低い任意のキューの前に、すべてのジョブを受信します。|
|-i \<DefaultPriority\>|各印刷ジョブに割り当てられている既定の優先順位を指定します。|
|{+ & #124;-} 共有|ネットワークでこのプリンターを共有するかどうかを指定します。|
|{+ &#124;-} ダイレクト|ドキュメントをスプールせず、プリンターに直接送信する必要があるかどうかを指定します。|
|{+ &#124;-} 発行|このプリンタを active directory に発行するかどうかを指定します。 プリンタを公開する場合は、他のユーザーが場所や (印刷とホチキス止めの色) などの機能に基づいて検索できます。|
|{+ &#124;-} 非表示|予約済みの関数です。|
|{+ & #124;-} rawonly|生データの印刷ジョブのみをこのキューにスプールできるかどうかを指定します。|
|{+ & #124; -} キューに置かれました。|プリンターを開始してから、ドキュメントの最後のページがスプールされた印刷ことを指定します。 印刷中のプログラムは、ドキュメントの印刷が完了するまでは使用できません。 ただし、このパラメーターを使用すると、ドキュメント全体を確実にプリンターに送信します。|
|{+ &#124; -} keepprintedjobs|スプーラが印刷後ドキュメントを保持するかどうかを指定します。 このオプションを有効にすると、プリンターに印刷中のプログラムからの代わりに、印刷キューからドキュメントを再送信するユーザーができます。|
|{+ & #124; -} workoffline|ユーザーが、コンピューターがネットワークに接続されていない場合は、印刷キューに印刷ジョブを送信することができるかどうかを指定します。|
|{+ &#124; -} enabledevq|(たとえば、PostScript ファイルが非 PostScript プリンターにスプールされ)、プリンターの設定と一致しない印刷ジョブをキューで保持するようにするかどうかを示す印刷されているのではなく。|
|{+ & #124; -} docompletefirst|スプーラがスプールを完了していない、優先順位の高い印刷ジョブを送信する前にスプールを完了した優先度の低い印刷ジョブを送信する必要があるかどうかを指定します。 このオプションが有効になっているドキュメントがスプールに完了しない場合は、スプーラーは複数の小さなする前に大きなドキュメントを送信します。 ジョブの優先順位がプリンターの効率を最大化したい場合は、このオプションを有効にする必要があります。 このオプションが無効になっている場合、スプーラ常に優先順位の高いジョブに対応するキュー最初送信します。|
|{+ & #124; -} enablebidi|プリンターがスプーラーにステータス情報を送信するかどうかを指定します。|
|/?|コマンド プロンプトにヘルプを表示します。|

## <a name="remarks"></a>注釈
-   **Prncnfg.vbs**コマンドは、%windir%\system32\ printing_Admin_Scripts\\<language> ディレクトリにある Visual Basic スクリプトです。 このコマンドを使用するには、コマンドプロンプトで「 **cscript** 」と入力し、prncnfg.vbs ファイルへの完全なパスを入力するか、ディレクトリを適切なフォルダーに変更します。 次に、例を示します。
    ```
    cscript %WINdir%\System32\printing_Admin_Scripts\en-US\prncnfg
    ```
-   入力した情報にスペースが含まれている場合は、テキストを引用符で囲みます (`"computer Name"`など)。

## <a name="BKMK_examples"></a>例
HRServer という名前のリモートコンピューターでホストされている印刷キューを使用して、colorprinter_2 という名前のプリンターの構成情報を表示するには、次のように入力します。
```
cscript prncnfg -g -S HRServer -P colorprinter_2 
```

Colorprinter_2 という名前のプリンターを構成して、HRServer という名前のリモートコンピューターのスプーラが印刷後に印刷ジョブを保持するようにするには、次のように入力します。
```
cscript prncnfg -t -S HRServer -P colorprinter_2 +keepprintedjobs 
```

HRServer という名前のリモートコンピューター上のプリンターの名前を colorprinter_2 から colorprinter 3 に変更するには、次のように入力します。
```
cscript prncnfg -x -S HRServer -P colorprinter_2 -z "colorprinter 3" 
```

#### <a name="additional-references"></a>その他の参照情報
[コマンドライン構文のキー](command-line-syntax-key.md)
[印刷コマンドリファレンス](print-command-reference.md)
