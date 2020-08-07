---
title: WSUS とカタログ サイト
description: Windows Server Update Service (WSUS) のトピック-Microsoft Update カタログサイトにアクセスして WSUS に修正プログラムをインポートする方法
ms.topic: article
ms.assetid: f19a8659-5a96-4fdd-a052-29e4547fe51a
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 25a9852935c47e0c005d78ae7ea24d14c7c1a546
ms.sourcegitcommit: 53d526bfeddb89d28af44210a23ba417f6ce0ecf
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/06/2020
ms.locfileid: "87896786"
---
# <a name="wsus-and-the-catalog-site"></a>WSUS とカタログ サイト

>適用先:Windows Server (半期チャネル)、Windows Server 2016、Windows Server 2012 R2、Windows Server 2012

カタログサイトは、修正プログラムおよびハードウェアドライバーをインポートできる Microsoft の場所です。

## <a name="the-microsoft-update-catalog-site"></a>Microsoft Update カタログサイト
WSUS に修正プログラムをインポートするには、WSUS コンピューターから Microsoft Update カタログサイトにアクセスする必要があります。 Wsus 管理コンソールがインストールされているコンピューターは、WSUS サーバーであるかどうかにかかわらず、カタログサイトから修正プログラムをインポートするために使用できます。 修正プログラムをインポートするには、コンピューターに管理者としてログオンする必要があります。

#### <a name="to-access-the-microsoft-update-catalog-site"></a>Microsoft Update カタログサイトにアクセスするには

1.  WSUS 管理コンソールで、最上位のサーバーノードまたは**更新プログラム**を選択し、[**操作**] ウィンドウで [**更新プログラムのインポート**] をクリックします。 Microsoft Update カタログ Web サイトでブラウザーウィンドウが開きます。

2.  このサイトで更新プログラムにアクセスするには、Microsoft Update Catalog activeX コントロールをインストールする必要があります。

3.  このサイトで Windows 修正プログラムおよびハードウェアドライバーを参照することができます。 必要なものが見つかったら、バスケットに追加します。

4.  参照が終了したら、バスケットに移動し、[インポート] をクリックして更新プログラムをインポートします。 更新プログラムをインポートせずにダウンロードするには、[ **Windows Server Update Services に直接インポート**する] チェックボックスをオフにします。

Microsoft Update カタログサイトからインポートされた承認済みの更新プログラムは、次回 WSUS サーバーが同期したときにダウンロードされます。 これらのファイルは、Microsoft Update カタログサイトからインポートするときにはダウンロードされません。

更新プログラムが WSUS と互換性のある形式でインポートされていることを確認するには、WSUS コンソールで Microsoft Update カタログサイトにアクセスする必要があることに注意してください。 Microsoft Update カタログ web サイトに手動でアクセスした場合、ダウンロードした更新プログラムは WSUS サーバーにインポートされず、個別の * としてダウンロードされます。MSU ファイル。 現在、WSUS には、でファイルをインポートするためのメカニズムがサポートされていません \* 。MSU 形式。

サーバークリーンアップウィザードを実行すると、承認されていない、または拒否済みとして設定された Microsoft Update カタログからインポートされた更新プログラムは、WSUS サーバーから削除される場合があります。 削除されている場合は、Microsoft Update カタログから再インポートできます。

> [!NOTE]
> WSUS サーバークリーンアップウィザードを実行して、[承認されていない] または [拒否済み] として設定されている Microsoft Update カタログからインポートされた更新プログラムを削除することができます。 Microsoft Update カタログを使用して、WSUS システムから以前に削除された更新プログラムを再インポートすることができます。

## <a name="restricting-access-to-hotfixes"></a>修正プログラムへのアクセスの制限
WSUS 管理者は、Microsoft Update カタログサイトからダウンロードした修正プログラムへのアクセスを制限することを検討できます。 この制限を行うには、次の手順に従います。

#### <a name="to-restrict-access-to-hotfixes"></a>修正プログラムへのアクセスを制限するには

1.  IIS コンテンツ vroot で Windows 認証を有効にします。

    -   IIS マネージャーを起動します。

    -   WSUS 管理 web サイトの下にあるコンテンツノードに移動します。

    -   コンテンツの**ホーム**ウィンドウで、[Authentication] \ (**認証**\) オプションをダブルクリックします。

    -   [**匿名認証**] を選択し、右側の [**操作**] ウィンドウで [**無効化**] をクリックします。

    -   [ **Windows 認証**] を選択し、右側の [**操作**] ウィンドウで [**有効にする**] をクリックします。

2.  修正プログラムが必要なコンピューターの WSUS ターゲットグループを作成し、グループに追加します。 コンピューターとグループの詳細については、このガイドの「 [Wsus クライアントコンピューターと wsus コンピューターグループの管理](managing-wsus-client-computers-and-wsus-computer-groups.md)」および「3.3 セクション」を参照してください[。](../deploy/2-configure-wsus.md#23-configure-wsus-computer-groups)「Wsus 展開ガイド」の「手順 3: wsus を構成する」の wsus コンピューターグループを構成します。

3.  修正プログラムのファイルをダウンロードします。

4.  これらのファイルのアクセス許可を設定して、これらのコンピューターのコンピューターアカウントのみが読み取り可能になるようにします。 また、Network Service アカウントにファイルへのフルアクセスを許可する必要があります。

5.  手順2で作成した WSUS ターゲットグループの修正プログラムを承認します。

## <a name="importing-updates-in-different-languages"></a>異なる言語での更新プログラムのインポート
Microsoft Update カタログ Web サイトには、複数の言語をサポートする更新プログラムが含まれています。 WSUS サーバーでサポートされている言語と、これらの更新プログラムでサポートされている言語を一致させることが非常に**重要**です。 WSUS サーバーが更新プログラムに含まれるすべての言語をサポートしていない場合、更新プログラムはクライアントコンピューターに展開されません。 同様に、複数の言語をサポートする更新プログラムが WSUS サーバーにダウンロードされていても、まだクライアントコンピューターに展開されていない場合に、管理者がその更新プログラムに含まれている言語のいずれかを選択解除すると、更新プログラムはクライアントに展開されません。
