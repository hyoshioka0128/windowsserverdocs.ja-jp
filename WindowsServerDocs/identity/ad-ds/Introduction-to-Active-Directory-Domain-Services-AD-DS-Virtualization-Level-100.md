---
title: Active Directory Domain Services (AD DS) の安全な仮想化
description: Active Directory の USN ロールバックと安全な仮想化
ms.topic: article
ms.prod: windows-server
author: MicrosoftGuyJFlo
ms.author: joflore
manager: mtillman
ms.date: 03/22/2019
ms.technology: identity-adds
ms.assetid: 7a3114c8-bda8-49bb-83a8-4e04340ab221
ms.openlocfilehash: b9009e4688665e972531b1d38a5ecc92fa990556
ms.sourcegitcommit: d5e27c1f2f168a71ae272bebf8f50e1b3ccbcca3
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/23/2020
ms.locfileid: "86955624"
---
# <a name="safely-virtualizing-active-directory-domain-services-ad-ds"></a>Active Directory Domain Services (AD DS) の安全な仮想化

>適用先:Windows Server

Windows Server 2012 以降、AD DS では安全に仮想化できる機能の導入により、ドメイン コントローラーの仮想化がより強力にサポートされています。 この記事では、ドメイン コントローラーのレプリケーションにおける USN と InvocationID の役割について説明し、発生する可能性のある問題についていくつか説明します。

## <a name="update-sequence-number-and-invocationid"></a>シーケンス番号と InvocationID の更新

論理クロック ベースのレプリケーション スキーマに依存する分散ワークロードに、仮想環境は特異な課題をもたらします。 AD DS レプリケーションは、たとえば各ドメイン コントローラー上でトランザクションに割り当てられる、単調に増加する値 (USN や Update Sequence Number と呼ばれる) を使用します。 各ドメイン コントローラーのデータベース インスタンスにも、InvocationID と呼ばれる識別子が与えられます。 ドメイン コントローラーの InvocationID と USN が組み合わされて 1 つの一意の識別子となり、この識別子が各ドメイン コントローラー上で実行される各書き込みトランザクションに関連付けられます。この識別子はフォレスト内で一意である必要があります。

AD DS レプリケーションは、各ドメイン コントローラー上の InvocationID と USN を使用し、どの変更を他のドメイン コントローラーにレプリケートする必要があるかを判断します。 ドメイン コントローラーが認識しないままそのドメイン コントローラーが適時にロールバックされ、まったく異なるトランザクションのために USN が要求された場合、レプリケーションは収束しません。これは、その InvocationID に関係する限り、他のドメイン コントローラーは再使用された USN に関連付けられた更新を既に受け取っていると考えるためです。

たとえば、次の図は USN ロールバックが VDC2 で検出された場合に Windows Server 2008 R2 以前のオペレーティング システムで発生する一連のイベントを示しています。VDC2 は、仮想マシンで実行されているレプリケート先ドメイン コントローラーです。 この図では、以前にレプリケーション パートナーで認識された最新の USN 値が VDC2 から送信されたことがレプリケーション パートナーによって検出された時点で、VDC2 上で USN ロールバックが検出され、それによって、VDC2 のデータベースの正常でないロールバックが時間内に行われたことが示されます。

![USN ロールバックが検出されたときのイベントのシーケンス](../media/Introduction-to-Active-Directory-Domain-Services--AD-DS--Virtualization--Level-100-/ADDS_Exampleofhowreplicationcanbecomeinconsistent.png)

仮想マシン (VM) を利用すると、ハイパーバイザー管理者はドメイン コントローラーの USN (その論理クロック) を簡単にロールバックできます。たとえば、ドメイン コントローラーに認識されないままスナップショットを適用するという方法でロールバックできます。 USN と USN ロールバックの詳細については、「 [USN and USN Rollback (USN と USN ロールバック)](/previous-versions/windows/it-pro/windows-server-2008-R2-and-2008/dd363553(v=ws.10)#usn_and_usn_rollback)」を参照してください (このページには検出されない USN ロールバック インスタンスを示した他の図もあります)。

Windows Server 2012 以降、VM 生成 ID と呼ばれる識別子を公開するハイパーバイザー プラットフォーム上でホストされる AD DS 仮想ドメイン コントローラーは、VM スナップショットの適用によって仮想マシンが適時にロールバックされるかどうかを調べ、必要な安全対策を講じて AD DS 環境を保護します。 VM-GenerationID 設計では、ハイパーバイザー ベンダーに依存しないメカニズムを使用して、ゲスト仮想マシンのアドレス空間でこの識別子を公開します。このため、VM-GenerationID をサポートするあらゆるハイパーバイザーで、安全な仮想化が一貫して実現されます。 仮想マシン内で稼働しているサービスとアプリケーションでこの識別子を抽出することにより、仮想マシンが適時にロールバックされたかを調べることができます。

## <a name="effects-of-usn-rollback"></a>USN ロールバックの影響

USN ロールバックが発生した場合、オブジェクトと属性に対する変更が、以前に USN が表示されていたレプリケート先ドメイン コントローラーによって入力方向にレプリケートされることはありません。

これらのレプリケート先ドメイン コントローラーは最新のものであると考えられているため、レプリケーション エラーがディレクトリ サービスのイベント ログに報告されることも、監視および診断ツールによって監視されることもありません。

USN ロールバックは、任意のパーティション内の任意のオブジェクトまたは属性のレプリケーションに影響を与える可能性があります。 最もよく見られる副作用は、ロールバック ドメイン コントローラー上で作成されたユーザー アカウントとコンピューター アカウントが、1 つまたは複数のレプリケーション パートナーに存在しないことです。 または、ロールバック ドメイン コントローラー上で発生したパスワードの更新がレプリケーション パートナーに存在しません。

USN ロールバックを使用すると、Active Directory パーティション内のオブジェクトの種類がレプリケートされないようにすることができます。 これらのオブジェクトには次の種類があります。

* Active Directory レプリケーション トポロジとスケジュール
* フォレスト内のドメイン コントローラーの存在と、これらのドメイン コントローラーによって保持される役割
* フォレスト内のドメインおよびアプリケーション パーティションの存在
* セキュリティ グループとその現在のグループ メンバーシップの存在
* Active Directory 統合 DNS ゾーン内での DNS レコードの登録

USN ホールのサイズは、ユーザー、コンピューター、信頼、パスワード、およびセキュリティ グループに対する何百、何千、何万もの変更を表している可能性があります。 USN ホールは、復元されたシステム状態のバックアップが作成されたときに存在していた最大の USN 番号と、オフラインになる前にロールバックされたドメイン コントローラー上で作成された変更の発生回数との差によって定義されます。

## <a name="detecting-a-usn-rollback"></a>USN ロールバックの検出

USN ロールバックの検出は困難であるため、ドメイン コントローラーでは、呼び出し ID 内に対応する変更なしで、以前に確認された USN 番号がソース ドメイン コントローラーから宛先ドメイン コントローラーに送信されたときに、イベント 2095 が記録されます。

正しく復元されていないドメイン コントローラー上で Active Directory に対する一意の更新が発生するのを防ぐために、Net Logon サービスが一時停止されます。 Net Logon サービスが一時停止されている場合、ユーザーおよびコンピューター アカウントは、このような変更を送信方向にレプリケートしないドメイン コントローラー上でパスワードを変更できません。 同様に、Active Directory 管理ツールでは、Active Directory 内のオブジェクトを更新するときに、正常なドメイン コントローラーが優先されます。

ドメイン コントローラー上では、以下の条件が満たされた場合に次のようなイベント メッセージが記録されます。

* A source domain controller sends a previously acknowledged USN number to a destination domain controller. (ソース ドメイン コントローラーが、事前に確認された USN 番号を宛先ドメイン コントローラーに送信します。)
* There is no corresponding change in the invocation ID. (呼び出し ID 内に対応する変更がありません。)

これらのイベントは、ディレクトリ サービスのイベント ログ内でキャプチャできます。 ただし、管理者によって確認される前に上書きされる可能性があります。

USN ロールバックが発生したが、対応するイベントがイベント ログ内にないと思われる場合は、レジストリ内に DSA Not Writable エントリがないかどうかを確認してください。 このエントリは、USN ロールバックが発生したことを示す証拠を提供します。

```
HKEY_LOCAL_MACHINE\System\CurrentControlSet\Services\NTDS\Parameters
Registry entry: Dsa Not Writable
Value: 0x4
```

> [!WARNING]
> Dsa Not Writable レジストリ エントリの値を削除または手動で変更すると、ロールバック ドメイン コントローラーが完全にサポートされていない状態になります。 そのため、このような変更はサポートされていません。 具体的には、値を変更すると、USN ロールバック検出コードによって追加された検疫動作が削除されます。 ロールバック ドメイン コントローラー上の Active Directory パーティションは、同じ Active Directory フォレスト内の直接および推移的なレプリケーション パートナーと完全に一貫性がなくなります。

このレジストリ キーと解決手順の詳細については、サポート記事「[Active Directory レプリケーション エラー 8456 または 8457:"ソース/宛先サーバーは現在、レプリケーション要求を拒否しています"](https://support.microsoft.com/help/2023007/active-directory-replication-error-8456-or-8457-the-source-destination)」を参照してください。

## <a name="virtualization-based-safeguards"></a>仮想化ベースのセーフガード

ドメイン コントローラーのインストール時に、AD DS は最初に VM GenerationID 識別子を msDS-GenerationID 属性の一部として、そのデータベース内にあるドメイン コントローラーのコンピューター オブジェクト上に格納します (このデータベースは通常ディクショナリ情報ツリーまたは DIT と呼ばれる)。 VM GenerationID は、仮想マシン内部の Windows ドライバーによって単独に追跡されます。

管理者が以前のスナップショットから仮想マシンを復元する際には、仮想マシン ドライバー内の VM GenerationID の現在値が DIT 内の値と比較されます。

これら 2 つの値が異なる場合、invocationID がリセットされ、RID プールが破棄されます。この結果、USN の再使用が防止されます。 値が同じ場合、トランザクションは通常どおりコミットされます。

AD DS は、ドメイン コントローラーが再起動されるときにも毎回仮想マシンの VM GenerationID の現在値と DIT 内の値を比較します。それらの値が異なると、invocationID をリセットして RID プールを破棄し、新しい値を使用して DIT を更新します。 AD DS は、安全に復元する対策として、SYSVOL フォルダーの権限のない同期も実行します。 この結果、シャットダウンされた VM 上のスナップショットのアプリケーションまでセーフガードの範囲が広がります。 Windows Server 2012 で導入されたこれらのセーフガードを活用すると、AD DS 管理者には仮想化された環境でドメイン コントローラーを展開して管理するというユニークな利点があります。

次の図は、VM-GenerationID をサポートするハイパーバイザー上で Windows Server 2012 を実行している仮想化ドメイン コントローラー上で同一の USN ロールバックが検出される場合に仮想化セーフガードがどのように適用されるかを示しています。

![同じ USN ロールバックが検出されたときに適用されるセーフガード](../media/Introduction-to-Active-Directory-Domain-Services--AD-DS--Virtualization--Level-100-/ADDS_VDC_Exampleofhowsafeguardswork.gif)

この場合、ハイパーバイザーが VM-GenerationID 値の変化を検知した時点で仮想化セーフガードがトリガーされます。この結果、仮想化 DC の InvocationID がリセットされる (上の例では A から B にリセットされる) と共に、ハイパーバイザーによって保存された新しい値 (G2) と一致するように VM 上に保存されている VM-GenerationID 値が更新されます。 これらのセーフガードにより、レプリケーション時には両方のドメイン コントローラーが確実に収束されます。

Windows Server 2012 では、AD DS は VM-GenerationID を認識するハイパーバイザー上でホストされる仮想ドメイン コントローラーにセーフガードを適用します。具体的には、USN バブルや残留オブジェクトなどのレプリケーション問題を防止することで、仮想マシンの状態をロールバックする可能性のあるハイパーバイザー対応メカニズム (誤操作によるスナップショット適用など) が AD DS 環境を妨害しないようにします。

ドメイン コントローラーのバックアップに代わる手段として、仮想マシン スナップショットの適用によってドメイン コントローラーを復元するという方法はお勧めできません。 引き続き Windows Server バックアップまたは他の VSS ライター ベース バックアップ ソリューションを使用することをお勧めします。

> [!CAUTION]
> 偶発的に運用環境内のドメイン コントローラーがスナップショットに戻った場合には、アプリケーションのベンダーと、その仮想マシンでホストされているサービスのベンダーに問い合わせ、スナップショットを復元した後でこれらのプログラムの状態を検証する方法を確認してください。

詳細については、「 [Virtualized domain controller safe restore architecture](../ad-ds/get-started/virtual-dc/Virtualized-Domain-Controller-Architecture.md#BKMK_SafeRestoreArch)」を参照してください。

## <a name="recovering-from-a-usn-rollback"></a>USN ロールバックからの回復

USN ロールバックから回復するアプローチには、次の 2 つがあります。

* ドメインからドメイン コントローラーを削除する
* 正常なバックアップのシステム状態を復元する

### <a name="remove-the-domain-controller-from-the-domain"></a>ドメインからドメイン コントローラーを削除する

1. ドメイン コントローラーから Active Directory を削除して、強制的にスタンドアロン サーバーにします。
2. 降格されたサーバーをシャット ダウンします。
3. 正常なドメイン コントローラーで、降格されたドメイン コントローラーのメタデータをクリーン アップします。
4. 不適切に復元されたドメイン コントローラーに操作マスターの役割がホストされている場合は、これらの役割を正常なドメイン コントローラーに転送します。
5. 降格されたサーバーを再起動します。
6. 必要な場合は、スタンドアロン サーバーに Active Directory をもう一度インストールします。
7. ドメイン コントローラーが以前はグローバル カタログであった場合は、ドメイン コントローラーをグローバル カタログとして構成します。
8. ドメイン コントローラーが以前に操作マスターの役割をホストしていた場合は、操作マスターの役割をドメイン コントローラーに転送します。

### <a name="restore-the-system-state-of-a-good-backup"></a>正常なバックアップのシステム状態を復元する

このドメイン コントローラーに対して有効なシステム状態のバックアップが存在するかどうかを評価します。 ロールバックされたドメイン コントローラーが誤って復元される前に有効なシステム状態のバックアップが作成され、ドメイン コントローラーで上行われた最近の変更がそのバックアップに含まれている場合は、最新のバックアップからシステム状態を復元します。

バックアップのソースとしてスナップショットを使用することもできます。 または、「[適切なシステム状態データのバックアップが使用できない場合の仮想ドメイン コントローラーの復元](/previous-versions/windows/it-pro/windows-server-2008-r2-and-2008/dd363553%28v%3dws.10%29#restoring-a-virtual-domain-controller-when-an-appropriate-system-state-data-backup-is-not-available)」セクションの手順を使用して、データベース自体に新しい呼び出し ID を与えるように設定することもできます

## <a name="next-steps"></a>次の手順

* 仮想化ドメイン コントローラーのトラブルシューティングにの詳細については、「 [Virtualized Domain Controller Troubleshooting](../ad-ds/manage/virtual-dc/Virtualized-Domain-Controller-Troubleshooting.md)」を参照してください。
* [Windows タイムサービス (W32Time) の詳細情報](../../networking/windows-time-service/windows-time-service-top.md)
