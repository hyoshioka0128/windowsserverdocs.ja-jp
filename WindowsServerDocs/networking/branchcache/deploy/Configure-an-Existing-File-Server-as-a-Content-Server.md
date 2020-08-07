---
title: 既存のファイル サーバーをコンテンツ サーバーとして構成する
description: このトピックは、BranchCache 展開ガイドの Windows Server 2016、ブランチ オフィスに WAN 帯域幅使用量を最適化するために分散され、ホスト型キャッシュ モードで BranchCache を展開する方法を示しますの一部
manager: brianlic
ms.topic: get-started-article
ms.assetid: bdac7d2a-25b4-4f61-bed1-b290700c18f3
ms.author: lizross
author: eross-msft
ms.openlocfilehash: ddb6a9d8ad14146d6f4aca27171649fde3b227eb
ms.sourcegitcommit: dfa48f77b751dbc34409aced628eb2f17c912f08
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/07/2020
ms.locfileid: "87971919"
---
# <a name="configure-an-existing-file-server-as-a-content-server"></a>既存のファイル サーバーをコンテンツ サーバーとして構成する

>適用先:Windows Server (半期チャネル)、Windows Server 2016

次の手順を使用して、Windows Server 2016 を実行しているコンピューターにファイルサービスサーバー役割の**ネットワークファイル用 BranchCache**役割サービスをインストールできます。

> [!IMPORTANT]
> ファイルサービスサーバーの役割がまだインストールされていない場合は、次の手順に従ってください。 「[新しいファイルサーバーをコンテンツサーバーとしてインストールする](../../branchcache/deploy/Install-a-New-File-Server-as-a-Content-Server.md)」を参照してください。

この手順を実行するには、 **Administrators**のメンバーシップ、またはそれと同等のメンバーシップが最低限必要です。

> [!NOTE]
> 管理者は、Windows PowerShell を実行する Windows PowerShell を使用して、この手順を実行するには、Windows PowerShell プロンプトで次のコマンドを入力し、ENTER キーを押します。
>
> `Install-WindowsFeature FS-BranchCache -IncludeManagementTools`
>
> データ重複除去の役割サービスをインストールするには、次のコマンドを入力して、enter キーを押します。
>
> `Install-WindowsFeature FS-Data-Deduplication -IncludeManagementTools`

### <a name="to-install-the-branchcache-for-network-files-role-service"></a>ネットワークファイル用 BranchCache 役割サービスをインストールするには

1.  サーバー マネージャーで、[**管理**] をクリックし、[**役割と機能の追加**] をクリックします。 役割と機能の追加ウィザードが開きます。 **[次へ]** をクリックします。

2.  **[インストールの種類の選択**] で、[**役割ベースまたは機能ベースのインストール**] が選択されていることを確認し、[**次へ**] をクリックします。

3.  **対象サーバーの選択**, 、適切なサーバーが選択されていることを確認し、をクリックして **次**します。

4.  **[サーバーの役割の選択**] の [**役割**] で、**ファイルサービスおよび記憶域サービス**の役割が既にインストールされていることに注意してください。役割名の左側にある矢印をクリックして役割サービスを選択し、[**ファイルサービスおよび ISCSI サービス**] の左側にある矢印をクリックします。

5.  [**ネットワークファイルの BranchCache**] のチェックボックスをオンにします。

    > [!TIP]
    > まだ行っていない場合は、[**データ重複除去**] のチェックボックスもオンにすることをお勧めします。

    **[次へ]** をクリックします。

6.  **機能の選択**, をクリックして **次**します。

7.  [**インストールオプションの確認**] で、選択内容を確認し、[**インストール**] をクリックします。 インストール中に [**インストールの進行状況**] ウィンドウが表示されます。 インストールが完了したら、クリックして **閉じる**します。



