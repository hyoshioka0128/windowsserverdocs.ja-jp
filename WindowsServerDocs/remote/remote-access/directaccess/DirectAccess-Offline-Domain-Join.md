---
title: DirectAccess オフライン ドメイン参加
description: このガイドでは、Windows Server 2016 への DirectAccess のオフライン ドメイン参加を実行する手順について説明します。
manager: brianlic
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: networking-da
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 55528736-6c19-40bd-99e8-5668169ef3c7
ms.author: pashort
author: shortpatti
ms.openlocfilehash: 59b5933a81c7021e58ea14e6ea4c4da374ce35cb
ms.sourcegitcommit: afb0602767de64a76aaf9ce6a60d2f0e78efb78b
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/20/2019
ms.locfileid: "67283657"
---
# <a name="directaccess-offline-domain-join"></a>DirectAccess オフライン ドメイン参加

>適用先:Windows Server 2016 の Windows Server (半期チャネル)

このガイドでは、DirectAccess と、オフライン ドメイン参加を実行する手順について説明します。 オフライン ドメイン参加では、中に物理接続または VPN 接続なしのドメインに参加するコンピューターが構成されています。  
  
このガイドには次のセクションが含まれます。  
  
- オフライン ドメイン参加の概要  
  
- オフライン ドメイン参加するための要件
  
- オフライン ドメイン参加プロセス
  
- オフライン ドメイン参加を実行する手順  
  
## <a name="offline-domain-join-overview"></a>オフライン ドメイン参加の概要  
Windows Server 2008 R2 で導入された、ドメイン コント ローラーには、オフライン ドメイン参加と呼ばれる機能が含まれます。 Djoin.exe をという名前のコマンド ライン ユーティリティを使用して、ドメイン参加操作の完了中にドメイン コント ローラーに物理的に接続せずにコンピューターをドメインに参加できます。 Djoin.exe を使用するための一般的な手順は次のとおりです。  
  
1.  実行**させる djoin/provision**コンピューター アカウントのメタデータを作成します。 このコマンドの出力は、base 64 でエンコードされた blob を含む .txt ファイルです。  
  
2.  実行**させる djoin/requestODJ** .txt ファイルから展開先コンピューターの Windows ディレクトリにコンピューター アカウントのメタデータを挿入します。  
  
3.  セットアップ先のコンピューターを再起動し、コンピューターがドメインに参加します。  
  
### <a name="BKMK_ODJOverview"></a>オフライン ドメイン参加に DirectAccess ポリシー シナリオの概要  
DirectAccess オフライン ドメイン参加は、Windows Server 2016、Windows Server 2012、Windows 10 および Windows 8 を実行しているコンピューターが企業のネットワークに物理的に結合することがなくドメインに参加することができますを使用して、または VPN 経由で接続するプロセスです。 場所からコンピューターをドメインに参加させるが可能になります。 企業ネットワークへの接続が存在しません。 Directaccess オフライン ドメイン参加では、リモートのプロビジョニングを許可するクライアントに DirectAccess ポリシーを提供します。  
  
ドメイン参加では、コンピューター アカウントを作成し、Windows オペレーティング システムと Active Directory ドメインを実行するコンピューター間の信頼関係を確立します。  
  
## <a name="BKMK_ODJRequirements"></a>オフライン ドメイン参加を準備します。  
  
1.  コンピューター アカウントを作成します。  
  
2.  コンピューター アカウントが所属するすべてのセキュリティ グループのメンバーシップをインベントリします。  
  
3.  必要なコンピューター証明書、グループ ポリシー、および新しいクライアントに適用するグループ ポリシー オブジェクトを収集します。  
  
. 次のセクションでは、オペレーティング システムの要件と Djoin.exe を使用して DirectAccess オフライン ドメイン参加を実行するための資格情報の要件について説明します。  
  
### <a name="operating-system-requirements"></a>オペレーティング システムの要件  
Windows Server 2016、Windows Server 2012 または Windows 8 を実行しているコンピューターでのみ、DirectAccess の Djoin.exe を行うことができます。 実行する Djoin.exe プロビジョニング コンピューター アカウントのデータを AD DS にコンピューターでは、Windows Server 2016、Windows 10、Windows Server 2012 または Windows 8 が実行されている必要があります。 Windows Server 2016、Windows 10、Windows Server 2012、または Windows 8、ドメインに参加するコンピューターを実行してもする必要があります。  
  
### <a name="credential-requirements"></a>資格情報の要件  
を、オフライン ドメイン参加を実行するには、ワークステーションをドメインに参加させるために必要な権限が必要です。 Domain Admins グループのメンバーは、既定では、これらの権限を持っています。 Domain Admins グループのメンバーでない場合は、ワークステーションをドメインに参加できるように、次の操作のいずれかの Domain Admins グループのメンバーが完了する必要があります。  
  
-   グループ ポリシーを使用して、必要なユーザー権利を付与します。 このメソッドでは、既定の Computers コンテナーおよび (Deny アクセス制御エントリ (Ace) には追加されません) 場合、後で作成された組織単位 (OU) では、コンピューターを作成できます。  
  
-   適切なアクセス許可を委任するドメインの既定の Computers コンテナーのアクセス制御リスト (ACL) を編集します。  
  
-   OU を作成しを付与するには、その OU の ACL を編集、 **- 子の作成を許可する**権限。 渡す、 **/machineOU**パラメーターを**させる djoin/provision**コマンド。  
  
次の手順では、グループ ポリシーを備えたユーザー権利を付与する方法と、適切なアクセス許可を委任する方法を示しています。  
  
#### <a name="granting-user-rights-to-join-workstations-to-the-domain"></a>ワークステーションをドメインに参加するユーザーの権限を付与します。  
グループ ポリシー管理コンソール (GPMC) を使用して、ドメイン ポリシーを変更またはドメインにワークステーションを追加するユーザーの権限を与える設定を持つ新しいポリシーを作成することができます。  
  
メンバーシップ**Domain Admins**、またはそれと同等のユーザーの権限を付与するために必要な最低限です。  適切なアカウントの使用に関する詳細を確認し、グループ メンバーシップ[ローカルおよびドメインの既定のグループ](https://go.microsoft.com/fwlink/?LinkId=83477)(https://go.microsoft.com/fwlink/?LinkId=83477) します。   
  
###### <a name="to-grant-rights-to-join-workstations-to-a-domain"></a>ワークステーションをドメインに参加させる権限を付与するには  
  
1.  をクリックして**開始**、 をクリックして**管理ツール**、順にクリックします**Group Policy Management**します。  
  
2.  フォレストの名前をダブルクリックし、ダブルクリックして**ドメイン**を右クリックして、コンピューターを参加するドメインの名前をダブルクリック**既定のドメイン ポリシー**、 をクリックし、 **編集**します。  
  
3.  コンソール ツリーで、ダブルクリック**コンピューターの構成**、 をダブルクリックします**ポリシー**、 をダブルクリックします**Windows 設定**、ダブルクリックして**セキュリティ設定**、ダブルクリック**ローカル ポリシー**、し、ダブルクリック**ユーザー権利の割り当て**します。  
  
4.  詳細ウィンドウでダブルクリック**ワークステーションをドメインに追加**します。  
  
5.  選択、**これらのポリシー設定を定義**チェック ボックスをオンにして**追加のユーザーまたはグループ**します。  
  
6.  クリックして、ユーザーの権限を付与するアカウントの名前を入力**OK** 2 回クリックします。  
  
## <a name="BKMK_ODKSxS"></a>オフライン ドメイン参加プロセス  
コンピューター アカウントのメタデータをプロビジョニングする管理者特権のコマンド プロンプトで Djoin.exe を実行します。 プロビジョニングのコマンドを実行すると、コンピューター アカウントのメタデータは、コマンドの一部として指定したバイナリ ファイルに作成されます。  
  
詳細については、オフライン ドメイン参加中のコンピューター アカウントのプロビジョニングに使用される NetProvisionComputerAccount 関数を参照してください。 [NetProvisionComputerAccount 関数](https://go.microsoft.com/fwlink/?LinkId=162426)(https://go.microsoft.com/fwlink/?LinkId=162426) します。 対象のコンピューターでローカルに実行される NetRequestOfflineDomainJoin 関数に関する詳細については、次を参照してください。 [NetRequestOfflineDomainJoin 関数](https://go.microsoft.com/fwlink/?LinkId=162427)(https://go.microsoft.com/fwlink/?LinkId=162427) します。  
  
## <a name="BKMK_ODJSteps"></a>DirectAccess のオフライン ドメイン参加を実行する手順  
オフライン ドメイン参加のプロセスには、次の手順が含まれています。  
  
1.  各リモート クライアントの新しいコンピューター アカウントを作成しから Djoin.exe コマンドを使用してプロビジョニング パッケージを生成、既にドメインは、企業ネットワーク内のコンピューターを参加しています。  
  
2.  クライアント コンピューターを DirectAccessClients セキュリティ グループに追加します。  
  
3.  ドメインに参加するリモート コンピューター (s) にプロビジョニング パッケージを安全に転送します。  
  
4.  プロビジョニング パッケージを適用し、クライアントをドメインに参加します。  
  
5.  ドメインへの参加を完了して、接続を確立するクライアントを再起動します。  
  
クライアントのプロビジョニングのパケットを作成するときに考慮すべき 2 つのオプションがあります。 PKI なしの DirectAccess をインストールする作業の開始ウィザードを使用した場合は、次の 1 のオプションを使用する必要があります。 高度なセットアップ ウィザードを使用して、PKI と DirectAccess をインストールした場合は、次の 2 のオプションを使用する必要があります。  
  
オフライン ドメイン参加を実行する次の手順を完了するには。  
  
##### <a name="option1-create-a-provisioning-package-for-the-client-without-pki"></a>オプション 1:PKI せず、クライアントのプロビジョニング パッケージを作成します。  
  
1.  リモート アクセス サーバーのコマンド プロンプトで、コンピューター アカウントをプロビジョニングするには、次のコマンドを入力します。  
  
    ```  
    Djoin /provision /domain <your domain name> /machine <remote machine name> /policynames DA Client GPO name /rootcacerts /savefile c:\files\provision.txt /reuse  
    ```  
  
##### <a name="option2-create-a-provisioning-package-for-the-client-with-pki"></a>Option2:Pki クライアントのプロビジョニング パッケージを作成します。  
  
1.  リモート アクセス サーバーのコマンド プロンプトで、コンピューター アカウントをプロビジョニングするには、次のコマンドを入力します。  
  
    ```  
    Djoin /provision /machine <remote machine name> /domain <Your Domain name> /policynames <DA Client GPO name> /certtemplate <Name of client computer cert template> /savefile c:\files\provision.txt /reuse  
    ```  
  
##### <a name="add-the-client-computer-to-the-directaccessclients-security-group"></a>クライアント コンピューターを DirectAccessClients セキュリティ グループに追加します。  
  
1.  ドメイン コント ローラーでから**開始**画面で「 **Active**選択**Active Directory ユーザーとコンピューター**から**アプリ**画面.  
  
2.  ドメインの下のツリーを展開し、選択、**ユーザー**コンテナー。  
  
3.  詳細ペインで右クリックして**DirectAccessClients**、 をクリック**プロパティ**します。  
  
4.  **[メンバー]** タブで **[追加]** をクリックします。  
  
5.  をクリックして**オブジェクトの種類**を選択します**コンピューター**、順にクリックします**OK**します。  
  
6.  クリックして追加するには、クライアント名を入力**OK**します。  
  
7.  をクリックして**OK**を閉じる、 **DirectAccessClients**プロパティ ダイアログ ボックスを閉じます**Active Directory ユーザーとコンピューター**します。  
  
##### <a name="copy-and-then-apply-the-provisioning-package-to-the-client-computer"></a>コピーし、クライアント コンピューターにプロビジョニング パッケージを適用  
  
1.  保存した場所、c:\provision\provision.txt クライアント コンピューターに、リモート アクセス サーバーで c:\files\provision.txt からプロビジョニング パッケージをコピーします。  
  
2.  クライアント コンピューターでは、管理者特権でコマンド プロンプトを開くし、ドメインへの参加を要求する次のコマンドを入力します。  
  
    ```  
    Djoin /requestodj /loadfile C:\provision\provision.txt /windowspath %windir% /localos  
    ```  
  
3.  クライアント コンピューターを再起動します。 コンピューターはドメインに参加します。 再起動の後、クライアントはドメインに結合し、DirectAccess で企業ネットワークに接続されています。  
  
## <a name="see-also"></a>関連項目  
[NetProvisionComputerAccount 関数](https://go.microsoft.com/fwlink/?LinkId=162426)  
[NetRequestOfflineDomainJoin 関数](https://go.microsoft.com/fwlink/?LinkId=162427)  
  


