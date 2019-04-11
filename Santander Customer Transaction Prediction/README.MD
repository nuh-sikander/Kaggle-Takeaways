

# Solution Links

[2nd place solution](https://www.kaggle.com/c/santander-customer-transaction-prediction/discussion/88939) by [ONODERA](https://www.kaggle.com/onodera)
[3rd place solution](https://www.kaggle.com/c/santander-customer-transaction-prediction/discussion/88902) by [Chua Cheng Hong](https://www.kaggle.com/burn874)
[4th place solution](https://www.kaggle.com/c/santander-customer-transaction-prediction/discussion/88891) by [ZFTurbo](https://www.kaggle.com/zfturbo) ([Kernel](https://www.kaggle.com/zfturbo/magic-feature-generator))
[5th place solution 1](https://www.kaggle.com/c/santander-customer-transaction-prediction/discussion/88897) by [Μαριος Μιχαηλιδης KazAnova](https://www.kaggle.com/kazanova)
[5th place solution 2](https://www.kaggle.com/c/santander-customer-transaction-prediction/discussion/88929) by [Kun Hao Yeh](https://www.kaggle.com/khyeh0719)
[8th place solution](https://www.kaggle.com/c/santander-customer-transaction-prediction/discussion/88886) by [Michael Jahrer](https://www.kaggle.com/mjahrer)
[9th place solution](https://www.kaggle.com/c/santander-customer-transaction-prediction/discussion/88913) by [gucio3](https://www.kaggle.com/guchio3) ([Github](https://github.com/guchio3/kaggle-santander-2019))
[12th place solution](https://www.kaggle.com/c/santander-customer-transaction-prediction/discussion/88906) by [spongebob](https://www.kaggle.com/baomengjiao)
[14th place solution](https://www.kaggle.com/c/santander-customer-transaction-prediction/discussion/88927) by [qrfaction](https://www.kaggle.com/action) ([Github](https://github.com/qrfaction/Kaggle_SCTP_gold_14th_solution))
[15th place solution](https://www.kaggle.com/c/santander-customer-transaction-prediction/discussion/88888) by [CPMP](https://www.kaggle.com/cpmpml) ([Github](https://github.com/jfpuget/Kaggle_Santander_2019))
[16th place solution](https://www.kaggle.com/c/santander-customer-transaction-prediction/discussion/88926#513154) by [Shize Su](https://www.kaggle.com/sushize) ([Kernel](https://www.kaggle.com/joaopmpeinado/let-s-show-some-magic-lb-0-922?scriptVersionId=12758872))
[17th place solution](https://www.kaggle.com/c/santander-customer-transaction-prediction/discussion/88936) by [Jiwei Liu](https://www.kaggle.com/jiweiliu) ([Kernel](https://www.kaggle.com/jiweiliu/lb-0-9228-nn-weight-sharing-of-var-group), [Github](https://github.com/daxiongshu/santander))
[21st place solution](https://www.kaggle.com/c/santander-customer-transaction-prediction/discussion/88901) by [Vasily Ryazanov](https://www.kaggle.com/ryazanoff)
[24th place solution](https://www.kaggle.com/c/santander-customer-transaction-prediction/discussion/88943) by [Tomoyo](https://www.kaggle.com/guziye)
[26th place solution](https://www.kaggle.com/c/santander-customer-transaction-prediction/discussion/88915) by [whitebird](https://www.kaggle.com/whitebird) ([Kernel](https://www.kaggle.com/whitebird/0-923-in-n-5-aug))

# TLDR;

- The magic feature is per column count of each independent var\_N value on merged table: train + test (with cleaned fakes).
- Adding variables like var_N \* count_N and var_N / count_ Probably original features were divided on counts. GBMs aren&#39;t so good about finding multiplication or division dependencies.
- Randomly shuffling columns during training. It&#39;s easier on neural nets, but can be used on GBM with expanding matrix multiple times with randomly shuffled columns. I mostly use x20 times for training.
- More folds usually gives better result. Like 10 better than 5.
- replace count == 1 features to NaN -\&gt; LB 0.917 ([https://github.com/guchio3/kaggle-santander-2019/blob/master/tools/features/f014\_non\_uniq\_real\_features.py](https://github.com/guchio3/kaggle-santander-2019/blob/master/tools/features/f014_non_uniq_real_features.py))
- replace count greater than 1 features to NaN -\&gt; LB 0.922 ([https://github.com/guchio3/kaggle-santander-2019/blob/master/tools/features/f021\_uniq\_real\_features.py](https://github.com/guchio3/kaggle-santander-2019/blob/master/tools/features/f021_uniq_real_features.py))
- Compute frequency of values using all data. This moved me to 0.901 public LB.
- Remove the fake test rows when computing frequency. This moved me to 0.913 public LB.
- Use Naive Bayes with 200 models. Each model is lgb trained on one of the original features plus the associated frequency feature. This moved me to 0.922 public LB. [https://www.kaggle.com/b5strbal/lightgbm-naive-bayes-santander-0-900](https://www.kaggle.com/b5strbal/lightgbm-naive-bayes-santander-0-900)

