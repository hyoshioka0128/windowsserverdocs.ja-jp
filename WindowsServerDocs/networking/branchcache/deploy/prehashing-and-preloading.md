---
title: (省略可能) ホスト型キャッシュ サーバー上の事前読み込みコンテンツの事前ハッシュと
description: このトピックでは、BranchCache 展開ガイドの Windows Server 2016、ブランチ オフィスに WAN 帯域幅の使用を最適化するために分散され、ホスト型キャッシュ モードで BranchCache を展開する方法を示しますの一部です。
manager: brianlic
ms.prod: windows-server-threshold
ms.technology: networking-bc
ms.topic: get-started-article
ms.assetid: 5a09d9f1-1049-447f-a9bf-74adf779af27
ms.author: pashort
author: shortpatti
ms.openlocfilehash: c3d1ed62c6dca5b1de0ff560fde0a2e43ed0d080
ms.sourcegitcommit: 19d9da87d87c9eefbca7a3443d2b1df486b0b010
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/28/2018
---
# <a name="prehashing-and-preloading-content-on-hosted-cache-servers-optional"></a>(省略可能) ホスト型キャッシュ サーバー上の事前読み込みコンテンツの事前ハッシュと

>適用対象: Windows Server (半期チャネル)、Windows Server 2016

この手順を使用すると、BranchCache が有効な Web サーバーとファイル サーバーでハッシュとも呼ばれます - コンテンツの情報の作成を強制します。 リモート ホスト型キャッシュ サーバーに転送できるパッケージにファイル サービスおよび Web サーバー上でデータを収集することもできます。  これにより、データを最初のクライアント アクセスに使用できるように、リモート ホスト型キャッシュ サーバー上のコンテンツをプリロードすること。  
  
メンバーである必要がある**管理者**、またはこの手順を実行することに相当します。  
  
### <a name="to-prehash-content-and-preload-the-content-on-hosted-cache-servers"></a>コンテンツのハッシュし、ホスト型キャッシュ サーバー上のコンテンツを事前読み込みするには  
  
1.  ファイルまたはプリロードするには、データを含む Web サーバーにログオンし、フォルダーと 1 つまたは複数のリモート ホスト型キャッシュ サーバーにロードするファイルを識別します。  
  
2.  Windows PowerShell を管理者として実行します。 各フォルダーおよびファイルのいずれかを実行、`Publish-BCFileContent`コマンドまたは`Publish-BCWebContent`ハッシュ生成を開始し、データをデータのパッケージに追加するコンテンツのサーバーの種類によっては、コマンドです。  
  
3.  すべてのデータをデータのパッケージに追加した後はエクスポートを使用して、`Export-BCCachePackage`データ パッケージ ファイルを生成するコマンドです。  
  
4.  ファイル転送テクノロジの選択を使用して、リモート ホスト型キャッシュ サーバーへのデータ パッケージ ファイルを移動します。  FTP、SMB、HTTP、DVD、およびポータブル ハード _ ディスクは、実行可能なすべてのトランスポートです。  
  
5.  使用してリモート ホスト型キャッシュ サーバー上のデータ パッケージ ファイルをインポート、`Import-BCCachePackage`コマンド。  
  

