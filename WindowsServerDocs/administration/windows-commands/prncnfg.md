---
title: prncnfg
description: Prncnfg.vbs コマンドのリファレンストピックでは、プリンターに関する構成情報を構成または表示します。
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 38a4e8fa-3122-495b-a125-35b926bc6415
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 07/11/2018
ms.openlocfilehash: b60faaa5537ebdf8860c9b0471cf879677b80f1d
ms.sourcegitcommit: 771db070a3a924c8265944e21bf9bd85350dd93c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/27/2020
ms.locfileid: "85472307"
---
# <a name="prncnfg"></a>prncnfg

> 適用対象: Windows Server (半期チャネル)、Windows Server 2019、Windows Server 2016、Windows Server 2012 R2、Windows Server 2012

プリンターに関する構成情報を表示または構成します。 このコマンドは、ディレクトリにある Visual Basic スクリプトです `%WINdir%\System32\printing_Admin_Scripts\<language>` 。 コマンドプロンプトでこのコマンドを使用するには、「 **cscript** 」に続けて prncnfg.vbs ファイルの完全なパスを入力するか、ディレクトリを適切なフォルダーに変更します。 たとえば、`cscript %WINdir%\System32\printing_Admin_Scripts\en-US\prncnfg` のように指定します。

## <a name="syntax"></a>構文

```
cscript prncnfg {-g | -t | -x | -?} [-S <Servername>] [-P <Printername>] [-z <newprintername>] [-u <Username>] [-w <password>] [-r <portname>] [-l <location>] [-h <sharename>] [-m <comment>] [-f <separatorfilename>] [-y <datatype>] [-st <starttime>] [-ut <untiltime>] [-i <defaultpriority>] [-o <priority>] [<+|->shared] [<+|->direct] [<+|->hidden] [<+|->published] [<+|->rawonly] [<+|->queued] [<+|->enablebidi] [<+|->keepprintedjobs] [<+|->workoffline] [<+|->enabledevq] [<+|->docompletefirst]
```

### <a name="parameters"></a>パラメーター

| パラメーター | 説明 |
|--|--|
| -g | プリンターに関する構成情報を表示します。 |
| -t | プリンターを構成します。 |
| -X | プリンターの名前を変更します。 |
| -S`<Servername>` | 管理するプリンターをホストするリモート コンピューターの名前を指定します。 コンピューターを指定しない場合は、ローカルコンピューターが使用されます。 |
| -P`<Printername>` | 管理するプリンターの名前を指定します。 必須です。 |
| -z`<newprintername>` | 新しいプリンター名を指定します。 必要があります、 **-x** と **-p** パラメーター。 |
| -u `<Username>` -w`<password>` | 管理するプリンターをホストするコンピューターに接続するアクセス許可を持つアカウントを指定します。 ターゲット コンピューターのローカル Administrators グループのすべてのメンバーはこれらのアクセス許可を持っていますが、アクセス許可を他のユーザーに与えることもできます。 アカウントを指定しない場合は、コマンドが機能するように、これらのアクセス許可を持つアカウントでログオンする必要があります。 |
| -r`<portname>` | プリンターが接続されているポートを指定します。 パラレル ポートまたはシリアル ポートの場合は、(LPT1 や COM1 など) のポートの ID を使用します。 TCP/IP ポートである場合は、ポートを追加したときに指定したポート名を使用します。 |
| -l`<location>` | **Copyroom**などのプリンターの場所を指定します。 場所にスペースが含まれている場合は、 **"コピールーム"** などのテキストを引用符で囲みます。|
| -h`<sharename>` | プリンターの共有名を指定します。 |
| -m`<comment>` | プリンターのコメントの文字列を指定します。 |
| -f`<separatorfilename>` | 区切りページに表示されるテキストを含むファイルを指定します。 |
| -y`<datatype>` | プリンターが受け入れることができるデータ型を指定します。 |
| -st`<starttime>` | 可用性に制限は、プリンターを構成します。 プリンターが使用可能な時刻を指定します。 利用できない場合、プリンターにドキュメントを送信する場合、ドキュメントの保持 (スプール)、プリンターが使用可能になるまでです。 時刻は、24 時間制を指定する必要があります。 たとえば、午後 11時 00分を指定する次のように入力します。 **2300**します。 |
| -ut`<endtime>` | 可用性に制限は、プリンターを構成します。 プリンターが存在しない時刻を指定します。 利用できない場合、プリンターにドキュメントを送信する場合、ドキュメントの保持 (スプール)、プリンターが使用可能になるまでです。 時刻は、24 時間制を指定する必要があります。 たとえば、午後 11時 00分を指定する次のように入力します。 **2300**します。 |
| -o`<priority>` | スプーラが印刷キューに印刷ジョブをルーティングに使用する優先順位を指定します。 優先順位の高い印刷キューでは、優先度の低い任意のキューの前に、すべてのジョブを受信します。 |
| -i`<defaultpriority>` | 各印刷ジョブに割り当てられている既定の優先順位を指定します。 |
| `{+|-}`共用 | ネットワークでこのプリンターを共有するかどうかを指定します。 |
| `{+|-}`接続 | ドキュメントをスプールせず、プリンターに直接送信する必要があるかどうかを指定します。 |
| `{+|-}`投稿 | このプリンタを active directory に発行するかどうかを指定します。 プリンタを公開する場合は、他のユーザーが場所や (印刷とホチキス止めの色) などの機能に基づいて検索できます。 |
| `{+|-}`hidden | 予約済みの関数です。 |
| `{+|-}`rawonly | 生データの印刷ジョブのみをこのキューにスプールできるかどうかを指定します。 |
| `{+|-}`} キューに登録済み | プリンターを開始してから、ドキュメントの最後のページがスプールされた印刷ことを指定します。 印刷中のプログラムは、ドキュメントの印刷が完了するまでは使用できません。 ただし、このパラメーターを使用すると、ドキュメント全体を確実にプリンターに送信します。 |
| `{+|-}`keepprintedjobs | スプーラが印刷後ドキュメントを保持するかどうかを指定します。 このオプションを有効にすると、プリンターに印刷中のプログラムからの代わりに、印刷キューからドキュメントを再送信するユーザーができます。 |
| `{+|-}`オフライン作業 | ユーザーが、コンピューターがネットワークに接続されていない場合は、印刷キューに印刷ジョブを送信することができるかどうかを指定します。 |
| `{+|-}`enabledevq | プリンターのセットアップに一致しない印刷ジョブ (PostScript 以外のプリンターにスプールされた PostScript ファイルなど) を、印刷ではなくキューに保持するかどうかを指定します。 |
| `{+|-}`docompletefirst | スプーラがスプールを完了していない、優先順位の高い印刷ジョブを送信する前にスプールを完了した優先度の低い印刷ジョブを送信する必要があるかどうかを指定します。 このオプションが有効になっているドキュメントがスプールに完了しない場合は、スプーラーは複数の小さなする前に大きなドキュメントを送信します。 ジョブの優先順位がプリンターの効率を最大化したい場合は、このオプションを有効にする必要があります。 このオプションが無効になっている場合、スプーラ常に優先順位の高いジョブに対応するキュー最初送信します。 |
| `{+|-}`enablebidi | プリンターがスプーラーにステータス情報を送信するかどうかを指定します。 |
| /? | コマンド プロンプトにヘルプを表示します。 |

### <a name="examples"></a>例

*Hrserver*という名前のリモートコンピューターでホストされている印刷キューを使用して、 *colorprinter_2*という名前のプリンターの構成情報を表示するには、次のように入力します。

```
cscript prncnfg -g -S HRServer -P colorprinter_2
```

*Colorprinter_2*という名前のプリンターを構成して、 *hrserver*という名前のリモートコンピューターのスプーラが印刷後に印刷ジョブを保持するようにするには、次のように入力します。

```
cscript prncnfg -t -S HRServer -P colorprinter_2 +keepprintedjobs
```

*Hrserver*という名前のリモートコンピューター上のプリンターの名前を*colorprinter_2*から*colorprinter 3*に変更するには、次のように入力します。

```
cscript prncnfg -x -S HRServer -P colorprinter_2 -z "colorprinter 3"
```

## <a name="additional-references"></a>その他のリファレンス

- [コマンド ライン構文の記号](command-line-syntax-key.md)

- [印刷コマンドのリファレンス](print-command-reference.md)
