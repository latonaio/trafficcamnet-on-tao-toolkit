# trafficcamnet-on-tao-toolkit
trafficcamnet-on-tao-toolkit は、NVIDIA TAO TOOLKIT を用いて TrafficCamNet の AIモデル最適化を行うマイクロサービスです。  

## 動作環境
- NVIDIA 
    - TAO TOOLKIT
- TrafficCamNet
- Docker
- TensorRT Runtime

## 動作手順

### engineファイルの生成
TrafficCamNet のAIモデルをデバイスに最適化するため、ResNet18 における TrafficCamNet の .etlt ファイルを engine file に変換します。
engine fileへの変換は、Makefile に記載された以下のコマンドにより実行できます。

```
tao-convert:
	docker exec -it trafficcamnet-tao-toolkit tao-converter -k tlt_encode -d 3,544,960 -e /app/src/trafficcamnet.engine /app/src/resnet18_trafficcamnet_pruned.etlt 
```

## 相互依存関係にあるマイクロサービス  
本マイクロサービスで最適化された TrafficCamNet の AIモデルを Deep Stream 上で動作させる手順は、[trafficcamnet-on-deepstream](https://github.com/latonaio/trafficcamnet-on-deepstream)を参照してください。  

## engineファイルについて
engineファイルである peoplenet.engine は、[trafficcamnet-on-deepstream](https://github.com/latonaio/trafficcamnet-on-deepstream)と共通のファイルであり、本レポジトリで作成した engineファイルを、当該リポジトリで使用しています。  

