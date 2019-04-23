---
title: アプリケーションの考慮事項
description: MultiPoint Services でのアプリの互換性情報
ms.custom: na
ms.prod: windows-server-threshold
ms.technology: multipoint-services
ms.reviewer: na
ms.suite: na
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 445e6184-4e1e-4f10-ad3c-042f2a6c2f5f
author: evaseydl
manager: scottman
ms.author: evas
ms.date: 08/04/2016
ms.openlocfilehash: 400f87c09f1b2e897d67f94e9b7ac12ae0a1e799
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/17/2019
ms.locfileid: "59839833"
---
# <a name="application-considerations"></a>アプリケーションの考慮事項
  
## <a name="application-compatibility"></a>アプリケーションの互換性

MultiPoint Services システムで実行する任意のアプリケーションでは、次の要件を満たす必要があります。
  
- インストールおよび Windows Server 2016 上で実行する必要があります。 
- セッション対応になる各ユーザーが MultiPoint システムで、アプリのインスタンスを実行するために必要です。
  
アプリケーションはこの要件を指定する場合は、アプリケーションをインストールするリモート デスクトップ セッションでの使用をお勧めします。 

## <a name="addressing-application-compatibility-problems"></a>アプリケーションの互換性の問題に対処  
MultiPoint Services ステーションを同じホスト コンピューターで仮想的に実行する Windows 10 Enterprise エディションの完全なインスタンスに関連付けるオプションを提供します。 重要なアプリケーションは、複数のユーザーに対して複数のインスタンスは実行されませんまたは 64 ビットのオペレーティング システムではインストールされませんでは、これは、ソリューションを指定できます。 この方法でデスクトップを展開するには、する MultiPoint マネージャーで仮想デスクトップ タブを使用する必要があります。  
  
-   仮想デスクトップを有効にします。  
-   デスクトップ テンプレートを作成します。  
-   問題のあるアプリケーションでテンプレートをカスタマイズします。  
-   カスタマイズされたテンプレートを使用してステーションを関連付け  

各ステーションは、すべての変更は、コンピューターが起動するたびに消去するため、同じテンプレートから開始します。  
  
>[!NOTE] 
>MultiPoint で実行するアプリケーションのライセンス要件を確認するのには重要です。 インストールするユーザーごとのライセンス コピーを 1 つのアプリケーションが必要があります。  
  
