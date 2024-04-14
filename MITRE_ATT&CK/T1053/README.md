# Scheduled Task/Job

| Tactics | Platforms | Permissions Required | Effective Permissions |
|-|-|-|-|
| Execution, Persistence, Privilege Escalation | Containers, Linux, Windows, macOS | Administrator, SYSTEM, User | Administrator, SYSTEM, User |

https://attack.mitre.org/techniques/T1053/

* 攻撃者は、タスクスケジューリング機能を悪用し、悪意あるコードの初回実行や反復実行を容易にする可能性がある。
  * すべての主要なオペレーティングシステムには、指定した日時に実行されるプログラムやスクリプトをスケジュールするユーティリティが存在する。
  * タスクは、適切な認証（例：Windows環境におけるRPCとファイルとプリンタの共有）を満たせば、リモートシステム上でスケジュールすることもできる。
    * リモートシステム上でタスクをスケジューリングするには、通常、リモートシステムの管理者または特権グループのメンバーであることが必要になるかもしれない。
* 攻撃者は、タスクスケジューリングを使って、システム起動時や、永続化のためにスケジュールされたベースでプログラムを実行することができる。
* また、これらの仕組みを悪用して、指定されたアカウント（昇格した権限/特権を持つアカウントなど）のコンテキスト下でプロセスを実行することも可能である。
* システムバイナリのプロキシ実行と同様に、敵対者はタスクスケジューリングを悪用して、信頼されたシステムプロセスの下で1回限りの実行をマスクする可能性もある。