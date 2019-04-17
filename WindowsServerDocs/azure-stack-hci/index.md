---
title: Azure のスタック HCI 概要
description: Azure スタック HCI は、必要に応じてクラウド ベースのバックアップ、サイト回復用の Azure サービスへの接続を使用するハイパーコンバージドの Windows Server 2019 クラスターは、仮想化されたワークロード、オンプレミスを実行するハードウェアを検証します。 Azure のスタック HCI ソリューションでは、Microsoft が検証済みのハードウェアを使用して、最適なパフォーマンスと信頼性を確認して、NVMe ドライブ、永続的なメモリ、およびリモート ダイレクト メモリ アクセス (RDMA) ネットワークなどのテクノロジのサポートが含まれます。
ms.technology: storage
ms.topic: article
author: jasongerend
ms.author: jgerend
ms.localizationpriority: medium
ms.prod: windows-server-threshold
ms.date: 03/26/2019
---

# Azure のスタック HCI 概要

>適用対象: Windows Server 2019

Azure スタック HCI は、必要に応じてクラウド ベースのバックアップ、サイト回復用の Azure サービスへの接続を使用するハイパーコンバージドの Windows Server 2019 クラスターは、仮想化されたワークロード、オンプレミスを実行するハードウェアを検証します。 Azure のスタック HCI ソリューションでは、Microsoft が検証済みのハードウェアを使用して、最適なパフォーマンスと信頼性を確認して、NVMe ドライブ、永続的なメモリ、およびリモート ダイレクト メモリ アクセス (RDMA) ネットワークなどのテクノロジのサポートが含まれます。

## Azure Stack ファミリ

Azure スタック HCI、Azure の一部であるし、記憶域、およびネットワークのソフトウェアとして Azure Stack、同じソフトウェア定義を使用して、Azure Stack ファミリを計算します。 さまざまなソリューションの簡単な概要を次に示します。

- [Azure](https://azure.microsoft.com)パブリック クラウド サービスを使用
- [Azure Stack](https://azure.microsoft.com/overview/azure-stack)の動作クラウド、オンプレミスのサービス
- [Azure スタック HCI](https://azure.microsoft.com/overview/azure-stack/hci) - 仮想化アプリ、オンプレミス、Azure へのオプションの接続での実行

![仮想化アプリケーション オンプレミスの azure と Azure スタック HCI の実行中に、クラウド サービスを実行する Azure Stack](media/azure-and-azure-stack-family.png)

詳細について説明します。

- 、2019 年 3 月 28 日、[ハイブリッド クラウド仮想イベント](https://info.microsoft.com/ww-landing-building-a-successful-hybrid-cloud-strategy.html)に登録します。
- 詳しくは、 [Azure スタック HCI](https://azure.microsoft.com/overview/azure-stack/hci)ソリューションの web サイト、について説明します。
- マイクロソフトのエキスパート Jeff Woolsey と Vijay Tewari[新しい Azure スタック HCI 解決策について説明](https://aka.ms/AzureStackOverviewVideo)をご覧ください。

## ハードウェア パートナー

15 パートナーから Windows Server 2019 を実行している検証済みの Azure スタック HCI ソリューションを購入することができます。 推奨される Microsoft パートナーでは、セットアップしてビルド時に時間がかかる設計することがなく実行してを取得し、サービスを実装し、サポートの連絡先の 1 つのポイントを提供します。

当社 70 + Azure スタック HCI 現在利用可能なソリューションこれらの Microsoft パートナーからを表示する[Azure スタック HCI web サイト](https://azure.microsoft.com/overview/azure-stack/hci)を参照してください: ASUS、Axellio、bluechip、DataON、Dell EMC、Fujitsu、HPE、Hitachi、Huawei、Lenovo、NEC、primeLine ソリューション、QCT、SecureGUARDSupermicro します。

## FAQ

### どのようなは Azure Stack および Azure スタック HCI ソリューションが共通のですか。 
Azure スタック HCI ソリューションは、HYPER-V ベースの同じソフトウェア定義のコンピューティング、ストレージ、およびネットワーク テクノロジを Azure Stack として機能します。 両方の製品満たす厳格なテストと検証の信頼性と、基になるハードウェア プラットフォームとの互換性を確認します。

### それらはどのように異なるかどうか。
Azure Stack をクラウドにオンプレミスでサービスを実行します。 PaaS サービスを一貫してビルドして、クラウド アプリケーション任意の場所では、オンプレミス Azure ポータルで管理を実行するオンプレミスと Azure IaaS を実行できます。

Windows Admin Center と使い慣れた Windows Server では、仮想化されたワークロード、オンプレミスを実行する Azure スタック HCI とツールを管理します。 必要に応じてハイブリッド シナリオなど、クラウド ベースのサイト回復、監視、およびその他のユーザーの Azure に接続できます。

### Microsoft は理由は、Azure Stack ファミリに提供するその HCI を移行するかどうか。 
Microsoft のハイパーコンバージド テクノロジは、既に Azure Stack の基盤です。 

多くの Microsoft のお客様が複雑な IT 環境ありの目標は、適切なビジネス向けの適切なテクノロジになっていることを満たしているソリューションを提供する必要があります。 Azure のスタック HCI は、ハードウェア パートナーから利用可能であった Windows Server 2016 に基づく windows server software-defined (WSSD) ソリューションの進化したものです。 おことに取り込ま Azure Stack ファミリまずは、インフラストラクチャの管理サービスの Azure とシームレスに接続する新しいオプションを提供するためです。 

### できますか Azure スタック HCI から Azure Stack にアップグレードするかどうか。 
いいえ、ユーザーは Azure Stack または Azure に Azure スタック HCI から特定のワークロードを移行することができます。

### Azure スタック HCI には、どのような Azure サービスに接続します。

Azure スタック HCI を接続する Azure サービスの更新された一覧は、 [Windows Server を Azure ハイブリッド サービスへの接続](../azure-hybrid-services/index.md)を参照してください。

### Azure スタック HCI ソリューションを購入する方法を教えてください。
次の手順に従います。

1. 推奨されるハードウェア パートナーから Microsoft が検証済みのハードウェア システムを購入します。
1. Windows Server 2019 Datacenter エディションと Windows Admin Center の管理とクラウド サービスを Azure に接続する機能をインストールします。
1. 必要に応じて、Azure アカウントを使用して、クラウド ベースの管理およびセキュリティ サービスをワークロードにアタッチします。