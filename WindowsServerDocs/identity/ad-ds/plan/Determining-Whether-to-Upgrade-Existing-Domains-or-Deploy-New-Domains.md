---
ms.assetid: c20231dd-2b83-4494-9385-1172272e00d6
title: 既存のドメインをアップグレードするか新しいドメインを展開するかを決定する
author: MicrosoftGuyJFlo
ms.author: joflore
manager: mtillman
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server
ms.technology: identity-adds
ms.openlocfilehash: 1e058240bc971d949de279407701e57cd021712c
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/08/2020
ms.locfileid: "80822602"
---
# <a name="determining-whether-to-upgrade-existing-domains-or-deploy-new-domains"></a>既存のドメインをアップグレードするか新しいドメインを展開するかを決定する

>適用対象: Windows Server 2016、Windows Server 2012 R2、Windows Server 2012

設計内の各ドメインは、新しいドメインか、または既存のアップグレードされたドメインになります。 アップグレードしていない既存のドメインのユーザーは、新しいドメインに移動する必要があります。  
  
ドメイン間でアカウントを移動すると、エンドユーザーに影響が及ぶ可能性があります。 ユーザーを新しいドメインに移動するか、既存のドメインをアップグレードするかを決定する前に、新しい AD DS ドメインの長期的な管理上の利点を、ユーザーをドメインに移動するコストと比較して評価してください。  
  
Active Directory ドメインを Windows Server 2008 にアップグレードする方法の詳細については、「 [Active Directory ドメインを Windows server 2008 および Windows server 2008 R2 AD DS ドメインにアップグレードする](https://technet.microsoft.com/library/cc731188.aspx)」を参照してください。  
  
フォレスト内およびフォレスト間の AD DS ドメインの再構築の詳細については、「Active Directory 移行ツールバージョン3.1 移行ガイド ([https://go.microsoft.com/fwlink/?LinkId=93678](https://go.microsoft.com/fwlink/?LinkId=93678))」を参照してください。  
  
新規およびアップグレードされたドメインの計画を作成する際に役立つワークシートについては、Windows Server 2003 Deployment Kit のジョブエイド ([https://go.microsoft.com/fwlink/?LinkID=102558](https://go.microsoft.com/fwlink/?LinkID=102558)) から Job_Aids_Designing_and_Deploying_Directory_and_Security_Services をダウンロードし、「ドメインの計画」 (DSSLOGI_5 .doc) を開いてください。  
  


