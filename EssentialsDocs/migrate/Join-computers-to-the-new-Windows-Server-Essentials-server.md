---
title: 新しい Windows Server Essentials server1 にコンピューターを参加させる
description: Windows Server Essentials の使用方法について説明します。
ms.date: 10/03/2016
ms.topic: article
ms.assetid: cdfa9504-9881-4265-b308-c7ee8721bfaa
author: nnamuhcs
ms.author: coreyp
manager: dongill
ms.openlocfilehash: cbc2276eb3c627ebb94469e0acef2b57d086b5e7
ms.sourcegitcommit: d99bc78524f1ca287b3e8fc06dba3c915a6e7a24
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/27/2020
ms.locfileid: "87180748"
---
# <a name="join-computers-to-the-new-windows-server-essentials-server1"></a>新しい Windows Server Essentials server1 にコンピューターを参加させる

>適用対象: windows Server 2016 Essentials、Windows Server 2012 R2 Essentials、Windows Server 2012 Essentials

##  <a name="BKMK_JoinComputers"></a>
 移行プロセスの次の手順では、クライアントコンピューターを新しい Windows Server Essentials ネットワークに参加させ、グループポリシーの設定を更新します。

> [!NOTE]
>  クライアント コンピューターが移行元サーバーに既に参加している場合、コンピューターを移行先サーバーに接続する前に、クライアント コンピューターでコネクタ ソフトウェアをアンインストールする必要があります。

 クライアント コンピューターをサーバーに接続するプロセスは、コンピューターがドメインに参加しているかどうかにかかわらず同じです。

- **http://**<em>移行先サーバー名</em>**/connect** を参照し、新しいコンピューターの場合と同じように Windows Server コネクタ ソフトウェアをインストールします。

> [!NOTE]
>  Windows Server コネクタ ソフトウェアは、Windows XP または Windows Vista を実行しているコンピューターはサポートしていません。 既にドメインに参加している Windows XP または Windows Vista を実行しているコンピューターがある場合は、この手順を省略できます。

### <a name="ensure-that-group-policy-has-updated"></a>グループ ポリシーが更新されたことを確認する

> [!NOTE]
>  これはオプションの手順であり、移行元サーバーがフォルダー リダイレクトなどのカスタム グループ ポリシーの設定で構成されていた場合にのみ必要です。

 移行元サーバーと移行先サーバーがまだオンラインの間に、グループ ポリシーの設定が移行先サーバーからクライアント コンピューターにレプリケートされたことを確認する必要があります。 各クライアント コンピューターで次の手順を実行します。

1.  コマンド プロンプト ウィンドウを開きます。

2.  コマンド プロンプトで「**GPRESULT /R**」と入力し、Enter キーを押します。

3.  によって適用されたグループポリシーセクションの結果出力を確認し、宛先サーバーが一覧表示されていることを確認します (例: **Destinationsrv. Domain. local**)。 次に例を示します。

    ```
    USER SETTINGS
    --------------
        CN=User,OU=Users,DC=DOMAIN,DC=Local
        Last time Group Policy was applied: 1/24/2011 at 1:26:27 PM
        Group Policy was applied from:      DestinationSrv.Domain.local
        Group Policy slow link threshold:   500 kbps
        Domain Name:                        Domain
        Domain Type:                        Windows 2011

    ```

4.  移行先サーバーが一覧に表示されない場合、コマンド プロンプトで「**gpupdate /force**」と入力して Enter キーを押し、グループ ポリシーの設定を更新します。 その後、前の手順を再度実行します。

5.  移行先サーバーがまだ表示されない場合は、グループ ポリシーの設定またはこの特定のクライアント コンピューターへのポリシーの適用にエラーがある可能性があります。 移行先サーバーが表示されない場合は、次の手順を実行してください。

    1.  [**スタート**] ボタンをクリックし、[**ファイル名を指定して実行**] をクリックし、「**rsop.msc**」 (ポリシーの結果セット) と入力して、Enter キーを押します。

    2.  ノードが表示されるまで、X 印の付いたツリーを展開します。

    3.  ノードを右クリックし、[**エラーの表示**] をクリックして、一覧のコンピューターでグループ ポリシーの設定が失敗する理由についての情報を確認します。
