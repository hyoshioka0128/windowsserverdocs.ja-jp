---
title: ユーザー アカウントに関する考慮事項
description: ユーザー アカウント、ユーザー名、および MultiPoint サービスのパスワードに関する考慮事項を提供します。
ms.custom: na
ms.prod: windows-server-threshold
ms.technology: multipoint-services
ms.reviewer: na
ms.suite: na
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: e225900b-cee9-48c9-b21c-394dc5e72b78
author: lizap
manager: dongill
ms.author: elizapo
ms.date: 08/04/2016
ms.openlocfilehash: 00fb5e83921ba0b8ad86a6f75bdfd7bf16419b73
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/17/2019
ms.locfileid: "59850793"
---
# <a name="user-account-considerations"></a>ユーザー アカウントに関する考慮事項
このトピックでは、管理ユーザーとして考慮すべき作成し、ユーザー アカウントを管理する際の問題について説明します。 MultiPoint マネージャーの [Users] タブ内のユーザー アカウントを管理します。 詳細については、「[ユーザー アカウントの管理](Manage-User-Accounts.md)」トピックを参照してください。  
  
## <a name="user-account-types"></a>ユーザー アカウントの種類  
ユーザー アカウントは、ユーザーがアクセスできるファイルとフォルダー、ユーザーが MultiPoint Services システムに行える変更、各ユーザーの優先設定 (デスクトップの背景など) を MultiPoint Services に伝える情報の集まりです。 各ユーザーが一意のユーザー名とパスワードを使用して自分のユーザー アカウントにアクセスします。 MultiPoint サービスには、次の 3 つの種類のユーザー アカウントがサポートされています。  
  
-   **管理者のユーザー アカウント** は MultiPoint マネージャーを使用してを使用して、MultiPoint サービス システムを管理する個人用です。 詳細については、「[管理ユーザー アカウントの作成](Create-an-Administrative-User-Account.md)」を参照してください。  
  
-   **標準ユーザー アカウント**は、定期的にステーションにアクセスするが、システムを管理しない個人のためのアカウントです。 通常は、MultiPoint Services システムのほとんどのユーザーに標準ユーザー アカウントを作成します。 詳細については、「[標準ユーザー アカウントの作成](Create-a-Standard-User-Account.md)」を参照してください。  
  
-   **MultiPoint ダッシュボード ユーザー アカウント**は、MultiPoint ダッシュボードを使用して標準ユーザー セッションを管理し、あらゆるステーションからのログオンが許可される個人のためのアカウントです。 詳細については、「[MultiPoint ダッシュボード ユーザー アカウントを作成する](Create-a-MultiPoint-Dashboard-User-Account.md)」を参照してください。  
  
## <a name="user-name-and-password-considerations"></a>ユーザー名とパスワードに関する考慮事項  
管理ユーザーは、ソフトウェアのインストールやセキュリティ設定の変更など、MultiPoint Services システムの他のすべてのユーザーに影響を与えるタスクを実行できます。 そのような理由から、管理ユーザーには一意の名前と管理ユーザーだけが知るパスワードを与えます。  
  
ユーザー アカウントの重要な考慮事項の 1 つが、ユーザー アカウントごとにエクスプローラーに一意の**ドキュメント** ライブラリを割り与えることです。このライブラリに **My Documents** フォルダーが含まれます。 MultiPoint Services システムの標準ユーザーがエクスプローラーの自分の**ドキュメント** ライブラリにプライベートな文書を保存する場合、標準ユーザーも一意のユーザー名と自分だけが知るパスワードで MultiPoint Services システムにログオンする必要があります。 エクスプローラーに文書を保管する方法については、「[ユーザー ファイルの管理](Manage-User-Files.md)」トピックを参照してください。  
  
> [!TIP]  
> システム セキュリティを強化するには、すべてのユーザーのパスワードに強力なパスワードを設定します。 強力なパスワードは、簡単に推測できない 1 つまたは解読は、少なくとも 8 長の文字をユーザーのアカウント名の全部または一部が含まれていない次の 4 種類の文字のうち少なくとも 3 種類が含まれています。 大文字、小文字、数字、キーボード上にある記号 (など!、@、#)。  
  
## <a name="see-also"></a>関連項目  
[管理ユーザー アカウントを作成します。](Create-an-Administrative-User-Account.md)  
[標準ユーザー アカウントを作成します。](Create-a-Standard-User-Account.md)  
[ユーザー ファイルを管理する](Manage-User-Files.md)
[ユーザー アカウントの管理](Manage-User-Accounts.md)