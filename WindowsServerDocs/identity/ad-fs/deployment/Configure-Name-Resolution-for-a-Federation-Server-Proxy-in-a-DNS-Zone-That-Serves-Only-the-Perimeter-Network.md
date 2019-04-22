---
ms.assetid: b7109e46-b66e-4c5c-8b87-a6611d68415a
title: 境界ネットワークのみを対象とする DNS ゾーンでフェデレーション サーバー プロキシの名前解決を構成する
description: ''
author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adfs
ms.author: billmath
ms.openlocfilehash: 32b8e3cc133ce95872881115608bb8cfb17b2427
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/17/2019
ms.locfileid: "59816013"
---
# <a name="configure-name-resolution-for-a-federation-server-proxy-in-a-dns-zone-that-serves-only-the-perimeter-network"></a>境界ネットワークのみを対象とする DNS ゾーンでフェデレーション サーバー プロキシの名前解決を構成する

>適用先:Windows Server 2016 では、Windows Server 2012 R2、Windows Server 2012

Active の Directory フェデレーション サービスでフェデレーション サーバーの名前解決が正常に作業できるように\(AD FS\)シナリオを 1 つまたは複数のドメイン名システム\(DNS\)ゾーン境界のみを提供します。ネットワークを次のタスクを完了する必要があります。  
  
-   フェデレーション サーバーの IP アドレスを追加するフェデレーション サーバー プロキシで hosts ファイルを更新する必要があります。  
  
-   AD FS のすべてのクライアント要求のホスト名、フェデレーション サーバー プロキシを解決するのには、境界ネットワークで DNS を構成する必要があります。 ホストを追加するには、 \(A\)フェデレーション サーバー プロキシの境界の DNS リソース レコード。  
  
> [!NOTE]  
> これらの手順は、あるホスト\(A\)リソース レコードのフェデレーション サーバーは、企業で既に作成されているネットワーク DNS。 このレコードが存在しない場合は、このレコードを作成し、これらの手順を実行します。 詳細については、ホストを作成する方法についての\(A\) 、フェデレーション サーバーのリソース レコードを参照してください[ホストを追加する&#40;A&#41;をフェデレーション サーバーの会社の DNS リソース レコード](Add-a-Host--A--Resource-Record-to-Corporate-DNS-for-a-Federation-Server.md)します。  
  
## <a name="add-the-ip-address-of-a-federation-server-to-the-hosts-file"></a>Hosts ファイルにフェデレーション サーバーの IP アドレスを追加します。  
フェデレーション サーバーの DNS ホスト名を指すフェデレーション サーバー プロキシで hosts ファイルにエントリを追加する必要があります、フェデレーション サーバー プロキシは、アカウント パートナーの境界ネットワークで期待どおりに作業できる、ように\(fs.fabrikam.com など\)と IP アドレス\(例: 192.168.1.4\)アカウント パートナーの企業ネットワークにします。 フェデレーション サーバー プロキシがクライアントを解決するのにはそれ自体に接続するを防ぎますこのエントリを hosts ファイルに追加\-アカウント パートナー フェデレーション サーバーへの呼び出しを開始します。  
  
この手順を実行するには、ローカル コンピューターの **Administrators**グループのメンバーシップか、それと同等のメンバーシップが最低限必要です。  適切なアカウントの使用方法の詳細を確認し、グループ メンバーシップ [ローカルおよびドメインの既定のグループ](https://go.microsoft.com/fwlink/?LinkId=83477)します。   
  
#### <a name="to-add-the-ip-address-of-a-federation-server-to-the-hosts-file"></a>Hosts ファイルにフェデレーション サーバーの IP アドレスを追加するには  
  
1.  %Systemroot% に移動します\\Winnt\\System32\\ドライバー ディレクトリのフォルダーを検索し、**ホスト**ファイル。  
  
2.  メモ帳を起動し、開きます、**ホスト**ファイル。  
  
3.  アカウント パートナーで、IP アドレスとのフェデレーション サーバーのホスト名を追加、**ホスト**ファイルを次の例に示すようにします。  
  
    **192.168.1.4fs.fabrikam.com**  
  
4.  ファイルを保存し、閉じます。  
  
## <a name="add-a-host-a-resource-record-to-perimeter-dns-for-a-federation-server-proxy"></a>ホストの追加\(A\)フェデレーション サーバー プロキシの境界の DNS リソース レコード  
ホストを作成する必要があります最初に、インターネット上のクライアントが、新しく展開されるフェデレーション サーバー プロキシを介してフェデレーション サーバーに正常にアクセスできるように\(A\)境界 DNS リソース レコード。 このリソース レコードは、アカウント フェデレーション サーバーのホスト名を解決\(fs.fabrikam.com など\)、アカウント フェデレーション サーバー プロキシの IP アドレスに\(など 131.107.27.68\)で、境界ネットワーク。  
  
> [!NOTE]  
> 使用している DNS サーバー、DNS サーバー サービスが、Windows 2000 Server、Windows Server 2003、または Windows Server 2008 を実行している境界の DNS ゾーンを制御することが前提です。  
  
メンバーシップ **管理者**, 、または同等の権限は、この手順を実行するために必要な最小値。  適切なアカウントの使用方法の詳細を確認し、グループ メンバーシップ [ローカルおよびドメインの既定のグループ](https://go.microsoft.com/fwlink/?LinkId=83477)します。   
  
#### <a name="to-add-a-host-a-resource-record-to-perimeter-dns-for-a-federation-server-proxy"></a>ホストを追加する\(A\)フェデレーション サーバー プロキシの境界の DNS リソース レコード  
  
1.  境界ネットワークの DNS サーバー、DNS スナップインを開きます\-でします。 クリックして**開始**、 をポイント**管理ツール**、順にクリックします**DNS**します。  
  
2.  コンソール ツリーで、右\-、適切な前方参照ゾーンをクリックし、クリックして**新しいホスト\(A または AAAA\)** します。  
  
3.  **名前**、フェデレーション サーバーのコンピューター名のみを入力します。 たとえば、完全修飾ドメイン名\(FQDN\) fs.fabrikam.com、型**fs**します。  
  
4.  **IP アドレス**、たとえば、新しいフェデレーション サーバー プロキシの IP アドレスを入力**131.107.27.68**します。  
  
5.  **[ホストの追加]** をクリックします。  
  
## <a name="additional-references"></a>その他の参照情報  
[チェックリスト:フェデレーション サーバー プロキシを設定します。](Checklist--Setting-Up-a-Federation-Server-Proxy.md)  
  
[フェデレーション サーバー プロキシの名前解決の要件](https://technet.microsoft.com/library/dd807055.aspx)  
  

