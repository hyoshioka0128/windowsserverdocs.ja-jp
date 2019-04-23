---
title: BranchCache 展開ガイド
description: このトピックは、BranchCache 展開ガイドの Windows Server 2016、ブランチ オフィスに WAN 帯域幅使用量を最適化するために分散され、ホスト型キャッシュ モードで BranchCache を展開する方法を示しますの一部
manager: brianlic
ms.prod: windows-server-threshold
ms.technology: networking-bc
ms.topic: get-started-article
ms.assetid: 3830b356-36d3-44f9-a1d7-990ff3e57403
ms.author: pashort
author: shortpatti
ms.openlocfilehash: 9bccf69f0a913159a395fabc670a63e2c159bd91
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/17/2019
ms.locfileid: "59888183"
---
# <a name="branchcache-deployment-guide"></a>BranchCache 展開ガイド

>適用対象:Windows Server 2016 の Windows Server (半期チャネル)

このガイドを使用すると、Windows Server 2016 での BranchCache を展開するのに方法について説明します。  
  
このトピックに加えは、このガイドには、次のセクションが含まれています。  
  
-   [BranchCache 設計の選択](../../branchcache/plan/Choosing-a-BranchCache-Design.md)  
  
-   [BranchCache を展開します。](../../branchcache/deploy/Deploy-BranchCache.md)  
  
## <a name="branchcache-deployment-overview"></a>BranchCache の展開の概要

BranchCache は Windows Server 2016、Windows Server の一部のエディションに含まれているワイド エリア ネットワーク (WAN) 帯域幅最適化テクノロジ&reg;2012 R2、Windows Server&reg; 2012、Windows Server&reg; 2008 R2、および関連します。Windows クライアント オペレーティング システム。  
  
WAN の帯域幅を最適化するため、BranchCache ではメイン オフィスのコンテンツ サーバーからコンテンツがコピーされ、ブランチ オフィスの場所にキャッシュされます。これにより、ブランチ オフィスのクライアント コンピューターは WAN を経由せずにローカルにコンテンツにアクセスできます。  
  
ブランチ オフィスには、コンテンツがキャッシュには、Windows Server 2016 の BranchCache 機能を実行しているサーバー、Windows Server 2012 R2、Windows Server 2012、または Windows Server 2008 R2、またはがある場合、ブランチ オフィスは、コンテンツで使用可能なサーバーがない cacWindows 10 を実行しているクライアント コンピューターで hed&reg;、Windows&reg; 8.1、Windows 8、または Windows 7&reg;します。  
  
経由でコンテンツ サーバーに接続するのではなく、コンテンツをローカルに、同じブランチ オフィスのある他のコンピューターを取得できます、クライアント コンピューターを要求してメイン オフィスまたはクラウドのデータ センターからコンテンツを受信すると、コンテンツがブランチ オフィスにキャッシュされた、WAN リンクです。  
  
**BranchCache を展開する利点**  
  
BranchCache キャッシュのファイル、web、およびブランチ オフィスの場所にアプリケーションのコンテンツは、低速の WAN 接続経由でコンテンツにアクセスするのではなく、ローカル エリア ネットワーク (LAN) を使用してデータにアクセスするコンピューターをクライアントに許可します。  
  
BranchCache は、WAN のトラフィックとブランチ オフィスのユーザー、ネットワーク上のファイルを開くために必要な時間の両方が軽減されます。  BranchCache が常に最新のデータをユーザーに提供し、ホスト型キャッシュ サーバーおよびクライアント コンピューター上のキャッシュを暗号化することで、コンテンツのセキュリティを保護します。  
  
### <a name="what-this-guide-provides"></a>このガイドの内容  
このデプロイ ガイドでは、次のモードで BranchCache を展開できます。  
  
-   分散キャッシュ モード。 このモードでは、ブランチ オフィスのクライアント コンピューターは、メイン オフィスまたはクラウドでのコンテンツ サーバーからコンテンツをダウンロードし、同じブランチ オフィスの他のコンピューターのコンテンツがキャッシュされます。 分散キャッシュ モードでは、ブランチ オフィスのサーバー コンピューターは必要ありません。  
  
-   ホスト型キャッシュ モード。 このモードでは、ブランチ オフィス クライアント コンピューター ダウンロードからメイン オフィスまたはクラウドでのコンテンツ サーバーとホスト型キャッシュ サーバーのコンテンツは、クライアントからコンテンツを取得します。 ホスト型キャッシュ サーバーは、他のクライアント コンピューターのコンテンツをキャッシュします。  
  
このガイドには、次の 3 つの種類のコンテンツ サーバーをデプロイする方法の手順も提供します。 コンテンツ サーバーはブランチ オフィスのクライアント コンピューターによってダウンロードされたソース コンテンツを含み、どちらのモードで BranchCache を展開する 1 つまたは複数のコンテンツ サーバーが必要です。 コンテンツ サーバーの種類があります。  
  
-   **Web コンテンツ サーバーのサーバー ベース**します。 これらのコンテンツ サーバーは、HTTP および HTTPS プロトコルを使用して、BranchCache クライアント コンピューターにコンテンツを送信します。 これらのコンテンツ サーバーが BranchCache をサポートする Windows Server 2016、Windows Server 2012 R2、Windows Server 2012、または Windows Server 2008 R2 のバージョンを実行する必要があり、BranchCache 機能がインストールされている時にします。  
  
-   **BITS ベースのアプリケーション サーバー**します。 これらのコンテンツ サーバーは、コンテンツをバック グラウンド インテリジェント転送サービス (BITS) を使用して、BranchCache クライアント コンピューターに送信します。 これらのコンテンツ サーバーが BranchCache をサポートする Windows Server 2016、Windows Server 2012 R2、Windows Server 2012、または Windows Server 2008 R2 のバージョンを実行する必要があり、BranchCache 機能がインストールされている時にします。  
  
-   **ファイル コンテンツ サーバーのサーバー ベース**します。 これらのコンテンツ サーバーが BranchCache をサポートする Windows Server 2016、Windows Server 2012 R2、Windows Server 2012、または Windows Server 2008 R2 のバージョンを実行する必要があり、ファイルがサービスにサーバーの役割をインストールします。 さらに、**ネットワーク ファイル用 BranchCache**ファイル サービス サーバーの役割の役割サービスをインストールして構成する必要があります。 これらのコンテンツ サーバーは、サーバー メッセージ ブロック (SMB) プロトコルを使用して、BranchCache クライアント コンピューターにコンテンツを送信します。  
  
詳細については、次を参照してください。[オペレーティング システムのバージョンの BranchCache](https://technet.microsoft.com/windows-server-docs/networking/branchcache/branchcache#a-namebkmkosaoperating-system-versions-for-branchcache)します。  
  
### <a name="branchcache-deployment-requirements"></a>BranchCache の展開の要件

このガイドを使用して BranchCache を展開するための要件を次に示します。  
  
-   **ファイル サービスおよび Web コンテンツ サーバー** BranchCache 機能を提供する次のオペレーティング システムのいずれかを実行する必要があります。Windows Server 2016、Windows Server 2012 R2、Windows Server 2012、または Windows Server 2008 R2。 Windows 8 およびそれ以降のクライアントを続行することはない Windows Server 2008 R2 を実行しているコンテンツ サーバーにアクセスするときに、BranchCache からメリットを表示する、新しいチャンクと Windows Server 2016、Windows Server 2012 でのテクノロジのハッシュの使用R2、および Windows Server 2012。  
  
-   **クライアント コンピューター**させるには、Windows 10、Windows 8.1、または Windows 8 を実行する必要があります、最新のデプロイ モデルのチャンキングおよび Windows Server 2012 で導入された機能強化のハッシュを使用します。  
  
-   **キャッシュ サーバーがホストされている**展開の機能強化を使用し、このドキュメントで説明する機能を拡張するには、Windows Server 2016、Windows Server 2012 R2、または Windows Server 2012 を実行する必要があります。  これを行うに適したトランスポート層セキュリティ (TLS 証明書を使用できる必要がありますが、Windows 7 を実行しているクライアント コンピューターを処理するために、ホスト型キャッシュ サーバーとして構成されているこれらのオペレーティング システムのいずれかを実行しているコンピューターは続行できます。)、Windows Server 2008 R2 および Windows 7」の説明に従って[BranchCache 展開ガイド](https://technet.microsoft.com/library/ee649232.aspx)します。  
  
-   **Active Directory ドメイン**グループ ポリシーとホスト型キャッシュの自動検出を利用するために必要なは、ドメインは、BranchCache を使用する必要はありません。  Windows PowerShell を使用して、個々 のコンピューターを構成できます。 さらに、新しい BranchCache グループ ポリシー設定を利用するには、2012 以降に、ドメイン コント ローラーが Windows Server を実行が必要です以前のオペレーティング システムを実行しているドメイン コント ローラー上に BranchCache の管理用テンプレートをインポートするか、Windows 10、Windows Server 2016、Windows 8.1 を実行している他のコンピューターにリモートでグループ ポリシー オブジェクトを作成します。Windows Server 2012 R2、Windows 8、または Windows Server 2012。

-   **Active Directory サイト**は自動的に検出できるホスト型キャッシュ サーバーのスコープを制限するために使用します。  ホスト型キャッシュ サーバーを自動的に検出するには、クライアントとサーバーの両方のコンピューターは、同じサイトに属している必要があります。 BranchCache では、クライアントとサーバーに最小限の影響を与える設計されており、追加のハードウェア要件にそれぞれのオペレーティング システムを実行するために必要なもの以外は設定されていません。  

**BranchCache の履歴とドキュメント**

BranchCache は Windows 7 で初めて導入されました&reg;および Windows Server&reg; 2008 R2、および Windows Server 2012、Windows 8、および以降のオペレーティング システムが強化されました。

> [!NOTE]
> Windows Server 2016 以外のオペレーティング システムで BranchCache を展開する場合は、次のドキュメント リソースを使用です。
> 
> - Windows 8、Windows 8.1、Windows Server 2012、および Windows Server 2012 R2 の BranchCache の詳細については、次を参照してください。 [BranchCache の概要](https://technet.microsoft.com/library/hh831696.aspx)します。  
> - Windows 7 および Windows Server 2008 R2 の BranchCache の詳細については、次を参照してください。 [Windows Server 2008 R2 の BranchCache](https://technet.microsoft.com/library/dd996634.aspx)します。  
  


