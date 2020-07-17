---
title: Active Directory Domain Services の概要
description: Windows Server のセキュリティ
ms.prod: windows-server
ms.technology: security-auditing
ms.topic: article
ms.assetid: 6cfe9479-5d17-41d5-939a-891e5233fdca
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/12/2016
ms.openlocfilehash: 73272086b176fa8fb086063ff3d4249a02b016b2
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/08/2020
ms.locfileid: "80857025"
---
# <a name="active-directory-domain-services-overview"></a>Active Directory Domain Services の概要

>適用対象: Windows Server (半期チャネル)、Windows Server 2016
  
ディレクトリは、ネットワーク上のオブジェクトに関する情報を格納する階層構造です。 Active Directory Domain Services (AD DS) などのディレクトリサービスには、ディレクトリデータを格納し、そのデータをネットワークユーザーと管理者が使用できるようにするためのメソッドが用意されています。 たとえば、AD DS は、名前、パスワード、電話番号などのユーザーアカウントに関する情報を格納し、同じネットワーク上の他の承認されたユーザーがこの情報にアクセスできるようにします。  
  
Active Directory は、ネットワーク上のオブジェクトに関する情報を格納すると共に、管理者とユーザーがその情報を簡単に検索および利用できるようにします。 Active Directory は、構造化されたデータ ストアを、ディレクトリ情報の論理的で階層的な編成の基盤として使用します。  
  
このデータストアは、ディレクトリとも呼ばれ、Active Directory オブジェクトに関する情報を格納します。 これらのオブジェクトには、通常、サーバー、ボリューム、プリンターなどの共有リソース、およびネットワークユーザーとコンピューターアカウントが含まれます。 Active Directory データストアの詳細については、「[ディレクトリデータストア](https://technet.microsoft.com/library/cc736627(v=ws.10).aspx)」を参照してください。  
  
セキュリティは、ログオン認証およびディレクトリ内のオブジェクトに対するアクセス制御によって、Active Directory に統合されます。 管理者は、単一のネットワークログオンで、ネットワーク全体のディレクトリデータと組織を管理できます。また、承認されたネットワークユーザーは、ネットワーク上の任意の場所にあるリソースにアクセスできます。 ポリシー ベースの管理により、複雑なネットワークの管理を容易に行うことができます。 Active Directory セキュリティの詳細については、「セキュリティの概要」を参照してください。  
  
Active Directory には次のものも含まれます。  
* スキーマである一連の規則。**スキーマ**では、ディレクトリに格納されているオブジェクトと属性のクラス、これらのオブジェクトのインスタンスの制約と制限、および名前の形式を定義します。 スキーマの詳細については、「スキーマ」を参照してください。  
  
  
* ディレクトリ内のすべてのオブジェクトに関する情報を含む**グローバルカタログ**。 これにより、ユーザーと管理者は、ディレクトリ内のどのドメインにデータが実際に格納されているかに関係なく、ディレクトリ情報を検索できます。 グローバルカタログの詳細については、「グローバルカタログの役割」を参照してください。  
  
  
* **クエリとインデックスのメカニズム**。オブジェクトとそのプロパティを発行して、ネットワークユーザーやアプリケーションが検出することができます。 ディレクトリに対するクエリの詳細については、「ディレクトリ情報の検索」を参照してください。  
  
  
* ネットワーク経由でディレクトリデータを分散する**レプリケーションサービス**。 ドメイン内のすべてのドメインコントローラーは、レプリケーションに参加し、ドメインのすべてのディレクトリ情報の完全なコピーを格納します。 ディレクトリ データへの変更は、ドメイン内のすべてのドメイン コントローラーに対してレプリケートされます。 Active Directory レプリケーションの詳細については、「レプリケーションの概要」を参照してください。  
  
## <a name="understanding-active-directory"></a>Active Directory について  
 このセクションでは、コア Active Directory の概念へのリンクを示します。  
   
* [Active Directory 構造およびストレージテクノロジ](https://technet.microsoft.com/library/cc759186(v=ws.10).aspx)  
* [ドメインコントローラーの役割](https://technet.microsoft.com/library/cc786438(v=ws.10).aspx)   
* Active Directory Schema   
* [信頼とは](https://technet.microsoft.com/library/cc771294(v=ws.10).aspx)   
* [Active Directory レプリケーションテクノロジ](https://technet.microsoft.com/library/cc786438(v=ws.10).aspx)   
* [Active Directory 検索と発行のテクノロジ](https://technet.microsoft.com/library/cc775686(v=ws.10).aspx)   
* DNS とグループポリシーとの相互運用   
* [スキーマについて](https://technet.microsoft.com/library/cc759402(v=ws.10).aspx)   
  
Active Directory の概念の詳細な一覧については、「 [Active Directory につい](https://technet.microsoft.com/library/cc781408(v=ws.10).aspx)て」を参照してください。   

