---
title: Active Directory Domain Services (AD DS) を安全に仮想化
description: USN のロールバックと Active Directory の安全な仮想化
ms.topic: article
ms.prod: windows-server-threshold
author: MicrosoftGuyJFlo
ms.author: joflore
manager: mtillman
ms.date: 03/22/2019
ms.technology: identity-adds
ms.assetid: 7a3114c8-bda8-49bb-83a8-4e04340ab221
ms.openlocfilehash: aa84e09e8a958193fee82c7b9c03cd1dca910c55
ms.sourcegitcommit: 2977c707a299929c6ab0d1e0adab2e1c644b8306
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/24/2019
ms.locfileid: "63684179"
---
# <a name="safely-virtualizing-active-directory-domain-services-ad-ds"></a>Active Directory Domain Services (AD DS) を安全に仮想化

>適用先:Windows Server

Windows Server 2012 以降では、AD DS ドメイン コント ローラーを安全に仮想化できる機能を導入することで仮想化のサポートが強化を提供します。 この記事では、ドメイン コント ローラーの複製における Usn と InvocationIDs の役割を説明し、発生することがいくつかの潜在的な問題について説明します。

## <a name="update-sequence-number-and-invocationid"></a>更新シーケンス番号と InvocationID

論理クロック ベースのレプリケーション スキーマに依存する分散ワークロードに、仮想環境は特異な課題をもたらします。 AD DS レプリケーションは、たとえば各ドメイン コントローラー上でトランザクションに割り当てられる、単調に増加する値 (USN や Update Sequence Number と呼ばれる) を使用します。 各ドメイン コント ローラーのデータベース インスタンスは、InvocationID と呼ばれる、id とも付けられます。 ドメイン コントローラーの InvocationID と USN が組み合わされて 1 つの一意の識別子となり、この識別子が各ドメイン コントローラー上で実行される各書き込みトランザクションに関連付けられます。この識別子はフォレスト内で一意である必要があります。

AD DS レプリケーションは、各ドメイン コントローラー上の InvocationID と USN を使用し、どの変更を他のドメイン コントローラーにレプリケートする必要があるかを判断します。 その他のドメイン コント ローラーは、更新プログラムを既に受け取っていると思われるために、レプリケーションが収束しない場合は、ドメイン コント ローラーがドメイン コント ローラーに認識外の特定のロールバックされ、まったく異なるトランザクションの USN が再利用、その InvocationID のコンテキストで再使用された USN に関連付けられました。

たとえば、次の図は USN ロールバックが VDC2 で検出された場合に Windows Server 2008 R2 以前のオペレーティング システムで発生する一連のイベントを示しています。VDC2 は、仮想マシンで実行されているレプリケート先ドメイン コントローラーです。 この図で USN ロールバックの検出 VDC2 で検出すると発生レプリケーション パートナー VDC2 が VDC2 のデータベースがロールバックことで時間を示すレプリケーション パートナーがこれまで見てきたが、最新の USN 値を送信します。不適切です。

![USN ロールバックが検出されたときのイベントのシーケンス](../media/Introduction-to-Active-Directory-Domain-Services--AD-DS--Virtualization--Level-100-/ADDS_Exampleofhowreplicationcanbecomeinconsistent.png)

仮想マシン (VM) 簡単ハイパーバイザー管理者は、ロールバック ドメイン コント ローラーの Usn (その論理クロック) によって、たとえば、ドメイン コント ローラーに認識スナップショットを適用します。 USN と USN ロールバックの詳細については、「 [USN and USN Rollback (USN と USN ロールバック)](https://technet.microsoft.com/library/virtual_active_directory_domain_controller_virtualization_hyperv(WS.10).aspx#usn_and_usn_rollback)」を参照してください (このページには検出されない USN ロールバック インスタンスを示した他の図もあります)。

Windows Server 2012 以降では、VM 生成 ID と呼ばれる識別子を公開するハイパーバイザー プラットフォームでホストされる AD DS 仮想ドメイン コント ローラー検出し、仮想マシンがロールバックされた場合は、AD DS 環境を保護するために必要な安全対策を施すVM スナップショットのアプリケーションでの時間。 VM-GenerationID 設計では、ハイパーバイザー ベンダーに依存しないメカニズムを使用して、ゲスト仮想マシンのアドレス空間でこの識別子を公開します。このため、VM-GenerationID をサポートするあらゆるハイパーバイザーで、安全な仮想化が一貫して実現されます。 仮想マシン内で稼働しているサービスとアプリケーションでこの識別子を抽出することにより、仮想マシンが適時にロールバックされたかを調べることができます。

## <a name="effects-of-usn-rollback"></a>USN ロールバックの効果

USN ロールバックが発生すると、オブジェクトや属性に対する変更は受信 USN が認識されていた送信先ドメイン コント ローラーによってレプリケート。

これらの変換先のドメイン コント ローラーでは、これらが最新の状態と思われる、ために、ディレクトリ サービス イベント ログで、または監視と診断ツールによって、レプリケーション エラーは報告されません。

USN ロールバックの任意のオブジェクトまたは任意のパーティションで属性のレプリケーションに影響を与える可能性があります。 最も頻繁に観察の副作用は、ユーザー アカウントと、ロールバック ドメイン コント ローラー上に作成されるコンピューター アカウントが存在しないことの 1 つまたは複数のレプリケーション パートナーです。 または、ロールバック ドメイン コント ローラー上で発生したパスワードの更新は、レプリケーション パートナーには存在しません。

USN のロールバックは、レプリケートから任意の Active Directory パーティションで任意のオブジェクト型を回避できます。 オブジェクトの種類を以下に示します。

* Active Directory レプリケーション トポロジとスケジュール
* フォレストとドメイン コント ローラーを保持するロールのドメイン コント ローラーが存在します。
* フォレストのドメインとアプリケーションのパーティションが存在します。
* セキュリティ グループとその現在のグループ メンバシップが存在します。
* Active Directory 統合 DNS ゾーンで DNS レコードは登録

USN 穴のサイズは、ユーザー、コンピューター、信頼、パスワード、およびセキュリティ グループに数百、何千、または変更の万もを表す可能性があります。 USN の穴は、最大 USN 数、復元されたシステム状態バックアップが行われた、送信元の数が変更したときに存在していたオフラインが行われる前に、ロールバック ドメイン コント ローラーで作成された間の差によって定義されます。

## <a name="detecting-a-usn-rollback"></a>USN ロールバックの検出

ドメイン コント ローラーが 2095 呼び出し ID に対応する変更なしの移行先ドメイン コント ローラーに、ソース ドメイン コント ローラーが以前確認済みの usn を送信するとのイベントをログ記録、USN ロールバックが検出を困難にあるため、

防ぐために一意の Active Directory に不適切に復元されたドメイン コント ローラーに作成する元の更新プログラム、Net Logon サービスが一時停止します。 Net Logon サービスが一時停止しているユーザーおよびコンピューター アカウントはない送信のレプリケーションなどの変更をドメイン コント ローラーでパスワードを変更できません。 同様に、Active Directory 管理ツールは、Active Directory 内のオブジェクトへの更新を行ったときに、正常なドメイン コント ローラーが優先されます。

ドメイン コント ローラーで、次の条件に該当する場合、次のようなイベント メッセージが記録されます。

* ソース ドメイン コント ローラーでは、移行先ドメイン コント ローラーを以前に受信確認済みの usn を送信します。
* 呼び出し ID に対応する変更はありません。

ディレクトリ サービス イベント ログでは、これらのイベントをキャプチャすることがあります。 ただし、管理者が確認する前に、このそれらを上書き可能性があります。

疑いがある場合は、USN ロールバックが発生しましたが、イベント ログ、レジストリの DSA いない書き込み可能なエントリを確認、対応するイベントに表示されません。 このエントリは、USN ロールバックが発生したこと、法的証拠を提供します。

```
HKEY_LOCAL_MACHINE\System\CurrentControlSet\Services\NTDS\Parameters
Registry entry: Dsa Not Writable
Value: 0x4
```

> [!WARNING]
> 削除または Dsa いない書き込み可能なレジストリ エントリの値を手動で変更は、ロールバック ドメイン コント ローラーを完全にサポートされていない状態になります。 そのため、このような変更はサポートされていません。 具体的には、値を変更するには、USN ロールバックの検出コードによって追加された検疫動作が削除されます。 ロールバック ドメイン コント ローラー上の Active Directory パーティションは同じ Active Directory フォレスト内の直接および推移的レプリケーション パートナーで一貫性のある永続的になります。

このレジストリ キーと解決手順の詳細については、サポート記事にあります[Active Directory レプリケーション エラー 8456 または 8457。"ソース |現在、移行先サーバーはレプリケーション要求を拒否して"](https://support.microsoft.com/help/2023007/active-directory-replication-error-8456-or-8457-the-source-destination)します。

## <a name="virtualization-based-safeguards"></a>ベースの仮想化セーフガード

最初に AD DS はドメイン コント ローラーのインストール時に、(多くの場合、ディレクトリ情報ツリーまたは DIT と呼ばれます)、データベース内のドメイン コント ローラーのコンピューター オブジェクトの Msds-generationid 属性の一部として VM GenerationID 識別子を格納します。 VM GenerationID は、仮想マシン内部の Windows ドライバーによって単独に追跡されます。

管理者が以前のスナップショットから仮想マシンを復元する際には、仮想マシン ドライバー内の VM GenerationID の現在値が DIT 内の値と比較されます。

これら 2 つの値が異なる場合、invocationID がリセットされ、RID プールが破棄されます。この結果、USN の再使用が防止されます。 値が同じ場合、トランザクションは通常どおりコミットされます。

AD DS は、ドメイン コントローラーが再起動されるときにも毎回仮想マシンの VM GenerationID の現在値と DIT 内の値を比較します。それらの値が異なると、invocationID をリセットして RID プールを破棄し、新しい値を使用して DIT を更新します。 AD DS は、安全に復元する対策として、SYSVOL フォルダーの権限のない同期も実行します。 この結果、シャットダウンされた VM 上のスナップショットのアプリケーションまでセーフガードの範囲が広がります。 Windows Server 2012 で導入されたこれらのセーフガードには、展開と管理仮想化環境内のドメイン コント ローラーの独自のメリットを享受する AD DS 管理者が有効にします。

次の図は、Vm-generationid をサポートするハイパーバイザー上で Windows Server 2012 を実行する仮想化ドメイン コント ローラーの同一の USN ロールバックが検出されたときに仮想化セーフガードを適用する方法を示します。

![同一の USN ロールバックが検出されたときに適用される保護機能](../media/Introduction-to-Active-Directory-Domain-Services--AD-DS--Virtualization--Level-100-/ADDS_VDC_Exampleofhowsafeguardswork.gif)

この場合、ハイパーバイザーが VM-GenerationID 値の変化を検知した時点で仮想化セーフガードがトリガーされます。この結果、仮想化 DC の InvocationID がリセットされる (上の例では A から B にリセットされる) と共に、ハイパーバイザーによって保存された新しい値 (G2) と一致するように VM 上に保存されている VM-GenerationID 値が更新されます。 これらのセーフガードにより、レプリケーション時には両方のドメイン コントローラーが確実に収束されます。

Windows Server 2012 では、AD DS は Vm-generationid を認識するハイパーバイザーでホストされている仮想ドメイン コント ローラーにセーフガードを適用およびのスナップショットまたは他のようなハイパーバイザー対応メカニズム仮想ロールバックの可能性のある、偶発的なアプリケーションを確実マシンの状態が (USN バブルなどのレプリケーションの問題の防止や残留オブジェクト) を AD DS 環境を妨害しません。

ドメイン コント ローラーをバックアップする代替手段としては、仮想マシンのスナップショットを適用することで、ドメイン コント ローラーを復元しないでください。 引き続き Windows Server バックアップまたは他の VSS ライター ベース バックアップ ソリューションを使用することをお勧めします。

> [!CAUTION]
> 運用環境でドメイン コント ローラーは、スナップショットに戻す、誤って場合は、アプリケーション、およびガイダンスについては後にこれらのプログラムの状態を検証する場合にその仮想マシンでホストされるサービスの仕入先を参照することをお勧めスナップショットの復元。

詳細については、「[仮想化ドメイン コントローラーの安全な復元アーキテクチャ](../ad-ds/get-started/virtual-dc/Virtualized-Domain-Controller-Architecture.md#BKMK_SafeRestoreArch)」を参照してください。

## <a name="recovering-from-a-usn-rollback"></a>USN ロールバックから回復します。

USN ロールバックから回復する 2 つの方法はあります。

* ドメイン コント ローラーをドメインから削除します。
* システム状態、適切なバックアップを復元します。

### <a name="remove-the-domain-controller-from-the-domain"></a>ドメイン コント ローラーをドメインから削除します。

1. Active Directory を強制するスタンドアロン サーバーにするには、ドメイン コント ローラーから削除します。
2. 降格されたサーバーをシャット ダウンします。
3. 正常なドメイン コント ローラーで、降格されたドメイン コント ローラーのメタデータをクリーンアップします。
4. 場合は、不適切に復元されたドメイン コント ローラーが操作マスターの役割、正常なドメイン コント ローラーにこれらの役割を転送します。
5. 降格されたサーバーを再起動します。
6. 必要がある場合、再度スタンドアロン サーバーに Active Directory をインストールします。
7. ドメイン コント ローラーが、以前にグローバル カタログであった場合は、グローバル カタログ ドメイン コント ローラーを構成します。
8. 場合は、ドメイン コント ローラーには、操作マスターの役割がホストされていた、操作マスターの役割を再びドメイン コント ローラーに転送します。

### <a name="restore-the-system-state-of-a-good-backup"></a>システム状態、適切なバックアップを復元します。

このドメイン コント ローラーの有効なシステム状態のバックアップが存在するかどうかを評価します。 ロールバック ドメイン コント ローラーが正しく復元し、バックアップには、ドメイン コント ローラーに加えられた最近の変更が含まれています。 前に、有効なシステム状態のバックアップが行われた場合は、最新のバックアップからシステム状態を復元します。

スナップショット バックアップのソースとして使用することもできます。 自体に、セクションの手順を使用する、新しい起動 ID を提供するデータベースを設定することも[適切なシステム状態データのバックアップが利用できない場合は、仮想ドメイン コント ローラーを復元します。](https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2008-R2-and-2008/dd363553%28v%3dws.10%29#restoring-a-virtual-domain-controller-when-an-appropriate-system-state-data-backup-is-not-available)

## <a name="next-steps"></a>次のステップ

* 仮想化ドメイン コントローラーのトラブルシューティングにの詳細については、「 [Virtualized Domain Controller Troubleshooting](../ad-ds/manage/virtual-dc/Virtualized-Domain-Controller-Troubleshooting.md)」を参照してください。
* [Windows タイム サービス (W32Time) に関する詳細情報](../../networking/windows-time-service/windows-time-service-top.md)
