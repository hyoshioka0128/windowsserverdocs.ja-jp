---
ms.assetid: e02bb152-d0db-40b0-9942-846dce75f6c7
title: "AD DS の展開要件"
description: 
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adds
ms.openlocfilehash: 7edd7de8077a077245416f859838a6bc55415edc
ms.sourcegitcommit: db290fa07e9d50686667bfba3969e20377548504
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/12/2017
---
# <a name="ad-ds-deployment-requirements"></a>AD DS の展開要件

>適用対象: Windows Server 2016、Windows Server 2012 R2、Windows Server 2012

既存の環境の構造体では、Windows Server 2008 Active Directory ドメイン サービス (AD DS) を展開するための戦略を決定します。 AD DS 環境を作成して、既存のドメイン構造がない場合は、AD DS 環境の作成を開始する前に、AD DS の設計を完了します。 次に、新しいフォレスト ルート ドメインを展開し、設計に従って、ドメイン構造の残りの部分を展開します。  
  
また、AD DS の展開の一部をアップグレードし、環境を再構成することができます。 など、組織に既存の Windows 2000 ドメイン構造がある場合は、いくつかのドメインのインプレース アップグレードを実行および他のユーザーを再構成する可能性があります。 さらに、フォレスト間でドメインの再構築またはフォレスト内のドメインを再構築する AD DS を展開した後で、環境の複雑さを軽減することができます。  
  
## <a name="deploying-a-windows-server-2008-forest-root-domain"></a>Windows Server 2008 のフォレスト ルート ドメインを展開します。  
フォレスト ルート ドメインは、AD DS フォレストのインフラストラクチャの基盤を提供します。 AD DS を展開するには、最初にフォレスト ルート ドメインを展開する必要があります。 これを行うには、AD DS の設計を確認する必要があります。フォレスト ルート ドメインの DNS サービスを構成します。フォレスト ルート ドメイン コント ローラーを展開して、フォレスト ルート ドメインのサイト トポロジの構成、操作マスターの役割 (フレキシブル シングル マスター操作または FSMO とも呼ばれます); の構成から成る、フォレスト ルート ドメインを作成します。フォレストとドメインの機能レベルを上げます。 次の図は、フォレスト ルート ドメインを展開する全体的なプロセスを示します。  
  
![AD DS の要件](media/AD-DS-Deployment-Requirements/033aad0b-25ff-4793-8825-88a6daa01a55.gif)  
  
詳細については、次を参照してください。 [Windows Server 2008 フォレスト ルート ドメインを展開する](https://technet.microsoft.com/library/cc731174.aspx)します。  
  
## <a name="deploying-windows-server-2008-regional-domains"></a>Windows Server 2008 地域ドメインの展開  
フォレスト ルート ドメインの展開を完了した後には、新しい Windows Server 2008 地域ドメインの展開の設計で指定されている準備ができたらします。 これを行うには、各地域ドメインのドメイン コント ローラーを展開する必要があります。 次の図では、地域ドメインの展開のプロセスを示します。  
  
![AD DS の要件](media/AD-DS-Deployment-Requirements/89a878c8-9a94-4180-ad43-ca75316a6318.gif)  
  
詳細については、次を参照してください。[を展開する Windows Server 2008 地域ドメイン](https://technet.microsoft.com/library/cc755118.aspx)します。  
  
## <a name="upgrading-active-directory-domains-to-windows-server-2008"></a>Windows Server 2008 への Active Directory ドメインのアップグレード  
ドメインをアップグレードする、Windows 2000 または Windows Server 2003 を Windows Server 2008 のドメインには、Windows Server 2008 の追加の機能と機能を活用する簡単な効率的な方法です。 現在ネットワークとドメインの構成中に、セキュリティ、スケーラビリティ、およびネットワーク インフラストラクチャの管理容易性の向上を維持するためにドメインをアップグレードすることができます。 Windows 2000 または Windows Server 2003 から Windows Server 2008 にアップグレードするには、最小限のネットワーク構成が必要です。 ユーザーの操作で、ほとんど影響のアップグレードもありません。 詳細については、次を参照してください。[を Windows Server 2008 および Windows Server 2008 R2 の AD DS ドメインの Active Directory ドメインのアップグレード](https://technet.microsoft.com/library/cc731188.aspx)します。  
  
## <a name="restructuring-ad-ds-domains"></a>AD DS ドメインの再構築  
Windows Server 2008 フォレスト (フォレスト間の再構築) 間のドメインを再構築するときに環境内でドメインの数を削減し、したがって管理の複雑さとオーバーヘッドを削減できます。 この作業の一環として、フォレスト間でオブジェクトを移行すると、再構築するプロセス、ソース ドメインとターゲット ドメインの両方の環境が同時に存在します。 これにより、ロールバックする、ソース環境を移行中に必要な場合ことが可能。  
  
Windows Server 2008 フォレスト (フォレスト内の再構成) 内の Windows Server 2008 ドメインを再構築するときに、ドメイン構造を統合し、したがって管理の複雑さとオーバーヘッドを削減できます。 フォレスト内のドメインを再構築するときに、移行されたアカウントは、ソース ドメインに存在しません。  
  
詳細については、Active Directory 移行ツール (ADMT) バージョン 3.1 (ADMT v3.1) を使用して、ドメインの再構築する方法について、次を参照してください。 [ADMT v3.1 Guide の移行](https://go.microsoft.com/fwlink/?LinkId=93678)します。  
  


