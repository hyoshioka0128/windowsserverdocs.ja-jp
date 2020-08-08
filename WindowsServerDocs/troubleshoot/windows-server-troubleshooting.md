---
title: Windows Server のトラブルシューティング
description: Windows Server の問題に関するトラブルシューティング記事へのリンクを取得する
ms.date: 1/24/2020
author: kaushika-msft
ms.author: kaushika
ms.openlocfilehash: fbebb44d687bfeb5660eab3b81c164f8cdf6196d
ms.sourcegitcommit: 68444968565667f86ee0586ed4c43da4ab24aaed
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/07/2020
ms.locfileid: "87996723"
---
# <a name="troubleshooting-windows-server-components"></a>Windows Server コンポーネントのトラブルシューティング

> [!TIP]
> 以前のバージョンの Windows Server に関する情報をお探しの場合は、 docs.microsoft.com の他の [Windows Server ライブラリ](/previous-versions/windows/)を参照してください。
>
> また、[このサイトで検索して](/search/index?dataSource=previousVersions&search=Windows+Server)、具体的な情報を確認することもできます。

Microsoft は、Windows Server の両方の更新プログラムを定期的にリリースします。 お客様のサーバーでセキュリティ更新プログラムなどの今後の更新プログラムを受信できることを確認するには、サーバーを最新の状態に維持する必要があります。 リリースされた更新プログラムの完全なリストについては、「[Windows 10 および Windows Server 2016 の更新履歴](https://support.microsoft.com/help/4000825/windows-10-windows-server-2016-update-history)」をご覧ください。

このセクションには、Windows Server の問題を解決するのに役立つ高度なトラブルシューティングのトピックとリンクが含まれています。 追加のトピックが利用可能になると追加されます。

## <a name="troubleshoot-activation"></a>アクティブ化のトラブルシューティング

- [Windows ボリューム ライセンス認証のトラブルシューティング](../get-started/activation-troubleshooting-guide.md)
- [KMS のトラブルシューティングに関するガイドライン](../get-started/activation-troubleshoot-kms-general.md)
- [ボリューム ライセンス認証情報を取得するための Slmgr.vbs オプション](../get-started/activation-slmgr-vbs-options.md)
- [Windows ライセンス認証のエラー コードの解決](../get-started/activation-error-codes.md)
- [KMS ライセンス認証の既知の問題](../get-started/activation-troubleshoot-kms-issues.md)
- [MAK ライセンス認証の既知の問題](../get-started/activation-troubleshoot-mak-issues.md)
- [DNS に関連するライセンス認証の問題のトラブルシューティングに関するガイドライン](../get-started/common-troubleshooting-procedures-kms-dns.md)
- [Tokens.dat ファイルの再構築](../get-started/activation-rebuild-tokens-dat-file.md)
- [ADBA クライアントのトラブルシューティング](../get-started/activation-troubleshoot-adba-clients.md)

## <a name="troubleshoot-startup-and-restart"></a>スタートアップと再起動のトラブルシューティング

- [Windows のスタートアップの高度なトラブルシューティング](/windows/client-management/troubleshoot-windows-startup)
- [64 ビット版 Windows 用の適切なページ ファイルのサイズを確認する方法](/windows/client-management/determine-appropriate-page-file-size)
- [カーネルまたは完全なクラッシュダンプを生成する](/windows/client-management/generate-kernel-or-complete-crash-dump)
- [ページファイルの概要](/windows/client-management/introduction-page-file)
- [Windows でのシステムエラーと回復オプションの構成](/windows/client-management/system-failure-recovery-options)
- [Windows の起動の問題の高度なトラブルシューティング](/windows/client-management/advanced-troubleshooting-boot-problems)
- [Windows ベースのコンピューターのフリーズの高度なトラブルシューティング](/windows/client-management/troubleshoot-windows-freeze)
- [Stop エラーまたはブルー スクリーン エラーの高度なトラブルシューティング](/windows/client-management/troubleshoot-stop-errors)
- [Stop エラー 7B または Inaccessible_Boot_Device の高度なトラブルシューティング](/windows/client-management/troubleshoot-inaccessible-boot-device)
- [イベント ID 41 の高度なトラブルシューティング "システムは最初に正常にシャットダウンされずに再起動されました"](/windows/client-management/troubleshoot-event-id-41-restart)
- [Box の Broadcom ネットワークアダプタードライバーを更新すると停止エラーが発生する](/windows/client-management/troubleshoot-stop-error-on-broadcom-driver-update)

## <a name="troubleshoot-ad-forest-recovery"></a>AD フォレストの回復に関するトラブルシューティング

- [AD フォレストの回復 - FAQ](../identity/ad-ds/manage/ad-forest-recovery-faq.md)

## <a name="troubleshoot-ad-replication"></a>AD レプリケーションのトラブルシューティング

- [Active Directory レプリケーションの問題のトラブルシューティングに関するページ](../identity/ad-ds/manage/troubleshoot/troubleshooting-active-directory-replication-problems.md)
- [仮想化ドメイン コントローラーのトラブルシューティング](../identity/ad-ds/manage/virtual-dc/virtualized-domain-controller-troubleshooting.md)
- [ドメイン コントローラーの展開のトラブルシューティング](../identity/ad-ds/deploy/troubleshooting-domain-controller-deployment.md)
- [トラブルシューティング用にコンピューターを構成する](../identity/ad-ds/manage/troubleshoot/configuring-a-computer-for-troubleshooting.md)

## <a name="troubleshoot-ad-fs"></a>AD FS のトラブルシューティング

- [AD FS のトラブルシューティング](../identity/ad-fs/troubleshooting/ad-fs-tshoot-overview.md)
- [AD FS のトラブルシューティング-イベントとログの監査](../identity/ad-fs/troubleshooting/ad-fs-tshoot-logging.md)
- [AD FS のトラブルシューティング-SQL 接続](../identity/ad-fs/troubleshooting/ad-fs-tshoot-sql.md)
- [AD FS のトラブルシューティング-要求の発行](../identity/ad-fs/troubleshooting/ad-fs-tshoot-claims-issuance.md)
- [AD FS トラブルシューティング-ループ検出](../identity/ad-fs/troubleshooting/ad-fs-tshoot-loop.md)
- [AD FS のトラブルシューティング-証明書](../identity/ad-fs/troubleshooting/ad-fs-tshoot-certs.md)
- [AD FS のトラブルシューティング-Fiddler](../identity/ad-fs/troubleshooting/ad-fs-tshoot-fiddler.md)
- [AD FS のトラブルシューティング-Fiddler](../identity/ad-fs/troubleshooting/ad-fs-tshoot-fiddler-ws-fed.md)
- [AD FS のトラブルシューティング-要求規則](../identity/ad-fs/troubleshooting/ad-fs-tshoot-claims-rules.md)
- [AD FS トラブルシューティング-統合 Windows 認証](../identity/ad-fs/troubleshooting/ad-fs-tshoot-iwa.md)
- [AD FS のトラブルシューティング-Azure AD](../identity/ad-fs/troubleshooting/ad-fs-tshoot-azure.md)
- [AD FS の FAQ](../identity/ad-fs/overview/ad-fs-faq.md)
- [AD FS ヘルプ診断アナライザー](../identity/ad-fs/troubleshooting/ad-fs-diagnostics-analyzer.md)

## <a name="troubleshoot-aovpn"></a>Vpn のトラブルシューティング

- [Always On VPN のトラブルシューティング](../remote/remote-access/vpn/always-on-vpn/deploy/always-on-vpn-deploy-troubleshooting.md)

## <a name="troubleshoot-converged-nic"></a>収束 NIC のトラブルシューティング

- [収束 NIC 構成のトラブルシューティング](../networking/technologies/conv-nic/cnic-app-troubleshoot.md)

## <a name="troubleshoot-dfsr"></a>DFSR のトラブルシューティング

- [DFS レプリケーション:よく寄せられる質問 (FAQ)](../storage/dfs-replication/dfsr-faq.md)

## <a name="troubleshoot-directaccess"></a>DirectAccess のトラブルシューティング

- [DirectAccess のトラブルシューティング](../remote/remote-access/directaccess/troubleshooting-directaccess.md)

## <a name="troubleshoot-disk-management"></a>ディスク管理のトラブルシューティング

- [ディスクの管理のトラブルシューティング](../storage/disk-management/troubleshooting-disk-management.md)

## <a name="troubleshoot-dns"></a>DNS のトラブルシューティング

- [ドメインネームシステム (DNS) に関する問題のトラブルシューティング](../networking/dns/troubleshoot/troubleshoot-dns-data-collection.md)
- [DNS クライアントのトラブルシューティング](../networking/dns/troubleshoot/troubleshoot-dns-client.md)
- [DNS クライアントでの DNS クライアント側キャッシュの無効化](../networking/dns/troubleshoot/disable-dns-client-side-caching.md)
- [DNS サーバーのトラブルシューティング](../networking/dns/troubleshoot/troubleshoot-dns-server.md)

## <a name="troubleshoot-failover-cluster"></a>フェールオーバークラスターのトラブルシューティング

- [Windows エラー報告を使用したフェールオーバー クラスターのトラブルシューティング](../failover-clustering/troubleshooting-using-wer-reports.md)
- [クラスター対応更新についてよく寄せられる質問](../failover-clustering/cluster-aware-updating-faq.md)
- [イベント ID 1135 のクラスターの問題のトラブルシューティング](./troubleshooting-cluster-event-id-1135.md)
- [アクティブなフェールオーバークラスターのメンバーシップからノードが削除されるという問題が発生する](./problem-nodes-failover-cluster.md)
- [VMWare ESX のフェールオーバークラスターメンバーシップから削除されているノード](./nodes-failover-cluster-vmware.md)
- [IaaS と SQL AlwaysOn - フェールオーバー クラスター ネットワークのしきい値の調整](./iaas-sql-failover-cluster.md)

## <a name="troubleshoot-dhcp"></a>DHCP のトラブルシューティング

- [動的ホスト構成プロトコル (DHCP) のトラブルシューティングガイド](./troubleshoot-dhcp-issue.md)
- [DHCP (動的ホスト構成プロトコル) の基本](./dynamic-host-configuration-protocol-basics.md)
- [DHCP のトラブルシューティングに関する一般的なガイダンス](./general-guidance-to-troubleshoot-dhcp.md)
- [DHCP サーバーなしで TCP/IP 自動アドレス指定を使用する方法](./how-to-use-automatic-tcpip-addressing-without-a-dh.md)
- [DHCP クライアントでの問題のトラブルシューティング](./troubleshoot-problems-on-dhcp-client.md)
- [DHCP サーバーでの問題のトラブルシューティング](./troubleshoot-problems-on-dhcp-server.md)

## <a name="troubleshoot-fsrm"></a>FSRM のトラブルシューティング

- [ファイル サーバー リソース マネージャーのトラブルシューティング](../storage/fsrm/troubleshooting-file-server-resource-manager.md)

## <a name="troubleshoot-guarded-fabric"></a>保護されたファブリックのトラブルシューティング

- [保護されたファブリック診断ツールを使用したトラブルシューティング](../security/guarded-fabric-shielded-vm/guarded-fabric-troubleshoot-diagnostics.md)
- [ホストガーディアンサービスのトラブルシューティング](../security/guarded-fabric-shielded-vm/guarded-fabric-troubleshoot-hgs.md)
- [ホストガーディアンサービスのトラブルシューティング](../security/guarded-fabric-shielded-vm/guarded-fabric-troubleshoot-hosts.md)

## <a name="troubleshoot-multi-site-ras"></a>マルチサイト RAS のトラブルシューティング

- [マルチサイト有効化のトラブルシューティング](../remote/remote-access/ras/multisite/troubleshoot/troubleshooting-enabling-multisite.md)
- [エントリポイント追加のトラブルシューティング](../remote/remote-access/ras/multisite/troubleshoot/troubleshooting-adding-entry-points.md)
- [エントリ ポイント ドメイン コントローラー設定のトラブルシューティング](../remote/remote-access/ras/multisite/troubleshoot/troubleshooting-setting-the-entry-point-domain-controller.md)
- [Web プローブ URL のトラブルシューティング](../remote/remote-access/ras/multisite/troubleshoot/troubleshooting-web-probe-urls.md)

## <a name="troubleshoot-nano-server"></a>Nano Server のトラブルシューティング

- [Nano Server のトラブルシューティング](../get-started/troubleshooting-nano-server.md)

## <a name="troubleshoot-nic-teaming"></a>NIC チーミングのトラブルシューティング

- [NIC チーミングのトラブルシューティング](../networking/technologies/nic-teaming/troubleshooting-nic-teaming.md)

## <a name="troubleshoot-otp-authentication"></a>OTP 認証のトラブルシューティング

- [認証の問題のトラブルシューティング](../remote/remote-access/ras/otp/troubleshoot/troubleshooting-authentication-issues.md)
- [OTP の有効化のトラブルシューティング](../remote/remote-access/ras/otp/troubleshoot/troubleshooting-enabling-otp.md)

## <a name="troubleshoot-qos"></a>QoS のトラブルシューティング

- [QoS に関してよく寄せられる質問](../networking/technologies/qos/qos-policy-faq.md)

## <a name="troubleshoot-s2d"></a>S2D のトラブルシューティング

- [記憶域スペースダイレクトのトラブルシューティング](../storage/storage-spaces/troubleshooting-storage-spaces.md)
- [記憶域スペースダイレクトに関してよく寄せられる質問](../storage/storage-spaces/storage-spaces-direct-faq.md)
- [正常性と動作状態の記憶域スペースダイレクト](../storage/storage-spaces/storage-spaces-states.md)
- [記憶域スペースダイレクトを使用した診断データの収集](../storage/storage-spaces/data-collection.md)
- [Windows での記憶域クラス メモリ (NVDIMM-N) の正常性管理](../storage/storage-spaces/storage-class-memory-health.md)

## <a name="troubleshoot-sdn"></a>SDN のトラブルシューティング

- [SDN のトラブルシューティング](../networking/sdn/troubleshoot/troubleshoot-software-defined-networking.md)
- [Windows Server ソフトウェア定義ネットワーク スタックのトラブルシューティング](../networking/sdn/troubleshoot/troubleshoot-windows-server-software-defined-networking-stack.md)

## <a name="troubleshoot-rds-session-connectivity"></a>RDS セッション接続のトラブルシューティング

- [リモート デスクトップ接続の一般的なトラブルシューティング](../remote/remote-desktop-services/troubleshoot/rdp-error-general-troubleshooting.md)
- [クライアントが接続できず、クラスが登録されていないというエラーが発生する](../remote/remote-desktop-services/troubleshoot/rdp-error-class-not-registered.md)
- [クライアントが接続できず、利用可能なライセンスがないというエラーが表示される](../remote/remote-desktop-services/troubleshoot/rdp-error-no-licenses-available.md)
- [ユーザーが認証できない、または 2 回認証する必要がある](../remote/remote-desktop-services/troubleshoot/cannot-authenticate-or-must-authenticate-twice.md)
- [接続時に、ユーザーがリモートデスクトップサービスを受信しています。現在ビジー状態です](../remote/remote-desktop-services/troubleshoot/remote-desktop-service-currently-busy.md)
- [リモート デスクトップ クライアントが切断され、同じセッションに再接続できない](../remote/remote-desktop-services/troubleshoot/rdp-client-disconnects-cannot-reconnect-same-session.md)
- [リモート ラップトップがワイヤレス ネットワークから切断される](../remote/remote-desktop-services/troubleshoot/remote-laptop-disconnects-wireless-network.md)
- [リモート デスクトップ接続時のパフォーマンスの低下またはアプリケーションの問題](../remote/remote-desktop-services/troubleshoot/poor-performance-or-application-problems.md)

## <a name="troubleshoot-shielded-vm"></a>シールドされた VM のトラブルシューティング

- [シールドされた Vm のトラブルシューティング](../security/guarded-fabric-shielded-vm/guarded-fabric-troubleshoot-shielded-vms.md)

## <a name="troubleshoot-software-restriction-policies"></a>ソフトウェアの制限のポリシーのトラブルシューティング

- [ソフトウェア制限ポリシーのトラブルシューティング](../identity/software-restriction-policies/troubleshoot-software-restriction-policies.md)

## <a name="troubleshoot-storage-migration"></a>記憶域の移行のトラブルシューティング

- [記憶域移行サービスの既知の問題](../storage/storage-migration-service/known-issues.md)
- [記憶域移行サービスに関してよく寄せられる質問 (FAQ)](../storage/storage-migration-service/faq.md)

## <a name="troubleshoot-storage-replica"></a>記憶域レプリカのトラブルシューティング

- [記憶域レプリカに関する既知の問題](../storage/storage-replica/storage-replica-known-issues.md)
- [記憶域レプリカについてよく寄せられる質問](../storage/storage-replica/storage-replica-frequently-asked-questions.md)

## <a name="troubleshoot-user-profiles"></a>ユーザー プロファイルのトラブルシューティング

- [イベントを使用したユーザー プロファイルのトラブルシューティング](../storage/folder-redirection/troubleshoot-user-profiles-events.md)

## <a name="troubleshoot-vrss"></a>VRSS のトラブルシューティング

- [vRSS に関してよく寄せられる質問](../networking/technologies/vrss/vrss-faq.md)

## <a name="troubleshoot-webproxy"></a>WebProxy のトラブルシューティング

- [Web アプリケーション プロキシのトラブルシューティング](../remote/remote-access/web-application-proxy/troubleshooting-web-application-proxy.md)

## <a name="troubleshoot-windows-admin-center"></a>Windows Admin Center のトラブルシューティング

- [Windows Admin Center の一般的なトラブルシューティングの手順](../manage/windows-admin-center/support/troubleshooting.md)
- [Windows Admin Center の既知の問題](../manage/windows-admin-center/support/known-issues.md)
- [Windows Admin Center についてよく寄せられる質問](../manage/windows-admin-center/understand/faq.md)