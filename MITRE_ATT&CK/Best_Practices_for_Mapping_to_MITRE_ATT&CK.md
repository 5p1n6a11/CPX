# Best Practices for MITRE ATT&CK Mapping

MITRE ATT&CK マッピングのベストプラクティス

## INTRODUCTION

はじめに

For the Cybersecurity and Infrastructure Security Agency (CISA), understanding adversary behavior is often the first step in protecting networks and data. The success network defenders have in detecting and mitigating cyberattacks depends on this understanding. The MITRE ATT&CK framework is a globally accessible knowledge base of adversary tactics and techniques based on real-world observations. ATT&CK provides details on 100+ threat actor groups, including the techniques and software they are known to use.[^1] ATT&CK can be used to identify defensive gaps, assess security tool capabilities, organize detections, hunt for threats, engage in red team activities, or validate mitigation controls. CISA uses ATT&CK as a lens through which to identify and analyze adversary behavior. CISA created this guide with the Homeland Security Systems Engineering and Development Institute (HSSEDI), a DHS-owned, federally funded research and development center (FFRDC) that works with the MITRE ATT&CK team.

Cybersecurity and Infrastructure Security Agency（CISA）にとって、敵の行動を理解することは、ネットワークとデータを保護するための最初のステップであることが多い。ネットワーク防御者がサイバー攻撃を検知し、軽減することができるかどうかは、この理解にかかっています。MITRE ATT&CK フレームワークは、実世界の観察に基づいた敵対者の戦術とテクニックに関するグローバルにアクセス可能な知識ベースです。ATT&CK は、100 を超える脅威行為者グループについて、彼らが使用することが知られている技 術やソフトウェアを含む詳細を提供します。[^1] ATT&CK は、防御のギャップの特定、セキュリティ・ツールの能力の評価、検出の編成、脅威のハント、レッ ド・チーム活動、または緩和策の検証に使用することができます。CISA は、ATT&CK を、敵の行動を特定し分析するためのレンズとして使用している。CISAは、MITREのATT&CKチームと協力しているDHS所有の連邦政府資金による研究開発センター（FFRDC）であるHomeland Security Systems Engineering and Development Institute（HSSEDI）と共にこのガイドを作成した。

[^1]: Not every adversary behavior is documented in ATT&CK （すべての敵の行動がATT&CKに記録されているわけではない。）

### What’s New

新着情報

Since the initial release of Best Practices for MITRE ATT&CK Mapping in June 2021, malicious cyber operators and operations have continued to evolve at a rapid pace. To maintain relevancy and maximize impact for defenders, MITRE ATT&CK has also evolved the ATT&CK framework, adding major new structures, features, and techniques. Beginning with ATT&CK version nine (v9) these changes include:

2021年6月にMITRE ATT&CK Mappingのベストプラクティスを最初にリリースして以来、悪意のあるサイバーオペレーターとオペレーションは急速なペースで進化し続けています。防衛側にとって適切性を維持しインパクトを最大化するために、MITRE ATT&CKはATT&CKフレームワークも進化させ、主要な新構造、新機能、新技法を追加しました。ATT&CK バージョン 9（v9）からは、以下のような変更が加えられています：

* The introduction of new platforms,
* 新しいプラットフォームの導入、

* Expansion of macOS and Linux coverage,
* macOSとLinuxのカバー範囲を拡大、

* Increased equity between the Industrial Control Systems (ICS), Mobile, and Enterprise matrices,
* 産業用制御システム（ICS）、モバイル、エンタープライズマトリックス間の公平性の向上、

* The redefinition of data sources and detections, and
* データソースと検出の再定義。

* The addition of ATT&CK Campaigns.
* ATT&CKキャンペーンの追加。

As of version 12 (v12), ATT&CK for Enterprise contains 14 tactics, 193 techniques, and 401 subtechniques.

バージョン12（v12）の時点で、ATT&CK for Enterpriseには14の戦術、193のテクニック、401のサブテクニックが含まれています。

The January 2023 update of Best Practices for MITRE ATT&CK Mapping covers the above list of ATT&CK updates. This version of the best practices also covers common analytical biases, mapping mistakes, and specific ATT&CK mapping guidance for ICS.

MITRE ATT&CK マッピングのベストプラクティスの 2023 年 1 月更新版は、上記の ATT&CK の更新リストをカバーしている。ベストプラクティスのこのバージョンは、一般的な分析バイアス、マッピングの間違い、ICSのための特定のATT&CKマッピングガイダンスもカバーしている。

### ATT&CK Levels

ATT&CKレベル

ATT&CK describes behaviors across the adversary lifecycle, commonly known as tactics, techniques, and procedures (TTPs). In ATT&CK, these behaviors correspond to four increasingly granular levels:

ATT&CKは、一般に戦術、技術、手順（TTP）として知られる敵のライフサイクル全体にわたる行動を記述する。ATT&CK では、これらの行動は次第に細かくなる 4 つのレベルに対応しています：

(1) Tactics represent the "why" of an ATT&CK technique or sub-technique. They are the adversary's technical goals, the reason for performing an action, and what they are trying to achieve. For example, an adversary may want to achieve credential access to gain access to a target network. Each tactic contains an array of techniques that network defenders have observed being used in the wild by threat actors. Note: The ATT&CK framework is not intended to be interpreted as linear-with the adversary moving through the tactics in a straight line (i.e., left to right) to accomplish their goal.[^2] Additionally, an adversary does not need to use all the ATT&CK tactics to achieve their operational goals.

(1) 戦術とは、ATT&CKのテクニックやサブテクニックの「理由」を表すものである。これは敵の技術的目標であり、行動を実行する理由であり、何を達成しようとしているかである。たとえば、敵対者はターゲット・ネットワークにアクセスするためにクレデンシャル・ア クセスを達成したいと考えるかもしれない。各戦術には、ネットワーク防御者が脅威行為者によって実際に使用されていることを観察したテクニックの数々が含まれています。注：ATT&CK フレームワークは、敵対者が目標を達成するために戦術を一直線に（つまり左から右に）移動するような、直線的なものとして解釈されることを意図していません。さらに、敵対者は作戦目標を達成するために ATT&CK の戦術をすべて使用する必要はありません。

(2) Techniques represent "how" an adversary achieves a tactical goal by performing an action. For example, an adversary may dump credentials to achieve credential access. Techniques may also represent what an adversary gains by performing an action. A technique is a specific behavior to achieve a goal and is often a single step in a string of activities intended to complete the adversary's overall mission. Note: Some of the techniques within ATT&CK enable an adversary to achieve multiple tactical goals and thus apply to multiple ATT&CK tactics. Many techniques also include legitimate system functions that can be used for malicious purposes (referred to as "living off the land").

(2) 手法は、敵対者が行動を実行することによって戦術的目標を達成する「方法」を表す。たとえば、敵対者はクレデンシャル・ア クセスを達成するためにクレデンシャルをダンプすることがある。テクニックは、敵対者が行動を実行することによって何を得るかを表すこともある。テクニックは目標を達成するための具体的な行動であり、多くの場合、敵対者の全体的な使命を完遂することを意図した一連の活動の単一ステップである。注：ATT&CK のテクニックの中には、敵対者が複数の戦術目標を達成することを可能にするものがあり、したがって複数の ATT&CK 戦術に適用される。また、多くのテクニックには、悪意のある目的のために使用することができる正当なシステム機能が含まれている（「土地を離れて生活する」と呼ばれる）。
   
(3) Sub-techniques provide more granular descriptions of techniques. For example, there are behaviors under the OS credential dumping [T1003] technique that describe specific methods to perform the technique, such as accessing Local Security Authority Subsystem Service (LSASS) memory [T1003.001], Security Account Manager [T1003.002], or `/etc/passwd` and `/etc/shadow` [T1003.008]. Sub-techniques are often, but not always, operating system- or platform-specific. Not all techniques have sub-techniques.

(3) サブテクニックは、技法のより詳細な記述を提供する。例えば、OS クレデンシャルダンプ[T1003]技法の下には、ローカルセキュリティオーソリティサブシステムサービス(LSASS)メモリへのアクセス[T1003.001]、セキュリティアカウントマネージャ[T1003.002]、`/etc/passwd` および `/etc/shadow` [T1003.008]など、技法を実行するための特定の方法を記述する動作があります。サブテクニックは、オペレーティングシステムやプラットフォームに固有であることが多いですが、必ずしもそうではありません。すべてのテクニックにサブテクニックがあるわけではありません。

(4) Procedures represent "what" an adversary did and are instances of how an adversary has used a technique or sub-technique. For example, there are many different procedures of OS credential dumping: LSASS memory [T1003.001] based on using different tools, utilities, and commands. Knowing procedures may be useful for replication of an incident with adversary emulation and for detecting malicious activity.

(4)手順は、敵が「何を」行ったかを表し、敵がテクニックまたはサブテクニックをどのように使用したかの例である。例えば、OS のクレデンシャルダンプには多くの異なる手順があります： LSASSメモリ[T1003.001]は、異なるツール、ユーティリティ、コマンドを使用することに基づいています。手順を知ることは、敵のエミュレーションによるインシデントの再現や、悪意のある活動を検出するのに役立つかもしれません。

[^2]:  For example, after initial access [TA0001] and during an operation, the adversary may exfiltrate data (exfiltration [TA0010]) and then implement additional persistence mechanisms (persistence [TA0003]), switching tactics from right to left. （例えば、最初のアクセス[TA0001]の後、作戦の間に、敵対者はデータを流出させ（流出[TA0010]）、その後、追加の永続化メカニズム（永続化[TA0003]）を実装し、戦術を右から左に切り替えるかもしれない。）

### ATT&CK Technology Domains

ATT&CKテクノロジー・ドメイン

ATT&CK is organized in three "technology domains"-the ecosystem within which an adversary operates. The ATT&CK domains have matrices that reflect associated platforms (or systems) within each technology domain:

ATT&CKは3つの「テクノロジー・ドメイン」（敵対者が活動するエコシステム）で構成されている。ATT&CKのドメインは、各テクノロジー・ドメイン内の関連プラットフォーム（またはシステム）を反映したマトリックスを持っている：

* MITRE ATT&CK - Enterprise:[^3]
* MITRE ATT&CK - エンタープライズ：
  * Operating systems: Windows, Linux, and MacOS
  * オペレーティングシステム Windows、Linux、MacOS
  * Cloud: Azure AD, Office 365, Google Workspace, Software-as-a-Service (SaaS), Infrastructure-as-a-Service (IaaS)
  * クラウド Azure AD、Office 365、Google Workspace、SaaS（Software-as-a-Service）、IaaS（Infrastructure-as-a-Service）
  * Network: Network infrastructure devices
  * ネットワーク ネットワークインフラ機器
  * Containers: Container technologies
  * コンテナ コンテナ技術
  * PRE: Covering preparatory techniques, deprecating the previous PRE-ATT&CK domain
  * PRE： 以前のPRE-ATT&CK領域を廃止し、準備技術をカバーする。
* MITRE ATT&CK - Mobile: Provides a model of adversarial tactics and techniques to operate within the Android and iOS platforms. ATT&CK for Mobile also contains a separate matrix of network-based effects, which are techniques that an adversary can employ without access to the mobile device itself.
* MITRE ATT&CK - モバイル： Android および iOS プラットフォームで動作する敵対的な戦術とテクニックのモデルを提供します。また、ATT&CK for Mobile には、敵対者がモバイルデバイス自体にアクセスすることなく使用できるテクニックである、ネットワークベースの効果に関する個別のマトリックスも含まれています。
* MITRE ATT&CK - Industrial Control Systems (ICS): Focuses on tactics and techniques of adversaries whose primary goal is disrupting an industrial control process, including supervisory control and data acquisition (SCADA) systems, and other control system configurations.
* MITRE ATT&CK - 産業制御システム（ICS）： 監督制御およびデータ収集（SCADA）システム、およびその他の制御システム構成を含む、産業制御プロセスの破壊を主目的とする敵対者の戦術と技術に焦点を当てる。

[^3]: ATT&CK Version 8 integrated PRE-ATT&CK techniques into ATT&CK for Enterprise, creating the new Reconnaissance and Resource Development tactics. The PRE-ATT&CK matrix was deprecated and although it remains in the knowledge base, it will no longer be updated. See MITRE's ATT&CK blog: Bringing PRE into Enterprise, October 27, 2020. （ATT&CK バージョン 8 は、PRE-ATT&CK テクニックを ATT&CK for Enterprise に統合し、新しい偵察戦術と資源開発戦術を生み出しました。PRE-ATT&CK マトリックスは非推奨となり、知識ベースには残っているが、今後更新されることはない。MITRE の ATT&CK ブログを参照： 2020年10月27日、PREをエンタープライズに導入する。）

### ATT&CK Mapping Guidance

ATT&CKマッピング・ガイダンス

CISA is providing this guidance to help analysts accurately and consistently map adversary behaviors to the relevant ATT&CK techniques as part of cyber threat intelligence (CTI) - whether the analyst wishes to incorporate ATT&CK into a cybersecurity publication or an analysis of raw data.

CISAは、サイバー脅威インテリジェンス（CTI）の一環として、アナリストがサイバーセキュリティの出版物や生データの分析にATT&CKを組み込むことを望むかどうかにかかわらず、敵の行動を関連するATT&CK技術に正確かつ一貫してマッピングできるよう、このガイダンスを提供しています。

Successful applications of ATT&CK should produce an accurate and consistent set of mappings, which will not directly solve security challenges but can be used to enable other operations such as:

ATT&CKの応用に成功すれば、正確で一貫性のあるマッピングのセットを作成することができるはずである。これは、セキュリティ上の課題を直接解決するものではないが、以下のような他の作業を可能にするために使用することができる：

* Developing adversary profiles.
* 敵のプロファイルを作成する。

* Conducting activity trend analysis.
* 活動傾向分析の実施

* Augmenting reports for detection, response, and mitigation purposes.
* 検知、対応、緩和を目的としたレポートの補強。

Although there are different ways to approach this task, this guidance provides a starting point. Note: CISA and MITRE ATT&CK recommend that analysts first become comfortable with mapping finished reports to ATT&CK, as there are often more clues within finished reports that can aid an analyst in determining the appropriate mapping.

この作業にはさまざまなアプローチ方法があるが、このガイダンスは出発点を示すものである。注：CISAとMITREのATT&CKは、アナリストが適切なマッピングを決定する際に役立つヒントが、完成したレポートの中にあることが多いため、まず完成したレポートをATT&CKにマッピングすることに慣れることを推奨している。

For additional resources on learning about and using the ATT&CK framework, see Appendix A. For guidance on mapping ATT&CK to ICS, see Appendix B.

ATT&CKフレームワークについて学び、活用するための追加資料については、付録Aを参照のこと。ATT&CKをICSにマッピングするためのガイダンスについては、付録Bを参照のこと。

To Map or Not to Map

地図を作るか作らないか

Why sufficient context matters

なぜ十分な文脈が重要なのか

Without adequate contextual technical details to sufficiently describe and add insight into an adversary behavior, there is little value to ATT&CK mapping. For example, a simple list of ATT&CK tactics or techniques-without associated technical context that explains how the adversary executed the techniques-may not be actionable enough to enable network defenders to detect, mitigate, or respond to the threat.

敵の行動を十分に説明し、洞察するための適切なコンテキスト技術的詳細がなければ、ATT&CK マッピングの価値はほとんどありません。例えば、ATT&CK の戦術やテクニックの単純なリストでは、敵対者がそのテクニックをどのように実行したかを説明する関連する技術的なコンテキストがないため、ネットワーク防御者が脅威を検出、緩和、または対応するのに十分な実用性がない可能性があります。

## References

https://www.cisa.gov/sites/default/files/2023-01/Best%20Practices%20for%20MITRE%20ATTCK%20Mapping.pdf
