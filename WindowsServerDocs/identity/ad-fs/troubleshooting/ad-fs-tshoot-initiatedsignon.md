---
title: AD FS のトラブルシューティング - Idp によって開始されたサインオンします。
description: このドキュメントでは、AD FS のサインオン ページのトラブルシューティングを行う方法について説明します。
author: billmath
ms.author: billmath
manager: mtillman
ms.date: 01/03/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adfs
ms.openlocfilehash: 61e9adc708e95a6ab4a82550280737b2f4bad0a1
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/17/2019
ms.locfileid: "59844943"
---
# <a name="ad-fs-troubleshooting---idp-initiated-sign-on"></a>AD FS のトラブルシューティング - Idp によって開始されたサインオンします。
AD FS のサインオン ページを使用して、認証が動作しているかどうかをテストできます。  これは、ページに移動し、サインインします。  また、すべての SAML 2.0 証明書利用コンポーネントが表示されていることを確認するのにには、サインイン ページを使用できます。

## <a name="enable-the-idp-intiated-sign-on-page"></a>Idp 押してサインオン ページを有効にします。
既定では、Windows 2016 の AD FS では有効になっているページで、サインオンありません。  有効にするためには、PowerShell コマンド Set-adfsproperties を使用することができます。  ページを有効にするのにには、次の手順を使用します。

1.  開いている Windows PowerShell
2.  入力:`Get-AdfsProperties`し、enter キーを押します
3.  いることを確認**EnableIdpInitiatedSignonPage**を false に設定されている![False](media/ad-fs-tshoot-initiatedsignon/idp2.png)
4.  PowerShell では、次のように入力します。  `Set-AdfsProperties -EnableIdpInitiatedSignonPage $true`
5.  したがって Get-adfsproperties をもう一度入力し、いることを確認の確認は表示されません**EnableIdpInitatedSignonPage**設定を true にします。
![True](media/ad-fs-tshoot-initiatedsignon/idp4.png)

## <a name="test-authentication"></a>認証のテスト
AD FS 認証 Idp-Initiated サインオン ページをテストするのにには、次の手順を使用します。

1.  Web ブラウザーを開き、Idp のサインオン ページに移動します。  例:  https://sts.contoso.com/adfs/ls/idpinitiatedsignon.htm
2.  サインインを求めるメッセージが表示する必要があります。  資格情報を入力します。
![シングル サインオン](media/ad-fs-tshoot-initiatedsignon/idp5.png)
3.  これが成功した場合署名する必要があります。


## <a name="test-authentication-using-a-seamless-logon-experience"></a>ログオンのシームレスなエクスペリエンスを使用して認証のテスト
ログオンのシームレスなエクスペリエンスをテストするには、AD FS サーバーの URL が、インターネット オプション のローカル イントラネット ゾーンに追加されていることを確認します。  次の手順を実行します。

1.  Windows 10 クライアントでは、[開始] をクリックして、インターネット オプションを入力し、インターネット オプションを選択します。
2.   セキュリティ タブをクリックして、ローカル イントラネット をクリックしておよびサイト ボタンをクリックします。
![シームレスです](media/ad-fs-tshoot-initiatedsignon/idp8.png)
1.  [詳細設定] をクリックします。
2.  Url を入力し、[追加] をクリックします。  [閉じる] をクリックします。
![Url を追加します。](media/ad-fs-tshoot-initiatedsignon/idp9.png)
1.  [Ok] をクリックします。  [Ok] をクリックします。  これにより、インターネット オプションが閉じる必要があります。
2.  Web ブラウザーを開き、Idp のサインオン ページに移動します。  例:  https://sts.contoso.com/adfs/ls/idpinitiatedsignon.htm
3.  サインイン ボタンをクリックします。  自動的にサインインする必要があり、資格情報を求められません。
![シームレスです](media/ad-fs-tshoot-initiatedsignon/idp6.png)

## <a name="next-steps"></a>次の手順

- [AD FS のトラブルシューティング](ad-fs-tshoot-overview.md)