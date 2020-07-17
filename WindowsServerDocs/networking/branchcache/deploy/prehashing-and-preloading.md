---
title: ホストされたキャッシュ サーバー上でのコンテンツの事前ハッシュおよび事前読み込み (省略可能)
description: このトピックは、Windows Server 2016 用の BranchCache 展開ガイドに含まれています。これは、ブランチオフィスでの WAN 帯域幅の使用を最適化するために、分散キャッシュモードとホスト型キャッシュモードで BranchCache を展開する方法を示しています。
manager: brianlic
ms.prod: windows-server
ms.technology: networking-bc
ms.topic: get-started-article
ms.assetid: 5a09d9f1-1049-447f-a9bf-74adf779af27
ms.author: lizross
author: eross-msft
ms.openlocfilehash: 7fe43b3a7c8dc7906e678a219b67ed096aa951d4
ms.sourcegitcommit: da7b9bce1eba369bcd156639276f6899714e279f
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/26/2020
ms.locfileid: "80319125"
---
# <a name="prehashing-and-preloading-content-on-hosted-cache-servers-optional"></a>ホストされたキャッシュ サーバー上でのコンテンツの事前ハッシュおよび事前読み込み (省略可能)

>適用対象: Windows Server (半期チャネル)、Windows Server 2016

この手順を使用すると、BranchCache が有効な Web サービスとファイル サーバー上でのハッシュとも呼ばれます - コンテンツの情報の作成を強制します。 リモート ホスト型キャッシュ サーバーに転送できます。 パッケージにファイルと web サーバーでデータを収集することもできます。  これにより、データを最初のクライアント アクセスに使用できるように、リモート ホスト型キャッシュ サーバー上のコンテンツをプリロードすることです。  
  
メンバーである必要があります **管理者**, 、またはこの手順を実行に相当します。  
  
### <a name="to-prehash-content-and-preload-the-content-on-hosted-cache-servers"></a>コンテンツを prehash し、ホスト型キャッシュ サーバー上のコンテンツをプリロードするには  
  
1.  ファイルまたはプリロードするデータを含む Web サーバーにログオンし、フォルダーと 1 つまたは複数のリモート ホスト型キャッシュ サーバーでのロード先のファイルを識別します。  
  
2.  Windows PowerShell を管理者として実行します。 フォルダーおよびファイルごとのいずれかを実行、 `Publish-BCFileContent` コマンドまたは `Publish-BCWebContent` ハッシュ生成を開始して、データをデータのパッケージに追加するコンテンツのサーバーの種類によっては、コマンドです。  
  
3.  すべてのデータがデータのパッケージに追加した後はエクスポートを使用して、 `Export-BCCachePackage` データ パッケージ ファイルを生成するコマンドです。  
  
4.  ファイル転送テクノロジの選択を使用して、リモート ホスト型キャッシュ サーバーにデータのパッケージ ファイルを移動します。  FTP、SMB、HTTP、DVD、およびポータブル ハード_ディスクは、実行可能なすべてのトランスポートです。  
  
5.  使用してリモートのホスト型キャッシュ サーバー上のデータ パッケージ ファイルをインポート、 `Import-BCCachePackage` コマンドです。  
  

