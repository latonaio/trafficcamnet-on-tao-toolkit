# trafficcamnet-on-tao-toolkit
trafficcamnet-on-tao-toolkit は、NVIDIA TAO TOOLKIT を用いて TrafficCamNet の AIモデル最適化を行うマイクロサービスです。  

## 動作環境
- NVIDIA 
    - TAO TOOLKIT
- TrafficCamNet
- Docker
- TensorRT Runtime

## TrafficCamNetについて
TrafficCamNet は、画像内の車、人、道路標識、および二輪車を検出し、カテゴリラベルを返すAIモデルです。  
TrafficCamNet は、特徴抽出にResNet18を使用しており、混雑した場所でも正確に物体検出を行うことができます。

## 動作手順

### engineファイルの生成
TrafficCamNet のAIモデルをデバイスに最適化するため、ResNet18 における TrafficCamNet の .etlt ファイルを engine file に変換します。  
現時点におけるNVIDIAの仕様では、GPUのアーキテクチャごとに engine file の生成が必要です。つまり、あるサーバで生成した engine file を別のサーバーにそのまま適用することはできません。  
本レポジトリに格納された trafficcamnet.engine は、実際に生成される engine file の参考例です。  
engine fileへの変換は、Makefile に記載された以下のコマンドにより実行できます。  

```
tao-convert:
	docker exec -it trafficcamnet-tao-toolkit tao-converter -k tlt_encode -d 3,544,960 -e /app/src/trafficcamnet.engine /app/src/resnet18_trafficcamnet_pruned.etlt 
```

## 相互依存関係にあるマイクロサービス  
本マイクロサービスで最適化された TrafficCamNet の AIモデルを Deep Stream 上で動作させる手順は、[trafficcamnet-on-deepstream](https://github.com/latonaio/trafficcamnet-on-deepstream)を参照してください。  

## engineファイルについて
engineファイルである peoplenet.engine は、[trafficcamnet-on-deepstream](https://github.com/latonaio/trafficcamnet-on-deepstream)と共通のファイルであり、本レポジトリで作成した engineファイルを、当該リポジトリで使用しています。  

