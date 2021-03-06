---
title: Windows Server のコア ネットワーク ガイド
description: このトピックでは、計画およびネットワークが完全に機能と Windows Server 2016 で、新しいフォレスト内の新しい Active Directory ドメインに必要なコア コンポーネントを展開することができます、コア ネットワーク ガイドの概要を提供します。
manager: brianlic
ms.prod: windows-server-threshold
ms.technology: networking
ms.topic: article
ms.date: ''
ms.assetid: 9b3ef3eb-4246-4e0e-8bf1-53224ca5f2f9
ms.author: pashort
author: shortpatti
ms.openlocfilehash: a905fd0c11237edd3a408998f8f71aa25a054328
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/17/2019
ms.locfileid: "59847903"
---
# <a name="core-network-guidance-for-windows-server"></a>Windows Server のコア ネットワーク ガイド

>適用対象:Windows Server、Windows Server 2016

このトピックでは、Windows server コア ネットワーク ガイドの概要を示します&reg;2016 では、次のセクションが含まれています。  
  
-   [Windows Server のコア ネットワークの概要](#bkmk_intro)  
  
-   [Windows server コア ネットワーク ガイド](#bkmk_core)  
  
## <a name="bkmk_intro"></a>Windows Server のコア ネットワークの概要

コア ネットワークは、ネットワーク ハードウェア、デバイス、およびソフトウェアのコレクションであり、組織の情報テクノロジ (IT) ニーズに対応するための基盤サービスを提供します。

Windows Server コア ネットワークには、次のような機能を提供する多くのメリットがあります。

- コンピューターと他の伝送制御プロトコル/インターネット プロトコル (TCP/IP) 互換デバイスとの間のネットワーク接続のためのコア プロトコル。 TCP/IP は、コンピューターを接続してネットワークを構築するための標準プロトコル スイートです。 TCP/IP ネットワーク プロトコル ソフトウェアでマイクロソフトに提供されるは&reg;Windows&reg;プロトコル スイートを実装し、TCP/IP をサポートしているオペレーティング システム。

- 動的ホスト構成プロトコル (DHCP) サーバーの IP アドレスの自動割り当て。 ネットワーク上のすべてのコンピューターに手動で IP アドレスを構成する作業は、DHCP サーバーからリースされる IP アドレスを、コンピューターおよびその他のデバイスに動的に割り当てるように構成する作業に比べ、時間がかかり柔軟性にも欠けます。

- ドメイン ネーム システム (DNS) の名前解決サービス。 DNS を使用することで、コンピューターまたはデバイスの完全修飾ドメイン名を使用して、ユーザー、コンピューター、アプリケーション、およびサービスからネットワーク上のコンピューターとデバイスの IP アドレスを検索できます。

- フォレスト。1 つまたは複数の Active Directory ドメインです。同じクラスと属性の定義 (スキーマ)、サイトとレプリケーションの情報 (構成)、およびフォレスト全体の検索機能 (グローバル カタログ) を共有します。

- フォレスト ルート ドメイン。新しいフォレストに作成される最初のドメインです。 Enterprise Admins グループと Schema Admins グループは、フォレスト全体の管理グループであり、フォレスト ルート ドメインに配置されます。 さらに、他のドメインと同様に、フォレスト ルート ドメインは、コンピューター、ユーザー、およびグループの各オブジェクトのコレクションです。管理者が Active Directory ドメイン サービス (AD DS) に定義します。 これらのオブジェクトは、共通のディレクトリ データベースおよびセキュリティ ポリシーを共有します。 また、組織の拡大に合わせてドメインを追加した場合、他のドメインとのセキュリティ関係を共有することもできます。 ディレクトリ サービスにはディレクトリ データも保存され、承認されたコンピューター、アプリケーション、およびユーザーがそのデータにアクセスできるように設定できます。

- ユーザーおよびコンピューターのアカウント データベース。 ディレクトリ サービスには、一元管理のユーザー アカウント データベースが用意されています。このデータベースを使用して、アプリケーション、データベース、共有のファイルおよびフォルダー、プリンターなどのネットワーク リソースに対する接続を承認されたユーザーとコンピューターのために、ユーザー アカウントおよびコンピューター アカウントを作成できます。

また、コア ネットワークにより、組織の成長と IT 要件の変化に合わせてネットワークの規模を拡張できます。 たとえば、コア ネットワークと、ドメイン、IP サブネット、リモート アクセス サービス、ワイヤレス サービスなど、他の機能および Windows Server 2016 で提供されるサーバーの役割を追加できます。

## <a name="bkmk_core"></a>Windows server コア ネットワーク ガイド

Windows Server 2016 コア ネットワーク ガイドは計画およびネットワークが完全に機能し、新しい Active Directory に必要なコア コンポーネントを展開する方法について説明&reg;新しいフォレストのドメイン。 このガイドを使用して、次の Windows サーバー コンポーネントで構成されたコンピューターを展開できます。

- Active Directory Domain Services (AD DS) サーバー役割

- ドメイン ネーム システム (DNS) サーバー役割

- 動的ホスト構成プロトコル (DHCP) サーバー役割

- ネットワーク ポリシーとアクセス サービス サーバー役割のネットワーク ポリシー サーバー (NPS) 役割サービス

- Web サーバー (IIS) サーバーの役割

- 個々のサーバーでの伝送制御プロトコル/インターネット プロトコル バージョン 4 (TCP/IP) 接続

このガイドは、次の場所で使用できます。

- [コア ネットワーク ガイド](../core-network-guide/Core-Network-Guide.md)Windows Server 2016 テクニカル ライブラリ。
  


