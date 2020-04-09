---
title: DirectAccess オフライン ドメイン参加
description: このガイドでは、Windows Server 2016 で DirectAccess を使用してオフラインドメイン参加を実行する手順について説明します。
manager: brianlic
ms.prod: windows-server
ms.technology: networking-da
ms.topic: article
ms.assetid: 55528736-6c19-40bd-99e8-5668169ef3c7
ms.author: lizross
author: eross-msft
ms.openlocfilehash: 43f0c606f16af00797f0325b793d476e6c2892f8
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/08/2020
ms.locfileid: "80815665"
---
# <a name="directaccess-offline-domain-join"></a>DirectAccess オフライン ドメイン参加

>適用対象: Windows Server (半期チャネル)、Windows Server 2016

このガイドでは、DirectAccess でオフラインドメイン参加を実行する手順について説明します。 オフラインドメイン参加中に、コンピューターが物理的または VPN 接続を使用せずにドメインに参加するように構成されている。  
  
このガイドには次のセクションが含まれます。  
  
- オフラインドメイン参加の概要  
  
- オフラインドメイン参加の要件
  
- オフラインドメイン参加プロセス
  
- オフラインドメイン参加を実行するための手順  
  
## <a name="offline-domain-join-overview"></a>オフラインドメイン参加の概要  
Windows Server 2008 R2 で導入されたドメインコントローラーには、Offline Domain Join と呼ばれる機能が含まれています。 Djoin .exe という名前のコマンドラインユーティリティを使用すると、ドメインへの参加操作の完了中にドメインコントローラーに物理的に接続しなくても、コンピューターをドメインに参加させることができます。 Djoin を使用するための一般的な手順は次のとおりです。  
  
1.  **Djoin.exe/プロビジョニング**を実行して、コンピューターアカウントのメタデータを作成します。 このコマンドの出力は、base-64 でエンコードされた blob を含む .txt ファイルです。  
  
2.  **Djoin.exe/requestODJ**を実行して、コンピューターアカウントのメタデータを .txt ファイルから対象コンピューターの Windows ディレクトリに挿入します。  
  
3.  対象のコンピューターを再起動すると、コンピューターがドメインに参加します。  
  
### <a name="offline-domain-join-with-directaccess-policies-scenario-overview"></a><a name="BKMK_ODJOverview"></a>DirectAccess ポリシーを使用したオフラインドメイン参加のシナリオの概要  
DirectAccess オフラインドメイン参加とは、windows Server 2016、Windows Server 2012、Windows 10、および Windows 8 を実行しているコンピューターが、企業ネットワークに物理的に参加したり、VPN 経由で接続したりせずにドメインに参加するために使用できるプロセスです。 これにより、企業ネットワークに接続されていない場所からドメインにコンピューターを参加させることができます。 DirectAccess のオフラインドメイン参加により、リモートプロビジョニングを可能にする DirectAccess ポリシーがクライアントに提供されます。  
  
ドメイン参加は、コンピューターアカウントを作成し、Windows オペレーティングシステムを実行しているコンピューターと Active Directory ドメインとの間に信頼関係を確立します。  
  
## <a name="prepare-for-offline-domain-join"></a><a name="BKMK_ODJRequirements"></a>オフラインドメイン参加の準備  
  
1.  コンピューターアカウントを作成します。  
  
2.  コンピューターアカウントが属しているすべてのセキュリティグループのメンバーシップをインベントリします。  
  
3.  新しいクライアントに適用される、必要なコンピューター証明書、グループポリシー、およびグループポリシーオブジェクトを収集します。  
  
。 次のセクションでは、Djoin を使用して DirectAccess のオフラインドメイン参加を実行するためのオペレーティングシステムの要件と資格情報の要件について説明します。  
  
### <a name="operating-system-requirements"></a>オペレーティング システムの要件  
DirectAccess では、Windows Server 2016、Windows Server 2012、または Windows 8 を実行しているコンピューターでのみ、Djoin を実行できます。 コンピューターアカウントデータを AD DS にプロビジョニングするために Djoin を実行するコンピューターでは、Windows Server 2016、Windows 10、Windows Server 2012、または Windows 8 が実行されている必要があります。 ドメインに参加させるコンピューターは、Windows Server 2016、Windows 10、Windows Server 2012、または Windows 8 も実行している必要があります。  
  
### <a name="credential-requirements"></a>資格情報の要件  
オフラインドメイン参加を実行するには、ワークステーションをドメインに参加させるために必要な権限を持っている必要があります。 Domain Admins グループのメンバーには、これらの権限が既定で与えられています。 Domain Admins グループのメンバーでない場合、domain Admins グループのメンバーは、次のいずれかの操作を完了して、ワークステーションをドメインに参加させることができます。  
  
-   グループポリシーを使用して、必要なユーザー権利を付与します。 この方法では、[既定のコンピューター] コンテナーと、後で作成される組織単位 (OU) にコンピューターを作成できます (アクセス制御エントリ (Ace) を拒否しない場合)。  
  
-   ドメインの [既定のコンピューター] コンテナーのアクセス制御リスト (ACL) を編集して、適切なアクセス許可を委任します。  
  
-   OU を作成し、その OU の ACL を編集して、 **create child-Allow**権限を付与します。 **/Machineou**パラメーターを**djoin.exe/プロビジョン**コマンドに渡します。  
  
次の手順では、グループポリシーにユーザー権利を付与する方法と、適切なアクセス許可を委任する方法について説明します。  
  
#### <a name="granting-user-rights-to-join-workstations-to-the-domain"></a>ワークステーションをドメインに参加させるためのユーザー権限を付与する  
グループポリシー管理コンソール (GPMC) を使用してドメインポリシーを変更したり、ユーザーにワークステーションをドメインに追加する権限を付与する設定を持つ新しいポリシーを作成したりできます。  
  
ユーザー権限を付与するには、 **Domain Admins**のメンバーシップ、またはそれと同等のメンバーシップが最低限必要です。  適切なアカウントおよびグループメンバーシップの使用方法の詳細については、「[ローカルおよびドメインの既定のグループ](https://go.microsoft.com/fwlink/?LinkId=83477)」 (https://go.microsoft.com/fwlink/?LinkId=83477)を参照してください。   
  
###### <a name="to-grant-rights-to-join-workstations-to-a-domain"></a>ドメインにワークステーションを参加させる権限を付与するには  
  
1.  **[スタート]** 、 **[管理ツール]** 、 **[グループポリシー管理]** の順にクリックします。  
  
2.  フォレストの名前をダブルクリックし、 **[ドメイン]** をダブルクリックします。次に、コンピューターに参加するドメインの名前をダブルクリックし、 **[既定のドメインポリシー]** を右クリックして、 **[編集]** をクリックします。  
  
3.  コンソールツリーで、 **[コンピューターの構成]** をダブルクリックし、 **[ポリシー]** をダブルクリックします。次に、 **[Windows の設定]** をダブルクリックし、 **[セキュリティの設定]** をダブルクリックします。次に、 **[ローカルポリシー]** をダブルクリックし、 **[ユーザー権利の割り当て]** をダブルクリックします。  
  
4.  詳細ウィンドウで、 **[ドメインへのワークステーションの追加]** をダブルクリックします。  
  
5.  **[これらのポリシーの設定を定義]** する チェックボックスをオンにし、 **[ユーザーまたはグループの追加]** をクリックします。  
  
6.  ユーザーに権限を付与するアカウントの名前を入力し、[ **OK]** を2回クリックします。  
  
## <a name="offline-domain-join-process"></a><a name="BKMK_ODKSxS"></a>オフラインドメイン参加プロセス  
管理者特権のコマンドプロンプトで Djoin を実行し、コンピューターアカウントのメタデータをプロビジョニングします。 プロビジョニングコマンドを実行すると、コンピューターアカウントのメタデータが、コマンドの一部として指定したバイナリファイルに作成されます。  
  
オフラインドメイン参加時にコンピューターアカウントをプロビジョニングするために使用される NetProvisionComputerAccount 関数の詳細については、「 [NetProvisionComputerAccount 関数](https://go.microsoft.com/fwlink/?LinkId=162426)(https://go.microsoft.com/fwlink/?LinkId=162426)」を参照してください。 対象のコンピューターでローカルに実行される NetRequestOfflineDomainJoin 関数の詳細については、「 [Netrequestofflinedomainjoin 関数](https://go.microsoft.com/fwlink/?LinkId=162427)(https://go.microsoft.com/fwlink/?LinkId=162427)」を参照してください。  
  
## <a name="steps-for-performing-a-directaccess-offline-domain-join"></a><a name="BKMK_ODJSteps"></a>DirectAccess オフラインドメイン参加を実行するための手順  
オフラインドメイン参加プロセスには、次の手順が含まれます。  
  
1.  リモートクライアントごとに新しいコンピューターアカウントを作成し、企業ネットワーク内の既存のドメインに参加しているコンピューターから、Djoin .exe コマンドを使用してプロビジョニングパッケージを生成します。  
  
2.  クライアントコンピューターを DirectAccessClients セキュリティグループに追加する  
  
3.  プロビジョニングパッケージを、ドメインに参加するリモートコンピューターに安全に転送します。  
  
4.  プロビジョニングパッケージを適用し、クライアントをドメインに参加させます。  
  
5.  クライアントを再起動して、ドメインへの参加を完了し、接続を確立します。  
  
クライアントのプロビジョニングパケットの作成時に考慮する必要があるオプションは2つあります。 はじめにウィザードを使用して PKI なしで DirectAccess をインストールした場合は、次のオプション1を使用する必要があります。 高度なセットアップウィザードを使用して、PKI と共に DirectAccess をインストールした場合は、次のオプション2を使用する必要があります。  
  
オフラインドメイン参加を実行するには、次の手順を実行します。  
  
##### <a name="option1-create-a-provisioning-package-for-the-client-without-pki"></a>オプション 1: PKI を使用しないクライアントのプロビジョニングパッケージを作成する  
  
1.  リモートアクセスサーバーのコマンドプロンプトで、次のコマンドを入力してコンピューターアカウントをプロビジョニングします。  
  
    ```  
    Djoin /provision /domain <your domain name> /machine <remote machine name> /policynames DA Client GPO name /rootcacerts /savefile c:\files\provision.txt /reuse  
    ```  
  
##### <a name="option2-create-a-provisioning-package-for-the-client-with-pki"></a>Option2: PKI を使用してクライアントのプロビジョニングパッケージを作成する  
  
1.  リモートアクセスサーバーのコマンドプロンプトで、次のコマンドを入力してコンピューターアカウントをプロビジョニングします。  
  
    ```  
    Djoin /provision /machine <remote machine name> /domain <Your Domain name> /policynames <DA Client GPO name> /certtemplate <Name of client computer cert template> /savefile c:\files\provision.txt /reuse  
    ```  
  
##### <a name="add-the-client-computer-to-the-directaccessclients-security-group"></a>クライアントコンピューターを DirectAccessClients セキュリティグループに追加する  
  
1.  ドメインコントローラーの**スタート**画面で「 **Active** 」と入力し、[**アプリ**から**ユーザーとコンピューターを Active Directory** ] 画面を選択します。  
  
2.  ドメインの下のツリーを展開し、 **[ユーザー]** コンテナーを選択します。  
  
3.  詳細ウィンドウで、 **[Directaccessclients]** を右クリックし、 **[プロパティ]** をクリックします。  
  
4.  **[メンバー]** タブで **[追加]** をクリックします。  
  
5.  **[オブジェクトの種類]** をクリックし、 **[コンピューター]** を選択して、[ **OK]** をクリックします。  
  
6.  追加するクライアント名を入力し、[ **OK]** をクリックします。  
  
7.  **OK** をクリックして **directaccessclients**のプロパティ ダイアログボックスを閉じ、 **Active Directory ユーザーとコンピューター** を閉じます。  
  
##### <a name="copy-and-then-apply-the-provisioning-package-to-the-client-computer"></a>クライアントコンピューターにプロビジョニングパッケージをコピーして適用する  
  
1.  クライアントコンピューターの c:\provision\provision.txt に、保存されたリモートアクセスサーバーの c:\files\provision.txt からプロビジョニングパッケージをコピーします。  
  
2.  クライアントコンピューターで、管理者特権でのコマンドプロンプトを開き、次のコマンドを入力して、ドメインへの参加を要求します。  
  
    ```  
    Djoin /requestodj /loadfile C:\provision\provision.txt /windowspath %windir% /localos  
    ```  
  
3.  クライアントコンピューターを再起動します。 コンピューターがドメインに参加します。 再起動後、クライアントはドメインに参加し、DirectAccess を使用して企業ネットワークに接続されます。  
  
## <a name="see-also"></a>参照  
[NetProvisionComputerAccount 関数](https://go.microsoft.com/fwlink/?LinkId=162426)  
[NetRequestOfflineDomainJoin 関数](https://go.microsoft.com/fwlink/?LinkId=162427)  
  


