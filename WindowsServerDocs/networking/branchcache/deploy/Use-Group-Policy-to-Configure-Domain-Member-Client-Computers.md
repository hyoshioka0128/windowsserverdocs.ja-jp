---
title: グループ ポリシーを使用して、ドメイン メンバー クライアント コンピューターを構成するには
description: このトピックは、BranchCache 展開ガイドの Windows Server 2016、ブランチ オフィスに WAN 帯域幅使用量を最適化するために分散され、ホスト型キャッシュ モードで BranchCache を展開する方法を示しますの一部
manager: dougkim
ms.prod: windows-server-threshold
ms.technology: networking-bc
ms.topic: get-started-article
ms.assetid: 911c1538-f79d-42e9-ba38-f4618f87b008
ms.author: pashort
author: shortpatti
ms.date: 06/02/2018
ms.openlocfilehash: 8e82d3e0ee7a84fbd6e2916d0f22472a8c117688
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/17/2019
ms.locfileid: "59855083"
---
# <a name="use-group-policy-to-configure-domain-member-client-computers"></a>グループ ポリシーを使用して、ドメイン メンバー クライアント コンピューターを構成するには

>適用対象:Windows Server 2016 の Windows Server (半期チャネル)

このセクションで、組織内のすべてのコンピューターのグループ ポリシー オブジェクトを作成、分散キャッシュ モードでドメイン メンバー クライアント コンピューターを構成またはキャッシュ モードでは、ホストされているして BranchCache を許可するセキュリティが強化された Windows ファイアウォールを構成します。トラフィック。  
  
このセクションでは、次の手順を説明します。  
  
1.  [グループ ポリシー オブジェクトを作成および BranchCache のモードを構成するには](#bkmk_gp)  
  
2.  [高度なセキュリティの受信トラフィックのルールで Windows ファイアウォールを構成するには](#bkmk_inbound)  
  
3.  [高度なのセキュリティ送信トラフィックのルールで Windows ファイアウォールを構成するには](#bkmk_outbound)  
  
> [!TIP]  
> 次の手順で、既定のドメイン ポリシーでグループ ポリシー オブジェクトの作成が指示された場合、組織単位 (OU) または展開に適切であるその他のコンテナーでオブジェクトを作成できます。  
  
メンバーである必要があります **Domain Admins**, 、またはこれらの手順に相当します。  
  
## <a name="bkmk_gp"></a>グループ ポリシー オブジェクトを作成および BranchCache のモードを構成するには  
  
1.  なる Active Directory ドメイン サービスのサーバーの役割がインストールされている、サーバー マネージャーで、コンピューターで **ツール**, 、 をクリックし、 **Group Policy Management**します。 グループ ポリシー管理コンソールが開きます。  
  
2.  グループ ポリシー管理コンソールでは、次のパスを展開します。**フォレスト:** *example.com*、**ドメイン**、 *example.com*、**グループ ポリシー オブジェクト**ここで、 *example.com*を構成する BranchCache クライアント コンピューターのアカウントが配置されているドメインの名前を指定します。  
  
3.  右クリック **グループ ポリシー オブジェクト**, 、クリックして **新規**します。 **新しい GPO**  ダイアログ ボックスが表示されます。 **名**, 、名前の新しいグループ ポリシー オブジェクト (GPO) を入力します。 たとえば、BranchCache クライアント コンピューター オブジェクトの名前を付ける場合は、「 **BranchCache クライアント コンピューター**します。 **[OK]** をクリックします。  
  
4.  グループ ポリシー管理コンソールで **グループ ポリシー オブジェクト** が選択されているし、詳細ウィンドウで、作成した GPO を右クリックします。 たとえば、GPO BranchCache クライアント コンピューターの名前を付けた場合を右クリックして **BranchCache クライアント コンピューター**します。 **[編集]** をクリックします。 グループ ポリシー管理エディター コンソールを開きます。  
  
5.  グループ ポリシー管理エディター コンソールでは、次のパスを展開します。**コンピューターの構成**、**ポリシー**、**管理用テンプレート。ポリシー定義 (ADMX ファイル) は、ローカル コンピューターから取得した**、**ネットワーク**、 **BranchCache**します。  
  
6.  をクリックして **BranchCache**, 、詳細ウィンドウをダブルクリック **BranchCache を有効にする**です。 ポリシーの設定 ダイアログ ボックスが開きます。  
  
7.  **BranchCache を有効にする** ダイアログ ボックスで、をクリックして **有効**, 、 をクリックし、 **ok**します。  
  
8.  詳細ウィンドウでの BranchCache 分散キャッシュ モードを有効にするにはダブルクリック **設定の BranchCache 分散キャッシュ モード**します。 ポリシーの設定 ダイアログ ボックスが開きます。  
  
9. **BranchCache の分散キャッシュの設定モード** ダイアログ ボックスで、をクリックして **有効**, 、 をクリックし、 **ok**します。  
  
10. ホスト型キャッシュ モードで BranchCache を展開して、展開した場所にそれらのオフィス内のキャッシュ サーバーがホストされている 1 つまたは複数のブランチ オフィスがある場合、ダブルクリック **を有効にする自動ホストされるキャッシュの検出サービス接続ポイントによる**します。 ポリシーの設定 ダイアログ ボックスが開きます。  
  
11. **を有効にする自動ホストされるキャッシュの検出サービス接続ポイントによる** ダイアログ ボックスで、をクリックして **有効**, 、 をクリックし、 **ok**します。  
  
    > [!NOTE]  
    > 有効にすると両方、 **設定の BranchCache 分散キャッシュ モード** と **を有効にする自動ホストされるキャッシュの検出サービス接続ポイントによる** ポリシー設定では、クライアント コンピューターで動作 BranchCache 分散キャッシュ モード ホスト型キャッシュ モードで動作するこの時点で、ブランチ オフィスでホスト型キャッシュ サーバーを検索する場合を除き、します。  
  
12. 以下の手順を使用すると、グループ ポリシーを使用してクライアント コンピューターでファイアウォールの設定を構成できます。  
  
## <a name="bkmk_inbound"></a>高度なセキュリティの受信トラフィックのルールで Windows ファイアウォールを構成するには  
  
1.  グループ ポリシー管理コンソールでは、次のパスを展開します。**フォレスト:** *example.com*、**ドメイン**、 *example.com*、**グループ ポリシー オブジェクト**ここで、 *example.com*を構成する BranchCache クライアント コンピューターのアカウントが配置されているドメインの名前を指定します。  
  
2.  グループ ポリシー管理コンソールで **グループ ポリシー オブジェクト** が選択されているし、詳細ウィンドウで、BranchCache クライアント コンピューターを以前に作成した GPO を右クリックします。 たとえば、GPO BranchCache クライアント コンピューターの名前を付けた場合を右クリックして **BranchCache クライアント コンピューター**します。 **[編集]** をクリックします。 グループ ポリシー管理エディター コンソールを開きます。  
  
3.  グループ ポリシー管理エディター コンソールでは、次のパスを展開します。**コンピューターの構成**、**ポリシー**、 **Windows 設定**、**セキュリティ設定**、 **セキュリティが強化されたWindowsファイアウォール**、 **LDAP のセキュリティが強化された Windows ファイアウォール**、**受信規則**します。  
  
4.  右クリック**受信の規則**、 をクリックし、**新しいルール**します。 新しい受信の規則ウィザードが開きます。  
  
5.  **規則の種類**, 、 をクリックして **定義済み**, 、選択肢の一覧を展開し、クリックして **BranchCache - コンテンツの取得 (HTTP を使用して)** します。 **[次へ]** をクリックします。  
  
6.  **事前定義された規則**, をクリックして **次**します。  
  
7.  **アクション**, 、いることを確認 **接続を許可する** クリックして選択すると、 **完了**します。  
  
    > [!IMPORTANT]  
    > 選択する必要があります **接続を許可する** BranchCache クライアントがこのポートでトラフィックを受信できるようにするためです。  
  
8.  Ws-discovery ファイアウォールの例外を作成するには、もう一度右クリック **受信の規則**, 、クリックして **新しいルール**します。 新しい受信の規則ウィザードが開きます。  
  
9. **規則の種類**, をクリックして **定義済み**, 、選択肢の一覧を展開し、クリックして **BranchCache - ピア検出 (を使用して WSD)** します。 **[次へ]** をクリックします。  
  
10. **事前定義された規則**, をクリックして **次**します。  
  
11. **アクション**, 、いることを確認 **接続を許可する** クリックして選択すると、 **完了**します。  
  
    > [!IMPORTANT]  
    > 選択する必要があります **接続を許可する** BranchCache クライアントがこのポートでトラフィックを受信できるようにするためです。  
  
## <a name="bkmk_outbound"></a>高度なのセキュリティ送信トラフィックのルールで Windows ファイアウォールを構成するには  
  
1.  グループ ポリシー管理エディター コンソールで、右クリック **送信の規則**, 、クリックして **新しいルール**します。 新しい送信規則ウィザードが開きます。  
  
2.  **規則の種類**, 、 をクリックして **定義済み**, 、選択肢の一覧を展開し、クリックして **BranchCache - コンテンツの取得 (HTTP を使用して)** します。 **[次へ]** をクリックします。  
  
3.  **事前定義された規則**, をクリックして **次**します。  
  
4.  **アクション**, 、いることを確認 **接続を許可する** クリックして選択すると、 **完了**します。  
  
    > [!IMPORTANT]  
    > 選択する必要があります **接続を許可する** BranchCache クライアントがこのポートでトラフィックを送信できるようにするためです。  
  
5.  Ws-discovery ファイアウォールの例外を作成するには、もう一度右クリック **送信の規則**, 、クリックして **新しいルール**します。 新しい送信規則ウィザードが開きます。  
  
6.  **規則の種類**, をクリックして **定義済み**, 、選択肢の一覧を展開し、クリックして **BranchCache - ピア検出 (を使用して WSD)** します。 **[次へ]** をクリックします。  
  
7.  **事前定義された規則**, をクリックして **次**します。  
  
8.  **アクション**, 、いることを確認 **接続を許可する** クリックして選択すると、 **完了**します。  
  
    > [!IMPORTANT]  
    > 選択する必要があります **接続を許可する** BranchCache クライアントがこのポートでトラフィックを送信できるようにするためです。  
  


