---
title: Active Directory Domain Services の概要
description: Windows Server のセキュリティ
ms.topic: article
ms.assetid: 6cfe9479-5d17-41d5-939a-891e5233fdca
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/12/2016
ms.openlocfilehash: 87f8aefb2645fa13ba1c9ac98e7970fc908e7bed
ms.sourcegitcommit: 68444968565667f86ee0586ed4c43da4ab24aaed
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/07/2020
ms.locfileid: "87997054"
---
# <a name="overview-of-active-directory-domain-services"></a>Active Directory Domain Services の概要

>適用先:Windows Server (半期チャネル)、Windows Server 2016

ディレクトリは、ネットワーク上のオブジェクトに関する情報を格納する階層構造です。 Active Directory Domain Services (AD DS) などのディレクトリサービスには、ディレクトリデータを格納し、そのデータをネットワークユーザーと管理者が使用できるようにするためのメソッドが用意されています。 たとえば、AD DS は、名前、パスワード、電話番号などのユーザーアカウントに関する情報を格納し、同じネットワーク上の他の承認されたユーザーがこの情報にアクセスできるようにします。

Active Directory は、ネットワーク上のオブジェクトに関する情報を格納すると共に、管理者とユーザーがその情報を簡単に検索および利用できるようにします。 Active Directory は、構造化されたデータ ストアを、ディレクトリ情報の論理的で階層的な編成の基盤として使用します。

このデータストアは、ディレクトリとも呼ばれ、Active Directory オブジェクトに関する情報を格納します。 これらのオブジェクトには、通常、サーバー、ボリューム、プリンターなどの共有リソース、およびネットワークユーザーとコンピューターアカウントが含まれます。 Active Directory データストアの詳細については、「[ディレクトリデータストア](/previous-versions/windows/it-pro/windows-server-2003/cc736627(v=ws.10))」を参照してください。

セキュリティは、ログオン認証およびディレクトリ内のオブジェクトに対するアクセス制御によって、Active Directory に統合されます。 管理者は、シングル ネットワーク ログオンで、ネットワーク全体のディレクトリ データおよび組織を管理できます。また、承認されたネットワーク ユーザーは、ネットワーク上の任意の場所にあるリソースにアクセスできます。 ポリシー ベースの管理により、複雑なネットワークの管理を容易に行うことができます。 Active Directory セキュリティの詳細については、「セキュリティの概要」を参照してください。

Active Directory には次のものも含まれます。
* スキーマである一連の規則。**スキーマ**では、ディレクトリに格納されているオブジェクトと属性のクラス、これらのオブジェクトのインスタンスの制約と制限、および名前の形式を定義します。 スキーマの詳細については、「スキーマ」を参照してください。


* ディレクトリ内のすべてのオブジェクトに関する情報を含む**グローバルカタログ**。 これにより、ユーザーと管理者は、ディレクトリ内のどのドメインにデータが実際に格納されているかに関係なく、ディレクトリ情報を検索できます。 グローバルカタログの詳細については、「グローバルカタログの役割」を参照してください。


* **クエリとインデックスのメカニズム**。オブジェクトとそのプロパティを発行して、ネットワークユーザーやアプリケーションが検出することができます。 ディレクトリに対するクエリの詳細については、「ディレクトリ情報の検索」を参照してください。


* ネットワーク経由でディレクトリデータを分散する**レプリケーションサービス**。 ドメイン内のすべてのドメインコントローラーは、レプリケーションに参加し、ドメインのすべてのディレクトリ情報の完全なコピーを格納します。 ディレクトリ データへの変更は、ドメイン内のすべてのドメイン コントローラーに対してレプリケートされます。 Active Directory レプリケーションの詳細については、「レプリケーションの概要」を参照してください。

## <a name="understanding-active-directory"></a>Active Directory について
 このセクションでは、コア Active Directory の概念へのリンクを示します。

* [Active Directory 構造およびストレージテクノロジ](/previous-versions/windows/it-pro/windows-server-2003/cc759186(v=ws.10))
* [ドメインコントローラーの役割](/previous-versions/windows/it-pro/windows-server-2003/cc786438(v=ws.10))
* Active Directory スキーマ
* [信頼とは](/previous-versions/windows/it-pro/windows-server-2008-R2-and-2008/cc771294(v=ws.10))
* [Active Directory レプリケーションテクノロジ](/previous-versions/windows/it-pro/windows-server-2003/cc786438(v=ws.10))
* [Active Directory 検索と発行のテクノロジ](/previous-versions/windows/it-pro/windows-server-2003/cc775686(v=ws.10))
* DNS とグループポリシーとの相互運用
* [スキーマについて](/previous-versions/windows/it-pro/windows-server-2003/cc759402(v=ws.10))

Active Directory の概念の詳細な一覧については、「 [Active Directory につい](/previous-versions/windows/it-pro/windows-server-2003/cc781408(v=ws.10))て」を参照してください。