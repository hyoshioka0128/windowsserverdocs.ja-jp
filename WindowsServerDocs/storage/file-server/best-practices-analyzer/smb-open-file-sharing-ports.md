---
title: 向けファイルとプリンターの共有ポートを開く
TOCTitle: 'SMB: File and printer sharing ports should be open'
ms.date: 07/02/2012
ms.prod: windows-server
ms.technology: storage
author: JasonGerend
manager: elizapo
ms.author: jgerend
ms.openlocfilehash: 22cd926fdb873538631a6f6850157dceb5a020d7
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/27/2019
ms.locfileid: "71385832"
---
# <a name="smb-file-and-printer-sharing-ports-should-be-open"></a>向けファイルとプリンターの共有ポートを開く


更新:2011年2月2日

適用先:Windows Server 2019、Windows Server 2016、Windows Server 2012 R2、windows server 2012、windows server 2008 R2

*This トピックは、ベストプラクティスアナライザースキャンによって識別される特定の問題に対処するためのものです。このトピックの情報は、ファイルベストプラクティスアナライザーサービスが実行されていて、このトピックで対処している問題が発生しているコンピューターにのみ適用する必要があります。ベストプラクティスとスキャンの詳細については、「@ no__t-0[ベストプラクティスアナライザー](http://go.microsoft.com/fwlink/?linkid=122786%0d%0a)」を参照してください。


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p><strong>オペレーティング システム</strong></p></td>
<td><p>Windows Server</p></td>
</tr>
<tr class="even">
<td><p><strong>製品/機能</strong></p></td>
<td><p>ファイル サービス</p></td>
</tr>
<tr class="odd">
<td><p><strong>順</strong></p></td>
<td><p>Error</p></td>
</tr>
<tr class="even">
<td><p><strong>カテゴリ</strong></p></td>
<td><p>構成</p></td>
</tr>
</tbody>
</table>

## <a name="issue"></a>問題

> *ファイルとプリンターの共有に必要なファイアウォールポートが開いていません (ポート445および 139)。*

## <a name="impact"></a>影響

> *コンピューターは、このサーバー上の共有フォルダーやその他のサーバーメッセージブロック (SMB) ベースのネットワークサービスにアクセスできなくなります。*

## <a name="resolution"></a>解決方法

> *ファイルとプリンターの共有がコンピューターのファイアウォールを経由して通信できるようにします。*

この手順を実行するには、**Administrators** グループのメンバーシップ、またはそれと同等のメンバーシップが最低限必要です。

## <a name="to-open-the-firewall-ports-to-enable-file-and-printer-sharing"></a>ファイアウォールポートを開いてファイルとプリンターの共有を有効にするには

1.  コントロールパネルを開き、 **[システムとセキュリティ]** をクリックし、 **[Windows ファイアウォール]** をクリックします。

2.  左側のウィンドウで、 **[詳細設定]** をクリックし、コンソールツリーで **[受信の規則]** をクリックします。

3.  **[受信の規則]** で、規則**ファイルとプリンターの共有 (NB セッション)** と、**ファイルとプリンターの共有 (SMB 受信)** を見つけます。

4.  各ルールについて、ルールを右クリックし、 **[ルールの有効化]** をクリックします。

## <a name="additional-references"></a>その他の参照情報

[共有フォルダーと Windows ファイアウォールについて](https://technet.microsoft.com/library/cc731402.aspx)(https://technet.microsoft.com/library/cc731402.aspx)

