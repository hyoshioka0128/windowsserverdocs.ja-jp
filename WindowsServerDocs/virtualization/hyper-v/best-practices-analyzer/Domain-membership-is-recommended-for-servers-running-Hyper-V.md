---
title: HYPER-V を実行しているサーバーのドメインのメンバーシップをお勧め
description: このベスト プラクティス アナライザー ルールのテキストのオンライン バージョン。
ms.prod: windows-server-threshold
ms.service: na
manager: dongill
ms.technology: compute-hyper-v
ms.author: kathydav
ms.topic: article
ms.assetid: 2f4578e5-0848-46b4-a50b-7dbd480b80bf
author: KBDAzure
ms.date: 8/16/2016
ms.openlocfilehash: e9db1d28cfe1ae4afd6c5dc1a93253c83fc42113
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/17/2019
ms.locfileid: "59860903"
---
# <a name="domain-membership-is-recommended-for-servers-running-hyper-v"></a>HYPER-V を実行しているサーバーのドメインのメンバーシップをお勧め

>適用先:Windows Server 2016


  
*ベスト プラクティスとスキャンの詳細については、次を参照してください。* [Best Practices Analyzer](https://go.microsoft.com/fwlink/?LinkId=122786)します。  
  
|プロパティ|詳細|  
|-|-|  
|**オペレーティング システム**|Windows Server 2016|  
|**製品/機能**|Hyper-V|  
|**重要度**|警告|  
|**カテゴリ**|構成|  
  
次のセクションでは、斜体は、この問題のためのベスト プラクティス アナライザー ツールで表示される UI テキストを示します。  
  
## <a name="issue"></a>問題  
  
*このサーバーは、ワークグループのメンバーです。*  
  
## <a name="impact"></a>影響  
  
*このサーバーのサーバーの全体管理ではありません。*  
  
このコンピューターをドメインに参加させると、id や、セキュリティ、監査ポリシーによって一元管理できます。  
  
## <a name="resolution"></a>解決方法  
  
*使用可能なドメイン環境があれば、そのドメインにこのサーバーを参加させます。*  
  
> [!IMPORTANT]  
> このコンピューターをドメインに参加させるのセキュリティに影響があるかどうかを判断するには、このコンピューターに仮想マシンで実行されるワークロードを確認することをお勧めします。 仮想化ドメイン コント ローラー仮想マシンのいずれかの場合を参照してください。 [Planning Considerations for 仮想化ドメイン コント ローラー](https://go.microsoft.com/fwlink/?LinkId=190192) (https://go.microsoft.com/fwlink/?LinkId=190192)します。  
  
コンピューターをドメインに参加させるには、コンピューターとドメインのアクセス許可が必要です。   
- コンピューターの Administrators グループのメンバーであるユーザー アカウントを必要があります。 この種類のアカウントを使用してログオンまたは、求められたら、アカウントのユーザー名とパスワードを入力します。   
- ドメインにコンピューターをドメインに参加する権限がユーザー アカウントを必要があります。 ユーザー名とパスワードを求めるメッセージが表示されます。  
  
手順については、次を参照してください。[コンピューターをドメインに参加させる](https://go.microsoft.com/fwlink/?LinkId=190193)(https://go.microsoft.com/fwlink/?LinkId=190193)します。  
  


