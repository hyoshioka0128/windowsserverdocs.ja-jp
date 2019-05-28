---
ms.assetid: 777aab65-c9c7-4dc9-a807-9ab73fac87b8
title: AD FS エクストラネット ロックアウト保護を構成します。
description: ''
author: billmath
ms.author: billmath
manager: femila
ms.date: 02/01/2019
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adfs
ms.openlocfilehash: 6612c05e664b50c5a50b10b712b91715cc85d230
ms.sourcegitcommit: 0b5fd4dc4148b92480db04e4dc22e139dcff8582
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/24/2019
ms.locfileid: "66189883"
---
# <a name="configure-ad-fs-extranet-lockout-protection"></a>AD FS エクストラネット ロックアウト保護を構成します。

Windows Server 2012 R2 で AD FS でエクストラネットのロックアウトと呼ばれるセキュリティ機能が導入されました。  この機能により、AD FS が「停止」一定期間の外部から「悪意のある」ユーザー アカウントを認証します。  これは、ユーザー アカウントが Active Directory でロックアウトされていることを防ぎます。  アカウントのロックアウトが AD からユーザーを保護できるだけでなく AD FS のエクストラネット ロックアウトも保護ブルート フォース パスワード推測攻撃から

> [!NOTE]
> この機能は、に対してのみ機能、**エクストラネット シナリオ**認証要求にのみ適用されます、Web アプリケーション プロキシ経由で**ユーザー名とパスワード認証**します。

## <a name="advantages-of-extranet-lockout"></a>エクストラネットのロックアウトの利点
エクストラネットのロックアウトは、次の主な利点を提供します。
- ユーザー アカウントを保護する**ブルート フォース攻撃による**攻撃者が継続的に認証要求を送信することによって、ユーザーのパスワードを推測しようとします。 この場合、AD FS がエクストラネット アクセス用の悪意のあるユーザー アカウントがロックされます。
- ユーザー アカウントを保護する**悪意のあるアカウントのロックアウト**攻撃者が間違ったパスワードで認証要求を送信することによって、ユーザー アカウントをロックアウトましょう。 この場合、ユーザー アカウントは、エクストラネット アクセス用の AD FS によってロックは、AD での実際のユーザー アカウントがロックアウトされていないと、組織内の企業リソースにもアクセスできます。 これと呼ばれますが、**ソフト ロックアウト**します。

## <a name="how-it-works"></a>動作のしくみ
この機能を有効にするように構成する必要がある AD FS での 3 つの設定があります。 
- **EnableExtranetLockout&lt;ブール&gt;** このブール値に設定エクストラネットのロックアウトを有効にする場合は True。
- **ExtranetLockoutThreshold&lt;整数&gt;** 無効なパスワード試行の最大数を定義します。 しきい値に達すると、AD FS はすぐに拒否されているパスワードは、良くも悪くも、エクストラネットの監視 ウィンドウが経過するまでかどうかに関係なく、認証ドメイン コント ローラーに接続を試みることがなくエクストラネットからの要求を使用します。 値をつまり**badPwdCount**を論理的なロックされているアカウントは、中に、AD アカウントの属性は向上しません。
- **ExtranetObservationWindow &lt;TimeSpan&gt;** を論理的なロック期間のユーザーのアカウントであるが決定します。AD FS は、ウィンドウが渡されるときにユーザー名とパスワードの認証をもう一度の実行が開始されます。 AD FS では、エクストラネットの監視 ウィンドウがかどうかに渡されるかどうかを決定するため、参照として AD 属性の badPasswordTime を使用します。 現在の場合、ウィンドウが経過時間 > badPasswordTime + ExtranetObservationWindow します。 

> [!NOTE]
> AD のロックアウト ポリシーから独立して AD FS エクストラネット ロックアウト機能です。 ただし、強くお勧めを設定すること、 **ExtranetLockoutThreshold**パラメーターの値を AD アカウント ロックアウトのしきい値よりも小さい値です。 そのために失敗すると、AD FS のアカウントが Active Directory でロックアウトされていることを防止することができませんが発生します。 

無効なパスワード試行とソフト ロックアウト期間の 30 分の 15 の数の最大のエクストラネットのロックアウトの機能を有効化の例は次のとおりです。

```powershell
Set-AdfsProperties -EnableExtranetLockout $true -ExtranetLockoutThreshold 15 -ExtranetObservationWindow (new-timespan -Minutes 30)
```

これらの設定は、AD FS サービスを認証できるすべてのドメインに適用されます。 動作する方法を AD FS は、認証要求を受け取る LDAP の呼び出しを通じて、プライマリ ドメイン コント ローラー (PDC) にアクセスし、参照を実行するは、 **badPwdCount** PDC 上のユーザーの属性。 AD FS の値が検出されると**badPwdCount** > = ExtranetLockoutThreshold 設定、エクストラネットの監視 ウィンドウで定義されている時間は過ぎていませんまだ、AD FS 要求を拒否、すぐにかどうかに関係なくことを意味して、ユーザーがエクストラネットから良くも悪くもパスワードを入力、AD FS が AD に資格情報を送信していないため、ログオンは失敗します。 AD FS に任意の状態に関係を保持しない**badPwdCount**またはユーザー アカウントがロックアウトします。 AD FS は AD を使用して、すべての状態を追跡します。 

> [!warning]
> Server 2012 R2 で AD FS エクストラネット ロックアウトが有効にすると、WAP 経由のすべての認証要求は、PDC で AD FS によって検証されます。 PDC が利用できない場合は、ユーザーは、エクストラネットから認証することできません。

Server 2016 には、PDC が利用できない場合は、AD FS を別のドメイン コント ローラーにフォールバックを許可する追加のパラメーターが用意されています。

- **ExtranetLockoutRequirePDC&lt;ブール&gt;** - 有効になっている場合: エクストラネットのロックアウトがプライマリ ドメイン コント ローラー (PDC) が必要です。 無効にした場合: PDC を利用できない場合、エクストラネットのロックアウトが別のドメイン コント ローラーにフォールバックします。

次の Windows PowerShell コマンドを使用して、Server 2016 で AD FS エクストラネット ロックアウトを構成することができます。

```powershell
Set-AdfsProperties -EnableExtranetLockout $true -ExtranetLockoutThreshold 15 -ExtranetObservationWindow (new-timespan -Minutes 30) -ExtranetLockoutRequirePDC $false
```

## <a name="working-with-the-active-directory-lockout-policy"></a>Active Directory のロックアウトのポリシーでの作業
AD FS でエクストラネットのロックアウトの機能は関係なく機能 AD ロックアウト ポリシーから。 ただし、実行設定を行うことを確認して、AD ロックアウト ポリシー セキュリティ目的が役立つように、エクストラネットのロックアウトが正しく構成されている必要があります。
AD ロックアウト ポリシーの確認を最初見てみましょう。 AD のロックアウトのポリシーに関する 3 つの設定があります。
- **アカウントのロックアウトしきい値**: この設定は AD FS で ExtranetLockoutThreshold 設定に似ています。 ユーザー アカウントがロックアウトされると、失敗したログオン試行の数が決定します。AD FS で ExtranetLockoutThreshold の値を設定すると、悪意のあるアカウント ロックアウトの攻撃からのユーザー アカウントを保護するために&lt;ad アカウント ロックアウトのしきい値の値
- **アカウントのロックアウト期間**: この設定は、アカウントのロックアウト、ユーザーはどのくらいの時間を決定します。この設定は必要ありませんはるかこの会話のように AD ロックアウトが正しく構成されている場合に発生する前に、常にエクストラネットのロックアウトが発生します。
- **アカウント ロックアウト カウンター後にリセット**: この設定を決定する前に、ユーザーの最後のログオン失敗からどれ時間だけが経過する必要があります**badPwdCount** 0 にリセットされます。 AD FS でエクストラネットのロックアウト機能に AD ロックアウト ポリシーで機能するにすることを確認して ExtranetObservationWindow の値では、AD FS &gt; ad リセット アカウント ロックアウト カウンターの後の値。 次の例では、その理由を説明します。  

2 つの例を見てを確認しましょう方法**badPwdCount**さまざまな設定と状態に基づいて時間の経過と共に変化します。 どちらの例で仮定**アカウント ロックアウトのしきい値**= 4 と**ExtranetLockoutThreshold** = 2 です。 **赤い**矢印が不正なパスワードの試行を表します、**緑色**矢印は、適切なパスワードの試行を表します。 例 1 で**ExtranetObservationWindow** &gt; **リセット アカウント ロックアウト カウンター後**します。 例 2 で**ExtranetObservationWindow** &lt; **リセット アカウント ロックアウト カウンター後**します。 

### <a name="example-1"></a>例 1
![例 1](media/Configure-AD-FS-Extranet-Lockout-Protection/one.png)

### <a name="example-2"></a>例 2
![例 1](media/Configure-AD-FS-Extranet-Lockout-Protection/two.png)

上記からわかるが 2 つある場合の条件**badPwdCount**は 0 にリセットされます。 1 つは、成功したログオンがある場合です。 定義されている、このカウンターをリセットするときに、もう一方は**リセット アカウント ロックアウト カウンター後**設定します。 ときに**リセット アカウント ロックアウト カウンター後** &lt; **ExtranetObservationWindow**アカウントには、AD によってロックアウトされる可能性はありません。 ただし場合、**リセット アカウント ロックアウト カウンター後** &gt; **ExtranetObservationWindow**アカウントがロックアウトされている AD によってが「遅延方式」で可能性があります。 によってロック AD 構成によっては AD FS で 1 つの無効なパスワード試行までには、その監視期間中にのみ許可されるアカウントを取得するしばらく時間がかかること**badPwdCount**に達すると**アカウント ロックアウトのしきい値**.

詳細については、次を参照してください。[を構成するアカウントのロックアウト](https://blogs.technet.microsoft.com/secguide/2014/08/13/configuring-account-lockout/)します。 

## <a name="known-issues"></a>既知の問題
既知の問題のために AD FS に認証できません AD ユーザー アカウントの場所、 **badPwdCount**属性は ADFS を照会しているドメイン コント ローラーにレプリケートされません。 参照してください[2971171](https://support.microsoft.com/help/2971171/adfs-authentication-issue-for-active-directory-users-when-extranet-loc)の詳細。 これまでにリリースされたすべての AD FS Qfe が見つかります[ここ](../deployment/updates-for-active-directory-federation-services-ad-fs.md)します。

## <a name="key-points-to-remember"></a>注意点
- エクストラネットのロックアウトの機能は、に対してのみ機能、**エクストラネット シナリオ**Web アプリケーション プロキシを介した認証要求はどこ
- エクストラネットのロックアウトの機能にのみ適用されます**ユーザー名とパスワードの認証**
- AD FS のトラックを保持しません**badPwdCount**またはアウト論理的なロックであるユーザー。AD FS は AD を使用してすべての状態の追跡用
- AD FS の参照を実行する、 **badPwdCount**属性を介してすべての認証試行のために PDC でユーザーに LDAP の呼び出し  
- AD FS 2016 よりも前は、PDC にアクセスできない場合は失敗します。 AD FS 2016 では、AD FS、PDC が発生した場合の他のドメイン コント ローラーにフォールバックすることはできませんを許可するための機能強化が導入されました。 
- AD FS will allow authentication requests from extranet if badPwdCount < ExtranetLockoutThreshold 
- 場合**badPwdCount** >= **ExtranetLockoutThreshold** AND **badPasswordTime** + **ExtranetObservationWindow** < 現在の時刻では、AD FS のエクストラネットからの認証要求は拒否
- 悪意のあるアカウントのロックアウトを避けるためには、必ず**ExtranetLockoutThreshold** < **アカウント ロックアウトのしきい値**AND **ExtranetObservationWindow**  > **ロックアウト カウンターのリセット**


## <a name="additional-references"></a>その他の参照情報  
- [Active Directory フェデレーション サービスをセキュリティで保護するためのベスト プラクティス](../../ad-fs/deployment/best-practices-securing-ad-fs.md)
- [管理者以外のユーザーへの AD FS Powershell コマンドレットのアクセスの委任](delegate-ad-fs-pshell-access.md)
- [Set-adfsproperties](https://technet.microsoft.com/itpro/powershell/windows/adfs/set-adfsproperties)

[AD FS の運用](../../ad-fs/AD-FS-2016-Operations.md)

    
