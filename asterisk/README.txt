IP電話サービス対応 Asterisk修正プログラム 説明書

                  Copyright (C) 2009-2017 Rakuten Communications Corp.
                                                           Aug 4, 2017

配布物について
==============

  配布物には以下のファイルが含まれます。

  README.txt                        : 本ドキュメント
  gpl-2.txt                         : GPL2ライセンス
  asterisk-13.16.0_rcom.patch       : 修正プログラム
  incoming.agi                      : agiプログラム
  outgoing.agi                      : agiプログラム
  sip.conf.sample                   : サンプル設定ファイル
  extensions.conf.sample            : サンプル設定ファイル


修正プログラムについて
======================

  本修正プログラムは、IP電話サービス(*1)でOSSのIP-PBX『Asterisk』を利
  用可能とするため(*2)、SIPモジュール chan_sip.so を構成するソースコー
  ド chan_sip.c および sip.h を修正したものです。

  (*1)楽天コミュニケーションズのIP加入電話サービスです。
      当サービスのご利用にあたっては当サービスの約款が適用されます。
  (*2)本修正プログラムの使用許諾契約に同意され、修正プログラムの適用お
      よび後述するagiプログラムの利用ならびにサンプル設定ファイルに示
      す適切な設定を行うことが条件となります。

  ■修正プログラムを適用する

  (Asteriskソースディレクトリ)に修正プログラムを格納します。
  修正プログラムを格納したディレクトリで次のコマンドを実行します。

  # patch --verbose -p1 < asterisk-13.16.0_rcom.patch

  修正プログラムの適用後、makeおよびmake installを行ってください。


agiプログラムについて
=====================

  本agiプログラムは、IP電話サービスのSIP I/Fに準拠させるためのもので
  す。

  ■agiプログラムを利用可能にする
    ※ Asteriskがインストール済みであることを前提とします。

  /var/lib/asterisk/agi-bin/ にファイルを格納します。
  格納したファイルに対して実行権を付与するコマンドを実行します。

  # chmod +x incoming.agi
  # chmod +x outgoing.agi


コンフィグについて
==================

  ■sip.conf

  修正プログラムではsip.confに記述するパラメータとして、次のオプション
  を新たに定義しています。

  fusioncom
      yesまたはnoに設定できます。
      yes：SIPチャネルが、IP電話サービスのSIP I/F準拠で動作します。
      no ：SIPチャネルが、Asterisk標準の仕様で動作します。

      ※ 記述がない場合はデフォルト値(yes)が設定されます。
      ※ yes/no選択可能としていますが、IP電話サービスのセクション
         には、記述なしとするかyesを設定してください。

  設定例は、sip.conf.sampleを確認してください。

  設定の確認は、CLI上で以下のコマンドを実行します。

  ・グローバルの設定を確認する場合
    # sip show settings
      ･･･
      FUSION Communications: (設定値)
      ･･･

  ・該当ピアの設定を確認する場合
    # sip show peer ピア名
      ･･･
      Use FUSION: (設定値)
      ･･･

  ・該当チャネルの設定を確認する場合
    # sip show channel チャネル名
      ･･･
      Use FUSION: (設定値)
      ･･･

  ■extensions.conf

  着信時の該当extenでincoming.agiを呼び出すよう記述します。
  発信時の該当extenでoutgoing.agiを呼び出すよう記述します。

  設定例は、extensions.conf.sampleを確認してください。


問い合わせ、サポート、免責について
==================================

  配布物に含まれるすべてのプログラムはGPL2に基づき無保証となります。
  詳しくは本修正プログラムのダウンロードページをご確認ください。
  https://comm.rakuten.co.jp/houjin/asterisk_ip/
