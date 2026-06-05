[Introducing midihum: An ML-Based MIDI Humanizing Tool](https://www.erichgrunewald.com/posts/introducing-midihum-an-ml-based-midi-humanizing-tool/)

>midihum is a command-line tool for humanizing MIDI – that is, for taking as input MIDI compositions and producing as output those same compositions with new velocity (loudness/dynamics) values for each of the contained notes. midihum uses gradient boosted trees, with ~400 engineered features, and is trained on 2.6K competition piano performances. You can use it to make your digital compositions sound more natural and expressive, and to find natural climaxes and moments of relaxation in a composition.

- take A as input and B as output
	- take a as a gradient, cook and serve b as meal
	- import A and export B


>Using midihum is easy enough, if you have a basic familiarity with the command line. After installing it, you navigate to the project directory and run

```
python main.py humanize /path/to/input.mid /path/to/output.mid
```
to humanize the MIDI file at `/path/to/input.mid`, saving the humanized file to `/path/to/output.mid`.

![[Pasted image 20260504123802.png]]
> I have worked on this tool on and off for the past five years, and have now gotten it to a state with which I am quite happy. It performs well, at least for solo piano works of roughly the type it was trained on, i.e., from the Baroque, Classical, and especially Romantic periods of Western art music. For example, the following plot shows the actual and predicted velocities for nine randomly chosen (not cherry-picked) performances from the validation set. (Each dot is a MIDI “note on” event, i.e., a note being sounded. The notes shown are a randomly sampled subset of those in the composition, to avoid cluttering the plot.) There is a strong correlation between the predicted and actual velocities.[1]

- on and off
	- To do something ==intermittently==; to perform a task ==periodically== rather than continuously.
- get it to a ==state==
	- To progress a project or task to ==a specific point== where it is functional, stable, or ready for the next step
- works of roughly the type (that)
	- 大まかにthat ~ のような種類の作品
- correlation
	- A mutual relationship or connection between two or more things.
	- mutual : Experienced or done by each of two or more parties toward the other; shared in common
	- 相関関係にある
- cherry-pick
	- 熟したものだけ取る＝都合のいいものだけを選りすぐって取る
- cluttering
	- Filling a space with too many objects or data points in an untidy or disorganized way
	- messing up
- subset
	- A smaller group or collection of things that are part of a larger group (the "set").
	- A portion of total data set
- validation
	- he action of checking or proving the validity or accuracy of something
	- valid - 妥当である

![[Pasted image 20260504133404.png]]
>You can also see that the velocities predicted by midihum are more extreme, in the sense that they tend more towards very high and very low values, than those performed by humans. I tuned the model that way because it suits my taste, but this is the result of a scaling factor applied in post-processing, and could easily be toned down to make the two line up better. The difference is especially obvious when comparing the distributions of velocity values, where the tails are somewhat fatter for the distribution of predicted velocities, as shown below.

- distribution
	- 配布・散らばり→ 分布（確率分布・頻度分布）
- Fat-tailed
	- 肥大した裾
	- 予測値の分布において、実測値よりも「極端な値（大きな値や小さな値）」が現れる確率が高くなっている。

> As mentioned, midihum uses gradient boosted trees (via XGBoost) for its model, where each observation is one MIDI “note on” event, with a large (~400, narrowed down from ~1K) set of engineered features. midihum’s predictive power is mostly a product of the engineered features, which were largely ==inspired by== instruments used in technical analysis of stocks and other securities. 

- (~400, narrowed down from ~1K) set
	- narrow down : limited
	- 絞り込み　400 ~ 1000
- technical analysis of stocks and other securities
	- A methodology used for forecasting the direction of prices through the study of past market data, primarily price and volume, often using charts and mathematical indicators.
	- 株価や債券などの金融商品の値動きを、過去のチャート（価格や出来高）から分析して将来を予測する手法です。この文章では、音楽データの特徴を抽出するための「手法の着想源（ヒント）」として使われています。

>Some of the most important features, according to the XGBoost feature_importances_ attribute, are:
- Features derived from the logarithm of the duration that a note was sustained, for example, [averages of the lowest and highest sustain values in a period, sometimes time-shifted](https://en.wikipedia.org/wiki/Ichimoku_Kink%C5%8D_Hy%C5%8D).
- The note’s octave and pitch.
- Features derived from the note’s pitch, for example, forward- and backward-looking [oscillators](https://en.wikipedia.org/wiki/Stochastic_oscillator) based on moving averages.
- Features derived from the logarithm of the time passed since a note was last pressed, for example, moving averages and oscillators based on those.

The value of some engineered features was obvious before even training the model. **Some of the features had correlations with the outcome (the actual velocity) of >0.25 or even >0.3**. Those correlations could be considered weak on their own, but when you have many, and partly uncorrelated, such features, and a model that can capture nonlinear relationships, they are a good sign and can get you a long way.

- derived from
	- Obtained or developed from a specific source; in data science, it refers to creating new information (features) by transforming raw data.
- duration
	- span, period, length, term, and time
- correlations with the outcome (the actual velocity) of >0.25 or even >0.3.
	- 通常、1から-1の間が強い相関関係を持つ（ばらつきがない）ということを意味する
	- この場合、弱い相関関係にある
	- でも、たくさんの関係の小さい特徴がたくさんあれば、そしてノンリニアな関係性を捉えるモデルがあるとするなら、これはサインとなるだろう

The midihum model was trained on performances from the International Piano-e-Competition for pianists aged 35 and under. midihum is dedicated to those talented young performers, and those who decided on and carried out the recording and publishing of those performances.

NB: midihum does not change the rhythmical timing of notes, nor does it take into account dynamics notated in sheet music. It is distributed with a GPLv3 license, which (quoting [TLDRLegal](https://www.tldrlegal.com/license/gnu-general-public-license-v3-gpl-3)) means you may “copy, distribute and modify the software as long as you track changes/dates in source files. Any modifications to or software including (via compiler) GPL-licensed code must also be made available under the GPL along with build & install instructions.” ==In addition, you may use the tool freely to make music, including music that you earn money from, without crediting me or this project==. I wish you the best of luck in doing so. You can find the full license, as well as the code and user instructions, in the [midihum GitHub repository](https://github.com/erwald/midihum).

- NB
	- An abbreviation for the Latin phrase _nota bene_, meaning "note well" or "take notice.
- sheet music
	- 楽譜
- take into account O
	- consider O
- dynamics notated
	- notate
		- mark / write expression mark in sheet music
	- 強弱法
- track
	- 追記する
	- you track changes/dates in source files.　ソースファイルに変更と日時を追記する限り
	- プログラミングやオープンソースの世界における「track changes/dates」には、具体的な「ルール」

