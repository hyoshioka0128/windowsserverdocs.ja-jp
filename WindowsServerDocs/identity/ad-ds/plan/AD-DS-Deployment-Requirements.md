---
ms.assetid: e02bb152-d0db-40b0-9942-846dce75f6c7
title: AD DS の展開の要件
description: ''
author: MicrosoftGuyJFlo
ms.author: joflore
manager: mtillman
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adds
ms.openlocfilehash: d21491f5ce9c15ecc514e4be24a91de28b0fd0ce
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/17/2019
ms.locfileid: "59890973"
---
# <a name="ad-ds-deployment-requirements"></a>AD DS の展開の要件

>適用先:Windows Server 2016 では、Windows Server 2012 R2、Windows Server 2012

既存の環境の構造は、Windows Server 2008 Active Directory Domain Services (AD DS) を展開するための戦略を決定します。 AD DS 環境を作成して既存のドメイン構造がない場合は、AD DS 環境の作成を開始する前に、AD DS の設計を完了します。 次に、新しいフォレスト ルート ドメインを展開し、設計に従ってドメインの構造の残りの部分を展開できます。  
  
また、AD DS の展開の一部として、アップグレードし、環境を再構成することがあります。 たとえば、組織に既存の Windows 2000 ドメイン構造がある場合は、一部のドメインのインプレース アップグレードを実行および他のユーザーを再構築可能性があります。 さらに、フォレスト間ドメインの再構築または AD DS を展開した後、フォレスト内のドメインの再構築のいずれかを環境の複雑さを軽減することがあります。  
  
## <a name="deploying-a-windows-server-2008-forest-root-domain"></a>Windows Server 2008 のフォレスト ルート ドメインを展開します。  
フォレスト ルート ドメインは、AD DS フォレストのインフラストラクチャの基盤を提供します。 AD DS の展開するには、まずフォレスト ルート ドメインを配置する必要があります。 これを行うには、AD DS の設計; を確認する必要があります。フォレスト ルート ドメインに対して DNS サービスを構成します。フォレスト ルート ドメイン コント ローラーを展開して、フォレスト ルート ドメインのサイト トポロジの構成、操作マスターの役割 (フレキシブル シングル マスター操作または FSMO とも呼ばれます); の構成で構成されるフォレスト ルート ドメインを作成します。フォレストおよびドメインの機能レベルを上げます。 次の図は、フォレスト ルート ドメインを展開するプロセス全体を示します。  
  
![AD DS 要件](media/AD-DS-Deployment-Requirements/033aad0b-25ff-4793-8825-88a6daa01a55.gif)  
  
詳細については、次を参照してください。 [Windows Server 2008 フォレスト ルート ドメインを展開する](https://technet.microsoft.com/library/cc731174.aspx)します。  
  
## <a name="deploying-windows-server-2008-regional-domains"></a>Windows Server 2008 地域ドメインの展開  
フォレスト ルート ドメインのデプロイが完了した後には、設計で指定されている新しい Windows Server 2008 地域ドメインをデプロイする準備が完了したら。 これを行うには、各地域ドメインのドメイン コント ローラーをデプロイする必要があります。 次の図は、地域ドメインの展開のプロセスを示します。  
  
![AD DS 要件](media/AD-DS-Deployment-Requirements/89a878c8-9a94-4180-ad43-ca75316a6318.gif)  
  
詳細については、次を参照してください。[を展開する Windows Server 2008 地域ドメイン](https://technet.microsoft.com/library/cc755118.aspx)します。  
  
## <a name="upgrading-active-directory-domains-to-windows-server-2008"></a>Active Directory ドメインを Windows Server 2008 にアップグレードします。  
Windows Server 2008 のドメインに、Windows 2000 または Windows Server 2003 ドメインをアップグレードするは、追加の Windows Server 2008 の機能と機能を活用するために、簡単で効率的な方法です。 現在ネットワークとドメインの構成、セキュリティ、スケーラビリティ、およびネットワーク インフラストラクチャの管理の容易性を向上させながらを維持するためにドメインをアップグレードすることができます。 Windows 2000 または Windows Server 2003 から Windows Server 2008 へのアップグレードには、最小限のネットワーク構成が必要です。 ユーザーの操作にほとんど影響がありますアップグレードします。 詳細については、次を参照してください。[を Windows Server 2008 および Windows Server 2008 R2 の AD DS ドメインの Active Directory ドメインのアップグレード](https://technet.microsoft.com/library/cc731188.aspx)します。  
  
## <a name="restructuring-ad-ds-domains"></a>AD DS ドメインの再構築  
Windows Server 2008 フォレスト (フォレスト間の再構成) 間のドメインを再構築するときに、環境内のドメインの数を減らすし、管理の複雑さとオーバーヘッドが削減します。 この一環として、フォレスト間でオブジェクトを移行すると、プロセスを再構築、ソース ドメインとターゲット ドメインの両方の環境が同時に存在します。 これにより、使用すると、ロールバック、ソース環境を移行中に必要な場合。  
  
Windows Server 2008 フォレスト (フォレスト内の再構成) 内の Windows Server 2008 のドメインを再構築するときに、ドメインの構造を統合し、管理の複雑さとオーバーヘッドが削減できます。 フォレスト内のドメインを再構築するときに、移行されたアカウントは、ソース ドメインに存在しません。  
  
Active Directory 移行ツール (ADMT) version 3.1 (ADMT v3.1) を使用して、ドメインの再構築する方法の詳細については、次を参照してください。 [ADMT v3.1 Guide の移行](https://go.microsoft.com/fwlink/?LinkId=93678)します。  
  


