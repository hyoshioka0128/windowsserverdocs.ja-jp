---
ms.assetid: d562ef46-f240-48be-bbd4-fd88fc6bbbdc
title: WIA をサポートしていないデバイスのイントラネットフォームベース認証の構成
description: ''
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adfs
ms.openlocfilehash: 6a730483f99e1c937c3618853ee6d3dbd175356b
ms.sourcegitcommit: 6f968368c12b9dd699c197afb3a3d13c2211f85b
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/26/2019
ms.locfileid: "68544588"
---
# <a name="configuring-intranet-forms-based-authentication-for-devices-that-do-not-support-wia"></a>WIA をサポートしていないデバイスのイントラネットフォームベース認証の構成


既定では、windows Server 2012 R2 の Active Directory フェデレーションサービス (AD FS) (AD FS) で Windows 統合認証 (WIA) が有効になっています。これは、組織の内部ネットワーク (イントラネット) 内で実行される認証要求が、認証用のブラウザー。 たとえば、WS-FEDERATION または SAML プロトコルを使用するブラウザーベースのアプリケーションや、OAuth プロトコルを使用する豊富なアプリケーションにすることができます。 WIA を使用すると、エンドユーザーは、資格情報を手動で入力しなくても、アプリケーションにシームレスにログオンできます。 ただし、一部のデバイスとブラウザーでは、WIA をサポートできないため、これらのデバイスからの認証要求は失敗します。 また、NTLM にネゴシエートする特定のブラウザーの操作は望ましくありません。 推奨される方法は、このようなデバイスやブラウザーのフォームベースの認証にフォールバックすることです。

Windows Server 2016 および Windows Server 2012 R2 の AD FS を使用すると、管理者は、フォームベースの認証へのフォールバックをサポートするユーザーエージェントの一覧を構成できます。 フォールバックは、次の2つの構成によって可能になります。


- コマンド`Set-ADFSProperties`レットの**wiasupporteduseragentstrings**プロパティ
- コマンド`Set-AdfsGlobalAuthenticationPolicy`レットの**windowsインテグレーション atedfallbackenabled**プロパティ

**Wiasupporteduseragentstrings**は、WIA をサポートするユーザーエージェントを定義します。 AD FS は、ブラウザーまたはブラウザーコントロールでログインを実行するときに、ユーザーエージェント文字列を分析します。 ユーザーエージェント文字列のコンポーネントが、 **Wiasupporteduseragentstrings**プロパティで構成されているユーザーエージェント文字列のコンポーネントのいずれとも一致しない場合、AD FS はフォームベースの**認証を提供します (Windowsインテグレーション Atedfallbackenabled**フラグが True に設定されています。

既定では、新しい AD FS のインストールには、一連のユーザーエージェント文字列の一致が作成されます。 ただし、これらは、ブラウザーおよびデバイスの変更に基づいて古くなっている可能性があります。 特に、Windows デバイスでは、トークンに多少の違いがある同様のユーザーエージェント文字列があります。 次の Windows PowerShell の例では、シームレスな WIA をサポートする現在の市場にあるデバイスの現在のセットについて、最適なガイダンスを提供しています。

    Set-AdfsProperties -WIASupportedUserAgents @("MSIE 6.0", "MSIE 7.0; Windows NT", "MSIE 8.0", "MSIE 9.0", "MSIE 10.0; Windows NT 6", "Windows NT 6.3; Trident/7.0", "Windows NT 6.3; Win64; x64; Trident/7.0", "Windows NT 6.3; WOW64; Trident/7.0", "Windows NT 6.2; Trident/7.0", "Windows NT 6.2; Win64; x64; Trident/7.0", "Windows NT 6.2; WOW64; Trident/7.0", "Windows NT 6.1; Trident/7.0", "Windows NT 6.1; Win64; x64; Trident/7.0", "Windows NT 6.1; WOW64; Trident/7.0", "MSIPC", "Windows Rights Management Client")

上のコマンドは、AD FS が WIA の次のユースケースのみをカバーするようにします。

ユーザーエージェント|使用事例|
-----|-----|
MSIE 6.0|IE 6.0|
MSIE 7.0;Windows NT|IE 7、イントラネットゾーンの IE。 "Windows NT" フラグメントは、デスクトップオペレーティングシステムによって送信されます。|
MSIE 8.0|IE 8.0 (デバイスがこれを送信することはないため、さらに具体的にする必要があります)|
MSIE 9.0|IE 9.0 (デバイスがこれを送信することはないため、これをより具体的にする必要はありません)|
MSIE 10.0;Windows NT 6|Windows XP およびそれ以降のバージョンのデスクトップオペレーティングシステムの IE 10.0</br></br>Windows Phone 8.0 デバイス (優先設定が mobile) は、送信されるため、除外されます。</br></br>ユーザーエージェント:Mozilla/5.0 (互換、MSIE 10.0;Windows Phone 8.0;Trident/6.0;IEMobile/10.0;分岐強くNOKIALumia 920)|
Windows NT 6.3;Trident/7.0</br></br>Windows NT 6.3;Win64x64Trident/7.0</br></br>Windows NT 6.3;WOW64Trident/7.0| Windows 8.1 デスクトップオペレーティングシステム、さまざまなプラットフォーム|
Windows NT 6.2;Trident/7.0</br></br>Windows NT 6.2;Win64x64Trident/7.0</br></br>Windows NT 6.2;WOW64Trident/7.0|Windows 8 デスクトップオペレーティングシステム、さまざまなプラットフォーム|
Windows NT 6.1;Trident/7.0</br></br>Windows NT 6.1;Win64x64Trident/7.0</br></br>Windows NT 6.1;WOW64Trident/7.0|Windows 7 デスクトップオペレーティングシステム、さまざまなプラットフォーム|
MSIPC を右クリックし| Microsoft Information Protection and Control クライアント|
Windows Rights Management クライアント|Windows Rights Management クライアント|

WIASupportedUserAgents 文字列に記載されていないユーザーエージェントに対して、代替のフォームベース認証を有効にするには、WindowsIntegratedFallbackEnabled フラグを true に設定します。

    Set-AdfsGlobalAuthenticationPolicy -WindowsIntegratedFallbackEnabled $true

また、フォームベースの認証がイントラネットで有効になっていることを確認します。

## <a name="configuring-wia-for-chrome"></a>Chrome 用の WIA の構成
Chrome または他のユーザーエージェントを、WIA をサポートする AD FS 構成に追加できます。 これにより、AD FS によって保護されたリソースにアクセスするときに資格情報を手動で入力しなくても、アプリケーションにシームレスにログオンできるようになります。 Chrome で WIA を有効にするには、次の手順に従います。

AD FS 構成で、Windows ベースのプラットフォームで Chrome 用のユーザーエージェント文字列を追加します。

    Set-AdfsProperties -WIASupportedUserAgents ((Get-ADFSProperties | Select -ExpandProperty WIASupportedUserAgents) + "Mozilla/5.0 (Windows NT")

同様に、Apple macOS の Chrome では、AD FS の構成に次のユーザーエージェント文字列を追加します。

    Set-AdfsProperties -WIASupportedUserAgents ((Get-ADFSProperties | Select -ExpandProperty WIASupportedUserAgents) + "Mozilla/5.0 (Macintosh; Intel Mac OS X")

Chrome のユーザーエージェント文字列が AD FS のプロパティで設定されていることを確認します。

    Get-AdfsProperties | Select -ExpandProperty WIASupportedUserAgents

(ここに新しいスクリーンショットが必要です)![認証の構成](media/Configure-intranet-forms-based-authentication-for-devices-that-do-not-support-WIA/chrome1.png) 

>[!NOTE]   
> 新しいブラウザーとデバイスがリリースされると、ユーザーエージェントの機能を調整し、それに応じて AD FS 構成を更新して、ブラウザーとデバイスを使用するときのユーザーの認証エクスペリエンスを最適化することをお勧めします。 具体的には、新しいデバイスまたはブラウザーの種類を WIA のサポートマトリックスに追加するときに、AD FS の**Wiasupporteduseragents**設定を再評価することをお勧めします。


