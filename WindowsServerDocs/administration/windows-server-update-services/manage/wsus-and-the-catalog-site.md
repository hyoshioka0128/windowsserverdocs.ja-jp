---
title: WSUS とカタログ サイト
description: Windows Server Update Service (WSUS) のトピックでは、Microsoft Update カタログのサイトにアクセスして、修正プログラムを WSUS にインポートする方法
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: manage-wsus
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: f19a8659-5a96-4fdd-a052-29e4547fe51a
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 298df36b856cba97ec19126f77456785e5eb6f50
ms.sourcegitcommit: 6ef4986391607bb28593852d06cc6645e548a4b3
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/07/2019
ms.locfileid: "66810929"
---
# <a name="wsus-and-the-catalog-site"></a>WSUS とカタログ サイト

>適用先:Windows Server (半期チャネル)、Windows Server 2016、Windows Server 2012 R2、Windows Server 2012

カタログのサイトでは、修正プログラムとハードウェアのドライバーのインポート元の Microsoft 場所です。

## <a name="the-microsoft-update-catalog-site"></a>Microsoft Update カタログ サイト
、修正プログラムを WSUS にインポートするには WSUS コンピューターから、Microsoft Update カタログ サイトにアクセスする必要があります。 カタログのサイトからの修正プログラムをインポートするのには、WSUS サーバーであるかどうかに WSUS 管理コンソールがインストールされているどのコンピューターを使用できます。 修正プログラムをインポートするには、コンピューターに管理者としてログオンする必要があります。

#### <a name="to-access-the-microsoft-update-catalog-site"></a>Microsoft Update カタログのサイトにアクセスするには

1.  WSUS 管理コンソールで、上位のサーバー ノードを選択します。 または**更新**、し、**アクション**ペイン をクリックします**更新プログラムをインポート**。 Microsoft Update カタログの Web サイト、ブラウザー ウィンドウが開きます。

2.  このサイトで更新するには、Microsoft Update カタログ activeX コントロールをインストールする必要があります。

3.  Windows 修正プログラムとハードウェアのドライバーのこのサイトを参照することができます。 必要なものが見つかったら、カートに追加します。

4.  参照が完了したら、バスケットに移動し、インポートをインポート、更新プログラムをクリックします。 インポートしなくても、更新プログラムをダウンロードするには、オフ、 **Windows Server Update Services に直接インポート**チェック ボックスをオンします。

Microsoft Update カタログのサイトからインポートされた承認済み更新プログラムは、次回 WSUS サーバーが同期にダウンロードされます。 Microsoft Update カタログ サイトからのインポート時にダウンロードされません。

アクセスを確認する必要があります、Microsoft Update カタログ サイトも、更新プログラムが WSUS と互換性のある形式でインポートされたことを確認する WSUS コンソール。 Microsoft Update カタログ web サイトを手動でアクセスすると、更新プログラムをダウンロードすることがあれば、WSUS サーバーにインポートされていないが代わりに、個人としてダウンロードは * です。MSU ファイル。 WSUS が内のファイルをインポートするためのサポートされているメカニズムを現在持っていない、\*します。MSU 形式です。

サーバー クリーンアップ ウィザードを実行する場合は、WSUS サーバーから承認されていない、または拒否済みとして設定されている Microsoft Update カタログからインポートされた更新を削除する可能性があります。 削除される場合が Microsoft Update カタログから再インポートできないことができます。

> [!NOTE]
> 更新プログラム、Microsoft Update カタログからインポートされている WSUS サーバー クリーンアップ ウィザードを実行していない承認または拒否済み のいずれかとして設定されているを削除することができます。 以前、Microsoft Update カタログから WSUS システムから削除された更新プログラムを再度インポートすることができます。

## <a name="restricting-access-to-hotfixes"></a>修正プログラムへのアクセスを制限します。
WSUS 管理者、Microsoft Update カタログ サイトからダウンロードした修正プログラムへのアクセスを制限することを検討します。 次の手順に従って、この制限できるようにします。

#### <a name="to-restrict-access-to-hotfixes"></a>修正プログラムへのアクセスを制限するには

1.  IIS コンテンツの vroot に Windows 認証を有効にします。

    -   IIS マネージャーを起動します。

    -   WSUS 管理 web サイトの下のコンテンツ ノードに移動します。

    -   **コンテンツ ホーム**ウィンドウで、ダブルクリックで、**認証**オプション。

    -   選択**匿名認証** をクリック**を無効にする**で、**アクション**右側のウィンドウ。

    -   選択**Windows 認証** をクリック**を有効にする**で、**アクション**右側のウィンドウ。

2.  修正プログラムは、必要なコンピューターの WSUS ターゲット グループを作成し、グループに追加します。 コンピューターおよびグループの詳細については、次を参照してください。 [WSUS クライアントを管理するコンピューターおよび WSUS コンピューター グループ](managing-wsus-client-computers-and-wsus-computer-groups.md)このガイドでは、とセクション[3.3 です。WSUS コンピューター グループを構成する](../deploy/2-configure-wsus.md#23-configure-wsus-computer-groups)手順 3。WSUS 展開ガイドでは、WSUS を構成します。

3.  修正プログラムのファイルをダウンロードします。

4.  これらのファイルのアクセス許可を設定するは、これらのマシンのマシン アカウントのみが読み取ることができるようにします。 また、ファイルをネットワーク サービス アカウントの完全なアクセスを許可する必要があります。

5.  手順 2 で作成した WSUS の対象グループの修正プログラムを承認します。

## <a name="importing-updates-in-different-languages"></a>さまざまな言語の更新プログラムをインポートします。
Microsoft Update カタログの Web サイトには、複数の言語をサポートする更新プログラムが含まれています。 これは非常に**重要な**これらの更新プログラムでサポートされる言語で、WSUS サーバーでサポートされる言語に一致するようにします。 WSUS サーバーが、更新プログラムに含まれるすべての言語をサポートしていない場合、更新プログラムはクライアント コンピュータに展開されません。 同様に、管理者の選択を解除し、複数の言語をサポートしている更新プログラムが WSUS サーバーにダウンロードされましたが、クライアント コンピューターに展開されていない場合、更新プログラム、言語のいずれかに含まれる、更新プログラムは、クライアントには配置されません。
