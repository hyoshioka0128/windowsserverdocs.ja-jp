---
ms.assetid: 026747c7-4c34-41c7-b7ea-27f9a7f64a35
title: 企業 DNS にフェデレーション サーバーのホスト (A) リソース レコードを追加する
description: ''
author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adfs
ms.author: billmath
ms.openlocfilehash: 5767fa45f8b25680aa1b1d97ddab630923d10fae
ms.sourcegitcommit: 0b5fd4dc4148b92480db04e4dc22e139dcff8582
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/24/2019
ms.locfileid: "66192488"
---
# <a name="add-a-host-a-resource-record-to-corporate-dns-for-a-federation-server"></a>企業 DNS にフェデレーション サーバーのホスト (A) リソース レコードを追加する



Windows 統合認証では、ホストを使用してフェデレーション サーバーに正常にアクセスする、企業でのクライアントのネットワークに対する\(A\)リソース レコードは、企業のドメイン ネーム システム内で最初に作成する必要があります\(DNS\)アカウント フェデレーション サーバーのホスト名を解決する\(fs.fabrikam.com など\)フェデレーション サーバーまたはフェデレーション サーバー クラスターの IP アドレスにします。 次の手順を使用するには、ホストを追加する\(A\)をフェデレーション サーバーの会社の DNS リソース レコード。  
  
メンバーシップ **管理者**, 、または同等の権限は、この手順を実行するために必要な最小値。  適切なアカウントの使用方法の詳細を確認し、グループ メンバーシップ [ローカルおよびドメインの既定のグループ](https://go.microsoft.com/fwlink/?LinkId=83477)します。   
  
### <a name="to-add-a-host-a-resource-record-to-corporate-dns-for-a-federation-server"></a>ホストを追加する\(A\)をフェデレーション サーバーの会社の DNS リソース レコード  
  
1.  企業ネットワークの DNS サーバー、DNS スナップインを開きます\-でします。  
  
2.  コンソール ツリーで、右\-、適切な前方参照ゾーンをクリックし、クリックして**新しいホスト\(A または AAAA\)** します。  
  
3.  **名前**、コンピューター名であるフェデレーション サーバーまたはフェデレーション サーバー クラスターの; たとえば、完全修飾ドメイン名のみを入力\(FQDN\) fs.fabrikam.com、型**fs**.  
  
4.  **IP アドレス**、フェデレーション サーバーまたはフェデレーション サーバー クラスター、192.168.1.4 などの IP アドレスを入力します。  
  
5.  **[ホストの追加]** をクリックします。  
  
## <a name="additional-references"></a>その他の参照情報  
[チェックリスト:フェデレーション サーバーのセットアップ](Checklist--Setting-Up-a-Federation-Server.md)  
  
[フェデレーション サーバーの名前解決の要件](https://technet.microsoft.com/library/dd807055.aspx)  
  

