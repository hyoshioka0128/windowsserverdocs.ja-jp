---
ms.assetid: 7e804590-6d6c-4cca-ac14-02d4dff06cec
title: "パスワードのカスタマイズを更新します。"
description: 
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adfs
ms.openlocfilehash: 4b06992bfb398b66988ad4882217a8a83738365e
ms.sourcegitcommit: 78d8839ccafa9530784cb9e38c3127ed2c215423
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/09/2018
---
# <a name="update-password-customization"></a>パスワードのカスタマイズを更新します。 

>適用対象: Windows Server 2016、Windows Server 2012 R2

場合によっては、ユーザーのアカウントのパスワードを変更する企業ネットワークに接続できませんしない場合があります。 この要素は、最も近いから離れた場所 live 可能性がありますしたリモート従業員のために特別に問題が発生することができます、本社します。 この特定のような場合にのみ、インターネットに接続してパスワード更新ページを使用できます。  
  
パスワード更新ページをカスタマイズするには、ページの説明を提供します。  
  
> パスワード更新ページを有効にするには、AD FS の管理下にあるエンドポイントに移動します。 パスワードの更新のエンドポイントは、[その他の ad fs/ポータル/updatepassword/の下部にあります。 エンドポイントを有効にした後は、AD FS サービスを再起動する必要があります。 これは手動で実行する必要があります。 Https:// に移動できますし、<fqdn>/adfs ポータル/updatepassword/職場に参加しているデバイスと、パスワード更新ページを参照してください。  
  
![更新プログラム](media/AD-FS-user-sign-in-customization/ADFS_Blue_Custom5.png)  
  
## <a name="customize-the-update-password-page-description"></a>パスワード更新ページの説明をカスタマイズします。  
パスワード更新ページの説明をカスタマイズするには、次の Windows PowerShell コマンドレットと構文を使用します。  
  

    Set-AdfsGlobalWebContent -UpdatePasswordPageDescriptionText "This is the Contoso Update Password page."  

## <a name="additional-references"></a>その他の参照 
[AD FS のユーザーのサインイン カスタマイズ](AD-FS-user-sign-in-customization.md)  
