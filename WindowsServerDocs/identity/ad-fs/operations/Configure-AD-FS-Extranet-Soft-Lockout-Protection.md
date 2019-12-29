---
ms.assetid: 777aab65-c9c7-4dc9-a807-9ab73fac87b8
title: AD FS エクストラネットロックアウト保護の構成
description: ''
author: billmath
ms.author: billmath
manager: femila
ms.date: 02/01/2019
ms.topic: article
ms.prod: windows-server
ms.technology: identity-adfs
ms.openlocfilehash: bb5958f8205271fe3ab2258ed9812ae03f2a0be0
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/27/2019
ms.locfileid: "71358210"
---
# <a name="configure-ad-fs-extranet-lockout-protection"></a>AD FS エクストラネットロックアウト保護の構成

Windows Server 2012 R2 の AD FS では、エクストラネットロックアウトと呼ばれるセキュリティ機能が導入されました。  この機能を使用すると、AD FS は、一定期間外に "悪意のある" ユーザーアカウントの認証を "停止" します。  これにより、Active Directory でユーザーアカウントがロックアウトされるのを防ぐことができます。  AD アカウントロックアウトを使用してユーザーを保護するだけでなく、AD FS のエクストラネットロックアウトでは、ブルートフォースパスワード推測攻撃から保護することもできます。

> [!NOTE]
> この機能は、認証要求が Web アプリケーションプロキシを経由し、**ユーザー名とパスワードの認証**にのみ適用される**エクストラネットシナリオ**に対してのみ機能します。

## <a name="advantages-of-extranet-lockout"></a>エクストラネットロックアウトの利点
エクストラネットのロックアウトには、次のような主な利点があります。
- 攻撃者が認証要求を継続的に送信することによってユーザーのパスワードを推測しようとする**ブルートフォース攻撃**からユーザーアカウントを保護します。 この場合、AD FS によって、エクストラネットアクセス用の悪意のあるユーザーアカウントがロックアウトされます。
- 悪意のある**アカウントロックアウト**からユーザーアカウントを保護します。攻撃者は、間違ったパスワードを使用して認証要求を送信することによってユーザーアカウントをロックアウトする必要があります。 この場合、ユーザーアカウントはエクストラネットアクセス用に AD FS によってロックアウトされますが、AD の実際のユーザーアカウントはロックアウトされず、ユーザーは引き続き組織内の企業リソースにアクセスできます。 これは、**ソフトロックアウト**と呼ばれます。

## <a name="how-it-works"></a>動作のしくみ
この機能を有効にするために構成する必要がある AD FS には、次の3つの設定があります。 
- **Enableexたり et&lt;ブール値&gt;** 、このブール値を True に設定して、エクストラネットロックアウトを有効にします。
- **Ex流出 Etlockoutthreshold &lt;整数&gt;** これにより、パスワードの無効な試行回数の最大値が定義されます。 しきい値に達すると AD FS は、エクストラネットの監視ウィンドウが渡されるまで、パスワードが適切かどうかにかかわらず、認証のためにドメインコントローラーに接続しようとせずに、エクストラネットからの要求を直ちに拒否します。 これは、アカウントがソフトロックアウトされている間、AD アカウントの**Badpwdcount**属性の値が増加しないことを意味します。
- **ExtranetObservationWindow &lt;TimeSpan&gt;** 、ユーザーアカウントがソフトロックアウトされる期間を決定します。ウィンドウが渡されると、AD FS によってユーザー名とパスワードの認証の実行が開始されます。 AD FS では、エクストラネットの監視ウィンドウが成功したかどうかを判断するために、AD 属性 badPasswordTime を参照として使用します。 現在の時刻 > badPasswordTime + ExtranetObservationWindow の場合、ウィンドウが渡されます。 

> [!NOTE]
> エクストラネットのロックアウト機能は、AD ロックアウトポリシーとは別に AD FS ます。 ただし、 **ex/Etlockoutthreshold**パラメーター値は、AD アカウントのロックアウトしきい値よりも小さい値に設定することを強くお勧めします。 この操作を行わないと、Active Directory でアカウントがロックアウトされるのを防ぐことができ AD FS ます。 

最大15個の無効なパスワード試行回数と30分のソフトロックアウト期間を持つエクストラネットロックアウト機能を有効にする例を次に示します。

```powershell
Set-AdfsProperties -EnableExtranetLockout $true -ExtranetLockoutThreshold 15 -ExtranetObservationWindow (new-timespan -Minutes 30)
```

これらの設定は、AD FS サービスが認証できるすべてのドメインに適用されます。 その方法として、AD FS が認証要求を受信すると、LDAP 呼び出しを使用してプライマリドメインコントローラー (PDC) にアクセスし、PDC 上のユーザーの**Badpwdcount**属性の参照を実行します。 AD FS が**Badpwdcount** > = Ex渡 Etlockoutthreshold 設定の値を検出し、エクストラネットの監視ウィンドウで定義されている時間がまだ渡されていない場合、AD FS は要求を直ちに拒否します。つまり、ユーザーがエクストラネットから適切なパスワードを入力したかどうかに関係なく、ログオンは AD FS 失敗します。 AD FS は、 **Badpwdcount**またはロックアウトされたユーザーアカウントに関して、状態を保持しません。 AD FS は、すべての状態追跡に AD を使用します。 

> [!warning]
> サーバー 2012 R2 で AD FS エクストラネットロックアウトが有効になっている場合、WAP 経由のすべての認証要求は、PDC で AD FS によって検証されます。 PDC が使用できなくなると、ユーザーはエクストラネットから認証できなくなります。

サーバー2016には追加のパラメーターが用意されています。これにより、PDC が使用できなくなったときに、AD FS が別のドメインコントローラーにフォールバックできます。

- **Ex/Etlockoutrequirepdc &lt;ブール&gt;** -有効になっている場合: エクストラネットロックアウトにはプライマリドメインコントローラー (PDC) が必要です。 無効になっている場合: PDC が使用できない場合に、エクストラネットのロックアウトが別のドメインコントローラーにフォールバックします。

次の Windows PowerShell コマンドを使用して、サーバー2016で AD FS エクストラネットロックアウトを構成できます。

```powershell
Set-AdfsProperties -EnableExtranetLockout $true -ExtranetLockoutThreshold 15 -ExtranetObservationWindow (new-timespan -Minutes 30) -ExtranetLockoutRequirePDC $false
```

## <a name="working-with-the-active-directory-lockout-policy"></a>Active Directory ロックアウトポリシーの使用
AD FS のエクストラネットロックアウト機能は、AD ロックアウトポリシーとは独立して動作します。 ただし、エクストラネットのロックアウトの設定が適切に構成されていることを確認して、AD ロックアウトポリシーでのセキュリティの目的を実現できるようにする必要があります。
まず、AD ロックアウトポリシーを見てみましょう。 AD のロックアウトポリシーには、次の3つの設定があります。
- **アカウントのロックアウトのしきい値**: この設定は、AD FS の [Ex/Etlockoutthreshold] 設定に似ています。 ユーザーアカウントがロックアウトされる原因となる、ログオン試行の失敗回数を決定します。悪意のあるアカウントのロックアウト攻撃からユーザーアカウントを保護するために、AD のアカウントロックアウトしきい値 &lt; AD FS に [Exて Etlockoutthreshold] の値を設定します。
- **アカウントのロックアウト期間**: この設定は、ユーザーアカウントがロックアウトされる期間を決定します。この設定は、このメッセージ交換ではあまり重要ではありません。正しく構成されている場合、AD ロックアウトが発生する前に、エクストラネットのロックアウトが発生するためです
- 次の期間に**アカウントロックアウトカウンターをリセット**: この設定は、ユーザーの最後のログオン失敗から、 **Badpwdcount**が0にリセットされるまでに経過する時間を決定します。 AD FS のエクストラネットロックアウト機能が AD ロックアウトポリシーとうまく連動するようにするには、AD の [アカウントのロックアウトのリセット] カウンターの値を [AD FS の ExtranetObservationWindow] に &gt; します。 次の例では、その理由について説明します。  

2つの例を見て、さまざまな設定と状態に基づいて時間の経過と共に**Badpwdcount**がどのように変化するかを見てみましょう。 **アカウントロックアウトのしきい値**= 4 と**Exシャー etlockoutthreshold** = 2 の両方の例を考えてみましょう。 **赤い**矢印は間違ったパスワードの試行を表し、**緑色**の矢印は適切なパスワードの試行を表します。 たとえば #1 では、 **ExtranetObservationWindow**は、の**後にアカウントロックアウトカウンターをリセット**&gt; ます。 たとえば #2 では、 **ExtranetObservationWindow**は、の**後にアカウントロックアウトカウンターをリセット**&lt; ます。 

### <a name="example-1"></a>例 1
![Example1](media/Configure-AD-FS-Extranet-Lockout-Protection/one.png)

### <a name="example-2"></a>例 2
![Example1](media/Configure-AD-FS-Extranet-Lockout-Protection/two.png)

上の例からわかるように、 **Badpwdcount**が0にリセットされる条件は2つあります。 1つは、ログオンに成功した場合です。 もう1つは、設定後に **[アカウントロックアウトカウンターのリセット]** で定義したカウンターをリセットする時間です。 **ExtranetObservationWindow**&lt;**後にアカウントロックアウトカウンターをリセット**すると、アカウントは AD によってロックアウトされるリスクがありません。 ただし、&gt; **ExtranetObservationWindow**の**後にアカウントロックアウトカウンターをリセット**した場合は、アカウントが AD によってロックアウトされる可能性がありますが、"遅延した形式" で表示される可能性があります。 構成によっては、AD によってアカウントがロックアウトされるまでにしばらく時間がかかることがあります。 AD FS では、 **Badpwdcount**が**Account Locked Threshold しきい値**に達するまで、監視期間中は1つの無効なパスワードの試行のみが許可されます。

詳細については、「[アカウントロックアウトの構成](https://blogs.technet.microsoft.com/secguide/2014/08/13/configuring-account-lockout/)」を参照してください。 

## <a name="known-issues"></a>の既知の問題
AD ユーザーアカウントが AD FS で認証できないという既知の問題があります。これは、ADFS がクエリを実行しているドメインコントローラーに**Badpwdcount**属性がレプリケートされていないためです。 詳細については、「 [2971171](https://support.microsoft.com/help/2971171/adfs-authentication-issue-for-active-directory-users-when-extranet-loc) 」を参照してください。 [ここ](../deployment/updates-for-active-directory-federation-services-ad-fs.md)までにリリースされたすべての AD FS qfe を見つけることができます。

## <a name="key-points-to-remember"></a>覚えておくべき重要事項
- エクストラネットのロックアウト機能は、認証要求が Web アプリケーションプロキシを経由する**エクストラネットシナリオ**に対してのみ機能します。
- エクストラネットのロックアウト機能は、**ユーザー名 & パスワード認証**にのみ適用されます。
- AD FS は、 **Badpwdcount**またはソフトロックアウトされているユーザーの追跡を保持しません。AD FS は、すべての状態追跡に AD を使用します。
- AD FS は、すべての認証試行について、PDC 上のユーザーの LDAP 呼び出しによって**Badpwdcount**属性の参照を実行します。  
- PDC にアクセスできない場合、2016より前の AD FS は失敗します。 AD FS 2016 では、PDC が使用できない場合に AD FS を他のドメインコントローラーに切り替えられるようにする機能強化が導入されました。 
- AD FS は、badPwdCount < Exri Etlockoutthreshold の場合、エクストラネットからの認証要求を許可します 
- **Badpwdcount** >= **ExExtranetObservationWindow Etlockoutthreshold**と**badpasswordtime** +  < 現在の時刻である場合、AD FS はエクストラネットからの認証要求を拒否します。
- 悪意のあるアカウントのロックアウトを回避するには、アカウントロックアウトの**しきい値**と ExtranetObservationWindow > アカウントロックアウトの**リセットカウンター**を使用**して、** を < 確認する必要があります。


## <a name="additional-references"></a>その他の参照情報  
- [Active Directory フェデレーションサービス (AD FS) をセキュリティで保護するためのベストプラクティス](../../ad-fs/deployment/best-practices-securing-ad-fs.md)
- [管理者以外のユーザーへの AD FS Powershell コマンドレットのアクセスの委任](delegate-ad-fs-pshell-access.md)
- [Set-adfsproperties](https://technet.microsoft.com/itpro/powershell/windows/adfs/set-adfsproperties)

[AD FS の運用](../../ad-fs/AD-FS-2016-Operations.md)

    
