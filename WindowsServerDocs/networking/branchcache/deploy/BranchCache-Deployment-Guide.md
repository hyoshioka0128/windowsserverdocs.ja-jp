---
title: BranchCache 展開ガイド
description: このトピックの「BranchCache 展開ガイドの Windows Server 2016、ブランチ オフィスに WAN 帯域幅使用を最適化するために分散され、ホスト型キャッシュ モードで BranchCache を展開する方法示しますの一部である
manager: brianlic
ms.prod: windows-server-threshold
ms.technology: networking-bc
ms.topic: get-started-article
ms.assetid: 3830b356-36d3-44f9-a1d7-990ff3e57403
ms.author: pashort
author: shortpatti
ms.openlocfilehash: e7aa35260213a8a236b7c27cf74e36692438cd2a
ms.sourcegitcommit: 19d9da87d87c9eefbca7a3443d2b1df486b0b010
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/28/2018
---
# <a name="branchcache-deployment-guide"></a>BranchCache 展開ガイド

>適用対象: Windows Server (半期チャネル)、Windows Server 2016

このガイドを使用すると、Windows Server 2016 での BranchCache を展開するのに方法について説明します。  
  
このトピックに加えは、このガイドには、次のセクションが含まれています。  
  
-   [BranchCache 設計の選択](../../branchcache/plan/Choosing-a-BranchCache-Design.md)  
  
-   [BranchCache を展開します。](../../branchcache/deploy/Deploy-BranchCache.md)  
  
## <a name="branchcache-deployment-overview"></a>BranchCache の展開の概要

BranchCache は Windows Server 2016、Windows Server の一部のエディションに含まれているワイド エリア ネットワーク (WAN) 帯域幅最適化テクノロジ&reg;2012 R2、Windows Server&reg; 、Windows Server 2012&reg; 2008 R2、および関連する Windows クライアント オペレーティング システムです。  
  
WAN の帯域幅を最適化するには、BranchCache は、メイン オフィスのコンテンツ サーバーからコンテンツをコピーし、クライアント コンピューターは WAN を経由ではなくローカルでコンテンツにアクセスするブランチ オフィスを許可するブランチ オフィスの場所にコンテンツをキャッシュします。  
  
ブランチ オフィスでコンテンツがキャッシュされ、Windows Server 2016 の BranchCache 機能を実行しているサーバー、Windows Server 2012 R2、Windows Server 2012、または Windows Server 2008 R2 でのいずれか、または Windows 10 を実行しているクライアント コンピューターでコンテンツがキャッシュがない場合のサーバー使用可能なブランチ オフィス内、&reg;、Windows&reg; 8.1、Windows 8、または Windows 7&reg;します。  
  
クライアント コンピューターを要求してメイン オフィスまたはクラウド データ センターからコンテンツを受信すると、コンテンツがブランチ オフィスにキャッシュされ、同じブランチ オフィスにある他のコンピューターは WAN リンク経由でコンテンツ サーバーに接続するのではなく、ローカルでコンテンツを取得できます。  
  
**BranchCache を展開する利点**  
  
BranchCache のキャッシュ ファイル、Web、およびアプリケーションのコンテンツをブランチ オフィスの場所にクライアント コンピューターに低速の WAN 接続経由でコンテンツにアクセスするのではなくローカル エリア ネットワーク (LAN) を使用してデータのアクセスが許可されます。  
  
BranchCache では、WAN トラフィックとブランチ オフィスのユーザーを開くには、ネットワーク上のファイルに必要な時間の両方が減少します。  BranchCache は、常に最新のデータを持つユーザーを提供し、ホスト型キャッシュ サーバーとクライアント コンピューターのキャッシュを暗号化することによって、コンテンツのセキュリティを保護します。  
  
### <a name="what-this-guide-provides"></a>このガイドの説明  
この展開ガイドでは、次のモードで BranchCache を展開することができます。  
  
-   分散キャッシュ モードです。 このモードでは、ブランチ オフィスのクライアント コンピューターは、メイン オフィスまたはクラウド内のコンテンツ サーバーからコンテンツをダウンロードし、同じブランチ オフィスの他のコンピューターのコンテンツをキャッシュします。 分散キャッシュ モードでは、ブランチ オフィス内のサーバー コンピューターは必要ありません。  
  
-   ホスト型キャッシュ モードです。 このモードでは、ブランチ オフィス クライアント コンピューターでのダウンロード、メイン オフィスまたはクラウド内のコンテンツ サーバーおよびホスト型キャッシュ サーバーからコンテンツは、クライアントからコンテンツを取得します。 ホスト型キャッシュ サーバーは、他のクライアント コンピューターのコンテンツをキャッシュします。  
  
このガイドでは、次の 3 つの種類のコンテンツ サーバーを展開する方法に関する手順についても提供します。 コンテンツ サーバーには、ブランチ オフィスのクライアント コンピューターにダウンロードされるソース コンテンツが含まれているし、どちらのモードで BranchCache を展開する 1 つまたは複数のコンテンツ サーバーが必要です。 コンテンツ サーバーの種類があります。  
  
-   **Web コンテンツ サーバーのサーバー ベース**します。 これらのコンテンツ サーバーは、HTTP および HTTPS プロトコルを使用して、BranchCache クライアント コンピューターにコンテンツを送信します。 これらのコンテンツ サーバーは、BranchCache をサポートする Windows Server 2016、Windows Server 2012 R2、Windows Server 2012、または Windows Server 2008 R2 のバージョンを実行されている必要があり、BranchCache 機能がインストールされている時にします。  
  
-   **BITS ベースのアプリケーション サーバー**します。 これらのコンテンツ サーバーは、コンテンツをバック グラウンド インテリジェント転送サービス (BITS) を使用して、BranchCache クライアント コンピューターに送信します。 これらのコンテンツ サーバーは、BranchCache をサポートする Windows Server 2016、Windows Server 2012 R2、Windows Server 2012、または Windows Server 2008 R2 のバージョンを実行されている必要があり、BranchCache 機能がインストールされている時にします。  
  
-   **ファイル サーバー ベースのコンテンツ サーバー**します。 これらのコンテンツ サーバーは、BranchCache をサポートする Windows Server 2016、Windows Server 2012 R2、Windows Server 2012、または Windows Server 2008 R2 のバージョンを実行されている必要があり、サーバーの役割のインストール ファイルがサービスにします。 さらに、**ネットワーク ファイル用 BranchCache**ファイル サービス サーバー役割の役割サービスをインストールおよび構成する必要があります。 これらのコンテンツ サーバーは、サーバー メッセージ ブロック (SMB) プロトコルを使用して、BranchCache クライアント コンピューターにコンテンツを送信します。  
  
詳細については、次を参照してください。[オペレーティング システムのバージョンの BranchCache](https://technet.microsoft.com/en-us/windows-server-docs/networking/branchcache/branchcache#a-namebkmkosaoperating-system-versions-for-branchcache)します。  
  
### <a name="branchcache-deployment-requirements"></a>BranchCache の展開の要件

このガイドを使用して BranchCache を展開するための要件を次に示します。  
  
-   **ファイル サービスおよび Web コンテンツ サーバー** BranchCache 機能を提供する次のオペレーティング システムのいずれかを実行する必要があります。Windows Server 2016、Windows Server 2012 R2、Windows Server 2012、または Windows Server 2008 R2。 Windows 8 およびそれ以降のクライアントを続行することはない Windows Server 2008 R2 を実行しているコンテンツ サーバーにアクセスするときに、BranchCache の利点を表示する、新しいチャンキングと Windows Server 2016、Windows Server 2012 R2、および Windows Server 2012 では、テクノロジのハッシュを使用します。  
  
-   **クライアント コンピューター**必要がありますが実行されているようにするには、Windows 10、Windows 8.1、または Windows 8 の最新の展開モデルのチャンキングと Windows Server 2012 で導入された機能強化のハッシュを使用します。  
  
-   **キャッシュ サーバーがホストされている**展開の機能強化を活用し、このドキュメントで説明する機能を拡張するには、Windows Server 2016、Windows Server 2012 R2、または Windows Server 2012 で実行する必要があります。  これらのオペレーティング システムのいずれかを実行するコンピューターは、ホスト型キャッシュ サーバーは、Windows 7 を実行しているクライアント コンピューターに対して機能するが、これを行うには引き続きように構成されているに適したトランスポート層セキュリティ (TLS) では、Windows Server 2008 R2 および Windows 7 の説明に従って証明書を使用できる必要があります[BranchCache 展開ガイド](https://technet.microsoft.com/en-us/library/ee649232.aspx)します。  
  
-   **Active Directory ドメイン**のグループ ポリシーとホスト型キャッシュの自動検出を利用するために必要なは、ドメインは、BranchCache を使用する必要はありません。  Windows PowerShell を使用して個々 のコンピューターを構成することができます。 さらに、それがないこと、ドメイン コントローラーを実行している Windows Server 2012 以降新しい BranchCache グループ ポリシー設定を使用するために必要な以前のオペレーティング システムを実行しているドメイン コントローラー上に BranchCache の管理用テンプレートをインポートするか、Windows 10、Windows Server 2016、Windows 8.1、Windows Server 2012 R2、Windows 8、または Windows Server 2012 を実行している他のコンピューターに対しリモートからグループ ポリシー オブジェクトを作成することができます。

-   **Active Directory サイト**は自動的に検出できるホスト型キャッシュ サーバーのスコープを制限するために使用されます。  ホスト型キャッシュ サーバーを自動的に検出するには、クライアントとサーバーの両方のコンピューターは、同じサイトに属している必要があります。 BranchCache は、クライアントとサーバーにほとんど影響を与えないように設計されています、追加のハードウェア要件以外にそれぞれのオペレーティング システムを実行する必要なアクセス許可されることはありません。  

**BranchCache の履歴とドキュメント**

BranchCache は、Windows 7 で初めて導入されました&reg;および Windows Server&reg; 2008 R2、Windows Server 2012、Windows 8、およびそれ以降のオペレーティング システムの機能が拡張されました。

> [!NOTE]
> Windows Server 2016 以外のオペレーティング システムで BranchCache を展開する場合は、次のドキュメント リソースを使用です。
> 
> - Windows 8、Windows 8.1、Windows Server 2012、および Windows Server 2012 R2 の BranchCache の詳細については、次を参照してください。[BranchCache の概要](https://technet.microsoft.com/en-us/library/hh831696.aspx)します。  
> - Windows 7 および Windows Server 2008 R2 の BranchCache の詳細については、次を参照してください。[Windows Server 2008 R2 の BranchCache](https://technet.microsoft.com/en-us/library/dd996634.aspx)します。  
  


