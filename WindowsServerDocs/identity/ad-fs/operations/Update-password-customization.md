---
ms.assetid: 7e804590-6d6c-4cca-ac14-02d4dff06cec
title: パスワードのカスタマイズの更新
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server
ms.technology: identity-adfs
ms.openlocfilehash: f43b3052d64c7a5766e014aa47063c7e17a7d2ab
ms.sourcegitcommit: 2cc251eb5bc3069bf09bc08e06c3478fcbe1f321
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/03/2020
ms.locfileid: "84333943"
---
# <a name="update-password-customization"></a>パスワードのカスタマイズの更新 


場合によっては、ユーザーがアカウント パスワードを変更するために企業ネットワークに接続できないことがあります。 これが問題となるのは、リモートで働く従業員が最寄りのオフィスから離れた場所に住んでいるような場合です。 このような特別な場合には、インターネット接続のみでパスワード更新ページを使用できます。  
  
パスワード更新ページは、独自の説明を追加してカスタマイズできます。  
  
> パスワード更新ページを有効化するには、[エンドポイント] の下にある [AD FS 管理] に移動します。 パスワード更新用のエンドポイントは、[その他] の下部にある /adfs/portal/updatepassword/ です。 このエンドポイントを有効化したら、AD FS サービスを再起動する必要があります。 この操作は手動で行う必要があります。 [パスワードの更新] web ページを外部で使用する場合、および Web アプリケーションプロキシを使用する場合は、同じオプションでプロキシで有効にする必要があります ([プロキシで有効にする])。 その後、ワークプレース ジョインが設定されたデバイスで https://<fqdn>/adfs/portal/updatepassword/ を開くと、パスワード更新ページが表示されます。  
  
![update](media/AD-FS-user-sign-in-customization/ADFS_Blue_Custom5.png)  
  
## <a name="customize-the-update-password-page-description"></a>パスワード更新ページの説明のカスタマイズ  
パスワード更新ページの説明をカスタマイズするには、次の Windows PowerShell コマンドレットと構文を使用します。  
  

    Set-AdfsGlobalWebContent -UpdatePasswordPageDescriptionText "This is the Contoso Update Password page."  

## <a name="additional-references"></a>その他の参照情報 
[AD FS ユーザーサインインのカスタマイズ](AD-FS-user-sign-in-customization.md)  
