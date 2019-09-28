---
ms.assetid: c20231dd-2b83-4494-9385-1172272e00d6
title: 既存のドメインをアップグレードするか新しいドメインを展開するかを決定する
description: ''
author: MicrosoftGuyJFlo
ms.author: joflore
manager: mtillman
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server
ms.technology: identity-adds
ms.openlocfilehash: 0effdb3ae3ba6294e8a28f4f6b780f4d0c6a8582
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/27/2019
ms.locfileid: "71402613"
---
# <a name="determining-whether-to-upgrade-existing-domains-or-deploy-new-domains"></a>既存のドメインをアップグレードするか新しいドメインを展開するかを決定する

>適用先:Windows Server 2016 では、Windows Server 2012 R2、Windows Server 2012

設計内の各ドメインは、新しいドメインか、または既存のアップグレードされたドメインになります。 アップグレードしていない既存のドメインのユーザーは、新しいドメインに移動する必要があります。  
  
ドメイン間でアカウントを移動すると、エンドユーザーに影響が及ぶ可能性があります。 ユーザーを新しいドメインに移動するか、既存のドメインをアップグレードするかを決定する前に、新しい AD DS ドメインの長期的な管理上の利点を、ユーザーをドメインに移動するコストと比較して評価してください。  
  
Active Directory ドメインを Windows Server 2008 にアップグレードする方法の詳細については、「 [Active Directory ドメインを Windows server 2008 および Windows server 2008 R2 AD DS ドメインにアップグレードする](https://technet.microsoft.com/library/cc731188.aspx)」を参照してください。  
  
フォレスト内およびフォレスト間の AD DS ドメインの再構築の詳細については、「Active Directory 移行ツールバージョン3.1 移行ガイド ([https://go.microsoft.com/fwlink/?LinkId=93678](https://go.microsoft.com/fwlink/?LinkId=93678))」を参照してください。  
  
新規およびアップグレードされたドメインの計画を文書化するためのワークシートについては、Windows Server 2003 Deployment Kit ([https://go.microsoft.com/fwlink/?LinkID=102558](https://go.microsoft.com/fwlink/?LinkID=102558)) のジョブエイドから Job_Aids_Designing_and_Deploying_Directory_and_Security_Services をダウンロードして、"ドメイン" を開きます。"(DSSLOGI_5)" を計画します。  
  


