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
ms.openlocfilehash: 425cfe794095f1515eb3fae2f1a5e5db90ba3d00
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/17/2019
ms.locfileid: "59856183"
---
# <a name="add-a-host-a-resource-record-to-corporate-dns-for-a-federation-server"></a>企業 DNS にフェデレーション サーバーのホスト (A) リソース レコードを追加する

>適用先:Windows Server 2016 では、Windows Server 2012 R2、Windows Server 2012


Windows 統合認証では、ホストを使用してフェデレーション サーバーに正常にアクセスする、企業でのクライアントのネットワークに対する\(A\)リソース レコードは、企業のドメイン ネーム システム内で最初に作成する必要があります\(DNS\)アカウント フェデレーション サーバーのホスト名を解決する\(fs.fabrikam.com など\)フェデレーション サーバーまたはフェデレーション サーバー クラスターの IP アドレスにします。 次の手順を使用するには、ホストを追加する\(A\)をフェデレーション サーバーの会社の DNS リソース レコード。  
  
メンバーシップ **管理者**, 、または同等の権限は、この手順を実行するために必要な最小値。  適切なアカウントの使用方法の詳細を確認し、グループ メンバーシップ [ローカルおよびドメインの既定のグループ](https://go.microsoft.com/fwlink/?LinkId=83477)します。   
  
### <a name="to-add-a-host-a-resource-record-to-corporate-dns-for-a-federation-server"></a>ホストを追加する\(A\)をフェデレーション サーバーの会社の DNS リソース レコード  
  
1.  企業ネットワークの DNS サーバー、DNS スナップインを開きます\-でします。  
  
2.  コンソール ツリーで、右\-、適切な前方参照ゾーンをクリックし、クリックして**新しいホスト\(A または AAAA\)** します。  
  
3.  **名前**、コンピューター名であるフェデレーション サーバーまたはフェデレーション サーバー クラスターの; たとえば、完全修飾ドメイン名のみを入力\(FQDN\) fs.fabrikam.com、型**fs**.  
  
4.  **IP アドレス**、フェデレーション サーバーまたはフェデレーション サーバー クラスター、192.168.1.4 などの IP アドレスを入力します。  
  
5.  **[ホストの追加]** をクリックします。  
  
## <a name="additional-references"></a>その他の参照情報  
[チェックリスト:フェデレーション サーバーを設定します。](Checklist--Setting-Up-a-Federation-Server.md)  
  
[フェデレーション サーバーの名前解決の要件](https://technet.microsoft.com/library/dd807055.aspx)  
  

