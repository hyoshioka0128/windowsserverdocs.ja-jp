---
title: Microsoft 製品用 Linux ソフトウェアリポジトリ
description: このドキュメントでは、Microsoft 製品用の Linux ソフトウェアパッケージを使用してインストールする方法について説明します。
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
ms.openlocfilehash: bade9fff306272188ac8d2b91a3d9921c80fe036
ms.sourcegitcommit: f6490192d686f0a1e0c2ebe471f98e30105c0844
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/10/2019
ms.locfileid: "70866892"
---
# <a name="linux-software-repository-for-microsoft-products"></a>Microsoft 製品用 Linux ソフトウェアリポジトリ

## <a name="overview"></a>概要
Microsoft では、Linux システム向けにさまざまなソフトウェア製品を構築してサポートしており、標準の APT および YUM パッケージリポジトリを通じて利用できます。 このドキュメントでは、Linux システムでリポジトリを構成する方法について説明します。その結果、ディストリビューションの標準のパッケージ管理ツールを使用して Microsoft の Linux ソフトウェアをインストールまたはアップグレードできるようになります。

Microsoft の Linux ソフトウェアリポジトリは、次の複数のサブリポジトリで構成されています。

 - 製品–運用サブリポジトリは、運用環境での使用を目的としたパッケージに対して指定されています。 これらのパッケージは、microsoft の適用されるサポート契約またはプログラムの条件に基づいて、マイクロソフトによって販売されています。

 - mssql-サーバー-これらのリポジトリには Microsoft SQL Server on Linux のパッケージが含まれています。[SQL Server on Linux](https://www.microsoft.com/en-us/sql-server/sql-server-vnext-including-Linux)。

> [!Note]
> Linux ソフトウェアリポジトリ内のパッケージには、パッケージにあるライセンス条項が適用されます。 パッケージを使用する前に、ライセンス条項をお読みください。 パッケージをインストールして使用すると、これらの条項に同意したものとなります。 ライセンス条項に同意しない場合は、パッケージを使用しないでください。


## <a name="configuring-the-repositories"></a>リポジトリの構成
リポジトリは、Linux ディストリビューションとバージョンに適用される Linux パッケージをインストールすることによって自動的に構成できます。 パッケージによって、リポジトリの構成と、apt/yum/zypper などのツールによって使用される GPG 公開キーがインストールされ、署名されたパッケージやリポジトリのメタデータを検証できます。

### <a name="enterprise-linux-rhel-and-variants"></a>Enterprise Linux (RHEL および variant)

 - Enterprise Linux 6 (64.RPM)

        sudo rpm -Uvh https://packages.microsoft.com/config/rhel/6/packages-microsoft-prod.rpm

 - Enterprise Linux 7 (EL7)

        sudo rpm -Uvh https://packages.microsoft.com/config/rhel/7/packages-microsoft-prod.rpm


### <a name="ubuntu"></a>Ubuntu

 - Ubuntu 14.04 (Trusty)

        curl https://packages.microsoft.com/keys/microsoft.asc | sudo apt-key add -
        sudo apt-add-repository https://packages.microsoft.com/ubuntu/14.04/prod
        sudo apt-get update

 - Ubuntu 16.04 (Xenial)

        curl https://packages.microsoft.com/keys/microsoft.asc | sudo apt-key add -
        sudo apt-add-repository https://packages.microsoft.com/ubuntu/16.04/prod
        sudo apt-get update

 - Ubuntu 18.04 (Bionic)

        curl https://packages.microsoft.com/keys/microsoft.asc | sudo apt-key add -
        sudo apt-add-repository https://packages.microsoft.com/ubuntu/18.04/prod
        sudo apt-get update

 - Ubuntu 18.10 (宇宙)

        curl https://packages.microsoft.com/keys/microsoft.asc | sudo apt-key add -
        sudo apt-add-repository https://packages.microsoft.com/ubuntu/18.10/prod
        sudo apt-get update

 - Ubuntu 19.04 (Disco)

        curl https://packages.microsoft.com/keys/microsoft.asc | sudo apt-key add -
        sudo apt-add-repository https://packages.microsoft.com/ubuntu/19.04/prod
        sudo apt-get update

### <a name="suse-linux-enterprise-12"></a>SUSE Linux Enterprise 12

        sudo rpm -Uvh https://packages.microsoft.com/config/sles/12/packages-microsoft-prod.rpm


## <a name="manual-configuration"></a>手動構成
リポジトリ構成ファイルは[packages.microsoft.com/config](https://packages.microsoft.com/config/)から入手できます。これらのファイルの名前と場所は、次の URI 名前付け規則を使用して見つけることができます。

        https://packages.microsoft.com/config/<Distribution>/<Version>/prod.(repo|list)

**パッケージとリポジトリの署名キー**

 - Microsoft の GPG 公開キーは、次の場所でダウンロードできます。[https://packages.microsoft.com/keys/microsoft.asc](https://packages.microsoft.com/keys/microsoft.asc)
 - 公開キー ID:Microsoft (リリース署名)<gpgsecurity@microsoft.com>
 - 公開キーのフィンガープリント:`BC52 8686 B50D 79E3 39D3 721C EB3E 94AD BE12 29CF`

### <a name="examples"></a>例 :

 - RHEL/CentOS 7

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



