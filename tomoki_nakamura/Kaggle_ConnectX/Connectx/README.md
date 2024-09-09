# Connect X

- Connect X
  - https://www.kaggle.com/competitions/connectx
- 参考notebookのソース
  -  https://www.kaggle.com/code/mhyodo/connectx-with-deep-q-learning-ver


## 仮想環境構築について
前提として、仮想環境を構築するにあたって下記を使う。
> pythonのバージョン管理: pyenv  
> パッケージ管理: venv

ここでは、`connectx-with-deep-q-learning-ver.ipynb`の10セル目まで、importエラーなしで実行できるようにするための、仮想環境構築の手順を示す。  
10セル目ではなぜか、「テンソルのサイズがおかしい」と怒られる。これは未解決。

---

以下仮想環境構築手順（Mac）

pyenvをインストール
```
brew install pyenv
```

python 3.10.12をインストール
```
pyenv install 3.10.12
```

作業ディレクトリ（ココでは`Connectx`）に移動する
```
cd Connectx
```

作業ディレクトリで利用するpyyhonのバージョンを指定する
```
pyenv local 3.10.12
```

仮想環境（ココでは`.connectx-env`）を作成する
```
python -m venv .connectx-env
```

作成した仮想環境に入る
```
source .connectx-env/bin/activate
```

`connectx-with-deep-q-learning-ver.ipynb`を実行するのに必要なライブラリを仮想環境にインストールする
```
pip install numpy gym tensorflow matplotlib tqdm
pip install 'kaggle-environments==0.1.6' > /dev/null 2>&1
```

ここで、`connectx-with-deep-q-learning-ver.ipynb`を１セルずつ実行していくと、10セル目で`ipywidgets`関連のライブラリが無いと言うエラーが発生する。
エラーメッセージに従って`ipywidgets`をインストール
```
pip install ipywidgets
```

ここまでできれば、10セル目まではライブラリに関するエラーなしで実行できるようになる。
10セル目のpythonコードは下記。

```python
pbar = tqdm(range(episodes))
for n in pbar:
    epsilon = max(min_epsilon, epsilon * decay)
    total_reward = play_game(env, TrainNet, TargetNet, epsilon, copy_step)
    all_total_rewards[n] = total_reward
    avg_reward = all_total_rewards[max(0, n - 100):(n + 1)].mean()
    all_avg_rewards[n] = avg_reward
    all_epsilons[n] = epsilon

    pbar.set_postfix({
        'episode reward': total_reward,
        'avg (100 last) reward': avg_reward,
        'epsilon': epsilon
    })

#     with summary_writer.as_default():
#         tf.summary.scalar('episode reward', total_reward, step=n)
#         tf.summary.scalar('running avg reward (100)', avg_reward, step=n)
#         tf.summary.scalar('epsilon', epsilon, step=n)
```

エラー内容は下記。現時点で未解決。

```
---------------------------------------------------------------------------
TypeError                                 Traceback (most recent call last)
Cell In[11], line 4
      2 for n in pbar:
      3     epsilon = max(min_epsilon, epsilon * decay)
----> 4     total_reward = play_game(env, TrainNet, TargetNet, epsilon, copy_step)
      5     all_total_rewards[n] = total_reward
      6     avg_reward = all_total_rewards[max(0, n - 100):(n + 1)].mean()

Cell In[6], line 8
      5 observations = env.reset()
      6 while not done:
      7     # epsilon-greedyで行動を選択
----> 8     action = TrainNet.get_action(observations, epsilon)
     10     # 前の状態
     11     prev_observations = observations

Cell In[5], line 53
     51     return int(np.random.choice([c for c in range(self.num_actions) if state.board[c] == 0]))
     52 else:
---> 53     prediction = self.predict(np.atleast_2d(self.preprocess(state)))[0].numpy()
     54     for i in range(self.num_actions):
     55         if state.board[i] != 0:

Cell In[5], line 16
...

too many positional arguments

Arguments received by DeepModel.call():
  • inputs=tf.Tensor(shape=(1, 43), dtype=float32)
```