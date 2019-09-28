---
title: 仮想化
description: コンテナー、Hyper-V、Hyper-V 仮想スイッチなどの仮想化テクノロジーの概要と、Windows Server 2016 以降のバージョンのオペレーティング システムに関する追加コンテンツへのリンクを示します。
ms.prod: windows-server
manager: dougkim
ms.technology: compute
ms.topic: article
author: shortpatti
ms.author: pashort
ms.localizationpriority: medium
ms.date: 03/16/2018
ms.openlocfilehash: bbbd8ea812a25b0d538dcb87a380184412235b99
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/27/2019
ms.locfileid: "71364037"
---
# <a name="virtualization"></a>仮想化

>適用先:Windows Server (半期チャネル)、Windows Server 2016 

>[!TIP]
> 以前のバージョンの Windows Server に関する情報をお探しの場合は、 docs.microsoft.com の他の [Windows Server ライブラリ](/previous-versions/windows/)を参照してください。 また、[このサイトで検索して](https://docs.microsoft.com/search/index?search=Windows+Server&dataSource=previousVersions)、具体的な情報を確認することもできます。

<img src="../media/landing-icons/virtualization.png" style='float:left; padding:.5em;' alt="Icon showing a box with spokes"> Windows Server 2016 の仮想化は、ソフトウェア定義インフラストラクチャを作成するために必要な基盤技術の 1 つです。 仮想化機能は、ネットワークやストレージとともに、お客様のワークロードの処理に必要な柔軟性を実現します。

Windows Server 仮想化テクノロジには、Hyper-v、Hyper-v 仮想スイッチ、および保護されたファブリックとシールドされた Virtual Machines @no__t 0VMs @ no__t-1 の更新プログラムが含まれており、セキュリティ、スケーラビリティ、および信頼性が向上しています。 フェールオーバー クラスタリング、ネットワーク、記憶域に対する更新により、Hyper-V で使用する場合でも、これらのテクノロジの展開と管理が容易になっています。 


<ul class="cardsI panelContent">
<li>
        <a href="../security/guarded-fabric-shielded-vm/guarded-fabric-and-shielded-vms-top-node.md">
          <div class="cardSize">
            <div class="cardPadding">
                <div class="card">
                    <div class="cardImageOuter">
                        <div class="cardImage">
                            <img src="../media/i-access.svg" alt="" />
                        </div>
                    </div>
                    <div class="cardText">
                        <h3>保護されたファブリックとシールドされた VM</h3>
                        <p>クラウド サービス プロバイダーやエンタープライズ プライベート クラウド管理者は、保護されたファブリックを使用して、セキュリティが強化された VM 環境を実現できます。 保護されたファブリックは、1 つのホスト ガーディアン サービス (HGS) (通常は、3 ノードのクラスター) と、1 つまたは複数の保護されたホストと、シールドされた VM のセットで構成されます。</p>
                    </div>
                </div>
            </div>
        </div>
       </a>
    </li>
<li>
        <a href="/hyper-v/Hyper-V-on-Windows-Server.md">
          <div class="cardSize">
            <div class="cardPadding">
                <div class="card">
                    <div class="cardImageOuter">
                        <div class="cardImage">
                            <img src="../media/i-access.svg" alt="" />
                        </div>
                    </div>
                    <div class="cardText">
                        <h3>エンタープライズ向け Windows 10: 作業用のデバイスを使用する方法</h3>
                        <p>Hyper-V テクノロジは、ハードウェア仮想化によって、コンピューティング リソースを提供します。 Hyper-V では、ソフトウェア バージョンのコンピューター (仮想マシン) が作成され、それを使用してオペレーティング システムとアプリケーションが実行されます。 複数の仮想マシンを同時に実行でき、必要に応じてそれらを作成および削除できます。 </p>
                    </div>
                </div>
            </div>
        </div>
       </a>
     </li>

<li>
        <a href="https://docs.microsoft.com/windows-server/virtualization/hyper-v/hyper-v-server-2016">
          <div class="cardSize">
            <div class="cardPadding">
                <div class="card">
                    <div class="cardImageOuter">
                        <div class="cardImage">
                            <img src="../media/i-access.svg" alt="" />
                        </div>
                    </div>
                    <div class="cardText">
                        <h3>Microsoft Hyper-V Server</h3>
                        <p>Hyper-V テクノロジは、ハードウェア仮想化によって、コンピューティング リソースを提供します。 Hyper-V では、ソフトウェア バージョンのコンピューター (仮想マシン) が作成され、それを使用してオペレーティング システムとアプリケーションが実行されます。 複数の仮想マシンを同時に実行でき、必要に応じてそれらを作成および削除できます。 </p>
                    </div>
                </div>
            </div>
        </div>
       </a>
     </li>


<li>
        <a href="hyper-v-virtual-switch/Hyper-V-Virtual-Switch.md">
          <div class="cardSize">
            <div class="cardPadding">
                <div class="card">
                    <div class="cardImageOuter">
                        <div class="cardImage">
                            <img src="../media/i-access.svg" alt="" />
                        </div>
                    </div>
                    <div class="cardText">
                        <h3>Hyper-V 仮想スイッチ</h3>
                        <p>Hyper-V 仮想スイッチは、すべてのバージョンの Hyper-V に含まれている、ソフトウェアベースのレイヤー 2 イーサネット ネットワーク スイッチです。</p>

                        <p>Hyper-V サーバーの役割をインストールすると、Hyper-V マネージャーで Hyper-V 仮想スイッチを使用できるようになります。</p>

                        <p>Hyper-V 仮想スイッチには、仮想マシンを仮想ネットワークと物理ネットワークの両方に接続するための、プログラムで管理される拡張可能な機能が含まれています。</p> 

                        <p>また、Hyper-V 仮想スイッチでは、セキュリティ、分離、およびサービスのレベルでポリシーを適用できます。</p>
                    </div>
                </div>
            </div>
        </div>
       </a>
     </li>


<li>
       <a href="https://docs.microsoft.com/virtualization/windowscontainers">
          <div class="cardSize">
            <div class="cardPadding">
                <div class="card">
                    <div class="cardImageOuter">
                        <div class="cardImage">
                            <img src="../media/i-access.svg" alt="" />
                        </div>
                    </div>
                    <div class="cardText">
                        <h3>Windows コンテナー</h3>
                        <p>Windows コンテナーは、1 つのシステムで複数の独立したアプリケーションを実行できるオペレーティング システム レベルの仮想化を実現します。 この機能では、2 種類のコンテナー ランタイムを使用します。それぞれ、アプリケーションの分離の度合いが異なります。</p>
                    </div>
                </div>
            </div>
        </div>
       </a>
     </li>




## <a name="related"></a>関連

Hyper-V では、仮想化環境を作成するために特定のハードウェアが必要です。 詳細については、「[Windows Server 2016 の Hyper-V のシステム要件](./hyper-v/system-requirements-for-hyper-v-on-windows.md)」を参照してください。 

詳細については、「[Windows 10 の Hyper-V](https://docs.microsoft.com/virtualization/hyper-v-on-windows)」を参照してください。

