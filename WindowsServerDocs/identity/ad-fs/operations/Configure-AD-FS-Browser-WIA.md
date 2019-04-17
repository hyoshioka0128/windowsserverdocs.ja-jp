---
title: "AD FS に Windows 統合認証 (WIA) を使用するようにブラウザーを構成します。"
description: "このドキュメントは、AD FS に WIA を使用するようにブラウザーを構成する方法を説明します。"
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.custom: it-pro
ms.prod: windows-server-threshold
ms.technology: identity-adfs
ms.openlocfilehash: f7d43931d1fe4958a539ff1b728e4cc154d06248
ms.sourcegitcommit: 70c1b6cedad55b9c7d2068c9aa4891c6c533ee4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/03/2017
---
# <a name="configure-browsers-to-use-windows-integrated-authentication-wia-with-ad-fs"></a>AD FS に Windows 統合認証 (WIA) を使用するようにブラウザーを構成します。

既定では、Windows 統合認証 (WIA) が有効になっている Active Directory フェデレーション サービス (AD FS) で Windows Server 2012 R2 ですべてのアプリケーションの認証用のブラウザーを使用する組織の内部ネットワーク (イントラネット) 内に発生する認証要求にします。

AD FS 2016 今すぐには、WIA しない、また、(不適切)、キャッチ Windows Phone もときに、Edge ブラウザーを有効にする既定の強化された設定があります。

    =~Windows\s*NT.*Edge

多くの場合が更新される場合でも、Edge の一般的なシナリオをサポートするために個々 のユーザー エージェント文字列を構成する必要が不要になった上記を意味します。

その他のブラウザーでは、AD FS のプロパティを構成**WiaSupportedUserAgents**を使用しているブラウザーに基づいて必要な値を追加します。  以下の手順を使用することができます。



### <a name="view-wiasupporteduseragent-settings"></a>WIASupportedUserAgent 設定を表示します。
**WIASupportedUserAgents** WIA をサポートするユーザー エージェントを定義します。 AD FS は、ブラウザーまたはブラウザー コントロールでログインを実行するときに、ユーザー エージェント文字列を分析します。

次の PowerShell の例を使用して、現在の設定を表示できます。

```powershell
    $strings = Get-AdfsProperties | select -ExpandProperty WiaSupportedUserAgents
```

![WIA サポート](../operations/media/Configure-AD-FS-Browser-WIA/wiasupport.png)

### <a name="change-wiasupporteduseragent-settings"></a>WIASupportedUserAgent 設定を変更します。
新しい AD FS のインストールでは既定では、作成したユーザー エージェント文字列の一致のセットがあります。 ただし、これらがあります有効期限切れのブラウザーやデバイスへの変更に基づいています。 特に、Windows デバイスでは、トークンでのマイナー バリエーションと同様のユーザー エージェント文字列があります。 次の Windows PowerShell の例では、シームレスな WIA をサポートしている現在の市場ではデバイスの現在のセットの最適なガイダンスを提供します。

```powershell
    Set-AdfsProperties -WIASupportedUserAgents @("MSIE 6.0", "MSIE 7.0; Windows NT", "MSIE 8.0", "MSIE 9.0", "MSIE 10.0; Windows NT 6", "Windows NT 6.3; Trident/7.0", "Windows NT 6.3; Win64; x64; Trident/7.0", "Windows NT 6.3; WOW64; Trident/7.0", "Windows NT 6.2; Trident/7.0", "Windows NT 6.2; Win64; x64; Trident/7.0", "Windows NT 6.2; WOW64; Trident/7.0", "Windows NT 6.1; Trident/7.0", "Windows NT 6.1; Win64; x64; Trident/7.0", "Windows NT 6.1; WOW64; Trident/7.0", "MSIPC", "Windows Rights Management Client")
```

上記のコマンドは、AD FS は、WIA の次のユース ケースをのみカバーことを確認します。

ユーザー エージェント|使用例|
-----|-----|
MSIE 6.0|IE 6.0|
MSIE 7.0。Windows NT|IE 7、イントラネット ゾーンで IE します。 "Windows NT"フラグメントは、デスクトップ オペレーティング システムによって送信されます。|
MSIE 8.0|IE 8.0 (デバイスがない送信、ためより具体的にする必要があります)|
MSIE 9.0|IE 9.0 (デバイスがない送信より具体的ために必要ないいえ)|
MSIE 10.0 です。Windows NT 6|Windows XP およびデスクトップ オペレーティング システムの新しいバージョンの IE 10.0</br></br>送信するため、Windows Phone 8.0 デバイス] (優先順位の設定をモバイル) は除外されます。</br></br>ユーザー エージェント: mozilla/5.0 (互換性のあります。MSIE 10.0 です。Windows Phone 8.0 です。Trident/6.0 です。IEMobile/10.0 です。ARM です。タッチ操作です。NOKIA です。Lumia 920)|
Windows NT; 6.3Trident/7.0</br></br>Windows NT; 6.3Win64 です。x64 です。Trident/7.0</br></br>Windows NT; 6.3WOW64 です。Trident/7.0| Windows 8.1 デスクトップ オペレーティング システム、さまざまなプラットフォーム|
Windows NT 6.2 です。Trident/7.0</br></br>Windows NT 6.2 です。Win64 です。x64 です。Trident/7.0</br></br>Windows NT 6.2 です。WOW64 です。Trident/7.0|Windows 8 のデスクトップ オペレーティング システム、さまざまなプラットフォーム|
Windows NT 6.1;Trident/7.0</br></br>Windows NT 6.1;Win64 です。x64 です。Trident/7.0</br></br>Windows NT 6.1;WOW64 です。Trident/7.0|Windows 7 のデスクトップ オペレーティング システム別 platoforms|
MSIPC| Microsoft Information Protection とクライアントの制御|
Windows Rights Management クライアント|Windows Rights Management クライアント|
