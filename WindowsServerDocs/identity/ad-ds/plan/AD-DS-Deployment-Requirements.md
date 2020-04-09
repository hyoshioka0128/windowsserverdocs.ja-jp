---
ms.assetid: e02bb152-d0db-40b0-9942-846dce75f6c7
title: AD DS の展開の要件
author: MicrosoftGuyJFlo
ms.author: joflore
manager: mtillman
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server
ms.technology: identity-adds
ms.openlocfilehash: dff95633b71d42e25aad33793abd609ac61adbdf
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/08/2020
ms.locfileid: "80822925"
---
# <a name="ad-ds-deployment-requirements"></a>AD DS の展開の要件

>適用対象: Windows Server 2016、Windows Server 2012 R2、Windows Server 2012

既存の環境の構造によって、Windows Server 2008 Active Directory Domain Services (AD DS) を展開するための戦略が決まります。 AD DS 環境を作成していて、既存のドメイン構造がない場合は、AD DS 環境の作成を開始する前に AD DS の設計を完了してください。 次に、新しいフォレストルートドメインを展開し、設計に応じて残りのドメイン構造をデプロイできます。  
  
また、AD DS 展開の一部として、環境をアップグレードして再構築することもできます。 たとえば、組織が既存の Windows 2000 ドメイン構造を持っている場合、一部のドメインのインプレースアップグレードを実行し、他のドメインを再構築することがあります。 また、AD DS を展開した後で、フォレスト間でドメインを再構築するか、フォレスト内のドメインを再構築することで、環境の複雑さを軽減することもできます。  
  
## <a name="deploying-a-windows-server-2008-forest-root-domain"></a>Windows Server 2008 フォレストルートドメインの展開  
フォレストルートドメインによって、AD DS フォレストインフラストラクチャの基盤が提供されます。 AD DS を展開するには、最初にフォレストのルートドメインを展開する必要があります。 これを行うには、AD DS 設計を確認する必要があります。フォレストルートドメインの DNS サービスを構成します。フォレストルートドメインを作成します。これには、フォレストルートドメインコントローラーの展開、フォレストルートドメインのサイトトポロジの構成、および操作マスターの役割 (フレキシブルシングルマスター操作または FSMO とも呼ばれます) の構成が含まれます。およびは、フォレストおよびドメインの機能レベルを上げます。 次の図は、フォレストルートドメインを展開するプロセス全体を示しています。  
  
![AD DS 要件](media/AD-DS-Deployment-Requirements/033aad0b-25ff-4793-8825-88a6daa01a55.gif)  
  
詳細については、「 [Windows Server 2008 のフォレストルートドメインの展開](https://technet.microsoft.com/library/cc731174.aspx)」を参照してください。  
  
## <a name="deploying-windows-server-2008-regional-domains"></a>Windows Server 2008 の地域ドメインの展開  
フォレストルートドメインの展開が完了したら、設計によって指定された新しい Windows Server 2008 地域ドメインをデプロイする準備が整います。 これを行うには、各地域ドメインにドメインコントローラーを展開する必要があります。 次の図は、地域ドメインを展開するプロセスを示しています。  
  
![AD DS 要件](media/AD-DS-Deployment-Requirements/89a878c8-9a94-4180-ad43-ca75316a6318.gif)  
  
詳細については、「 [Windows Server 2008 の地域ドメインの展開](https://technet.microsoft.com/library/cc755118.aspx)」を参照してください。  
  
## <a name="upgrading-active-directory-domains-to-windows-server-2008"></a>Active Directory ドメインの Windows Server 2008 へのアップグレード  
Windows 2000 または Windows Server 2003 ドメインを Windows Server 2008 ドメインにアップグレードすることは、Windows Server 2008 の追加機能を利用するための効率的で簡単な方法です。 ドメインをアップグレードすることで、現在のネットワークとドメインの構成を維持しながら、ネットワークインフラストラクチャのセキュリティ、スケーラビリティ、および管理の容易さを向上させることができます。 Windows 2000 または Windows Server 2003 から Windows Server 2008 にアップグレードするには、最小限のネットワーク構成が必要です。 また、アップグレードはユーザーの操作にほとんど影響しません。 詳細については、「 [Windows server 2008 および Windows server 2008 R2 AD DS ドメインへの Active Directory ドメインのアップグレード](https://technet.microsoft.com/library/cc731188.aspx)」を参照してください。  
  
## <a name="restructuring-ad-ds-domains"></a>AD DS ドメインの再構築  
Windows Server 2008 フォレスト間でドメインを再構築すると (フォレストの再構築)、環境内のドメインの数を減らすことができるため、管理の複雑さとオーバーヘッドが軽減されます。 この再構築プロセスの一環として、フォレスト間でオブジェクトを移行する場合、ソースドメインとターゲットドメインの両方の環境が同時に存在します。 これにより、必要に応じて移行中にソース環境にロールバックすることができます。  
  
Windows server 2008 フォレスト (フォレスト内再構築) 内で Windows Server 2008 ドメインを再構築すると、ドメイン構造を統合できるため、管理の複雑さとオーバーヘッドが軽減されます。 フォレスト内のドメインを再構築すると、移行されたアカウントはソースドメインに存在しなくなります。  
  
Active Directory 移行ツール (ADMT) バージョン 3.1 (ADMT v1.0) を使用してドメインを再構築する方法の詳細については、「 [ADMT V1.0 移行ガイド](https://go.microsoft.com/fwlink/?LinkId=93678)」を参照してください。  
  


