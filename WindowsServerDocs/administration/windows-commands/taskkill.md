---
title: taskkill
description: 'Windows コマンドに関するトピック * * * *- '
ms.custom: na
ms.prod: windows-server
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 2b71e792-08b6-46d4-95a5-cb6336a79524
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 21aec17c649960daffd1aeba80d4448bb9d0ecf7
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/27/2019
ms.locfileid: "71383663"
---
# <a name="taskkill"></a>taskkill

>適用先:Windows Server (半期チャネル)、Windows Server 2016、Windows Server 2012 R2、Windows Server 2012

1 つまたは複数のタスクまたはプロセスを終了します。 プロセス ID またはイメージ名を使用してプロセスを終了できます。 **taskkill**は、 **kill**ツールを置き換えます。
このコマンドを使用する方法の例については、[例](#examples)を参照してください。

## <a name="syntax"></a>構文

```
taskkill [/s <computer> [/u [<Domain>\]<UserName> [/p [<Password>]]]] {[/fi <Filter>] [...] [/pid <ProcessID> | /im <ImageName>]} [/f] [/t]
```

## <a name="parameters"></a>パラメーター

|         パラメーター         |                                                                                                                                        説明                                                                                                                                        |
|---------------------------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
|      /s \<コンピューター >       |                                                                                    名前またはリモート コンピューターの IP アドレスを指定します (円記号を使用しない)。 既定はローカル コンピュータです。                                                                                     |
| /u \<ドメイン >\\ユーザー名>\< | 指定されているユーザーのアカウント権限でコマンドを実行して *UserName* または *ドメイン*\\*ユーザー名*します。 **/u** 場合にのみ指定できる **/s** を指定します。 既定では、コマンドを発行しているコンピューターに現在ログオンしているユーザーのアクセス許可です。 |
|      /p \<パスワード >       |                                                                                                   指定されているユーザー アカウントのパスワードを指定します、 **/u** パラメーター。                                                                                                   |
|       /fi \<フィルター >       |          タスクのセットを選択するフィルターを適用します。 複数のフィルターを使用することも、ワイルドカード文字 ( **\\** \*) を使用してすべてのタスクまたはイメージ名を指定することもできます。 次を参照してください [有効なフィルター名のテーブル](#filter-names-operators-and-values), 、演算子、および値。           |
|     /pid \<ProcessID >     |                                                                                                                 終了するプロセスのプロセス ID を指定します。                                                                                                                 |
|     /im \<ImageName >      |                                                                                終了するプロセスのイメージの名前を指定します。 すべてのイメージ名を **\\** 指定するには、ワイルドカード文字 (\*) を使用します。                                                                                |
|            /f             |                                                                    プロセスが強制的に終了することを指定します。 リモート プロセスでこのパラメーターは無視されます。すべてのリモート プロセスが強制的に終了します。                                                                     |
|            /t             |                                                                                                          指定されたプロセスおよびそれによって開始されたすべての子プロセスを終了します。                                                                                                          |

#### <a name="filter-names-operators-and-values"></a>フィルター名、演算子、および値

| フィルター名 |    有効な演算子     |                                                                有効な値                                                                |
|-------------|------------------------|----------------------------------------------------------------------------------------------------------------------------------------------|
|   STATUS    |         eq、ne         |                                                 実行する (&) #124 文字です。稼働中と #124; できません。不明な                                                 |
|  IMAGENAME  |         eq、ne         |                                                                  イメージの名前                                                                  |
|     PID     | eq、ne、gt、lt、ge、le |                                                                  PID 値                                                                   |
|   SESSION   | eq、ne、gt、lt、ge、le |                                                                セッション番号                                                                |
|   CpuTime   | eq、ne、gt、lt、ge、le | CPU 時間の形式で <em>HH</em> **:** <em>MM</em> **:** <em>SS</em>, ここで、 *MM* と *SS* 0 ~ 59 の間、および *HH* 符号なしのいずれかの数は、 |
|  MEMUSAGE   | eq、ne、gt、lt、ge、le |                                                              メモリの使用量 (KB 単位)                                                              |
|  USERNAME   |         eq、ne         |                                               任意の有効なユーザー名 (*ユーザー* または *ドメイン*\\*ユーザー*)                                               |
|  サービス   |         eq、ne         |                                                                 [サービス名]                                                                 |
| WINDOWTITLE |         eq、ne         |                                                                 ウィンドウのタイトル                                                                 |
|   モジュール   |         eq、ne         |                                                                   DLL 名                                                                   |

## <a name="remarks"></a>コメント
* リモート システムが指定されているときに、WINDOWTITLE と状態のフィルターはサポートされていません。
* ワイルドカード文字 ( **\\** ) は、フィルターが適用されている場合にのみ<em>、* */im</em>オプションに受け入れられ*ます。
* リモート プロセスの終了は常に実行が強制的に、かどうかに関係なく、 **/f** オプションを指定します。
* ホスト名フィルターにコンピューター名を指定すると、シャットダウンが発生し、すべてのプロセスが停止します。
* 使用する **tasklist** プロセスを終了するプロセス ID (PID) を確認します。

## <a name="examples"></a>使用例

プロセス Id が 1230 とプロセスを終了するには、1241、および 1253 に入力します。

```
taskkill /pid 1230 /pid 1241 /pid 1253
```

強制的にプロセスを終了するには、"Notepad.exe"システムが起動した場合、次のように入力します。

```
taskkill /f /fi "USERNAME eq NT AUTHORITY\SYSTEM" /im notepad.exe
```

Hiropln、ユーザー アカウントの資格情報を使用しているときに、イメージ名で始まる「メモ」には、"Srvmain"のリモート コンピューター上のすべてのプロセスを終了するには、次のように入力します。

```
taskkill /s srvmain /u maindom\hiropln /p p@ssW23 /fi "IMAGENAME eq note*" /im *
```

プロセス ID 2134 とすべての子プロセスを終了するのには、開始されると、これには、管理者アカウントでこれらのプロセスが開始された場合にのみを入力したを処理します。

```
taskkill /pid 2134 /t /fi "username eq administrator"
```

そのイメージの名前に関係なく、1000 以上のプロセス ID を持つすべてのプロセスを終了して次のように入力します。

```
taskkill /f /fi "PID ge 1000" /im *
```

#### <a name="additional-references"></a>その他の参照情報
[コマンド ライン構文の記号](command-line-syntax-key.md)
