---
title: "Active Directory ドメイン サービスの概要"
description: "Windows Server のセキュリティ"
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.service: na
ms.suite: na
ms.technology: security-auditing
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 6cfe9479-5d17-41d5-939a-891e5233fdca
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/12/2016
ms.openlocfilehash: 3d0e849edbff3a481ffd28f83d7f14089030920d
ms.sourcegitcommit: 583355400f6b0d880dc0ac6bc06f0efb50d674f7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/17/2017
---
# <a name="active-directory-domain-services-overview"></a>Active Directory ドメイン サービスの概要

>適用対象: Windows Server (半期チャネル)、Windows Server 2016
  
ディレクトリは、ネットワーク上のオブジェクトに関する情報を格納する階層構造です。 Active Directory ドメイン サービス (AD DS) などのディレクトリ サービスでは、ディレクトリ データを格納すると、ネットワーク ユーザーと管理者がこのデータを使用できるメソッドを提供します。 たとえば、AD DS 名、パスワード、電話番号、およびなどのユーザー アカウントに関する情報を格納でき、この情報にアクセスする権限のある他のユーザーを同じネットワーク上です。  
  
Active Directory はネットワーク上のオブジェクトについての情報を格納し、この情報を検索して使用するには、管理者とユーザーを容易に行います。 Active Directory ディレクトリ情報の組織の論理的な階層的な基準として、構造化されたデータ ストアを使用します。  
  
このデータ ストア、ディレクトリとも呼ばれるには、Active Directory オブジェクトに関する情報が含まれています。 通常、これらのオブジェクトには、サーバー、ボリューム、プリンター、およびネットワークのユーザーおよびコンピューター アカウントなどの共有リソースが含まれます。 Active Directory データ ストアの詳細については、次を参照してください。[ディレクトリ データ ストア](https://technet.microsoft.com/library/cc736627(v=ws.10).aspx)します。  
  
セキュリティは、ログオン認証およびディレクトリ内のオブジェクトへのアクセス制御によって Active Directory と統合されています。 単一のネットワーク ログオンでは、管理者は、ネットワーク全体の組織のディレクトリ データおよび管理でき、承認済みネットワーク ユーザーがネットワーク上の任意のリソースにアクセスできます。 ポリシー ベースの管理には、複雑なネットワークの管理が容易になります。 Active Directory のセキュリティの詳細については、セキュリティの概要を参照してください。  
  
Active Directory も含まれています。  
* 一連の規則を**スキーマ**オブジェクトのクラスを定義してに含まれている属性、ディレクトリ、制約、およびこれらのオブジェクトのインスタンスと名の形式に制限します。 スキーマの詳細については、スキーマを参照してください。  
  
  
* A**グローバル カタログ**ディレクトリ内のすべてのオブジェクトに関する情報が含まれる。 これにより、ユーザーと情報を検索するディレクトリに関係なく、ディレクトリ内のどのドメイン データを含む実際には管理者です。 グローバル カタログの詳細については、グローバル カタログの役割を参照してください。  
  
  
* A**クエリとインデックス機能**、オブジェクトとそのプロパティを公開およびネットワークのユーザーまたはアプリケーションが検出されるようにします。 ディレクトリのクエリの詳細については、「ディレクトリ情報を検索」を参照してください。  
  
  
* A**レプリケーション サービス**ディレクトリ データをネットワーク経由で配布します。 ドメイン内のすべてのドメイン コント ローラーは、レプリケーションに参加し、そのドメインのすべてのディレクトリ情報の完全なコピーが含まれています。 ディレクトリ データへの変更は、ドメイン内のすべてのドメイン コント ローラーにレプリケートされます。 Active Directory レプリケーションの詳細については、レプリケーションの概要を参照してください。  
  
## <a name="understanding-active-directory"></a>Active Directory を理解します。  
 ここでは、Active Directory の主要な概念へのリンクを示します。  
   
* [Active Directory 構造と記憶域テクノロジ](https://technet.microsoft.com/library/cc759186(v=ws.10).aspx)  
* [ドメイン コント ローラーの役割](https://technet.microsoft.com/library/cc786438(v=ws.10).aspx)   
* Active Directory スキーマ   
* [信頼とは](https://technet.microsoft.com/library/cc771294(v=ws.10).aspx)   
* [Active Directory のレプリケーション テクノロジ](https://technet.microsoft.com/library/cc786438(v=ws.10).aspx)   
* [Active Directory の検索とパブリケーション テクノロジ](https://technet.microsoft.com/library/cc775686(v=ws.10).aspx)   
* DNS とグループ ポリシーとの相互運用   
* [スキーマとは](https://technet.microsoft.com/library/cc759402(v=ws.10).aspx)   
  
Active Directory の概念の詳細な一覧についてを参照してください。[について Active Directory](https://technet.microsoft.com/library/cc781408(v=ws.10).aspx)します。   

