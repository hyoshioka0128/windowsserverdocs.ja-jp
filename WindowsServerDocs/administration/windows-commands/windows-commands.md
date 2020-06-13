---
title: Windows のコマンド
description: リファレンス
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: c703d07c-8227-4e86-94a6-8ef390f94cdc
author: jasongerend
ms.author: jgerend
manager: dongill
ms.date: 06/09/2020
ms.prod: windows-server
ms.openlocfilehash: 66de80652f764840af70e88dfd39df2398ae495c
ms.sourcegitcommit: 99d548141428c964facf666c10b6709d80fbb215
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/12/2020
ms.locfileid: "84721117"
---
# <a name="windows-commands"></a>Windows のコマンド

サポートされているすべてのバージョンの Windows (サーバーとクライアント) には、に組み込まれている一連の Win32 コンソールコマンドがあります。

この一連のドキュメントでは、スクリプトまたはスクリプトツールを使用してタスクを自動化するために使用できる Windows コマンドについて説明します。

特定のコマンドに関する情報を検索するには、次の A-Z メニューで、コマンドの開始文字をクリックし、コマンド名をクリックします。

[A](#a)  |
[B](#b)  |
[C](#c)  |
[D](#d)  |
[E](#e)  |
[F](#f)  |
[G](#g)  |
[H](#h)  |
[I](#i)  |
[J](#j)  |
[K](#k)  |
[L](#l)  |
[M](#m)  |
[N](#n)  |
[O](#o)  |
[P](#p)  |
[Q](#q)  |
[R](#r)  |
[S](#s)  |
[T](#t)  |
[U](#u)  |
[V](#v)  |
[W](#w)  |
[X](#x) |Y |方向

## <a name="prerequisites"></a>前提条件

このトピックに記載されている情報は、以下に適用されます。

- Windows Server 2019
- Windows Server (半期チャネル)
- Windows Server 2016
- Windows Server 2012 R2
- Windows Server 2012
- Windows Server 2008 R2
- Windows Server 2008
- Windows 10
- Windows 8.1

### <a name="command-shell-overview"></a>コマンド シェルの概要

コマンドシェルは、ユーザーアカウント管理や夜間バックアップなどの日常的なタスクをバッチ (.bat) ファイルで自動化するために Windows に組み込まれた最初のシェルでした。 Windows スクリプトホストを使用すると、コマンドシェルでより高度なスクリプトを実行できます。 詳細については、「 [cscript](cscript.md)または[wscript](wscript.md)」を参照してください。 ユーザーインターフェイスを使用する場合よりも、スクリプトを使用すると操作をより効率的に実行できます。 スクリプトは、コマンドラインで使用可能なすべてのコマンドを受け入れます。

Windows には、コマンドシェルと[PowerShell](https://docs.microsoft.com/powershell/scripting/powershell-scripting?view=powershell-6)という2つのコマンドシェルがあります。 各シェルは、ユーザーとオペレーティングシステムまたはアプリケーションとの直接通信を提供するソフトウェアプログラムであり、IT 運用を自動化するための環境を提供します。

PowerShell は、コマンドシェルの機能を拡張して、コマンドレットと呼ばれる PowerShell コマンドを実行するように設計されています。 コマンドレットは Windows コマンドに似ていますが、より拡張可能なスクリプト言語を提供します。 Powershell では Windows コマンドと PowerShell コマンドレットを実行できますが、コマンドシェルで実行できるのは PowerShell コマンドレットではなく Windows コマンドだけです。

最も堅牢で最新の Windows オートメーションの場合は、windows コマンドや windows スクリプトホストの代わりに PowerShell を使用することをお勧めします。

> [!NOTE]
>Powershell のオープンソースバージョンである[Powershell Core](https://docs.microsoft.com/powershell/scripting/whats-new/what-s-new-in-powershell-core-60?view=powershell-6)をダウンロードしてインストールすることもできます。

> [!CAUTION]
> レジストリを正しく編集しないと、システムが正常に動作しなくなる場合があります。 レジストリに次の変更を加える前に、コンピューター上の重要なデータをバックアップする必要があります。

> [!NOTE]
> コンピューターまたはユーザーのログオンセッションでコマンドシェルのファイル名とディレクトリ名の入力候補を有効または無効にするには、 **regedit.exe**を実行し、次の**reg_DWOrd 値**を設定します。
>
> HKEY_LOCAL_MACHINE \Software\Microsoft\Command Processor\ reg_DWOrd
>
> **Reg_DWOrd**値を設定するには、特定の関数に対して制御文字の16進数の値を使用します (たとえば、 **0 9**は Tab、 **0 08**は Backspace です)。 ユーザー指定の設定はコンピューターの設定よりも優先され、コマンドラインオプションはレジストリ設定よりも優先されます。

## <a name="command-line-reference-a-z"></a>コマンドラインリファレンス A-z

特定の Windows コマンドに関する情報を検索するには、次の A-Z メニューで、コマンドの開始文字をクリックし、コマンド名をクリックします。

[A](#a)  |
[B](#b)  |
[C](#c)  |
[D](#d)  |
[E](#e)  |
[F](#f)  |
[G](#g)  |
[H](#h)  |
[I](#i)  |
[J](#j)  |
[K](#k)  |
[L](#l)  |
[M](#m)  |
[N](#n)  |
[O](#o)  |
[P](#p)  |
[Q](#q)  |
[R](#r)  |
[S](#s)  |
[T](#t)  |
[U](#u)  |
[V](#v)  |
[W](#w)  |
[X](#x) |Y |方向

### <a name="a"></a>A

- [active](active.md)
- [add](add.md)
- [add alias](add-alias.md)
- [add volume](add-volume.md)
- [append](append.md)
- [arp](arp.md)
- [assign](assign.md)
- [assoc](assoc.md)
- [at](at.md)
- [atmadm](atmadm.md)
- [attach-vdisk](attach-vdisk.md)
- [attrib](attrib.md)
- [attributes](attributes.md)
  - [attributes disk](attributes-disk.md)
  - [attributes volume](attributes-volume.md)
- [auditpol](auditpol.md)
  - [auditpol backup](auditpol-backup.md)
  - [auditpol clear](auditpol-clear.md)
  - [auditpol get](auditpol-get.md)
  - [auditpol list](auditpol-list.md)
  - [auditpol remove](auditpol-remove.md)
  - [auditpol resourcesacl](auditpol-resourcesacl.md)
  - [auditpol restore](auditpol-restore.md)
  - [auditpol set](auditpol-set.md)
- [autochk](autochk.md)
- [autoconv](autoconv.md)
- [autofmt](autofmt.md)
- [automount](automount.md)

### <a name="b"></a>B

- [bcdboot](bcdboot.md)
- [bcdedit](bcdedit.md)
- [bdehdcfg](bdehdcfg.md)
  - [bdehdcfg driveinfo](bdehdcfg-driveinfo.md)
  - [bdehdcfg newdriveletter](bdehdcfg-newdriveletter.md)
  - [bdehdcfg quiet](bdehdcfg-quiet.md)
  - [bdehdcfg restart](bdehdcfg-restart.md)
  - [bdehdcfg size](bdehdcfg-size.md)
  - [bdehdcfg target](bdehdcfg-target.md)
- [begin backup](begin-backup.md)
- [begin restore](begin-restore.md)
- [bitsadmin](bitsadmin.md)
  - [bitsadmin addfile](bitsadmin-addfile.md)
  - [bitsadmin addfileset](bitsadmin-addfileset.md)
  - [bitsadmin addfilewithranges](bitsadmin-addfilewithranges.md)
  - [bitsadmin cache](bitsadmin-cache.md)
    - [bitsadmin cache および delete](bitsadmin-cache-and-delete.md)
    - [bitsadmin cache および deleteurl](bitsadmin-cache-and-deleteurl.md)
    - [bitsadmin cache および getexpirationtime](bitsadmin-cache-and-getexpirationtime.md)
    - [bitsadmin cache および getlimit](bitsadmin-cache-and-getlimit.md)
    - [bitsadmin cache および help](bitsadmin-cache-and-help.md)
    - [bitsadmin cache および info](bitsadmin-cache-and-info.md)
    - [bitsadmin cache および list](bitsadmin-cache-and-list.md)
    - [bitsadmin cache および setexpirationtime](bitsadmin-cache-and-setexpirationtime.md)
    - [bitsadmin cache および setlimit](bitsadmin-cache-and-setlimit.md)
    - [bitsadmin cache および clear](bitsadmin-cache-clear.md)
  - [bitsadmin cancel](bitsadmin-cancel.md)
  - [bitsadmin complete](bitsadmin-complete.md)
  - [bitsadmin create](bitsadmin-create.md)
  - [bitsadmin の例](bitsadmin-examples.md)
  - [bitsadmin getaclflags](bitsadmin-getaclflags.md)
  - [bitsadmin getbytestotal](bitsadmin-getbytestotal.md)
  - [bitsadmin getbytestransferred](bitsadmin-getbytestransferred.md)
  - [bitsadmin getclientcertificate](bitsadmin-getclientcertificate.md)
  - [bitsadmin getcompletiontime](bitsadmin-getcompletiontime.md)
  - [bitsadmin getcreationtime](bitsadmin-getcreationtime.md)
  - [bitsadmin getcustomheaders](bitsadmin-getcustomheaders.md)
  - [bitsadmin getdescription](bitsadmin-getdescription.md)
  - [bitsadmin getdisplayname](bitsadmin-getdisplayname.md)
  - [bitsadmin geterror](bitsadmin-geterror.md)
  - [bitsadmin geterrorcount](bitsadmin-geterrorcount.md)
  - [bitsadmin getfilestotal](bitsadmin-getfilestotal.md)
  - [bitsadmin getfilestransferred](bitsadmin-getfilestransferred.md)
  - [bitsadmin gethelpertokenflags](bitsadmin-gethelpertokenflags.md)
  - [bitsadmin gethelpertokensid](bitsadmin-gethelpertokensid.md)
  - [bitsadmin gethttpmethod](bitsadmin-gethttpmethod.md)
  - [bitsadmin getmaxdownloadtime](bitsadmin-getmaxdownloadtime.md)
  - [bitsadmin getminretrydelay](bitsadmin-getminretrydelay.md)
  - [bitsadmin getmodificationtime](bitsadmin-getmodificationtime.md)
  - [bitsadmin getnoprogresstimeout](bitsadmin-getnoprogresstimeout.md)
  - [bitsadmin getnotifycmdline](bitsadmin-getnotifycmdline.md)
  - [bitsadmin getnotifyflags](bitsadmin-getnotifyflags.md)
  - [bitsadmin getnotifyinterface](bitsadmin-getnotifyinterface.md)
  - [bitsadmin getowner](bitsadmin-getowner.md)
  - [bitsadmin getpeercachingflags](bitsadmin-getpeercachingflags.md)
  - [bitsadmin getpriority](bitsadmin-getpriority.md)
  - [bitsadmin getproxybypasslist](bitsadmin-getproxybypasslist.md)
  - [bitsadmin getproxylist](bitsadmin-getproxylist.md)
  - [bitsadmin getproxyusage](bitsadmin-getproxyusage.md)
  - [bitsadmin getreplydata](bitsadmin-getreplydata.md)
  - [bitsadmin getreplyfilename](bitsadmin-getreplyfilename.md)
  - [bitsadmin getreplyprogress](bitsadmin-getreplyprogress.md)
  - [bitsadmin getsecurityflags](bitsadmin-getsecurityflags.md)
  - [bitsadmin getstate](bitsadmin-getstate.md)
  - [bitsadmin gettemporaryname](bitsadmin-gettemporaryname.md)
  - [bitsadmin gettype](bitsadmin-gettype.md)
  - [bitsadmin getvalidationstate](bitsadmin-getvalidationstate.md)
  - [bitsadmin help](bitsadmin-help.md)
  - [bitsadmin info](bitsadmin-info.md)
  - [bitsadmin list](bitsadmin-list.md)
  - [bitsadmin listfiles](bitsadmin-listfiles.md)
  - [bitsadmin makecustomheaderswriteonly](bitsadmin-makecustomheaderswriteonly.md)
  - [bitsadmin monitor](bitsadmin-monitor.md)
  - [bitsadmin nowrap](bitsadmin-nowrap.md)
  - [bitsadmin peercaching](bitsadmin-peercaching.md)
    - [bitsadmin peercaching および getconfigurationflags](bitsadmin-peercaching-and-getconfigurationflags.md)
    - [bitsadmin peercaching および help](bitsadmin-peercaching-and-help.md)
    - [bitsadmin peercaching および setconfigurationflags](bitsadmin-peercaching-and-setconfigurationflags.md)
  - [bitsadmin peers](bitsadmin-peers.md)
    - [bitsadmin peers および clear](bitsadmin-peers-and-clear.md)
    - [bitsadmin peers および discover](bitsadmin-peers-and-discover.md)
    - [bitsadmin peers および help](bitsadmin-peers-and-help.md)
    - [bitsadmin peers および list](bitsadmin-peers-and-list.md)
  - [bitsadmin rawreturn](bitsadmin-rawreturn.md)
  - [bitsadmin removeclientcertificate](bitsadmin-removeclientcertificate.md)
  - [bitsadmin removecredentials](bitsadmin-removecredentials.md)
  - [bitsadmin replaceremoteprefix](bitsadmin-replaceremoteprefix.md)
  - [bitsadmin reset](bitsadmin-reset.md)
  - [bitsadmin resume](bitsadmin-resume.md)
  - [bitsadmin setaclflag](bitsadmin-setaclflag.md)
  - [bitsadmin setclientcertificatebyid](bitsadmin-setclientcertificatebyid.md)
  - [bitsadmin setclientcertificatebyname](bitsadmin-setclientcertificatebyname.md)
  - [bitsadmin setcredentials](bitsadmin-setcredentials.md)
  - [bitsadmin setcustomheaders](bitsadmin-setcustomheaders.md)
  - [bitsadmin setdescription](bitsadmin-setdescription.md)
  - [bitsadmin setdisplayname](bitsadmin-setdisplayname.md)
  - [bitsadmin sethelpertoken](bitsadmin-sethelpertoken.md)
  - [bitsadmin sethelpertokenflags](bitsadmin-sethelpertokenflags.md)
  - [bitsadmin sethttpmethod](bitsadmin-sethttpmethod.md)
  - [bitsadmin setmaxdownloadtime](bitsadmin-setmaxdownloadtime.md)
  - [bitsadmin setminretrydelay](bitsadmin-setminretrydelay.md)
  - [bitsadmin setnoprogresstimeout](bitsadmin-setnoprogresstimeout.md)
  - [bitsadmin setnotifycmdline](bitsadmin-setnotifycmdline.md)
  - [bitsadmin setnotifyflags](bitsadmin-setnotifyflags.md)
  - [bitsadmin setpeercachingflags](bitsadmin-setpeercachingflags.md)
  - [bitsadmin setpriority](bitsadmin-setpriority.md)
  - [bitsadmin setproxysettings](bitsadmin-setproxysettings.md)
  - [bitsadmin setreplyfilename](bitsadmin-setreplyfilename.md)
  - [bitsadmin setsecurityflags](bitsadmin-setsecurityflags.md)
  - [bitsadmin setvalidationstate](bitsadmin-setvalidationstate.md)
  - [bitsadmin suspend](bitsadmin-suspend.md)
  - [bitsadmin takeownership](bitsadmin-takeownership.md)
  - [bitsadmin transfer](bitsadmin-transfer.md)
  - [bitsadmin util](bitsadmin-util.md)
    - [bitsadmin util および enableanalyticchannel](bitsadmin-util-and-enableanalyticchannel.md)
    - [bitsadmin util および getieproxy](bitsadmin-util-and-getieproxy.md)
    - [bitsadmin util および help](bitsadmin-util-and-help.md)
    - [bitsadmin util および repairservice](bitsadmin-util-and-repairservice.md)
    - [bitsadmin util および setieproxy](bitsadmin-util-and-setieproxy.md)
    - [bitsadmin util および version](bitsadmin-util-and-version.md)
  - [bitsadmin wrap](bitsadmin-wrap.md)
- [bootcfg](bootcfg.md)
  - [bootcfg addsw](bootcfg-addsw.md)
  - [bootcfg copy](bootcfg-copy.md)
  - [bootcfg dbg1394](bootcfg-dbg1394.md)
  - [bootcfg debug](bootcfg-debug.md)
  - [bootcfg default](bootcfg-default.md)
  - [bootcfg delete](bootcfg-delete.md)
  - [bootcfg ems](bootcfg-ems.md)
  - [bootcfg query](bootcfg-query.md)
  - [bootcfg raw](bootcfg-raw.md)
  - [bootcfg rmsw](bootcfg-rmsw.md)
  - [bootcfg timeout](bootcfg-timeout.md)
- [break](break_1.md)

### <a name="c"></a>C

- [cacls](cacls.md)
- [call](call.md)
- [cd](cd.md)
- [certreq](certreq_1.md)
- [certutil](certutil.md)
- [change](change.md)
  - [change logon](change-logon.md)
  - [change port](change-port.md)
  - [change user](change-user.md)
- [chcp](chcp.md)
- [chdir](chdir.md)
- [chglogon](chglogon.md)
- [chgport](chgport.md)
- [chgusr](chgusr.md)
- [chkdsk](chkdsk.md)
- [chkntfs](chkntfs.md)
- [choice](choice.md)
- [cipher](cipher.md)
- [clean](clean.md)
- [cleanmgr](cleanmgr.md)
- [clip](clip.md)
- [cls](cls.md)
- [cmd](Cmd.md)
- [cmdkey](cmdkey.md)
- [cmstp](cmstp.md)
- [color](color.md)
- [comp](comp.md)
- [compact](compact.md)
- [compact vdisk](compact-vdisk.md)
- [convert](convert.md)
  - [convert basic](convert-basic.md)
  - [convert dynamic](convert-dynamic.md)
  - [convert gpt](convert-gpt.md)
  - [convert mbr](convert-mbr.md)
- [copy](copy.md)
- [cprofile](cprofile.md)
- [create](create.md)
  - [create partition efi](create-partition-efi.md)
  - [[拡張パーティション](create-partition-extended.md)を作成する
  - [create partition logical](create-partition-logical.md)
  - [create partition msr](create-partition-msr.md)
  - [パーティションのプライマリの作成](create-partition-primary.md)
  - [ボリュームミラーの作成](create-volume-mirror.md)
  - [create volume raid](create-volume-raid.md)
  - [create volume simple](create-volume-simple.md)
  - [create volume stripe](create-volume-stripe.md)
- [cscript](cscript.md)

### <a name="d"></a>D

- [date](date.md)
- [dcgpofix](dcgpofix.md)
- [defrag](defrag.md)
- [del](del.md)
- [delete](delete.md)
  - [ディスクの削除](delete-disk.md)
  - [delete partition](delete-partition.md)
  - [影の削除](delete-shadows.md)
  - [delete volume](delete-volume.md)
- [vdisk のデタッチ](detach-vdisk.md)
- [データ](detail.md)
  - [detail disk](detail-disk.md)
  - [detail partition](detail-partition.md)
  - [詳細 vdisk](detail-vdisk.md)
  - [detail volume](detail-volume.md)
- [dfsdiag](dfsdiag.md)
  - [dfsdiag testdcs](dfsdiag-testdcs.md)
  - [dfsdiag testdfsconfig](dfsdiag-testdfsconfig.md)
  - [dfsdiag testdfsintegrity](dfsdiag-testdfsintegrity.md)
  - [dfsdiag testreferral](dfsdiag-testreferral.md)
  - [dfsdiag testsites](dfsdiag-testsites.md)
- [dfsrmig](dfsrmig.md)
- [diantz](diantz.md)
- [dir](dir.md)
- [diskcomp](diskcomp.md)
- [diskcopy](diskcopy.md)
- [diskpart](diskpart.md)
- [diskperf](diskperf.md)
- [diskraid](diskraid.md)
- [diskshadow](diskshadow.md)
- [dispdiag](dispdiag.md)
- [あるいは](dnscmd.md)
- [doskey](doskey.md)
- [driverquery](driverquery.md)

### <a name="e"></a>E

- [echo](echo.md)
- [edit](edit.md)
- [endlocal](endlocal.md)
- [復元の終了](end-restore.md)
- [erase](erase.md)
- [eventcreate](eventcreate.md)
- [eventquery](eventquery.md)
- [eventtriggers](eventtriggers.md)
- [Evntcmd](evntcmd.md)
- [exec](exec.md)
- [exit](exit_2.md)
- [expand](expand.md)
- [vdisk を展開する](expand-vdisk.md)
- [さらす](expose.md)
- [extend](extend.md)
- [extract](extract.md)

### <a name="f"></a>F

- [fc](fc.md)
- [filesystems](filesystems.md)
- [find](find.md)
- [findstr](findstr.md)
- [finger](finger.md)
- [flattemp](flattemp.md)
- [fondue](fondue.md)
- [for](for.md)
- [forfiles](forfiles.md)
- [format](format.md)
- [freedisk](freedisk.md)
- [fsutil](fsutil.md)
  - [fsutil 8dot3name](fsutil-8dot3name.md)
  - [fsutil behavior](fsutil-behavior.md)
  - [fsutil dirty](fsutil-dirty.md)
  - [fsutil file](fsutil-file.md)
  - [fsutil fsinfo](fsutil-fsinfo.md)
  - [fsutil hardlink](fsutil-hardlink.md)
  - [fsutil objectid](fsutil-objectid.md)
  - [fsutil quota](fsutil-quota.md)
  - [fsutil repair](fsutil-repair.md)
  - [fsutil reparsepoint](fsutil-reparsepoint.md)
  - [fsutil resource](fsutil-resource.md)
  - [fsutil sparse](fsutil-sparse.md)
  - [fsutil tiering](fsutil-tiering.md)
  - [fsutil transaction](fsutil-transaction.md)
  - [fsutil usn](fsutil-usn.md)
  - [fsutil volume](fsutil-volume.md)
  - [fsutil wim](fsutil-wim.md)
- [ftp](ftp.md)
  - [ftp append](ftp-append.md)
  - [ftp ascii](ftp-ascii.md)
  - [ftp bell](ftp-bell_1.md)
  - [ftp binary](ftp-binary.md)
  - [ftp bye](ftp-bye.md)
  - [ftp cd](ftp-cd.md)
  - [ftp close](ftp-close_1.md)
  - [ftp debug](ftp-debug.md)
  - [ftp delete](ftp-delete.md)
  - [ftp dir](ftp-dir.md)
  - [ftp disconnect](ftp-disconnect_1.md)
  - [ftp get](ftp-get.md)
  - [ftp glob](ftp-glob_1.md)
  - [ftp hash](ftp-hash_1.md)
  - [ftp lcd](ftp-lcd.md)
  - [ftp literal](ftp-literal_1.md)
  - [ftp ls](ftp-ls_1.md)
  - [ftp mget](ftp-mget.md)
  - [ftp mkdir](ftp-mkdir.md)
  - [ftp mls](ftp-mls_1.md)
  - [ftp mput](ftp-mput_1.md)
  - [ftp open](ftp-open_1.md)
  - [ftp prompt](ftp-prompt_1.md)
  - [ftp put](ftp-put.md)
  - [ftp pwd](ftp-pwd_1.md)
  - [ftp quit](ftp-quit.md)
  - [ftp quote](ftp-quote.md)
  - [ftp recv](ftp-recv.md)
  - [ftp remotehelp](ftp-remotehelp_1.md)
  - [ftp rename](ftp-rename.md)
  - [ftp rmdir](ftp-rmdir.md)
  - [ftp send](ftp-send_1.md)
  - [ftp status](ftp-status.md)
  - [ftp trace](ftp-trace_1.md)
  - [ftp type](ftp-type.md)
  - [ftp user](ftp-user.md)
  - [ftp verbose](ftp-verbose_1.md)
  - [ftp mdelete](ftp-.mdelete_1.md)
  - [ftp mdir](ftp.mdir.md)
- [ftype](ftype.md)
- [fveupdate](fveupdate.md)

### <a name="g"></a>G

- [getmac](getmac.md)
- [gettype](gettype.md)
- [goto](goto.md)
- [gpfixup](gpfixup.md)
- [gpresult](gpresult.md)
- [gpt](gpt.md)
- [gpupdate](gpupdate.md)
- [graftabl](graftabl.md)

### <a name="h"></a>H

- [help](help.md)
- [helpctr](helpctr.md)
- [hostname](hostname.md)

### <a name="i"></a>I

- [icacls](icacls.md)
- [if](if.md)
- [インポート (shadowdisk)](import.md)
- [インポート (diskpart)](import_1.md)
- [inactive](inactive.md)
- [inuse](inuse.md)
- [ipconfig](ipconfig.md)
- [ipxroute](ipxroute.md)
- [irftp](irftp.md)

### <a name="j"></a>J

- [jetpack](jetpack.md)

### <a name="k"></a>K

- [klist](klist.md)
- [ksetup](ksetup.md)
  - [ksetup addenctypeattr](ksetup-addenctypeattr.md)
  - [ksetup addhosttorealmmap](ksetup-addhosttorealmmap.md)
  - [ksetup addkdc](ksetup-addkdc.md)
  - [ksetup addkpasswd](ksetup-addkpasswd.md)
  - [ksetup addrealmflags](ksetup-addrealmflags.md)
  - [ksetup changepassword](ksetup-changepassword.md)
  - [ksetup delenctypeattr](ksetup-delenctypeattr.md)
  - [ksetup delhosttorealmmap](ksetup-delhosttorealmmap.md)
  - [ksetup delkdc](ksetup-delkdc.md)
  - [ksetup delkpasswd](ksetup-delkpasswd.md)
  - [ksetup delrealmflags](ksetup-delrealmflags.md)
  - [ksetup domain](ksetup-domain.md)
  - [ksetup dumpstate](ksetup-dumpstate.md)
  - [ksetup getenctypeattr](ksetup-getenctypeattr.md)
  - [ksetup listrealmflags](ksetup-listrealmflags.md)
  - [ksetup mapuser](ksetup-mapuser.md)
  - [ksetup removerealm](ksetup-removerealm.md)
  - [ksetup server](ksetup-server.md)
  - [ksetup setcomputerpassword](ksetup-setcomputerpassword.md)
  - [ksetup setenctypeattr](ksetup-setenctypeattr.md)
  - [ksetup setrealm](ksetup-setrealm.md)
  - [ksetup setrealmflags](ksetup-setrealmflags.md)
- [ktmutil](ktmutil.md)
- [ktpass](ktpass.md)

### <a name="l"></a>L

- [label](label.md)
- [list](list.md)
  - [プロバイダーの一覧表示](list-providers.md)
  - [影の一覧表示](list-shadows.md)
  - [ライターの一覧表示](list-writers.md)
- [メタデータの読み込み](load-metadata.md)
- [lodctr](lodctr.md)
- [logman](logman.md)
  - [logman create](logman-create.md)
  - [logman 作成アラート](logman-create-alert.md)
  - [logman api の作成](logman-create-api.md)
  - [logman 作成 cfg](logman-create-cfg.md)
  - [logman カウンターの作成](logman-create-counter.md)
  - [logman 作成トレース](logman-create-trace.md)
  - [logman delete](logman-delete.md)
  - [logman インポートと logman エクスポート](logman-import-export.md)
  - [logman query](logman-query.md)
  - [logman の開始と logman の停止](logman-start-stop.md)
  - [logman update](logman-update.md)
  - [logman 更新アラート](logman-update-alert.md)
  - [logman 更新 api](logman-update-api.md)
  - [logman 更新 cfg](logman-update-cfg.md)
  - [logman 更新カウンター](logman-update-counter.md)
  - [logman 更新トレース](logman-update-trace.md)
- [logoff](logoff.md)
- [lpq](lpq.md)
- [lpr](lpr.md)

### <a name="m"></a>M

- [macfile](macfile.md)
- [makecab](makecab.md)
- [bde の管理](manage-bde.md)
  - [bde の状態の管理](manage-bde-status.md)
  - [bde の管理](manage-bde-on.md)
  - [bde を無効にする](manage-bde-off.md)
  - [bde の一時停止を管理する](manage-bde-pause.md)
  - [bde の管理の再開](manage-bde-resume.md)
  - [bde ロックの管理](manage-bde-lock.md)
  - [bde のロック解除の管理](manage-bde-unlock.md)
  - [bde 自動ロック解除の管理](manage-bde-autounlock.md)
  - [bde プロテクターの管理](manage-bde-protectors.md)
  - [bde tpm の管理](manage-bde-tpm.md)
  - [bde setidentifier の管理](manage-bde-setidentifier.md)
  - [bde forcerecovery の管理](manage-bde-forcerecovery.md)
  - [bde の changepassword を管理する](manage-bde-changepassword.md)
  - [bde changepin の管理](manage-bde-changepin.md)
  - [bde 変更キーの管理](manage-bde-changekey.md)
  - [bde keypackage の管理](manage-bde-keypackage.md)
  - [bde のアップグレードの管理](manage-bde-upgrade.md)
  - [bde wipefreespace 領域の管理](manage-bde-wipefreespace.md)
- [mapadmin](mapadmin.md)
- [md](md.md)
- [マージ vdisk](merge-vdisk.md)
- [mkdir](mkdir.md)
- [mklink](mklink.md)
- [mmc](mmc.md)
- [mode](mode.md)
- [more](more.md)
- [mount](mount.md)
- [mountvol](mountvol.md)
- [move](move.md)
- [mqbkup](mqbkup.md)
- [mqsvc](mqsvc.md)
- [mqtgsvc](mqtgsvc.md)
- [msdt](msdt.md)
- [msg](msg.md)
- [msiexec](msiexec.md)
- [msinfo32](msinfo32.md)
- [mstsc](mstsc.md)

### <a name="n"></a>N

- [nbtstat](nbtstat.md)
- [netcfg](netcfg.md)
- [net print](net-print.md)
- [netsh](netsh.md)
- [netstat](netstat.md)
- [nfsadmin](nfsadmin.md)
- [nfsshare](nfsshare.md)
- [nfsstat](nfsstat.md)
- [nlbmgr](nlbmgr.md)
- [nslookup](nslookup.md)
  - [nslookup exit コマンド](nslookup-exit-command.md)
  - [nslookup finger コマンド](nslookup-finger-command.md)
  - [nslookup help](nslookup-help.md)
  - [nslookup ls](nslookup-ls.md)
  - [nslookup lserver](nslookup-lserver.md)
  - [nslookup root](nslookup-root.md)
  - [nslookup server](nslookup-server.md)
  - [nslookup set](nslookup-set.md)
  - [nslookup set all](nslookup-set-all.md)
  - [nslookup set class](nslookup-set-class.md)
  - [nslookup set d2](nslookup-set-d2.md)
  - [nslookup set debug](nslookup-set-debug.md)
  - [nslookup set domain](nslookup-set-domain.md)
  - [nslookup set port](nslookup-set-port.md)
  - [nslookup set querytype](nslookup-set-querytype.md)
  - [nslookup set recurse](nslookup-set-recurse.md)
  - [nslookup set retry](nslookup-set-retry.md)
  - [nslookup set root](nslookup-set-root.md)
  - [nslookup set search](nslookup-set-search.md)
  - [nslookup set srchlist](nslookup-set-srchlist.md)
  - [nslookup set timeout](nslookup-set-timeout.md)
  - [nslookup set type](nslookup-set-type.md)
  - [nslookup set vc](nslookup-set-vc.md)
  - [nslookup view](nslookup-view.md)
- [ntbackup](ntbackup.md)
- [ntcmdprompt](ntcmdprompt.md)
- [ntfrsutl](ntfrsutl.md)

### <a name="o"></a>O

- [なっ](offline.md)
  - [オフラインディスク](offline-disk.md)
  - [オフラインボリューム](offline-volume.md)
- [オンライン](online.md)
  - [オンラインディスク](online-disk.md)
  - [オンラインボリューム](online-volume.md)
- [openfiles](openfiles.md)

### <a name="p"></a>P

- [pagefileconfig](pagefileconfig.md)
- [path](path.md)
- [pathping](pathping.md)
- [pause](pause.md)
- [pbadmin](pbadmin.md)
- [pentnt](pentnt.md)
- [perfmon](perfmon.md)
- [ping](ping.md)
- [pnpunattend](pnpunattend.md)
- [pnputil](pnputil.md)
- [popd](popd.md)
- [powershell](powershell.md)
- [powershell ise](powershell_ise.md)
- [print](print.md)
- [prncnfg](prncnfg.md)
- [prndrvr](prndrvr.md)
- [prnjobs](prnjobs.md)
- [prnmngr](prnmngr.md)
- [prnport](prnport.md)
- [prnqctl](prnqctl.md)
- [prompt](prompt.md)
- [pubprn](pubprn.md)
- [pushd](pushd.md)
- [pushprinterconnections](pushprinterconnections.md)
- [pwlauncher](pwlauncher.md)

### <a name="q"></a>Q

- [qappsrv](qappsrv.md)
- [qprocess](qprocess.md)
- [query](query.md)
  - [query process](query-process.md)
  - [query session](query-session.md)
  - [クエリ termserver](query-termserver.md)
  - [ユーザーのクエリ](query-user.md)
- [quser](quser.md)
- [qwinsta](qwinsta.md)

### <a name="r"></a>R

- [rcp](rcp.md)
- [rd](rd.md)
- [rdpsign](rdpsign.md)
- [recover](recover.md)
- [ディスクグループの回復](recover_1.md)
- [reg](reg.md)
  - [reg add](reg-add.md)
  - [reg 比較](reg-compare.md)
  - [reg コピー](reg-copy.md)
  - [reg の削除](reg-delete.md)
  - [reg エクスポート](reg-export.md)
  - [reg インポート](reg-import.md)
  - [reg 読み込み](reg-load.md)
  - [reg クエリ](reg-query.md)
  - [reg 復元](reg-restore.md)
  - [reg 保存](reg-save.md)
  - [reg アンロード](reg-unload.md)
- [regini](regini.md)
- [regsvr32](regsvr32.md)
- [relog](relog.md)
- [rem バッチファイル](rem.md)
- [rem スクリプト](rem_1.md)
- [remove](remove.md)
- [ren](ren.md)
- [rename](rename.md)
- [修復](repair.md)
  - [bde の修復](repair-bde.md)
- [replace](replace.md)
- [再スキャン](rescan.md)
- [reset](reset.md)
  - [reset session](reset-session.md)
- [日数](retain.md)
- [反転](revert.md)
- [rexec](rexec.md)
- [risetup](risetup.md)
- [rmdir](rmdir.md)
- [robocopy](robocopy.md)
- [ルート ws2008](route_ws2008.md)
- [rpcinfo](rpcinfo.md)
- [rpcping](rpcping.md)
- [rsh](rsh.md)
- [rundll32](rundll32.md)
- [rundll32 printui.dll](rundll32-printui.md)
- [rwinsta](rwinsta.md)

### <a name="s"></a>S

- [san](san.md)
- [sc 構成](sc-config.md)
- [sc の作成](sc-create.md)
- [sc の削除](sc-delete.md)
- [sc クエリ](sc-query.md)
- [schtasks](schtasks.md)
- [scwcmd](scwcmd.md)
  - [scwcmd 分析](scwcmd-analyze.md)
  - [scwcmd の構成](scwcmd-configure.md)
  - [scwcmd レジスタ](scwcmd-register.md)
  - [scwcmd ロールバック](scwcmd-rollback.md)
  - [scwcmd 変換](scwcmd-transform.md)
  - [scwcmd ビュー](scwcmd-view.md)
- [secedit](secedit.md)
  - [secedit 分析](secedit-analyze.md)
  - [secedit 構成](secedit-configure.md)
  - [secedit エクスポート](secedit-export.md)
  - [secedit generaterollback](secedit-generaterollback.md)
  - [secedit インポート](secedit-import.md)
  - [secedit 検証](secedit-validate.md)
- [select](select.md)
  - [select disk](select-disk.md)
  - [パーティションの選択](select-partition.md)
  - [vdisk の選択](select-vdisk.md)
  - [select volume](select-volume.md)
- [serverceipoptin](serverceipoptin.md)
- [servermanagercmd.exe](servermanagercmd.md)
- [serverweroptin](serverweroptin.md)
- [環境変数の設定](set_1.md)
- [シャドウコピーの設定](set_2.md)
  - [コンテキストの設定](set-context.md)
  - [id の設定](set-id.md)
  - [setlocal](setlocal.md)
  - [メタデータの設定](set-metadata.md)
  - [set オプション](set-option.md)
  - [詳細の設定](set-verbose.md)
- [setx](setx.md)
- [sfc](sfc.md)
- [shadow](shadow.md)
- [shift](shift.md)
- [showmount](showmount.md)
- [shrink](shrink.md)
- [shutdown](shutdown.md)
- [復元のシミュレーション](simulate-restore.md)
- [sort](sort.md)
- [start](start.md)
- [サブコマンドのデバイスの設定](subcommand-set-device.md)
- [サブコマンド set drivergroup](subcommand-set-drivergroup.md)
- [サブコマンド set drivergroupfilter](subcommand-set-drivergroupfilter.md)
- [サブコマンド set driverpackage](subcommand-set-driverpackage.md)
- [サブコマンドの設定イメージ](subcommand-set-image.md)
- [サブコマンドによる imagegroup の設定](subcommand-set-imagegroup.md)
- [サブコマンドセットサーバー](subcommand-set-server.md)
- [サブコマンド set transportserver](subcommand-set-transportserver.md)
- [サブコマンド set/get-multicasttransmission](subcommand-start-multicasttransmission.md)
- [サブコマンドの名前空間の開始](subcommand-start-namespace.md)
- [サブコマンドの起動サーバー](subcommand-start-server.md)
- [サブコマンドは transportserver を開始します](subcommand-start-transportserver.md)
- [サブコマンドはサーバーを停止します](subcommand-stop-server.md)
- [サブコマンドは transportserver を停止します](subcommand-stop-transportserver.md)
- [subst](subst.md)
- [sxstrace](sxstrace.md)
- [sysocmgr](sysocmgr.md)
- [systeminfo](systeminfo.md)


### <a name="t"></a>T

- [takeown](takeown.md)
- [tapicfg](tapicfg.md)
- [taskkill](taskkill.md)
- [tasklist](tasklist.md)
- [tcmsetup](tcmsetup.md)
- [telnet](telnet.md)
  - [telnet の終了](telnet-close.md)
  - [telnet の表示](telnet-display.md)
  - [telnet を開く](telnet-open.md)
  - [telnet 終了](telnet-quit.md)
  - [telnet 送信](telnet-send.md)
  - [telnet セット](telnet-set.md)
  - [telnet の状態](telnet-status.md)
  - [telnet の設定解除](telnet-unset.md)
- [tftp](tftp.md)
- [time](time.md)
- [timeout](timeout_1.md)
- [title](title_1.md)
- [tlntadmn](tlntadmn.md)
- [tpmtool](tpmtool.md)
- [tpmvscmgr](tpmvscmgr.md)
- [tracerpt](tracerpt_1.md)
- [tracert](tracert.md)
- [tree](tree.md)
- [tscon](tscon.md)
- [tsdiscon](tsdiscon.md)
- [tsecimp](tsecimp_1.md)
- [tskill](tskill.md)
- [tsprof](tsprof.md)
- [type](type.md)
- [typeperf](typeperf.md)
- [tzutil](tzutil.md)

### <a name="u"></a>U

- [を非公開](unexpose.md)
- [uniqueid](uniqueid.md)
- [unlodctr](unlodctr_1.md)

### <a name="v"></a>V

- [ver](ver.md)
- [verifier](verifier.md)
- [verify](verify_1.md)
- [vol](vol.md)
- [vssadmin](vssadmin.md)
  - [vssadmin delete shadows](vssadmin-delete-shadows.md)
  - [vssadmin list shadows](vssadmin-list-shadows.md)
  - [vssadmin list writers](vssadmin-list-writers.md)
  - [vssadmin resize shadowstorage](vssadmin-resize-shadowstorage.md)

### <a name="w"></a>W

- [waitfor](waitfor.md)
- [wbadmin](wbadmin.md)
  - [wbadmin delete カタログ](wbadmin-delete-catalog.md)
  - [wbadmin delete systemstatebackup](wbadmin-delete-systemstatebackup.md)
  - [wbadmin のバックアップの無効化](wbadmin-disable-backup.md)
  - [wbadmin のバックアップの有効化](wbadmin-enable-backup.md)
  - [wbadmin のディスクの取得](wbadmin-get-disks.md)
  - [wbadmin の項目の取得](wbadmin-get-items.md)
  - [wbadmin の状態の取得](wbadmin-get-status.md)
  - [wbadmin get のバージョン](wbadmin-get-versions.md)
  - [wbadmin restore カタログ](wbadmin-restore-catalog.md)
  - [wbadmin のバックアップの開始](wbadmin-start-backup.md)
  - [wbadmin の回復の開始](wbadmin-start-recovery.md)
  - [wbadmin start sysrecovery](wbadmin-start-sysrecovery.md)
  - [wbadmin start systemstatebackup](wbadmin-start-systemstatebackup.md)
  - [wbadmin start systemstaterecovery](wbadmin-start-systemstaterecovery.md)
  - [wbadmin 停止ジョブ](wbadmin-stop-job.md)
- [wdsutil](wdsutil.md)
- [wecutil](wecutil.md)
- [wevtutil](wevtutil.md)
- [where](where_1.md)
- [whoami](whoami.md)
- [winnt](winnt.md)
- [winnt32](winnt32.md)
- [winpop](winpop.md)
- [winrs](winrs.md)
- [winsat メモリ](winsat-mem.md)
- [winsat の mfmedia](winsat-mfmedia.md)
- [wmic](wmic.md)
- [writer](writer.md)
- [wscript](wscript.md)

### <a name="x"></a>X

- [xcopy](xcopy.md)
