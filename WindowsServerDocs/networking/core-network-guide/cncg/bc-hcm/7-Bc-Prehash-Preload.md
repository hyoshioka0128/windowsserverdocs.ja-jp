---
title: ホスト型キャッシュ サーバーでコンテンツの事前ハッシュと事前読み込みを行う (省略可能)
description: このガイドでは、Windows Server 2016 と Windows 10 を実行するコンピューターに、ホスト型キャッシュモードで BranchCache を展開する手順について説明します。
manager: brianlic
ms.prod: windows-server
ms.technology: networking-bc
ms.topic: article
ms.assetid: 7e79c66a-8555-4d8e-8691-d6c37377aab4
ms.author: lizross
author: eross-msft
ms.openlocfilehash: f47fbb5c10828d16a18b5cf486e620b3ace458c7
ms.sourcegitcommit: da7b9bce1eba369bcd156639276f6899714e279f
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/26/2020
ms.locfileid: "80318457"
---
# <a name="prehash-and-preload-content-on-the-hosted-cache-server-optional"></a>ホスト型キャッシュサーバー上でのコンテンツの事前ハッシュと事前読み込み \(オプション\)

>適用対象: Windows Server (半期チャネル)、Windows Server 2016、Windows Server 2012 R2、Windows Server 2012

このセクションの手順を使用して、コンテンツサーバーのコンテンツを事前にハッシュし、データパッケージにコンテンツを追加して、ホスト型キャッシュサーバーにコンテンツを事前に読み込むことができます。 

ホスト型キャッシュサーバーにコンテンツを事前にハッシュし、事前に読み込む必要がないため、これらの手順は省略できます。 

コンテンツを事前に読み込んでいない場合、データは WAN 接続を介してクライアントがダウンロードするときに、自動的にホスト型キャッシュに追加されます。

>[!IMPORTANT]
>これらの手順は総称して省略可能ですが、ホスト型キャッシュサーバーにコンテンツを事前にハッシュし、事前に読み込む場合は、両方の手順を実行する必要があります。

- [Web およびファイルコンテンツ&#40;のコンテンツサーバーデータパッケージを作成する (省略可能)&#41;](8-Bc-Data-Packages.md)
  
- [ホスト型キャッシュサーバー &#40;にデータパッケージをインポートする (オプション)&#41;](9-Bc-Import-Data.md)

このガイドを続行するには、「 [Web およびファイル&#40;コンテンツのコンテンツサーバーデータパッケージ&#41;を作成する (省略可能)](8-Bc-Data-Packages.md)」を参照してください。