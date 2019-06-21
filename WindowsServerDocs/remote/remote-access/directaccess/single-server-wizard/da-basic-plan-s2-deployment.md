---
title: 手順 2. 基本的な DirectAccess 展開を計画します。
description: このトピックは、作業の開始ウィザードの Windows Server 2016 を使用して単一の DirectAccess サーバー展開ガイドの一部です。
manager: brianlic
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: networking-da
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 7ddcb162-dd92-406c-acab-d3de7239c644
ms.author: pashort
author: shortpatti
ms.openlocfilehash: c82d5e48f26d9defceb3b7583e06eeedbc71a082
ms.sourcegitcommit: afb0602767de64a76aaf9ce6a60d2f0e78efb78b
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/20/2019
ms.locfileid: "67281662"
---
# <a name="step-2-plan-the-basic-directaccess-deployment"></a>手順 2. 基本的な DirectAccess 展開を計画します。

>適用先:Windows Server 2016 の Windows Server (半期チャネル)

DirectAccess インフラストラクチャを計画するには後の基本的な設定を 1 台のサーバーに DirectAccess を展開するのには、次の手順は、作業の開始ウィザードの設定を計画することです。  
  
|タスク|説明|  
|----|--------|  
|クライアント展開の計画|既定では、作業の開始ウィザード DirectAccess を展開しますすべてのラップトップやノートブック コンピューター、ドメインのクライアント設定の GPO に WMI フィルターを適用することで|  
|DirectAccess サーバー展開の計画|DirectAccess サーバーの展開方法を計画します。|  
  
## <a name="bkmk_2_1_client"></a>クライアント展開の計画  
クライアントの展開の計画時には 2 つの決定事項があります。  
  
1.  DirectAccess をモバイル コンピューターのみから使用できるようにするか、すべてのコンピューターから使用できるようにするか  
  
    作業の開始ウィザードで DirectAccess クライアントを構成するときに DirectAccess を使用して接続する指定したセキュリティ グループのモバイル コンピューターのみを許可することもできます。 モバイル コンピューターへのアクセスを制限する場合、DirectAccess は自動的に、DirectAccess クライアントが指定したセキュリティ グループでのモバイル コンピューターのみに GPO を適用することを確認する WMI フィルターを構成します。 DirectAccess 管理者には、この設定を有効にするグループ ポリシー WMI フィルター作成または変更するアクセス許可が必要です。  
  
2.  どのセキュリティ グループに DirectAccess クライアント コンピューターを含めるか  
  
    DirectAccess 設定は DirectAccess クライアント GPO に含まれます。 GPO は、作業の開始ウィザードで指定したセキュリティ グループの一部であるコンピューターに適用されます。 サポートされる任意のドメインに含まれるセキュリティ グループを指定できます。 DirectAccess を構成する前に、セキュリティ グループを作成する必要があります。 DirectAccess の展開を完了した後、セキュリティ グループにコンピューターを追加できますが、セキュリティ グループに別のドメイン内に存在するクライアント コンピューターを追加する場合、クライアント GPO は適用されませんこれらのクライアントに注意してください。 たとえば、ドメイン A に DirectAccess クライアント用の SG1 を作成し、後でドメイン B のクライアントをこのグループに追加した場合、クライアント GPO はドメイン B のクライアントに適用されません。この問題を回避するには、クライアント コンピューターを含むドメインごとに、新しいクライアント セキュリティ グループを作成します。 または新しいセキュリティ グループを作成しない場合は、新しいドメインに対して、新しい GPO の名前で Add-DAClient コマンドレットを実行します。  
  
## <a name="bkmk_2_2_server"></a>DirectAccess サーバー展開の計画  
DirectAccess サーバーの展開を計画する際に決定を数多くあります。  
  
-   **ネットワーク トポロジ**-DirectAccess サーバーをデプロイするときに 2 つのトポロジを使用してあります。  
  
    -   **2 つのアダプター** -2 つのネットワーク アダプター、インターネットに直接接続されている 1 つのネットワーク アダプターで DirectAccess を構成でき、もう一方が内部ネットワークに接続されています。 または、サーバーをファイアウォールやルーターなどの境界デバイスの内側にインストールします。 この構成では、一方のネットワーク アダプターを境界ネットワークに接続し、他方を内部ネットワークに接続します。  
  
    -   **単一のネットワーク アダプター** -ファイアウォールやルーターなどのエッジ デバイスの背後にあるこの構成は、DirectAccess サーバーがインストールされています。 ネットワーク アダプターは内部ネットワークに接続します。  
  
-   **ネットワーク アダプター** -DirectAccess ウィザードは、DirectAccess サーバーで構成されたネットワーク アダプターを自動的に検出します。 正しいアダプターが選択されていることを確認することができます、**レビュー**ページ。  
  
-   **IP-HTTPS 証明書**-この展開で必要な PKI がないため、ウィザードは IP-HTTPS およびネットワーク ロケーション サーバー (存在する証明書がない場合) の自己署名証明書を自動的にプロビジョニングし、自動的に有効Kerberos プロキシ。 このウィザードでは、IPv4 専用環境でプロトコル変換のための NAT64 と DNS64 もできます。 ウィザードでは、構成の適用が完了したら、クリックして **閉じる**します。  
  
-   **Windows 7 クライアント**-作業の開始ウィザードから Windows 7 クライアントのサポートを有効にすることはできません。 これは、高度なセットアップ ウィザードから有効にできます。 詳細については、次を参照してください。[詳細設定を使用する単一の DirectAccess サーバーをデプロイ](../single-server-advanced/Deploy-a-Single-DirectAccess-Server-with-Advanced-Settings.md)します。  
  
-   **VPN 構成**-DirectAccess を構成する前に、リモート クライアントに VPN アクセスを提供しようとしているかどうかを決定します。 DirectAccess の接続をサポートしていない組織内のクライアント コンピューターがある場合は、VPN アクセスを提供する必要があります (、管理されていないか、DirectAccess がサポートされていないオペレーティング システムを実行するため)。 作業の開始ウィザードでは、DHCP を使用して VPN の IP アドレスの割り当てを構成し、Active Directory を使用して認証する VPN クライアントを構成します。  
  
-   **強制的にトンネリング**-使用する必要があります、強制トンネリングを使用する場合がありますが、将来に追加するか、[詳細設定を使用する単一の DirectAccess サーバーをデプロイ](../single-server-advanced/Deploy-a-Single-DirectAccess-Server-with-Advanced-Settings.md)2 つのトンネル構成をデプロイします。 セキュリティの考慮事項によりは単一のトンネル構成では、強制トンネリングはサポートされていません。  
  
## <a name="BKMK_Links"></a>前の手順  
  
-   [ステップ 1: 基本的な DirectAccess インフラストラクチャを計画する](da-basic-plan-s1-infrastructure.md)  
  


