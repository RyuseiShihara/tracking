# tracking
物体検出(yolov5)と物体追跡(DeepSORT)を用いて通過した人とその方向を検出し、入退室を測定することができます。

カメラから取得した画像データの1フレームごとの処理<br>
① 画像データをカメラより取得後、初めに3-1-1の方法で、歩行者の検出を行う <br>
② 検出した歩行者に対して、3-3の方法で、過去の追跡結果の予測位置と比較して、同一
の人物か判定する<br>
③ ②で、該当する人物が存在しない場合、3-2-2 の方法で新規の IDを付与して、新たな
人物として認識する<br> 
④ 次に、bounding box の座標から重心を求めて、前のフレームとの軌跡が境界線と交差
したかを判定する。境界線は、図 6 の赤線のように取得した画像上の座標(0,ℎ/
 2),(𝑤,ℎ/2)の 2 点を結ぶ線分として設定する。この境界線との交差判定の具体的な方
法は4-2-1で述べる<br>
⑤ ④で交差したと判定した場合、次に境界線に対して重心がどちら側にあるかを判定す
る。これにより、追跡している歩行者が入室方向か退出方向に進んだかを判定する。
この具体的な方法は4-2-2で述べる<br>
⑥ 最後に、tracksのデータを更新して、次のフレームの処理に進む<br>

<img src="https://github.com/RyuseiShihara/tracking/assets/69947656/1e04af8b-dfaa-4b9b-80e0-edd97484f12f" width="70%">


・デモ動画
https://www.youtube.com/shorts/HCB6ao4Xulg
上方向を入室、下方向を退出としたとき、このカメラを入口に設置した場所の人数を測定することができます。
