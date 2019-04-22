---
title: Windows コマンド
description: Windows コマンド
ms.custom: na
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: c703d07c-8227-4e86-94a6-8ef390f94cdc
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 05/22/2018
ms.prod: windows-server-threshold
ms.openlocfilehash: 4cc9bc5c288eb063f333fa598dbb3511f7be5966
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/17/2019
ms.locfileid: "59820473"
---
# <a name="windows-commands"></a>Windows コマンド

Windows (サーバーとクライアント) のサポートされているすべてのバージョンがある一連の Win32 コンソールのコマンドが組み込まれています。

このドキュメント セットでは、タスクを自動化するスクリプトを使用して、またはスクリプト ツールで使用できる Windows コマンドについて説明します。

次の A ~ Z のメニューで、特定のコマンドに関する情報を検索するには、コマンドを使用すると、開始する文字をクリックし、コマンド名をクリックします。

[A](#BKMK_a) |
[B](#BKMK_b) | 
[C](#BKMK_c) | 
[D](#BKMK_d) | 
[E](#BKMK_e)  | 
 [F](#BKMK_f) | 
[G](#BKMK_g) | 
[H](#BKMK_h) | 
[は](#BKMK_i) |
 [J](#BKMK_j) | 
[K](#BKMK_k) | 
[L](#BKMK_l) | 
[M](#BKMK_m) | 
[N](#BKMK_n) | 
 [O](#BKMK_o) | 
[P](#BKMK_p) | 
[Q](#BKMK_q) | 
[R](#BKMK_r)  | 
[S](#BKMK_s) | 
[T](#BKMK_t) | 
[U](#BKMK_u) | 
[V](#BKMK_v) | 
 [W](#BKMK_w) | 
[X](#BKMK_x) | 
[Y](#BKMK_y) | 
[Z](#BKMK_z)

## <a name="BKMK_PREREQ"></a>前提条件
この PDF に含まれる情報に適用されます。

-   Windows Server 2019
-   Windows Server (半期チャネル)
-   Windows Server 2016
-   Windows Server 2012 R2
-   Windows Server 2012 
-   Windows Server 2008 R2
-   Windows Server 2008
-   Windows 10
-   Windows 8.1

### <a name="BKMK_OVR"></a>コマンド シェルの概要
コマンド シェルでは、バッチ (.bat) ファイルでユーザー アカウントの管理または夜間のバックアップなどの日常的なタスクを自動化する Windows に組み込まれている最初のシェルをしました。 Windows スクリプト ホストでは、コマンド シェルでより高度なスクリプトを実行できます。 詳細については、次を参照してください。 [cscript](cscript.md)または[wscript](wscript.md)します。 ユーザー インターフェイスを使用するよりも、スクリプトを使用して、操作をより効率的に実行できます。 スクリプトは、コマンドラインで使用できるすべてのコマンドをそのまま使用します。

Windows では、2 つのコマンド シェルがあります。コマンド シェルと[PowerShell](https://docs.microsoft.com/powershell/scripting/powershell-scripting?view=powershell-6)します。 各シェルとして、オペレーティング システムまたは IT 操作を自動化するための環境を提供する、アプリケーションの間の直接の通信を提供するソフトウェア プログラムです。

PowerShell は、コマンドレットと呼ばれる PowerShell コマンドを実行するコマンド シェルの機能を拡張する設計されました。 コマンドレットは Windows のコマンドに似ていますが、拡張可能なスクリプト言語を提供します。 Powershell では、Windows のコマンドと PowerShell コマンドレットを実行することができますが、コマンド シェルには、Windows のコマンドと PowerShell コマンドレットではないのみを実行できます。

最も信頼性が高く、最新 Windows automation、PowerShell を使用して、Windows コマンドまたは Windows スクリプト ホストの Windows のオートメーションではなくをお勧めします。 
> [!NOTE]
>ダウンロードしてインストールすることができますも[PowerShell Core](https://docs.microsoft.com/powershell/scripting/whats-new/what-s-new-in-powershell-core-60?view=powershell-6)PowerShell のオープン ソース バージョン。 

> [!CAUTION]
> レジストリを正しく編集しないと、システムが正常に動作しなくなる場合があります。 レジストリに次の変更を加える前に、コンピューターの重要なデータをバックアップする必要があります。

> [!NOTE]
> 実行を有効または、ファイルとディレクトリ名の補完機能コマンド シェルで、コンピューターまたはユーザーのログオン セッションを無効にする、 **regedit.exe** 、以下の設定と**reg_DWOrd 値**:
> 
> 次のレジストリ Processor\completionChar\reg_DWOrd
> 
> 設定する、 **reg_DWOrd**値には、特定の機能の制御文字の 16 進数の値を使用して (たとえば、 **0 9**  タブと**0 08** backspace キーが)。 ユーザーが指定した設定は、コンピューターの設定より優先し、コマンド ライン オプションのレジストリ設定より優先します。

## <a name="BKMK_CmdRef"></a>コマンド ライン リファレンス A ~ Z
次の A ~ Z のメニューで、特定の Windows コマンドに関する情報を検索するには、コマンドを使用すると、開始する文字をクリックし、コマンド名をクリックします。

[A](#BKMK_a) |
[B](#BKMK_b) | 
[C](#BKMK_c) | 
[D](#BKMK_d) | 
[E](#BKMK_e)  | 
 [F](#BKMK_f) | 
[G](#BKMK_g) | 
[H](#BKMK_h) | 
[は](#BKMK_i) |
 [J](#BKMK_j) | 
[K](#BKMK_k) | 
[L](#BKMK_l) | 
[M](#BKMK_m) | 
[N](#BKMK_n) | 
 [O](#BKMK_o) | 
[P](#BKMK_p) | 
[Q](#BKMK_q) | 
[R](#BKMK_r)  | 
[S](#BKMK_s) | 
[T](#BKMK_t) | 
[U](#BKMK_u) | 
[V](#BKMK_v) | 
 [W](#BKMK_w) | 
[X](#BKMK_x) | 
[Y](#BKMK_y) | 
[Z](#BKMK_z)

### <a name="BKMK_a"></a>A
-   [追加](append.md)
-   [arp](arp.md)
-   [assoc](assoc.md)
-   [at](at.md)
-   [atmadm](atmadm.md)
-   [attrib](attrib.md)
-   [auditpol](auditpol.md)
-   [autochk](autochk.md)
-   [autoconv](autoconv.md)
-   [autofmt](autofmt.md)

### <a name="BKMK_b"></a>B
-   [bcdboot](bcdboot.md)
-   [bcdedit](bcdedit.md)
-   [bdehdcfg](bdehdcfg.md)
-   [bitsadmin](bitsadmin.md)
  -   [bitsadmin addfile](bitsadmin-addfile.md)
  -   [bitsadmin addfileset](bitsadmin-addfileset.md)
  -   [bitsadmin addfilewithranges](bitsadmin-addfilewithranges.md)
  -   [bitsadmin キャンセル](bitsadmin-cancel.md)
  -   [完全な bitsadmin](bitsadmin-complete.md)
  -   [bitsadmin を作成します。](bitsadmin-create.md)
  -   [bitsadmin getaclflags](bitsadmin-getaclflags.md)
  -   [bitsadmin getbytestotal](bitsadmin-getbytestotal.md)
  -   [bitsadmin getbytestransferred](bitsadmin-getbytestransferred.md)
  -   [bitsadmin getcompletiontime](bitsadmin-getcompletiontime.md)
  -   [bitsadmin getcreationtime](bitsadmin-getcreationtime.md)
  -   [bitsadmin getdescription](bitsadmin-getdescription.md)
  -   [bitsadmin getdisplayname](bitsadmin-getdisplayname.md)
  -   [bitsadmin geterror](bitsadmin-geterror.md)
  -   [bitsadmin geterrorcount](bitsadmin-geterrorcount.md)
  -   [bitsadmin getfilestotal](bitsadmin-getfilestotal.md)
  -   [bitsadmin getfilestransferred](bitsadmin-getfilestransferred.md)
  -   [bitsadmin getminretrydelay](bitsadmin-getminretrydelay.md)
  -   [bitsadmin getmodificationtime](bitsadmin-getmodificationtime.md)
  -   [bitsadmin getnoprogresstimeout](bitsadmin-getnoprogresstimeout.md)
  -   [bitsadmin getnotifycmdline](bitsadmin-getnotifycmdline.md)
  -   [bitsadmin getnotifyflags](bitsadmin-getnotifyflags.md)
  -   [bitsadmin getnotifyinterface](bitsadmin-getnotifyinterface.md)
  -   [bitsadmin getowner](bitsadmin-getowner.md)
  -   [bitsadmin get の優先順位](bitsadmin-getpriority.md)
  -   [bitsadmin getproxybypasslist](bitsadmin-getproxybypasslist.md)
  -   [bitsadmin getproxylist](bitsadmin-getproxylist.md)
  -   [bitsadmin getproxyusage](bitsadmin-getproxyusage.md)
  -   [bitsadmin getreplydata](bitsadmin-getreplydata.md)
  -   [bitsadmin getreplyfilename](bitsadmin-getreplyfilename.md)
  -   [bitsadmin getreplyprogress](bitsadmin-getreplyprogress.md)
  -   [bitsadmin getstate](bitsadmin-getstate.md)
  -   [bitsadmin gettype](bitsadmin-gettype.md)
  -   [bitsadmin ヘルプ](bitsadmin-help.md)
  -   [bitsadmin 情報](bitsadmin-info.md)
  -   [bitsadmin 一覧](bitsadmin-list.md)
  -   [bitsadmin/listfiles という](bitsadmin-listfiles.md)
  -   [bitsadmin モニター](bitsadmin-monitor.md)
  -   [bitsadmin nowrap](bitsadmin-nowrap.md)
  -   [bitsadmin rawreturn](bitsadmin-rawreturn.md)
  -   [bitsadmin removecredentials](bitsadmin-removecredentials.md)
  -   [bitsadmin replaceremoteprefix](bitsadmin-replaceremoteprefix.md)
  -   [bitsadmin リセット](bitsadmin-reset.md)
  -   [bitsadmin の再開](bitsadmin-resume.md)
  -   [bitsadmin setaclflag](bitsadmin-setaclflag.md)
  -   [bitsadmin setcredentials](bitsadmin-setcredentials.md)
  -   [bitsadmin setdescription](bitsadmin-setdescription.md)
  -   [bitsadmin setdisplayname](bitsadmin-setdisplayname.md)
  -   [bitsadmin setminretrydelay](bitsadmin-setminretrydelay.md)
  -   [bitsadmin setnoprogresstimeout](bitsadmin-setnoprogresstimeout.md)
  -   [bitsadmin setnotifycmdline](bitsadmin-setnotifycmdline.md)
  -   [bitsadmin setnotifyflags](bitsadmin-setnotifyflags.md)
  -   [bitsadmin setpriority](bitsadmin-setpriority.md)
  -   [bitsadmin setproxysettings](bitsadmin-setproxysettings.md)
  -   [bitsadmin setreplyfilename](bitsadmin-setreplyfilename.md)
  -   [bitsadmin 中断します。](bitsadmin-suspend.md)
  -   [bitsadmin takeownership](bitsadmin-takeownership.md)
  -   [bitsadmin 転送](bitsadmin-transfer.md)
  -   [bitsadmin ユーティリティ](bitsadmin-util.md)
  -   [bitsadmin ラップ](bitsadmin-wrap.md)
-   [bootcfg](bootcfg.md)
  -   [bootcfg addsw](bootcfg-addsw.md)
  -   [bootcfg コピー](bootcfg-copy.md)
  -   [bootcfg dbg1394](bootcfg-dbg1394.md)
  -   [bootcfg デバッグ](bootcfg-debug.md)  
  -   [bootcfg 既定](bootcfg-default.md)
  -   [bootcfg delete](bootcfg-delete.md)
  -   [bootcfg ems](bootcfg-ems.md)
  -   [bootcfg query](bootcfg-query.md)
  -   [bootcfg 生](bootcfg-raw.md)
  -   [bootcfg rmsw](bootcfg-rmsw.md)
  -   [bootcfg タイムアウト](bootcfg-timeout.md)
-   [break](break_1.md)

### <a name="BKMK_c"></a>C
-   [cacls](cacls_1.md)
-   [call](call.md)
-   [cd](cd.md)
-   [certreq](certreq_1.md)
-   [certutil](certutil.md)
-   [change](change.md)
  -   [ログオン時に変更します。](change-logon.md)
  -   [ポートを変更します。](change-port.md)
  -   [ユーザーを変更します。](change-user.md)
-   [chcp](chcp.md)
-   [chdir](chdir_1.md)
-   [chglogon](chglogon.md)
-   [chgport](chgport.md)
-   [chgusr](chgusr.md)
-   [chkdsk](chkdsk.md)
-   [chkntfs](chkntfs.md)
-   [選択しました。](choice.md)
-   [暗号](cipher.md)
-   [クリップ](clip.md)
-   [cls](cls.md)
-   [cmd](Cmd.md)
-   [cmdkey](cmdkey.md)
-   [cmstp](cmstp.md)
-   [色](color.md)
-   [comp](comp.md)
-   [Compact](compact.md)
-   [変換](convert.md)
-   [コピー](copy.md)
-   [cprofile](cprofile.md)
-   [cscript](cscript.md)

### <a name="BKMK_d"></a>D
-   [date](date.md)
-   [dcgpofix](dcgpofix.md)
-   [defrag](defrag.md)
-   [del](del.md)
-   [dfsrmig](dfsrmig.md)
-   [diantz](diantz.md)
-   [dir](dir.md)
-   [diskcomp](diskcomp.md)
-   [diskcopy](diskcopy.md)
-   [diskpart](diskpart.md)
-   [diskperf](diskperf.md)
-   [diskraid](diskraid.md)
-   [diskshadow](diskshadow.md)
-   [dispdiag](dispdiag.md)
-   [dnscmd](Dnscmd.md)
-   [doskey](doskey.md)
-   [driverquery](driverquery.md)

### <a name="BKMK_e"></a>E
-   [echo](echo.md)
-   [edit](edit.md)
-   [endlocal](endlocal.md)
-   [erase](erase.md)
-   [eventcreate](eventcreate.md)
-   [eventquery](eventquery.md)
-   [eventtrigger](eventtriggers.md)
-   [evntcmd](Evntcmd.md)
-   [終了](exit_2.md)
-   [展開](expand.md)
-   [抽出](extract.md)

### <a name="BKMK_f"></a>F
-   [fc](fc.md)
-   [検索](find.md)
-   [findstr](findstr.md)
-   [指](finger.md)
-   [flattemp](flattemp.md)
-   [fondue](fondue.md)
-   [の](for.md)
-   [ファイルを探す](forfiles.md)
-   [format](format.md)
-   [freedisk](freedisk.md)
-   [Fsutil](fsutil.md)
  -   [fsutil 8dot3name](fsutil-8dot3name.md) 
  -   [fsutil の動作](fsutil-behavior.md) 
  -   [fsutil ファイル](fsutil-file.md)
  -   [fsutil fsinfo](fsutil-fsinfo.md)
  -   [fsutil hardlink](fsutil-hardlink.md)
  -   [fsutil の objectid](fsutil-objectid.md)
  -   [Fsutil クォータ](fsutil-quota.md)
  -   [fsutil の修復](fsutil-repair.md)
  -   [fsutil reparsepoint](fsutil-reparsepoint.md)
  -   [fsutil リソース](fsutil-resource.md)
  -   [fsutil スパース](fsutil-sparse.md)
  -   [fsutil の階層制御](fsutil-tiering.md)
  -   [fsutil トランザクション](fsutil-transaction.md)
  -   [fsutil usn](fsutil-usn.md)
  -   [fsutil ボリューム](fsutil-volume.md)
  -   [fsutil wim](fsutil-wim.md)
-   [ftp](ftp.md)
-   [ftype](ftype.md)
-   [fveupdate](fveupdate.md)

### <a name="BKMK_g"></a>G
-   [getmac](getmac.md)
-   [gettype](gettype.md)
-   [goto](goto.md)
-   [gpfixup](gpfixup.md)
-   [gpresult](gpresult.md)
-   [gpupdate](gpupdate.md)
-   [与えます](graftabl.md)

### <a name="BKMK_h"></a>H
-   [help](help.md)
-   [helpctr](helpctr.md)
-   [hostname](hostname.md)

### <a name="BKMK_i"></a>私
-   [icacls](icacls.md)
-   [if](if.md)
-   [inuse](inuse.md)
-   [ipconfig](ipconfig.md)
-   [ipxroute](ipxroute.md)
-   [irftp](irftp.md)

### <a name="BKMK_j"></a>J
-   [jetpack](jetpack.md)

### <a name="BKMK_k"></a>K
-   [klist](klist.md)
-   [ksetup](ksetup.md)
  -   [ksetup:setrealm](ksetup-setrealm.md)
  -   [ksetup:mapuser](ksetup-mapuser.md)
  -   [ksetup:addkdc](ksetup-addkdc.md)
  -   [ksetup:delkdc](ksetup-delkdc.md)
  -   [ksetup:addkpasswd](ksetup-addkpasswd.md)
  -   [ksetup:delkpasswd](ksetup-delkpasswd.md)
  -   [ksetup:server](ksetup-server.md)
  -   [ksetup:setcomputerpassword](ksetup-setcomputerpassword.md)
  -   [ksetup:removerealm](ksetup-removerealm.md)
  -   [ksetup:domain](ksetup-domain.md)
  -   [ksetup:changepassword](ksetup-changepassword.md)
  -   [ksetup:listrealmflags](ksetup-listrealmflags.md)
  -   [ksetup:setrealmflags](ksetup-setrealmflags.md)
  -   [ksetup:addrealmflags](ksetup-addrealmflags.md)
  -   [ksetup:delrealmflags](ksetup-delrealmflags.md)
  -   [ksetup:dumpstate](ksetup-dumpstate.md)
  -   [ksetup:addhosttorealmmap](ksetup-addhosttorealmmap.md)
  -   [ksetup:delhosttorealmmap](ksetup-delhosttorealmmap.md)
  -   [ksetup:setenctypeattr](ksetup-setenctypeattr.md)
  -   [ksetup:getenctypeattr](ksetup-getenctypeattr.md)
  -   [ksetup:addenctypeattr](ksetup-addenctypeattr.md)
  -   [ksetup:delenctypeattr](ksetup-delenctypeattr.md) 
-   [ktmutil](ktmutil.md)
-   [ktpass](ktpass.md)

### <a name="BKMK_l"></a>L
-   [label](label.md)
-   [lodctr](lodctr.md)
-   [logman](logman.md)
  -   [logman を作成します。](logman-create.md)
  -   [logman クエリ](logman-query.md)
  -   [logman start & #124;停止](logman-start-stop.md)
  -   [logman delete](logman-delete.md)
  -   [logman update](logman-update.md)
  -   [logman import & #124;エクスポート](logman-import-export.md)
-   [logoff](logoff.md)
-   [lpq](lpq.md)
-   [lpr](lpr.md)

### <a name="BKMK_m"></a>M
-   [macfile](macfile.md)
-   [makecab](makecab.md)
-   [manage-bde](manage-bde.md)
  -   [manage-bde: ステータス](manage-bde-status.md)
  -   [manage-bde: on](manage-bde-on.md)
  -   [manage-bde: off](manage-bde-off.md)
  -   [manage-bde: 一時停止](manage-bde-pause.md)
  -   [manage-bde: resume](manage-bde-resume.md)
  -   [manage-bde: lock](manage-bde-lock.md)
  -   [manage-bde: unlock](manage-bde-unlock.md)
  -   [manage-bde: autounlock](manage-bde-autounlock.md)
  -   [manage-bde: protectors](manage-bde-protectors.md)
  -   [manage-bde: tpm](manage-bde-tpm.md)
  -   [manage-bde: setidentifier](manage-bde-setidentifier.md)
  -   [manage-bde:ForceRecovery](manage-bde-forcerecovery.md)
  -   [manage-bde: changepassword](manage-bde-changepassword.md)
  -   [manage-bde: changepin](manage-bde-changepin.md)
  -   [manage-bde: changekey](manage-bde-changekey.md)
  -   [manage-bde:KeyPackage](manage-bde-keypackage.md)
  -   [manage-bde: upgrade](manage-bde-upgrade.md)
  -   [manage-bde:WipeFreeSpace](manage-bde-wipefreespace.md)
-   [mapadmin](mapadmin.md)
-   [md](Md.md)
-   [mkdir](mkdir.md)
-   [mklink](mklink.md)
-   [mmc](mmc.md)
-   [mode](mode.md)
-   [もっとその](more.md)
-   [マウント](mount.md)
-   [mountvol](mountvol.md)
-   [move](move.md)
-   [mqbkup](mqbkup.md)
-   [mqsvc](mqsvc.md)
-   [mqtgsvc](mqtgsvc.md)
-   [msdt](msdt.md)
-   [msg](msg.md)
-   [msiexec](msiexec.md)
-   [msinfo32](msinfo32.md)
-   [mstsc](mstsc.md)

### <a name="BKMK_n"></a>N
-   [nbtstat](nbtstat.md)
-   [netcfg](netcfg.md)
-   [netsh](netsh.md)
-   [netstat](netstat.md)
-   [Net の印刷](net-print.md)
-   [nfsadmin](nfsadmin.md)
-   [nfsshare](nfsshare.md)
-   [nfsstat](nfsstat.md)
-   [nlbmgr](nlbmgr.md)
-   [nslookup](nslookup.md)
  -   [nslookup exit コマンド](nslookup-exit-command.md)
  -   [本の指で nslookup コマンド](nslookup-finger-command.md)
  -   [nslookup のヘルプ](nslookup-help.md)
  -   [nslookup %.*ls](nslookup-ls.md)
  -   [nslookup lserver](nslookup-lserver.md)
  -   [nslookup ルート](nslookup-root.md)
  -   [nslookup サーバー](nslookup-server.md)
  -   [nslookup セット](nslookup-set.md)
  -   [nslookup のすべての設定](nslookup-set-all.md)
  -   [nslookup set クラス](nslookup-set-class.md)
  -   [nslookup set d2](nslookup-set-d2.md)
  -   [nslookup デバッグの設定](nslookup-set-debug.md)
  -   [nslookup でドメインを設定](nslookup-set-domain.md)
  -   [nslookup ポートを設定します。](nslookup-set-port.md)
  -   [nslookup querytype を設定します。](nslookup-set-querytype.md)
  -   [nslookup recurse の設定](nslookup-set-recurse.md)
  -   [nslookup 再試行の設定](nslookup-set-retry.md)
  -   [nslookup ルートの設定](nslookup-set-root.md)
  -   [nslookup セットの検索](nslookup-set-search.md)
  -   [nslookup srchlist を設定します。](nslookup-set-srchlist.md)
  -   [nslookup のタイムアウトを設定します。](nslookup-set-timeout.md)
  -   [nslookup の種類を設定します。](nslookup-set-type.md)
  -   [nslookup set vc](nslookup-set-vc.md)
  -   [nslookup ビュー](nslookup-view.md)
-   [ntbackup](ntbackup.md)
-   [ntcmdprompt](ntcmdprompt.md)
-   [ntfrsutl](ntfrsutl.md)

### <a name="BKMK_o"></a>O
-   [openfiles](openfiles.md)

### <a name="BKMK_p"></a>P
-   [pagefileconfig](pagefileconfig.md)
-   [パス](path.md)
-   [pathping](pathping.md)
-   [pause](pause.md)
-   [pbadmin](pbadmin.md)
-   [pentnt](pentnt.md)
-   [perfmon](perfmon.md)
-   [Ping](ping.md)
-   [pnpunattend](pnpunattend.md)
-   [pnputil](pnputil.md)
-   [popd](popd.md)
-   [PowerShell](PowerShell.md)
-   [PowerShell_ise](PowerShell_ise.md)
-   [印刷](print.md)
-   [prncnfg](prncnfg.md)
-   [prndrvr](prndrvr.md)
-   [prnjobs](prnjobs.md)
-   [prnmngr](prnmngr.md)
-   [prnport](prnport.md)
-   [prnqctl](prnqctl.md)
-   [prompt](prompt.md)
-   [pubprn](pubprn.md)
-   [pushd](pushd.md)
-   [pushprinterconnections](pushprinterconnections.md)

### <a name="BKMK_q"></a>Q
-   [qappsrv](qappsrv.md)
-   [qprocess](qprocess.md)
-   [query](query.md)
-   [quser](quser.md)
-   [qwinsta](qwinsta.md)

### <a name="BKMK_r"></a>R
-   [rcp](rcp.md)
-   [rd](rd.md)
-   [rdpsign](rdpsign.md)
-   [recover](recover.md)
-   [reg](reg.md)
  -   [Reg を追加します。](reg-add.md)
  -   [Reg の比較](reg-compare.md)
  -   [Reg のコピー](reg-copy.md)
  -   [reg delete](reg-delete.md)
  -   [Reg のエクスポート](reg-export.md)
  -   [Reg のインポート](reg-import.md)
  -   [Reg ロード](reg-load.md)
  -   [Reg クエリ](reg-query.md)
  -   [Reg 復元](reg-restore.md)
  -   [Reg 保存](reg-save.md)
  -   [reg unload](reg-unload.md)
-   [regini](regini.md)
-   [regsvr32](regsvr32.md)
-   [relog](relog.md)
-   [rem](rem.md)
-   [ren](ren.md)
-   [rename](rename.md)
-   [repair-bde](repair-bde.md)
-   [replace](replace.md)
-   [セッションをリセットします。](reset-session.md)
-   [rexec](rexec.md)
-   [risetup](risetup.md)
-   [rmdir](rmdir.md)
-   [robocopy](robocopy.md)
-   [route_ws2008](route_ws2008.md)
-   [rpcinfo](rpcinfo.md)
-   [rpcping](rpcping.md)
-   [rsh](rsh.md)
-   [rundll32](rundll32.md)
-   [rwinsta](rwinsta.md)

### <a name="BKMK_s"></a>S
-   [schtasks](schtasks.md)
-   [scwcmd](Scwcmd.md)
  -   [scwcmd: 分析](scwcmd-analyze.md)
  -   [scwcmd: configure](scwcmd-configure.md)
  -   [scwcmd: register](scwcmd-register.md) 
  -   [scwcmd: rollback](scwcmd-rollback.md) 
  -   [scwcmd: transform](scwcmd-transform.md) 
  -   [scwcmd: view](scwcmd-view.md) 
-   [secedit](secedit.md)
  -   [secedit:analyze](secedit-analyze.md)
  -   [secedit:configure](secedit-configure.md)
  -   [secedit:export](secedit-export.md)
  -   [secedit:generaterollback](secedit-generaterollback.md)
  -   [secedit:import](secedit-import.md)
  -   [secedit:validate](secedit-validate.md)
-   [serverceipoptin](serverceipoptin.md)
-   [Servermanagercmd](Servermanagercmd.md)
-   [serverweroptin](serverweroptin.md)
-   [set](set_1.md)
-   [setlocal](setlocal.md)
-   [setx](setx.md)
-   [sfc](sfc.md)
-   [shadow](shadow.md)
-   [shift](shift.md)
-   [showmount](showmount.md)
-   [shutdown](shutdown.md)
-   [並べ替え](sort.md)
-   [start](start.md)
-   [subst](subst.md)
-   [sxstrace](sxstrace.md)
-   [sysocmgr](sysocmgr.md)
-   [systeminfo](systeminfo.md)

### <a name="BKMK_t"></a>T
-   [takeown](takeown.md)
-   [tapicfg](tapicfg.md)
-   [taskkill](taskkill.md)
-   [tasklist](tasklist.md)
-   [tcmsetup](tcmsetup.md)
-   [telnet](telnet.md)
-   [tftp](tftp.md)
-   [time](time.md)
-   [timeout](timeout_1.md)
-   [title](title_1.md)
-   [tlntadmn](tlntadmn.md)
-   [tpmvscmgr](tpmvscmgr.md)
-   [tracerpt](tracerpt_1.md)
-   [tracert](tracert.md)
-   [ツリー](tree.md)
-   [tscon](tscon.md)
-   [tsdiscon](tsdiscon.md)
-   [tsecimp](tsecimp_1.md)
-   [tskill](tskill.md)
-   [tsprof](tsprof.md)
-   [type](type.md)
-   [typeperf](typeperf.md)
-   [tzutil](tzutil.md)

### <a name="BKMK_u"></a>U
-   [unlodctr](unlodctr_1.md)

### <a name="BKMK_v"></a>V
-   [ver](ver.md)
-   [検証方法](verifier.md)
-   [確認します](verify_1.md)
-   [vol](vol.md)
-   [vssadmin](vssadmin.md)- 

### <a name="BKMK_w"></a>W
-   [waitfor](waitfor.md)
-   [wbadmin](wbadmin.md)
  -   [wbadmin バックアップの有効化](wbadmin-enable-backup.md)
  -   [バックアップを無効に wbadmin](wbadmin-disable-backup.md)
  -   [wbadmin start backup](wbadmin-start-backup.md)
  -   [wbadmin の停止ジョブ](wbadmin-stop-job.md)
  -   [wbadmin get バージョン](wbadmin-get-versions.md)
  -   [wbadmin get 項目](wbadmin-get-items.md)
  -   [wbadmin start recovery](wbadmin-start-recovery.md)
  -   [wbadmin get 状態](wbadmin-get-status.md)
  -   [wbadmin get ディスク](wbadmin-get-disks.md)
  -   [wbadmin start systemstaterecovery](wbadmin-start-systemstaterecovery.md)
  -   [wbadmin start systemstatebackup](wbadmin-start-systemstatebackup.md)
  -   [wbadmin delete systemstatebackup](wbadmin-delete-systemstatebackup.md)
  -   [wbadmin start sysrecovery](wbadmin-start-sysrecovery.md)
  -   [wbadmin restore catalog](wbadmin-restore-catalog.md)
  -   [wbadmin delete カタログ](wbadmin-delete-catalog.md)
-   [wdsutil](wdsutil.md)
-   [wecutil](wecutil.md)
-   [wevtutil](wevtutil.md)
-   [where](where_1.md)
-   [whoami](whoami.md)
-   [winnt](winnt.md)
-   [winnt32](winnt32.md)
-   [winpop](winpop.md)
-   [winrs](winrs.md)
-   [wlbs](wlbs_1.md)
-   [Wmic](wmic.md)
-   [wscript](wscript.md)

### <a name="BKMK_x"></a>X
-   [xcopy](xcopy.md)
