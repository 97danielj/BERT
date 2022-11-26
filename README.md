[toc]

# BERT

BERT를 사용한 nlp 작업

**BERT 란?**

BERT(Bidirectional Encoder Representations from Transformers)는 구글이 공개한 사전 훈련된 모델이다.

![img](https://wikidocs.net/images/page/35594/%ED%8C%8C%EC%9D%B8%ED%8A%9C%EB%8B%9D.PNG)

레이블이 없는 방대한 데이터로 사전 훈련된 모델을 가지고, 레이블이 있는 다른 작업(Task)에서 추가 훈련과 함께 하이퍼파라미터를 재조정하여 이 모델을 사용할 수 있다.

## 사전훈련 방법

### 마스크드 언어 모델 (Masked Language Model, MLM)

BERT는 사전 훈련을 위해서 인공 신경망의 입력으로 들어가는 입력 텍스트의 15%의 단어를 랜덤으로 마스킹(Masking)합니다. 그리고 인공 신경망에게 이 가려진 단어들을(Masked words) 예측한다.

![img](https://wikidocs.net/images/page/115055/%EC%A0%84%EC%B2%B4%EB%8B%A8%EC%96%B4.PNG)

중간에 단어들에 구멍을 뚫어놓고, 구멍에 들어갈 단어들을 예측하게 하는 식이다. 전체 단어의 85%는 마스크드 언어 모델의 학습에 사용되지 않는다. 마스크드 언어 모델의 학습에 사용되는 단어는 전체 단어의 15%이다.

0. **BERT_subword_tokenizer**

   BERT의 워드피스 임베딩 벡터를 위한 서브 워드 토큰나이저를 알아본다.

1. **BERT_predict_token(Masked Language Model, MLM)**

   BERT의 사전 훈련 방식인 마스크드 언어 모델을 로드하여 [MASK]에 들어갈 단어를 확률로 알아본다.

2. **Korean BERT - MLM**

   Kobert는 사전훈련된 한글 BERT이다. Kobert의 MLM을 로드하여 [MASK]에 들어갈 단어를 확률로 알아본다.

### 다음 문장 예측(Next Sentence Prediction, NSP)

BERT는 두 개의 문장을 준 후에 이 문장이 이어지는 문장인지 아닌지를 맞추는 방식으로 훈련시킨다. 이를 위해서 50:50비율로 실제 이어지는 두 개의 문장과 랜덤으로 이어붙인 두 개의 문장을 주고 훈련시킨다.

![img](https://wikidocs.net/images/page/115055/%EA%B7%B8%EB%A6%BC10.PNG)

[SEP]라는 특별 토큰을 사용해서 문장을 구분한다. 그리고 이  두 문장이 실제 이어지는 문장인지 아닌지를 [CLS]  토큰의 위치의 출력층에서 이진 분류 문제를 푼다. 위의 그림과 같이 마스크드 언어 모델과 다음 문장 예측은 loss를 합하여 학습이 동시에 이루어진다.

3. **구글 BERT의 다음 문장 예측(Next Sentence Prediction)**

   문맥상 실제로 이어지는 두개의 문장을 입력으로 사용하여 분류 결과를 확인한다.

4. **한국어 BERT의 다음 문장 예측(Next Sentence Prediction**)

   문맥상 실제로 이어지는 두개의 문장(한국어)을 입력으로 사용하여 분류 결과를 확인한다.

## 파인 튜닝 방식

BERT를 사용하여 자연어 처리를 위한 추가 작업이 가능하다. 레이블이 있는 데이터를 태스크에 맞게 추가 학습(파인튜닝)  시킨다.

5. KoBERT를 이용한 네이버 영화 리뷰 분류하기

   영화 리뷰와 긍부정 레이블로 구성된 데이터를 BERT에 추가 학습시켜서 임의의 리뷰 데이터를 입력한 후 출력된 레이블을 확인한다. 영화 리뷰에 대한 감성분석이다.

6. kor_bert_kornli_model_from_trarnsformers(자연어추론)

   BERT의 파인 튜닝으로는 자연어 추론작업이 있다. 두 문장이 주어졌을 때, 하나의 문장이 다른 문장과 논리적으로 어떤 관계에 있는지를 분류하는 것이다. 유형으로는 모순 관계(contradiction), 함의 관계(entailment), 중립 관계(neutral)가 있습니다.

   다중 분류 모델이다.







