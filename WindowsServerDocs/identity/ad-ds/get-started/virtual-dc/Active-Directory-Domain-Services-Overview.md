---
ms.assetid: f052dfcd-dace-4485-8d0a-cc7df5cf3751
title: Active Directory Domain Services の概要
description: ''
author: MicrosoftGuyJFlo
ms.author: joflore
manager: mtillman
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adds
ms.openlocfilehash: ed8a22881cd20633e6fcd61b146f3b0aad7a757b
ms.sourcegitcommit: be243a92f09048ca80f85d71555ea6ee3751d712
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/11/2019
ms.locfileid: "67792281"
---
# <a name="active-directory-domain-services-overview"></a>Active Directory Domain Services の概要

>適用先:Windows Server 2016 では、Windows Server 2012 R2、Windows Server 2012


ディレクトリは、ネットワーク上のオブジェクトに関する情報を格納する階層構造です。 Active Directory Domain Services (AD DS) などのディレクトリ サービスは、ディレクトリ データを格納すると、ネットワーク ユーザーおよび管理者にこのデータを使用できるようにするメソッドを提供します。 たとえば、AD DS では、名、パスワード、電話番号、およびなどのユーザー アカウントに関する情報が格納され、により、この情報にアクセスする権限のある他のユーザーを同じネットワーク上。

Active Directory では、ネットワーク上のオブジェクトに関する情報を格納し、この情報を検索して使用するには、管理者とユーザーの簡単します。 Active Directory では、ディレクトリ情報の論理的かつ階層組織の基準として構造化データ ストアを使用します。

ディレクトリとも呼ばれる、このデータ ストアには、Active Directory オブジェクトに関する情報が含まれています。 通常、これらのオブジェクトには、サーバー、ボリューム、プリンター、およびネットワークのユーザーおよびコンピューター アカウントなどの共有リソースが含まれます。 Active Directory データ ストアの詳細については、次を参照してください。 [Directory データ ストア](https://technet.microsoft.com/library/cc736627(v=ws.10).aspx)します。

セキュリティは、ログオン認証およびディレクトリ内のオブジェクトへのアクセス制御によって、Active Directory と統合されます。 シングル ネットワーク ログオン管理者は、ディレクトリのデータと組織、ネットワーク全体を管理でき、承認済みネットワーク ユーザーがネットワーク上の任意のリソースにアクセスできます。 ポリシー ベースの管理により、複雑なネットワークの管理を容易に行うことができます。 Active Directory のセキュリティの詳細については、次を参照してください。[セキュリティの概要](../../plan/security-best-practices/best-practices-for-securing-active-directory.md)します。

Active Directory が含まれています。
* ルールのセットを**スキーマ**オブジェクトのクラスを定義して、属性に含まれる、ディレクトリ、制約、およびこれらのオブジェクトのインスタンスと名前の形式に制限します。 スキーマの詳細については、スキーマを参照してください。


* A**グローバル カタログ**ディレクトリ内のすべてのオブジェクトに関する情報を格納します。 これにより、ユーザーと管理者情報を検索するディレクトリに関係なく、ディレクトリ内のどのドメイン データを実際に格納できます。 グローバル カタログの詳細については、グローバル カタログの役割を参照してください。


* A**クエリとインデックス機能**いるため、オブジェクトとそのプロパティを公開してネットワークのユーザーまたはアプリケーションが見つかりました。 ディレクトリのクエリの詳細については、ディレクトリ情報を検索するを参照してください。


* A**レプリケーション サービス**をネットワーク経由でディレクトリ データを分散します。 ドメイン内のすべてのドメイン コント ローラーは、レプリケーションに参加し、そのドメインのすべてのディレクトリ情報の完全なコピーを含みます。 ディレクトリ データへの変更は、ドメイン内のすべてのドメイン コントローラーに対してレプリケートされます。 Active Directory レプリケーションの詳細については、レプリケーションの概要を参照してください。

## <a name="understanding-active-directory"></a>Active Directory を理解します。
 ここでは、Active Directory の中心概念へのリンクを示します。
 
* [Active Directory 構造と記憶域テクノロジ](https://technet.microsoft.com/library/cc759186(v=ws.10).aspx)
* [ドメイン コント ローラーの役割](https://technet.microsoft.com/library/cc786438(v=ws.10).aspx) 
* [Active Directory スキーマ](https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2008-R2-and-2008/cc771796(v=ws.10))
* [信頼とは](https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2008-R2-and-2008/cc771568(v=ws.10)) 
* [Active Directory のレプリケーション テクノロジ](https://technet.microsoft.com/library/cc786438(v=ws.10).aspx) 
* [Active Directory の検索とパブリケーションのテクノロジ](https://technet.microsoft.com/library/cc775686(v=ws.10).aspx) 
* [DNS とグループ ポリシーとの相互運用](https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2008-R2-and-2008/dd197486(v=ws.10))
* [スキーマとは](https://technet.microsoft.com/library/cc759402(v=ws.10).aspx) 

Active Directory の概念の詳細な一覧についてを参照してください。 [Understanding Active Directory](https://technet.microsoft.com/library/cc781408(v=ws.10).aspx)します。 


