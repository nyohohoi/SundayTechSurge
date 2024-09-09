# SundayTechSurge
日曜勉強会でのコラボレーションハブ  
※ 2024/12/31まで利用予定


## 概要
このリポジトリでプログラミング作業を共有し、仮想環境の構築中やプログラミング中に発生したエラーに対し、他のメンバーの成功例を参考に解決策を模索できるようにする

このリポジトリの活動スコープは下記
- [ゼロから作るDeep Learning ❹ ―強化学習編](https://www.amazon.co.jp/%E3%82%BC%E3%83%AD%E3%81%8B%E3%82%89%E4%BD%9C%E3%82%8BDeep-Learning-%E2%80%95%E5%BC%B7%E5%8C%96%E5%AD%A6%E7%BF%92%E7%B7%A8-%E6%96%8E%E8%97%A4-%E5%BA%B7%E6%AF%85/dp/4873119758)
- [Kaggleの「ConnectX」コンペティション](https://www.kaggle.com/competitions/connectx)


## リポジトリ構造
各メンバー専用の作業スペースを作りコードを管理  
リポジトリは以下のように構成: 
```
SundayTechSurge
│
├── <ずきさんのディレクトリ>/
│   ├── DeepLearning4_Reinforcement/
│   └── Kaggle_ConnectX/
│
├── <新崎くんのディレクトリ>/
│   ├── DeepLearning4_Reinforcement/
│   └── Kaggle_ConnectX/
│
├── <中村のディレクトリ>/
│   ├── DeepLearning4_Reinforcement/
│   └── Kaggle_ConnectX/
│
│── .gitignore
└── README.md
```

## 注意事項
仮想環境ディレクトリはサイズが大きく、クローンやフェッチの時間が長くなるため、`.gitignore`ファイルに追加して、Gitの追跡対象から外すこと  
仮想環境は`requirements.txt`に変換してもらえると良いかと
```
pip freeze > requirements.txt
```