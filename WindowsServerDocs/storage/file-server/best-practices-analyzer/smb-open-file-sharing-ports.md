---
title: 'SMB: ファイルとプリンターの共有ポートが開いていること'
TOCTitle: 'SMB: File and printer sharing ports should be open'
ms.date: 07/02/2012
ms.prod: windows-server
ms.technology: storage
author: JasonGerend
manager: elizapo
ms.author: jgerend
ms.openlocfilehash: 80cc75f983d4593e4ee98309d1fa39c024b7b379
ms.sourcegitcommit: 083ff9bed4867604dfe1cb42914550da05093d25
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/14/2020
ms.locfileid: "75950293"
---
# <a name="smb-file-and-printer-sharing-ports-should-be-open"></a>SMB: ファイルとプリンターの共有ポートが開いていること


更新日: 2011 年2月2日

適用対象: windows Server 2019、Windows Server 2016、Windows Server 2012 R2、windows server 2012、windows server 2008 R2

*このトピックは、ベストプラクティスアナライザースキャンによって識別される特定の問題に対処することを目的としています。このトピックの情報は、ファイルベストプラクティスアナライザーサービスが実行されていて、このトピックで対処している問題が発生しているコンピューターにのみ適用する必要があります。ベストプラクティスとスキャンの詳細については、「* [ベストプラクティスアナライザー](https://go.microsoft.com/fwlink/?linkid=122786%0d%0a)」を参照してください。


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
<td><p><strong>[重大度]</strong></p></td>
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

## <a name="resolution"></a>解像度

> *ファイルとプリンターの共有がコンピューターのファイアウォールを経由して通信できるようにします。*

この手順を実行するには、 **Administrators** グループのメンバーシップ、またはそれと同等のメンバーシップが最低限必要です。

## <a name="to-open-the-firewall-ports-to-enable-file-and-printer-sharing"></a>ファイアウォールポートを開いてファイルとプリンターの共有を有効にするには

1.  コントロールパネルを開き、 **[システムとセキュリティ]** をクリックし、 **[Windows ファイアウォール]** をクリックします。

2.  左側のウィンドウで、 **[詳細設定]** をクリックし、コンソールツリーで **[受信の規則]** をクリックします。

3.  **[受信の規則]** で、規則**ファイルとプリンターの共有 (NB セッション)** と、**ファイルとプリンターの共有 (SMB 受信)** を見つけます。

4.  各規則を右クリックして、 **[規則の有効化]** をクリックします。

## <a name="additional-references"></a>その他の参照情報

[共有フォルダーと Windows ファイアウォールについて](https://technet.microsoft.com/library/cc731402.aspx)(https://technet.microsoft.com/library/cc731402.aspx)

