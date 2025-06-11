# 🎵 2000년대 및 2010년대 Spotify 음악 데이터 분석: 인기곡 예측 및 트렌드 분석

이 프로젝트는 Spotify의 2000년대와 2010년대의 방대한 음악 데이터를 심층 분석하여, 두 시대의 음악적 특성 변화를 탐색하고 시각화하는 프로젝트입니다. 이 분석은 각 시대의 음악 트렌드와 인기 요인을 정량적으로 파악하는 데 기여하며, 궁극적으로는 **대중적으로 인기 있는 음악이 가지는 공통적인 특성을 파악하고 앞으로 음악 시장에서 어떤 곡이 히트할지 예상하는 것을 목표**로 합니다.

## ✨ 프로젝트 개요

음악 산업은 시대에 따라 끊임없이 변화하며, 이는 음악의 장르, 스타일, 심지어 곡의 기술적 특성에서도 나타납니다. 본 프로젝트는 2000년대와 2010년대의 Spotify 데이터를 활용하여 이러한 변화를 정량적으로 분석하고, 다음 질문에 답하고자 합니다:
* 2000년대와 2010년대 Spotify 상위 곡들의 주요 음악적 특성(춤추기 가능성, 에너지, 음량, 어쿠스틱함 등)은 어떻게 다른가요?
* 두 시대에 걸쳐 음악 트렌드는 어떻게 변화했나요?
* 특정 음악적 특성이 시대별 인기와 어떤 관련이 있나요?
* **대중적으로 인기 있는 음악의 공통적인 특성은 무엇이며, 이를 통해 히트곡을 예측할 수 있는가요?** 

## 📊 데이터셋

본 프로젝트는 다음 Kaggle 링크에서 다운로드한 Spotify 음악 데이터를 사용합니다.
* **출처:** [Spotify Song Popularity & Genre Exploration on Kaggle](https://www.kaggle.com/code/akiboy96/spotify-song-popularity-genre-exploration/input?scriptVersionId=51654626)
* **포함된 정보:** 곡명, 아티스트, 앨범, 발매 연도, 그리고 Spotify가 제공하는 다양한 음악적 특성(예: `danceability`, `energy`, `loudness`, `acousticness`, `instrumentalness`, `liveness`, `valence`, `tempo` 등).
* **데이터 기간:** 2000년대 (2000-2009) 및 2010년대 (2010-2019)
* **인기도 정의:** 데이터의 주요 컬럼 중 하나인 `'Popularity'`는 해당 곡이 특정 10년 동안 빌보드 Hot-100 차트에 한 번이라도 진입한 경우 `'1'` (Hit), 그렇지 않은 경우 `'0'` (Flop)으로 정의하여 인기도를 나타냈습니다.
* **주요 컬럼 예시:** 트랙의 코러스 시작 시점(밀리초)을 나타내는 `'chorus_hit'` 과 트랙의 섹션 수를 나타내는 `'sections'`  등이 사용되었습니다.

## ⚙️ 데이터 전처리 과정

데이터 분석을 시작하기 전에 다음과 같은 전처리 과정이 수행되었습니다.
* **데이터 타입 및 결측값 확인**: 데이터의 구조와 누락된 값들을 파악했습니다.
* **Outlier 제거**: 분석의 정확성을 높이기 위해 이상치(outlier)를 처리했습니다.
* **데이터 정규화**: 변수들의 스케일을 맞추어 모델의 성능을 향상시켰습니다.
* **다중공선성 분석 및 처리**:
    * `'loudness'`와 `'energy'`는 VIF(분산 팽창 요인) 값이 1.663157로 10 미만이었습니다.
    * `'valence'`와 `'danceability'`는 VIF 값이 6.070815로 10 미만이었습니다. 이 두 쌍의 변수 모두 다중공선성 문제가 크지 않다고 판단되었습니다.
    * 하지만 `'duration_s'`와 `'sections'`는 VIF 값이 24.470168로 10을 초과하여 다중공선성 문제가 심각함을 확인했습니다. 이에 따라 `'sections'` 컬럼은 분석에서 제외되었습니다.
* **범주형 변수 전처리**: `key` 컬럼과 `genre` 컬럼 같은 범주형 변수들에 대해 적절한 전처리(예: One-Hot Encoding)가 진행되었습니다.

## 💡 분석 내용 및 결과

`00s_10s_spotify_music_data_analysis.ipynb` Jupyter Notebook 파일에는 다음 내용이 포함되어 있습니다:
* **데이터 로드 및 전처리:** Kaggle에서 다운로드한 데이터를 불러오고, 위에서 언급된 전처리 과정을 상세히 적용합니다.
* **탐색적 데이터 분석 (EDA):** 각 시대별 음악적 특성(예: `danceability`, `energy`, `valence` 등)의 분포와 변화 추이 시각화 (히스토그램, 박스 플롯, 라인 플롯 등).
* **시대별 트렌드 비교:** 2000년대와 2010년대의 주요 음악적 특성 평균값 비교 및 통계적 유의성 검정 (필요시).
* **인기 요인 분석:** 특정 음악적 특성이 시대별 Top 곡의 인기와 어떤 상관관계를 가지는지 분석.

### 적용 모델 및 결과 

인기 음악 예측을 위해 다음과 같은 세 가지 머신러닝 분류 모델이 적용되었습니다:
* **Logistic Regression** 
* **Decision Tree** 
* **Random Forest** 

적용된 세 가지 모델의 정확도를 비교한 결과는 다음과 같습니다:
* **Random Forest:** 83% 
* **Logistic Regression:** 78% 
* **Decision Tree:** 70% 

분석 결과, Random Forest 모델이 83%의 정확도로 가장 높은 예측 성능을 보였습니다.

### 히트곡 예측 주요 변수 

가장 높은 정확도를 보인 Random Forest 모델을 기반으로 히트곡 예측에 영향을 미치는 주요 변수들을 중요도 순으로 파악했습니다. 주요 변수는 다음과 같습니다:
* `instrumentalness` 
* `energy` 
* `acousticness` 
* `danceability` 
* `loudness` 
* `duration_s` 
* `valence` 
* `speechiness` 
* `tempo` 
* `chorus_hit` 
* `liveness` 

## 🚧 한계점

본 분석에는 다음과 같은 한계점들이 존재합니다:
* One-Hot Encoding을 통해 처리된 `key` 변수와 `genre` 변수의 특성이 분석 결과에 잘 반영되지 못한 측면이 있습니다. 이는 범주형 변수의 복잡한 특성을 단순화하는 과정에서 정보 손실이 발생했을 가능성을 시사합니다.
* 원본 데이터의 `genre` 컬럼 중 `'pop'` 변수에 다양한 하위 장르가 너무 많이 포함되어 있어, 장르 특성을 정확히 구분하고 분석하는 데 어려움이 있었습니다. 이는 장르 기반의 심층 분석에 제약을 주었습니다.
* Confusion matrix를 확인했을 때, 모든 모델에서 False Positive (실제로는 히트곡이 아닌데 히트곡으로 잘못 예측한 경우) 값이 높게 나타나는 경향을 보였습니다. 이는 모델이 히트곡이 아닌 곡을 히트곡으로 잘못 분류하는 오류가 상대적으로 높다는 의미로, 실제 서비스 적용 시 추가적인 보완이 필요할 수 있습니다.

## 🛠️ 기술 스택

* **언어:** Python
* **라이브러리:**
    * `pandas`: 데이터 처리 및 분석
    * `numpy`: 수치 계산
    * `matplotlib`, `seaborn`, `plotly`: 데이터 시각화
    * `scikit-learn`: 머신러닝 모델 구현 (Logistic Regression, Decision Tree, Random Forest 등)
* **개발 환경:** Jupyter Notebook

## 🚀 프로젝트 실행 방법

1.  **저장소 클론:**
    ```bash
    git clone [https://github.com/YourUsername/spotify-music-analysis.git](https://github.com/YourUsername/spotify-music-analysis.git)
    cd spotify-music-analysis
    ```
    (여기서 `YourUsername`은 본인의 GitHub 사용자 이름으로, `spotify-music-analysis`는 저장소 이름으로 대체하세요.)

2.  **데이터 다운로드:**
    * 본 프로젝트에서 사용하는 데이터는 다음 Kaggle 링크에서 다운로드할 수 있습니다:
        [https://www.kaggle.com/code/akiboy96/spotify-song-popularity-genre-exploration/input?scriptVersionId=51654626](https://www.kaggle.com/code/akiboy96/spotify-song-popularity-genre-exploration/input?scriptVersionId=51654626)
    * 다운로드 받은 데이터 파일(예: `songs_normalize.csv` 등)을 `data/raw/` 폴더 안에 위치시켜 주세요.

3.  **가상 환경 설정 및 라이브러리 설치:**
    ```bash
    python -m venv venv
    source venv/bin/activate  # Windows: .\venv\Scripts\activate
    pip install -r requirements.txt
    ```
    * `requirements.txt` 파일은 프로젝트 실행에 필요한 모든 Python 라이브러리를 포함해야 합니다. 이 파일이 없다면, `pip install pandas numpy matplotlib seaborn plotly scikit-learn` 등 필요한 라이브러리를 직접 설치하세요.

4.  **Jupyter Notebook 실행:**
    ```bash
    jupyter notebook notebooks/00s_10s_spotify_music_data_analysis.ipynb
    ```
    * 웹 브라우저에서 Jupyter Notebook이 열리면, 각 셀을 순서대로 실행하여 분석 과정을 따라갈 수 있습니다.

## 📚 참고 자료

* [프로젝트 발표 자료 (PDF)](./docs/spotify_data_analysis.pdf)
