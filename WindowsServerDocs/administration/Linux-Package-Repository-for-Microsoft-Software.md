---
title: Microsoft 製品用の Linux ソフトウェア リポジトリ
description: このドキュメントを使用して、Microsoft 製品の Linux ソフトウェア パッケージをインストールする方法について説明します。
ms.custom: na
ms.prod: windows-server-threshold
ms.service: na
manager: szark
ms.technology: compute
ms.topic: article
ms.assetid: b5387444-595f-4f38-abb7-163a70ea1895
author: szarkos
ms.author: szark
ms.date: 10/16/2017
ms.openlocfilehash: dbdbd0f436645f7e19c07e4f3278c5073636a547
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/17/2019
ms.locfileid: "59831863"
---
# <a name="linux-software-repository-for-microsoft-products"></a>Microsoft 製品用の Linux ソフトウェア リポジトリ

## <a name="overview"></a>概要
Microsoft は、ビルドし Linux システムのさまざまなソフトウェア製品をサポートしていますや標準の APT や YUM パッケージ リポジトリを使用して利用できるようにします。 このドキュメントでは、することができますし、インストール/アップグレード Microsoft's Linux ソフトウェアが、ディストリビューションの標準のパッケージ管理ツールを使用するために、Linux システムでリポジトリを構成する方法が説明します。

Microsoft の Linux ソフトウェア リポジトリは、複数のサブ リポジトリで構成されます。

 - prod – パッケージの実稼働環境で使用するためのサブ リポジトリが指定されている運用します。 これらのパッケージは、条件の該当するサポート契約または Microsoft と必要のあるプログラムの下で販売されている Microsoft によってサポートされます。

 - mssql server - これらのリポジトリ パッケージを含む Microsoft SQL Server on Linux の参照のも。[SQL Server on Linux](https://www.microsoft.com/en-us/sql-server/sql-server-vnext-including-Linux)します。

>[!Note]
Linux ソフトウェア リポジトリ内のパッケージ、パッケージ内にあるライセンス条項を受けます。 パッケージを使用する前に、ライセンス条項をお読みください。 インストールおよびパッケージの使用は、これらの条項に同意するを構成します。 ライセンス条項に同意しない場合は、パッケージを使用しないでください。


## <a name="configuring-the-repositories"></a>リポジトリを構成します。
リポジトリは、Linux ディストリビューションとバージョンに適用される Linux パッケージをインストールすることによって自動的に構成できます。 パッケージは、apt/yum の zypper などのツールによって、署名付きパッケージやリポジトリ メタデータの検証に使用する鍵の公開キーと共にリポジトリの構成でインストールされます。

### <a name="enterprise-linux-rhel-and-variants"></a>Enterprise Linux (RHEL およびバリアント)

 - Enterprise Linux 6 (EL6)

        sudo rpm -Uvh https://packages.microsoft.com/config/rhel/6/packages-microsoft-prod.rpm

 - Enterprise Linux 7 (EL7)

        sudo rpm -Uvh https://packages.microsoft.com/config/rhel/7/packages-microsoft-prod.rpm


### <a name="ubuntu"></a>Ubuntu

 - Ubuntu 14.04 (信頼性)

        wget https://packages.microsoft.com/config/ubuntu/14.04/packages-microsoft-prod.deb
        sudo dpkg -i packages-microsoft-prod.deb
        sudo apt-get update

 - Ubuntu 16.04 (Xenial)

        wget https://packages.microsoft.com/config/ubuntu/16.04/packages-microsoft-prod.deb
        sudo dpkg -i packages-microsoft-prod.deb
        sudo apt-get update

 - Ubuntu 16.10 (Yakkety)

        wget https://packages.microsoft.com/config/ubuntu/16.10/packages-microsoft-prod.deb
        sudo dpkg -i packages-microsoft-prod.deb
        sudo apt-get update


### <a name="suse-linux-enterprise-12"></a>SUSE Linux Enterprise 12

        sudo rpm -Uvh https://packages.microsoft.com/config/sles/12/packages-microsoft-prod.rpm


## <a name="manual-configuration"></a>手動による構成
リポジトリ構成ファイルから[packages.microsoft.com/config](https://packages.microsoft.com/config/)します。これらのファイルの場所と名前は、次の URI 名前付け規則を使用して配置できます。

        https://packages.microsoft.com/config/<Distribution>/<Version>/prod.(repo|list)

**パッケージとリポジトリの署名キー**

 - ここで Microsoft の鍵の公開キーをダウンロードする可能性があります。 [https://packages.microsoft.com/keys/microsoft.asc](https://packages.microsoft.com/keys/microsoft.asc)
 - パブリック キー ID:Microsoft (リリース署名) <gpgsecurity@microsoft.com>
 - パブリック キーのフィンガー プリント: `BC52 8686 B50D 79E3 39D3 721C EB3E 94AD BE12 29CF`

### <a name="examples"></a>例:

 - Rhel/centos 7

        # Install repository configuration
        curl https://packages.microsoft.com/config/rhel/7/prod.repo > ./microsoft-prod.repo
        sudo cp ./microsoft-prod.repo /etc/yum.repos.d/

        # Install Microsoft's GPG public key
        curl https://packages.microsoft.com/keys/microsoft.asc > ./microsoft.asc
        sudo rpm --import ./microsoft.asc

 - Ubuntu 16.04

        # Install repository configuration
        curl https://packages.microsoft.com/config/ubuntu/16.04/prod.list > ./microsoft-prod.list
        sudo cp ./microsoft-prod.list /etc/apt/sources.list.d/

        # Install Microsoft GPG public key
        curl https://packages.microsoft.com/keys/microsoft.asc | gpg --dearmor > microsoft.gpg
        sudo cp ./microsoft.gpg /etc/apt/trusted.gpg.d/



