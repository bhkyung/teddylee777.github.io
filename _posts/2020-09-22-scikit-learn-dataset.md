---
layout: page
title: "scikit-learn 데이터셋(dataset) 다루기"
description: "scikit-learn 데이터셋(dataset) 다루는 방법에 대해 알아보겠습니다."
headline: "scikit-learn 데이터셋(dataset) 다루는 방법에 대해 알아보겠습니다."
categories: scikit-learn
tags: [python, tensorflow, scikit-learn, datasets, iris, load_iris, 텐서플로우, data science, 데이터 분석, 딥러닝, 딥러닝 자격증, 머신러닝, 빅데이터, 테디노트]
comments: true
published: true
typora-copy-images-to: ../images/2020-09-22
---



scikit-learn의 패키지에 포함된 dataset 패키지에서 Toy Dataset을 로딩하여 학습해 보는 튜토리얼입니다.  



## 코드

![Colab으로 열기](../images/2020-09-22/colab_logo_32px.png) [Colab으로 열기](https://colab.research.google.com/github/teddylee777/machine-learning/blob/master/10-scikit-learn/03-%EB%8D%B0%EC%9D%B4%ED%84%B0%EC%85%8B%20(Dataset)%20%EB%8B%A4%EB%A3%A8%EA%B8%B0.ipynb)

![GitHub](../images/2020-09-22/GitHub-Mark-32px.png) [GitHub에서 소스보기](https://github.com/teddylee777/machine-learning/blob/master/10-scikit-learn/03-%EB%8D%B0%EC%9D%B4%ED%84%B0%EC%85%8B%20(Dataset)%20%EB%8B%A4%EB%A3%A8%EA%B8%B0.ipynb)

<br/>

<body>

<div class="border-box-sizing" id="notebook" >
<div class="container" id="notebook-container">
<div class="cell border-box-sizing text_cell rendered"><div class="inner_cell">
<div class="text_cell_render border-box-sizing rendered_html">
<h1 id="데이터-셋-(Dataset)-다루기">데이터 셋 (Dataset) 다루기</h1>
</div>
</div>
</div>
<div class="cell border-box-sizing text_cell rendered"><div class="inner_cell">
<div class="text_cell_render border-box-sizing rendered_html">
<p><code>sklearn.dataset</code> 안에는 빌트인 (built-in) 데이터 셋들이 존재합니다. 물론 튜토리얼 진행을 위한 수준이므로, 규모가 크지는 않습니다 (Toy Dataset 이라고도 불리웁니다.)</p>
<p>그렇지만, mldata.org 데이터 셋은 조금 더 규모가 큰 데이터 셋을 제공하며, 온라인에서 동적으로 다운로드를 받을 수 있습니다.</p>
<p>이번 튜토리얼에서는 Built-in 데이터 셋을 활용하는 방법에 대해서 알아보도록 하겠습니다.</p>
</div>
</div>
</div>
<div class="cell border-box-sizing text_cell rendered"><div class="inner_cell">
<div class="text_cell_render border-box-sizing rendered_html">
<h2 id="빌트인-(Built-in)-데이터셋-활용">빌트인 (Built-in) 데이터셋 활용</h2>
</div>
</div>
</div>
<div class="cell border-box-sizing text_cell rendered"><div class="inner_cell">
<div class="text_cell_render border-box-sizing rendered_html">
<h3 id="데이터-셋의-종류">데이터 셋의 종류</h3>
</div>
</div>
</div>
<div class="cell border-box-sizing text_cell rendered"><div class="inner_cell">
<div class="text_cell_render border-box-sizing rendered_html">
<ul>
<li><code>load_boston</code>: 보스톤 집값 데이터</li>
<li><code>load_iris</code>: 아이리스 붓꽃 데이터</li>
<li><code>load_diabetes</code>: 당뇨병 환자 데이터</li>
<li><code>load_digits</code>: 손글씨 데이터</li>
<li><code>load_linnerud</code>: multi-output regression 용 데이터</li>
<li><code>load_wine</code>: 와인 데이터</li>
<li><code>load_breast_cancer</code>: 위스콘신 유방암 환자 데이터</li>
</ul>
</div>
</div>
</div>
<div class="cell border-box-sizing text_cell rendered"><div class="inner_cell">
<div class="text_cell_render border-box-sizing rendered_html">
<h3 id="데이터-셋-조회">데이터 셋 조회</h3>
</div>
</div>
</div>
<div class="cell border-box-sizing text_cell rendered"><div class="inner_cell">
<div class="text_cell_render border-box-sizing rendered_html">
<p>빌트인 데이터셋은 <code>sklearn.utils.Bunch</code> 라는 자료구조를 활용합니다.</p>
<p><strong>key-value</strong> 형식으로 구성되어 있으며, 사전(dict)형 타입과 유사한 구조를 가지고 있습니다.</p>
<p>공통 <strong>key</strong>는 다음과 같습니다.</p>
<ul>
<li><code>data</code>: 샘플 데이터, Numpy 배열로 이루어져 있습니다.</li>
<li><code>target</code>: Label 데이터, Numpy 배열로 이루어져 있습니다.</li>
<li><code>feature_names</code>: Feature 데이터의 이름</li>
<li><code>target_names</code>: Label 데이터의 이름</li>
<li><code>DESCR</code>: 데이터 셋의 설명</li>
<li><code>filename</code>: 데이터 셋의 파일 저장 위치 (csv)</li>
</ul>
</div>
</div>
</div>
<div class="cell border-box-sizing text_cell rendered"><div class="inner_cell">
<div class="text_cell_render border-box-sizing rendered_html">
<p>간단한 실습으로 빌트인 데이터셋의 활용법에 대하여 알아보겠습니다.</p>
</div>
</div>
</div>
<div class="cell border-box-sizing text_cell rendered"><div class="inner_cell">
<div class="text_cell_render border-box-sizing rendered_html">
<h3 id="iris-붓꽃-데이터-로드하기">iris 붓꽃 데이터 로드하기</h3>
</div>
</div>
</div>
<div class="cell border-box-sizing code_cell rendered">
<div class="input">

<div class="inner_cell">
<div class="input_area">
<div class="highlight hl-ipython3"><pre><span></span><span class="kn">from</span> <span class="nn">IPython.display</span> <span class="k">import</span> <span class="n">Image</span>
</pre></div>
</div>
</div>
</div>
</div>
<div class="cell border-box-sizing code_cell rendered">
<div class="input">

<div class="inner_cell">
<div class="input_area">
<div class="highlight hl-ipython3"><pre><span></span><span class="n">Image</span><span class="p">(</span><span class="n">url</span><span class="o">=</span><span class="s1">'https://user-images.githubusercontent.com/15958325/56006707-f69f3680-5d10-11e9-8609-25ba5034607e.png'</span><span class="p">)</span>
</pre></div>
</div>
</div>
</div>
<div class="output_wrapper">
<div class="output">
<div class="output_area">

<div class="output_html rendered_html output_subarea output_execute_result">
<img src="https://user-images.githubusercontent.com/15958325/56006707-f69f3680-5d10-11e9-8609-25ba5034607e.png"/>
</div>
</div>
</div>
</div>
</div>
<div class="cell border-box-sizing code_cell rendered">
<div class="input">

<div class="inner_cell">
<div class="input_area">
<div class="highlight hl-ipython3"><pre><span></span><span class="c1"># iris 붓꽃 데이터 로드</span>
<span class="kn">from</span> <span class="nn">sklearn.datasets</span> <span class="k">import</span> <span class="n">load_iris</span>
</pre></div>
</div>
</div>
</div>
</div>
<div class="cell border-box-sizing text_cell rendered"><div class="inner_cell">
<div class="text_cell_render border-box-sizing rendered_html">
<p><code>load_iris</code>로 데이터 셋을 불러와서 임시 변수에 저장합니다.</p>
</div>
</div>
</div>
<div class="cell border-box-sizing code_cell rendered">
<div class="input">

<div class="inner_cell">
<div class="input_area">
<div class="highlight hl-ipython3"><pre><span></span><span class="n">iris</span> <span class="o">=</span> <span class="n">load_iris</span><span class="p">()</span>
</pre></div>
</div>
</div>
</div>
</div>
<div class="cell border-box-sizing text_cell rendered"><div class="inner_cell">
<div class="text_cell_render border-box-sizing rendered_html">
<p>변수를 출력해 보면 다음과 같이 key-value 로 이루어진 데이터셋이 로드됩니다.</p>
</div>
</div>
</div>
<div class="cell border-box-sizing code_cell rendered">
<div class="input">

<div class="inner_cell">
<div class="input_area">
<div class="highlight hl-ipython3"><pre><span></span><span class="n">iris</span>
</pre></div>
</div>
</div>
</div>
</div>
<div class="cell border-box-sizing text_cell rendered"><div class="inner_cell">
<div class="text_cell_render border-box-sizing rendered_html">
<h2 id="Feature-데이터-(X)">Feature 데이터 (X)</h2>
</div>
</div>
</div>
<div class="cell border-box-sizing text_cell rendered"><div class="inner_cell">
<div class="text_cell_render border-box-sizing rendered_html">
<h3 id="feature-데이터-값-조회하기">feature 데이터 값 조회하기</h3>
</div>
</div>
</div>
<div class="cell border-box-sizing text_cell rendered"><div class="inner_cell">
<div class="text_cell_render border-box-sizing rendered_html">
<p>feature data는 <code>data</code> 키로 접근하여 가져올 수 있습니다.</p>
</div>
</div>
</div>
<div class="cell border-box-sizing code_cell rendered">
<div class="input">

<div class="inner_cell">
<div class="input_area">
<div class="highlight hl-ipython3"><pre><span></span><span class="n">features</span> <span class="o">=</span> <span class="n">iris</span><span class="p">[</span><span class="s1">'data'</span><span class="p">]</span>
</pre></div>
</div>
</div>
</div>
</div>
<div class="cell border-box-sizing text_cell rendered"><div class="inner_cell">
<div class="text_cell_render border-box-sizing rendered_html">
<p>5개만 출력해 본다면 다음과 같은 모양새를 띄고 있습니다.</p>
</div>
</div>
</div>
<div class="cell border-box-sizing code_cell rendered">
<div class="input">

<div class="inner_cell">
<div class="input_area">
<div class="highlight hl-ipython3"><pre><span></span><span class="n">features</span><span class="p">[:</span><span class="mi">5</span><span class="p">]</span>
</pre></div>
</div>
</div>
</div>
<div class="output_wrapper">
<div class="output">
<div class="output_area">

<div class="output_text output_subarea output_execute_result">
<pre>array([[5.1, 3.5, 1.4, 0.2],
       [4.9, 3. , 1.4, 0.2],
       [4.7, 3.2, 1.3, 0.2],
       [4.6, 3.1, 1.5, 0.2],
       [5. , 3.6, 1.4, 0.2]])</pre>
</div>
</div>
</div>
</div>
</div>
<div class="cell border-box-sizing text_cell rendered"><div class="inner_cell">
<div class="text_cell_render border-box-sizing rendered_html">
<p>feature data 에 대한 이름은 <code>feature_names</code> 로 가져올 수 있습니다.</p>
<p>iris 데이터의 경우 총 <strong>4개의 feature</strong>를 가지고 있음을 확인할 수 있습니다.</p>
<p>[참고]</p>
<ul>
<li>sepal: 꽃받침</li>
<li>petal: 꽃잎</li>
</ul>
</div>
</div>
</div>
<div class="cell border-box-sizing code_cell rendered">
<div class="input">

<div class="inner_cell">
<div class="input_area">
<div class="highlight hl-ipython3"><pre><span></span><span class="n">feature_names</span> <span class="o">=</span> <span class="n">iris</span><span class="p">[</span><span class="s1">'feature_names'</span><span class="p">]</span>
<span class="n">feature_names</span>
</pre></div>
</div>
</div>
</div>
<div class="output_wrapper">
<div class="output">
<div class="output_area">

<div class="output_text output_subarea output_execute_result">
<pre>['sepal length (cm)',
 'sepal width (cm)',
 'petal length (cm)',
 'petal width (cm)']</pre>
</div>
</div>
</div>
</div>
</div>
<div class="cell border-box-sizing text_cell rendered"><div class="inner_cell">
<div class="text_cell_render border-box-sizing rendered_html">
<h2 id="Label-데이터-(Y)">Label 데이터 (Y)</h2>
</div>
</div>
</div>
<div class="cell border-box-sizing text_cell rendered"><div class="inner_cell">
<div class="text_cell_render border-box-sizing rendered_html">
<p>label data는 <code>target</code> 키로 접근하여 가져올 수 있습니다.</p>
</div>
</div>
</div>
<div class="cell border-box-sizing code_cell rendered">
<div class="input">

<div class="inner_cell">
<div class="input_area">
<div class="highlight hl-ipython3"><pre><span></span><span class="n">labels</span> <span class="o">=</span> <span class="n">iris</span><span class="p">[</span><span class="s1">'target'</span><span class="p">]</span>
<span class="n">labels</span>
</pre></div>
</div>
</div>
</div>
<div class="output_wrapper">
<div class="output">
<div class="output_area">

<div class="output_text output_subarea output_execute_result">
<pre>array([0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0,
       0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0,
       0, 0, 0, 0, 0, 0, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1,
       1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1,
       1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 2, 2, 2, 2, 2, 2, 2, 2, 2, 2,
       2, 2, 2, 2, 2, 2, 2, 2, 2, 2, 2, 2, 2, 2, 2, 2, 2, 2, 2, 2, 2, 2,
       2, 2, 2, 2, 2, 2, 2, 2, 2, 2, 2, 2, 2, 2, 2, 2, 2, 2])</pre>
</div>
</div>
</div>
</div>
</div>
<div class="cell border-box-sizing text_cell rendered"><div class="inner_cell">
<div class="text_cell_render border-box-sizing rendered_html">
<p>feature data와 마찬가지로, label 데이터도 <code>target_names</code>라는 키로 target에 대한 클래쓰 이름을 확인해 볼 수 있습니다.</p>
</div>
</div>
</div>
<div class="cell border-box-sizing text_cell rendered"><div class="inner_cell">
<div class="text_cell_render border-box-sizing rendered_html">
<h2 id="데이터-셋을-DataFrame으로-변환">데이터 셋을 DataFrame으로 변환</h2>
</div>
</div>
</div>
<div class="cell border-box-sizing code_cell rendered">
<div class="input">

<div class="inner_cell">
<div class="input_area">
<div class="highlight hl-ipython3"><pre><span></span><span class="kn">import</span> <span class="nn">pandas</span> <span class="k">as</span> <span class="nn">pd</span>
</pre></div>
</div>
</div>
</div>
</div>
<div class="cell border-box-sizing text_cell rendered"><div class="inner_cell">
<div class="text_cell_render border-box-sizing rendered_html">
<p>첫번째로 <code>data</code>와 <code>feature_names</code> 키로 가져온 데이터를 활용하여 데이터 프레임을 만들어 줍니다.</p>
</div>
</div>
</div>
<div class="cell border-box-sizing code_cell rendered">
<div class="input">

<div class="inner_cell">
<div class="input_area">
<div class="highlight hl-ipython3"><pre><span></span><span class="n">df</span> <span class="o">=</span> <span class="n">pd</span><span class="o">.</span><span class="n">DataFrame</span><span class="p">(</span><span class="n">features</span><span class="p">,</span> <span class="n">columns</span><span class="o">=</span><span class="n">feature_names</span><span class="p">)</span>
<span class="n">df</span><span class="o">.</span><span class="n">head</span><span class="p">()</span>
</pre></div>
</div>
</div>
</div>
<div class="output_wrapper">
<div class="output">
<div class="output_area">

<div class="output_html rendered_html output_subarea output_execute_result">
<div>
<style scoped="">
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }
    
    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
<thead>
<tr style="text-align: right;">
<th></th>
<th>sepal length (cm)</th>
<th>sepal width (cm)</th>
<th>petal length (cm)</th>
<th>petal width (cm)</th>
</tr>
</thead>
<tbody>
<tr>
<th>0</th>
<td>5.1</td>
<td>3.5</td>
<td>1.4</td>
<td>0.2</td>
</tr>
<tr>
<th>1</th>
<td>4.9</td>
<td>3.0</td>
<td>1.4</td>
<td>0.2</td>
</tr>
<tr>
<th>2</th>
<td>4.7</td>
<td>3.2</td>
<td>1.3</td>
<td>0.2</td>
</tr>
<tr>
<th>3</th>
<td>4.6</td>
<td>3.1</td>
<td>1.5</td>
<td>0.2</td>
</tr>
<tr>
<th>4</th>
<td>5.0</td>
<td>3.6</td>
<td>1.4</td>
<td>0.2</td>
</tr>
</tbody>
</table>
</div>
</div>
</div>
</div>
</div>
</div>
<div class="cell border-box-sizing text_cell rendered"><div class="inner_cell">
<div class="text_cell_render border-box-sizing rendered_html">
<p>혹은 다음과 같이 가져와도 동일하겠죠?</p>
</div>
</div>
</div>
<div class="cell border-box-sizing code_cell rendered">
<div class="input">

<div class="inner_cell">
<div class="input_area">
<div class="highlight hl-ipython3"><pre><span></span><span class="n">df</span> <span class="o">=</span> <span class="n">pd</span><span class="o">.</span><span class="n">DataFrame</span><span class="p">(</span><span class="n">iris</span><span class="p">[</span><span class="s1">'data'</span><span class="p">],</span> <span class="n">columns</span><span class="o">=</span><span class="n">iris</span><span class="p">[</span><span class="s1">'feature_names'</span><span class="p">])</span>
<span class="n">df</span><span class="o">.</span><span class="n">head</span><span class="p">()</span>
</pre></div>
</div>
</div>
</div>
<div class="output_wrapper">
<div class="output">
<div class="output_area">

<div class="output_html rendered_html output_subarea output_execute_result">
<div>
<style scoped="">
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }
    
    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
<thead>
<tr style="text-align: right;">
<th></th>
<th>sepal length (cm)</th>
<th>sepal width (cm)</th>
<th>petal length (cm)</th>
<th>petal width (cm)</th>
</tr>
</thead>
<tbody>
<tr>
<th>0</th>
<td>5.1</td>
<td>3.5</td>
<td>1.4</td>
<td>0.2</td>
</tr>
<tr>
<th>1</th>
<td>4.9</td>
<td>3.0</td>
<td>1.4</td>
<td>0.2</td>
</tr>
<tr>
<th>2</th>
<td>4.7</td>
<td>3.2</td>
<td>1.3</td>
<td>0.2</td>
</tr>
<tr>
<th>3</th>
<td>4.6</td>
<td>3.1</td>
<td>1.5</td>
<td>0.2</td>
</tr>
<tr>
<th>4</th>
<td>5.0</td>
<td>3.6</td>
<td>1.4</td>
<td>0.2</td>
</tr>
</tbody>
</table>
</div>
</div>
</div>
</div>
</div>
</div>
<div class="cell border-box-sizing text_cell rendered"><div class="inner_cell">
<div class="text_cell_render border-box-sizing rendered_html">
<p>그런 다음 <code>target</code> 데이터를 새로운 컬럼을 만들어 추가해 줍니다. 여기서 target 데이터의 column 명 임의로 지정해 주면 됩니다.</p>
</div>
</div>
</div>
<div class="cell border-box-sizing code_cell rendered">
<div class="input">

<div class="inner_cell">
<div class="input_area">
<div class="highlight hl-ipython3"><pre><span></span><span class="n">df</span><span class="p">[</span><span class="s1">'target'</span><span class="p">]</span> <span class="o">=</span> <span class="n">iris</span><span class="p">[</span><span class="s1">'target'</span><span class="p">]</span>
</pre></div>
</div>
</div>
</div>
</div>
<div class="cell border-box-sizing code_cell rendered">
<div class="input">

<div class="inner_cell">
<div class="input_area">
<div class="highlight hl-ipython3"><pre><span></span><span class="n">df</span><span class="o">.</span><span class="n">head</span><span class="p">()</span>
</pre></div>
</div>
</div>
</div>
<div class="output_wrapper">
<div class="output">
<div class="output_area">

<div class="output_html rendered_html output_subarea output_execute_result">
<div>
<style scoped="">
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }
    
    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
<thead>
<tr style="text-align: right;">
<th></th>
<th>sepal length (cm)</th>
<th>sepal width (cm)</th>
<th>petal length (cm)</th>
<th>petal width (cm)</th>
<th>target</th>
</tr>
</thead>
<tbody>
<tr>
<th>0</th>
<td>5.1</td>
<td>3.5</td>
<td>1.4</td>
<td>0.2</td>
<td>0</td>
</tr>
<tr>
<th>1</th>
<td>4.9</td>
<td>3.0</td>
<td>1.4</td>
<td>0.2</td>
<td>0</td>
</tr>
<tr>
<th>2</th>
<td>4.7</td>
<td>3.2</td>
<td>1.3</td>
<td>0.2</td>
<td>0</td>
</tr>
<tr>
<th>3</th>
<td>4.6</td>
<td>3.1</td>
<td>1.5</td>
<td>0.2</td>
<td>0</td>
</tr>
<tr>
<th>4</th>
<td>5.0</td>
<td>3.6</td>
<td>1.4</td>
<td>0.2</td>
<td>0</td>
</tr>
</tbody>
</table>
</div>
</div>
</div>
</div>
</div>
</div>
<div class="cell border-box-sizing text_cell rendered"><div class="inner_cell">
<div class="text_cell_render border-box-sizing rendered_html">
<h2 id="로드한-DataFrame-시각화">로드한 DataFrame 시각화</h2>
</div>
</div>
</div>
<div class="cell border-box-sizing code_cell rendered">
<div class="input">

<div class="inner_cell">
<div class="input_area">
<div class="highlight hl-ipython3"><pre><span></span><span class="kn">import</span> <span class="nn">matplotlib.pyplot</span> <span class="k">as</span> <span class="nn">plt</span>
<span class="kn">import</span> <span class="nn">seaborn</span> <span class="k">as</span> <span class="nn">sns</span>
</pre></div>
</div>
</div>
</div>
</div>
<div class="cell border-box-sizing text_cell rendered"><div class="inner_cell">
<div class="text_cell_render border-box-sizing rendered_html">
<p>Sepal (꽃받침)의 길이 넓이에 따른 꽃의 종류가 어떻게 다르게 나오는지 살펴보겠습니다.</p>
</div>
</div>
</div>
<div class="cell border-box-sizing code_cell rendered">
<div class="input">

<div class="inner_cell">
<div class="input_area">
<div class="highlight hl-ipython3"><pre><span></span><span class="n">plt</span><span class="o">.</span><span class="n">figure</span><span class="p">(</span><span class="n">figsize</span><span class="o">=</span><span class="p">(</span><span class="mi">10</span><span class="p">,</span> <span class="mi">7</span><span class="p">))</span>
<span class="n">sns</span><span class="o">.</span><span class="n">scatterplot</span><span class="p">(</span><span class="n">df</span><span class="o">.</span><span class="n">iloc</span><span class="p">[:,</span> <span class="mi">0</span><span class="p">],</span> <span class="n">df</span><span class="o">.</span><span class="n">iloc</span><span class="p">[:,</span> <span class="mi">1</span><span class="p">],</span> <span class="n">hue</span><span class="o">=</span><span class="n">df</span><span class="p">[</span><span class="s1">'target'</span><span class="p">],</span> <span class="n">palette</span><span class="o">=</span><span class="s1">'muted'</span><span class="p">)</span>
<span class="n">plt</span><span class="o">.</span><span class="n">title</span><span class="p">(</span><span class="s1">'Sepal'</span><span class="p">,</span> <span class="n">fontsize</span><span class="o">=</span><span class="mi">17</span><span class="p">)</span>
<span class="n">plt</span><span class="o">.</span><span class="n">show</span><span class="p">()</span>
</pre></div>
</div>
</div>
</div>
<div class="output_wrapper">
<div class="output">
<div class="output_area">
<div class="prompt"></div>
<div class="output_png output_subarea">
<img src="data:image/png;base64,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XHTRRRx77LEce+yxPPbYY6xfv56bbrqJ//mf/2HZsmU88sgjB1z3hNvAW0RERGR31157LS+99BLPP/88juOQSCSor6+nq6uL448/nvPPPx+A1157jR/96EfccMMNbN26la997Ws8++yz1NXVccYZZ3D00UcDcPXVV/PpT3+ak046iY0bN3LOOeewcuVKPvrRjxKJRPjsZz87KnUrhImIiMikYa3lC1/4Ag8//DAej4ctW7awY8cOABYsWMDxxx8PwNNPP82pp55KU1MTAO9973t5/fXXAbj//vt55ZVXhu4zGo0yMDAw6rUqhIlISfFUDmshUuOtdikiIkX97Gc/o7OzkxUrVuD3+2lraxtav6u2tnbouGKL1buuyxNPPEFNTU1Fa9WcMBHZq2Q6x6sb43z95+v5vz9bz0vrYiRSuWqXJSJSoK6ubuhKVX9/P62trfj9fv7617+yYcOGEfu8+c1v5qGHHqK3txfHcfj1r3899LWzzz6b66+/fuj2888/P+w8o0EhTET2qqs/yz/ftJpnV8V4fk2Mz928hh29mWqXJSJSoLm5mRNPPJElS5bw/PPP09HRQXt7Oz/72c84/PDDR+wzZ84cvvCFL3Dcccdx1llnccQRR9DQkN858brrrqOjo4OlS5dyxBFHcNNNNwHwzne+kzvvvHPUJuZXbO/IStHekSJj53/v3crtD3UWtJ17XBOfuGDulF8dW0TesHLlShYvXlztMvZZLBYjEongOA4XXnghV1xxBRdeeOF+399I34eq7B0pIhNfS0NgWFtrY0ABTEQmha985SssW7aMJUuWsHDhQt71rneN6fk1MV9E9urEJQ385pFOtg8OQU5v8HPW8qYqVyUiMjq++c1vVvX8CmEisldNdX6+9Y+HsH5HCte1HDSrhml1/mqXJSIyKSiEiUhR0+r8Cl4iIhWgOWEiIiIiVaAQJiIiIlIFCmEiIiIy4d17770cdthhHHLIIVx77bXVLqcsCmEiIiIyoeVyOT7+8Y/zxz/+kVdeeYVf/OIXBXs/jleamC8iIiJj6oHnerjlvu109mVpafRz2dkzOeNN+7/8zdNPP80hhxzCQQcdBMDFF1/MXXfdxRFHHDFaJVeEroSJiIjImHnguR6uu3MzO/uyWGBnX5br7tzMA8/17Pd9btmyhXnz5g3dnjt3Llu2bBmFaitLIUxERETGzC33bSedLdwyMZ213HLf9v2+z5G2YJwIO3sohImIiMiY6ezL7lN7OebOncumTZuGbm/evJnZs2fv9/2NFYUwERERGTMtjSMv/ry39nIce+yxrFq1inXr1pHJZPjlL3/J+eefv9/3N1YUwkRERGTMXHb2TIL+wqHCoN9w2dkz9/s+fT4f119/Peeccw6LFy/mfe97H0ceeeSBllpxenekiIiIjJld74IczXdHApx77rmce+65o1HimFEIExERkTF1xpuaDjh0TQYajhQRERGpAoUwERERkSpQCBMRERGpAoUwERERkSpQCBMRERGpAoUwERERmfCuuOIKWltbWbJkSbVLKZtCmIiIiEx4H/rQh7j33nurXcY+0TphIiIiMqbSL/2V1IO34Ea78NRPJ3TaZQSXnH5A93nKKaewfv360SlwjCiEiYiIyJhJv/RXEn/4f+CkAXCjnfnbcMBBbKLRcKTIBBONO+zsy9DVnyGWzFW7HBGRfZJ68JahADbESefbpxhdCROZQPpiDt+6YyPPvDaAx8A5xzZz2dkzaajVr7KITAxutGuf2iczXQkTmSCstTzytz6eeW0AANfCH5/uZv32ZJUrExEpn6d++j61T2YKYSITRDZneWFNbFj7yxsSVahGRGT/hE67DHzBwkZfMN9+AC655BJOOOEEXnvtNebOncsPf/jDA7q/saAxDJEJIuDzcOKRDTz2cn9B+zGH1lWpIhGRfbdr8v1ovzvyF7/4xWiUN6YUwkQmkOWL6rjgLdP5w1Pd+H2GvztzBrOaA9UuS0RknwSXnD7l3gk5EoUwkQmkodbHZefM5H2ntgIQqfES8GtWgYjIRKQQJjLB1AS81AS81S5DREQOkP6EFhEREakChTARERGRKlAIExEREakChTARERGZ0DZt2sTpp5/O4sWLOfLII/nOd75T7ZLKoon5IiIiMqH5fD7++7//m+XLlzMwMMAxxxzDW9/6Vo444ohql1aUQpiIiIiMqae7n+TurXfSm+lhWqCJ82dfyJubj9/v+5s1axazZs0CoK6ujsWLF7NlyxaFMJGJIpezRBMOPq+hLqxfDRGRSni6+0l+vuFWsjYDQG+mh59vuBXggILYLuvXr+e5557juOOOO+D7qjS90ogA0bjD/c/1cO/TPUyr8/EP581hXksQv0/TJkVERtPdW+8cCmC7ZG2Gu7fe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
"/>
</div>
</div>
</div>
</div>
</div>
<div class="cell border-box-sizing text_cell rendered"><div class="inner_cell">
<div class="text_cell_render border-box-sizing rendered_html">
<p>이번에는, Petal (꽃잎)의 길이 넓이에 따른 꽃의 종류가 어떻게 다르게 나오는지 살펴보겠습니다.</p>
</div>
</div>
</div>
<div class="cell border-box-sizing code_cell rendered">
<div class="input">

<div class="inner_cell">
<div class="input_area">
<div class="highlight hl-ipython3"><pre><span></span><span class="n">plt</span><span class="o">.</span><span class="n">figure</span><span class="p">(</span><span class="n">figsize</span><span class="o">=</span><span class="p">(</span><span class="mi">10</span><span class="p">,</span> <span class="mi">7</span><span class="p">))</span>
<span class="n">sns</span><span class="o">.</span><span class="n">scatterplot</span><span class="p">(</span><span class="n">df</span><span class="o">.</span><span class="n">iloc</span><span class="p">[:,</span> <span class="mi">2</span><span class="p">],</span> <span class="n">df</span><span class="o">.</span><span class="n">iloc</span><span class="p">[:,</span> <span class="mi">3</span><span class="p">],</span> <span class="n">hue</span><span class="o">=</span><span class="n">df</span><span class="p">[</span><span class="s1">'target'</span><span class="p">],</span> <span class="n">palette</span><span class="o">=</span><span class="s1">'muted'</span><span class="p">)</span>
<span class="n">plt</span><span class="o">.</span><span class="n">title</span><span class="p">(</span><span class="s1">'Petal'</span><span class="p">,</span> <span class="n">fontsize</span><span class="o">=</span><span class="mi">17</span><span class="p">)</span>
<span class="n">plt</span><span class="o">.</span><span class="n">show</span><span class="p">()</span>
</pre></div>
</div>
</div>
</div>
<div class="output_wrapper">
<div class="output">
<div class="output_area">
<div class="prompt"></div>
<div class="output_png output_subarea">
<img src="data:image/png;base64,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
"/>
</div>
</div>
</div>
</div>
</div>
<div class="cell border-box-sizing text_cell rendered"><div class="inner_cell">
<div class="text_cell_render border-box-sizing rendered_html">
<h2 id="데이터-분할-(train_test_split)">데이터 분할 (train_test_split)</h2>
</div>
</div>
</div>
<div class="cell border-box-sizing text_cell rendered"><div class="inner_cell">
<div class="text_cell_render border-box-sizing rendered_html">
<p>기계학습에서 데이터 분할을 중요한 전처리 과정입니다.</p>
<p><code>sklearn.model_selection</code>의 <code>train_test_split</code>은 클래스 이름 그대로 <strong>학습과 검증 (혹은 테스트) 셋</strong>을 나누어 주는 역할을 합니다.</p>
<p>학습 (Train) / 검증 (Validation or Test) 세트로 나누며, 검증 세트로 <strong>과대 적합</strong>여부를 모니터링 할 수 있습니다.</p>
<p>또한, 검증 세트를 활용하여 모델의 성능 평가를 진행할 수 있습니다.</p>
</div>
</div>
</div>
<div class="cell border-box-sizing text_cell rendered"><div class="inner_cell">
<div class="text_cell_render border-box-sizing rendered_html">
<p><strong>샘플 데이터</strong> 확인</p>
</div>
</div>
</div>
<div class="cell border-box-sizing code_cell rendered">
<div class="input">

<div class="inner_cell">
<div class="input_area">
<div class="highlight hl-ipython3"><pre><span></span><span class="n">df</span><span class="o">.</span><span class="n">head</span><span class="p">()</span>
</pre></div>
</div>
</div>
</div>
<div class="output_wrapper">
<div class="output">
<div class="output_area">

<div class="output_html rendered_html output_subarea output_execute_result">
<div>
<style scoped="">
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }
    
    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
<thead>
<tr style="text-align: right;">
<th></th>
<th>sepal length (cm)</th>
<th>sepal width (cm)</th>
<th>petal length (cm)</th>
<th>petal width (cm)</th>
<th>target</th>
</tr>
</thead>
<tbody>
<tr>
<th>0</th>
<td>5.1</td>
<td>3.5</td>
<td>1.4</td>
<td>0.2</td>
<td>0</td>
</tr>
<tr>
<th>1</th>
<td>4.9</td>
<td>3.0</td>
<td>1.4</td>
<td>0.2</td>
<td>0</td>
</tr>
<tr>
<th>2</th>
<td>4.7</td>
<td>3.2</td>
<td>1.3</td>
<td>0.2</td>
<td>0</td>
</tr>
<tr>
<th>3</th>
<td>4.6</td>
<td>3.1</td>
<td>1.5</td>
<td>0.2</td>
<td>0</td>
</tr>
<tr>
<th>4</th>
<td>5.0</td>
<td>3.6</td>
<td>1.4</td>
<td>0.2</td>
<td>0</td>
</tr>
</tbody>
</table>
</div>
</div>
</div>
</div>
</div>
</div>
<div class="cell border-box-sizing text_cell rendered"><div class="inner_cell">
<div class="text_cell_render border-box-sizing rendered_html">
<p>feature(x), label(y) 데이터를 분할 합니다.</p>
</div>
</div>
</div>
<div class="cell border-box-sizing code_cell rendered">
<div class="input">

<div class="inner_cell">
<div class="input_area">
<div class="highlight hl-ipython3"><pre><span></span><span class="kn">from</span> <span class="nn">sklearn.model_selection</span> <span class="k">import</span> <span class="n">train_test_split</span>
</pre></div>
</div>
</div>
</div>
</div>
<div class="cell border-box-sizing code_cell rendered">
<div class="input">

<div class="inner_cell">
<div class="input_area">
<div class="highlight hl-ipython3"><pre><span></span><span class="n">x</span> <span class="o">=</span> <span class="n">df</span><span class="o">.</span><span class="n">iloc</span><span class="p">[:,</span> <span class="p">:</span><span class="mi">4</span><span class="p">]</span>
<span class="n">x</span><span class="o">.</span><span class="n">head</span><span class="p">()</span>
</pre></div>
</div>
</div>
</div>
<div class="output_wrapper">
<div class="output">
<div class="output_area">

<div class="output_html rendered_html output_subarea output_execute_result">
<div>
<style scoped="">
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }
    
    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
<thead>
<tr style="text-align: right;">
<th></th>
<th>sepal length (cm)</th>
<th>sepal width (cm)</th>
<th>petal length (cm)</th>
<th>petal width (cm)</th>
</tr>
</thead>
<tbody>
<tr>
<th>0</th>
<td>5.1</td>
<td>3.5</td>
<td>1.4</td>
<td>0.2</td>
</tr>
<tr>
<th>1</th>
<td>4.9</td>
<td>3.0</td>
<td>1.4</td>
<td>0.2</td>
</tr>
<tr>
<th>2</th>
<td>4.7</td>
<td>3.2</td>
<td>1.3</td>
<td>0.2</td>
</tr>
<tr>
<th>3</th>
<td>4.6</td>
<td>3.1</td>
<td>1.5</td>
<td>0.2</td>
</tr>
<tr>
<th>4</th>
<td>5.0</td>
<td>3.6</td>
<td>1.4</td>
<td>0.2</td>
</tr>
</tbody>
</table>
</div>
</div>
</div>
</div>
</div>
</div>
<div class="cell border-box-sizing code_cell rendered">
<div class="input">

<div class="inner_cell">
<div class="input_area">
<div class="highlight hl-ipython3"><pre><span></span><span class="n">y</span> <span class="o">=</span> <span class="n">df</span><span class="p">[</span><span class="s1">'target'</span><span class="p">]</span>
<span class="n">y</span><span class="o">.</span><span class="n">head</span><span class="p">()</span>
</pre></div>
</div>
</div>
</div>
<div class="output_wrapper">
<div class="output">
<div class="output_area">

<div class="output_text output_subarea output_execute_result">
<pre>0    0
1    0
2    0
3    0
4    0
Name: target, dtype: int64</pre>
</div>
</div>
</div>
</div>
</div>
<div class="cell border-box-sizing text_cell rendered"><div class="inner_cell">
<div class="text_cell_render border-box-sizing rendered_html">
<p><strong>주요 hyperparameter</strong></p>
<ul>
<li><code>test_size</code>: validation set에 할당할 비율 (20% -&gt; 0.2), 기본값 0.25</li>
<li><code>stratify</code>: 분할된 샘플의 class 갯수가 동일한 비율로 유지</li>
<li><code>random_state</code>: 랜덤 시드값</li>
<li><code>shuffle</code>: 셔플 옵션, 기본값 True</li>
</ul>
</div>
</div>
</div>
<div class="cell border-box-sizing code_cell rendered">
<div class="input">

<div class="inner_cell">
<div class="input_area">
<div class="highlight hl-ipython3"><pre><span></span><span class="n">x_train</span><span class="p">,</span> <span class="n">x_test</span><span class="p">,</span> <span class="n">y_train</span><span class="p">,</span> <span class="n">y_test</span> <span class="o">=</span> <span class="n">train_test_split</span><span class="p">(</span><span class="n">x</span><span class="p">,</span> <span class="n">y</span><span class="p">,</span> <span class="n">stratify</span><span class="o">=</span><span class="n">y</span><span class="p">,</span> <span class="n">test_size</span><span class="o">=</span><span class="mf">0.2</span><span class="p">,</span> <span class="n">random_state</span><span class="o">=</span><span class="mi">30</span><span class="p">)</span>
</pre></div>
</div>
</div>
</div>
</div>
<div class="cell border-box-sizing text_cell rendered"><div class="inner_cell">
<div class="text_cell_render border-box-sizing rendered_html">
<p>원본 <strong>x</strong>의 shape</p>
</div>
</div>
</div>
<div class="cell border-box-sizing code_cell rendered">
<div class="input">

<div class="inner_cell">
<div class="input_area">
<div class="highlight hl-ipython3"><pre><span></span><span class="n">x</span><span class="o">.</span><span class="n">shape</span>
</pre></div>
</div>
</div>
</div>
<div class="output_wrapper">
<div class="output">
<div class="output_area">

<div class="output_text output_subarea output_execute_result">
<pre>(150, 4)</pre>
</div>
</div>
</div>
</div>
</div>
<div class="cell border-box-sizing text_cell rendered"><div class="inner_cell">
<div class="text_cell_render border-box-sizing rendered_html">
<p>분할된 <strong>x</strong>의 shape</p>
</div>
</div>
</div>
<div class="cell border-box-sizing code_cell rendered">
<div class="input">

<div class="inner_cell">
<div class="input_area">
<div class="highlight hl-ipython3"><pre><span></span><span class="n">x_train</span><span class="o">.</span><span class="n">shape</span><span class="p">,</span> <span class="n">x_test</span><span class="o">.</span><span class="n">shape</span>
</pre></div>
</div>
</div>
</div>
<div class="output_wrapper">
<div class="output">
<div class="output_area">

<div class="output_text output_subarea output_execute_result">
<pre>((120, 4), (30, 4))</pre>
</div>
</div>
</div>
</div>
</div>
<div class="cell border-box-sizing text_cell rendered"><div class="inner_cell">
<div class="text_cell_render border-box-sizing rendered_html">
<p>원본 <strong>y</strong>의 shape</p>
</div>
</div>
</div>
<div class="cell border-box-sizing code_cell rendered">
<div class="input">

<div class="inner_cell">
<div class="input_area">
<div class="highlight hl-ipython3"><pre><span></span><span class="n">y</span><span class="o">.</span><span class="n">shape</span>
</pre></div>
</div>
</div>
</div>
<div class="output_wrapper">
<div class="output">
<div class="output_area">

<div class="output_text output_subarea output_execute_result">
<pre>(150,)</pre>
</div>
</div>
</div>
</div>
</div>
<div class="cell border-box-sizing text_cell rendered"><div class="inner_cell">
<div class="text_cell_render border-box-sizing rendered_html">
<p>분할된 <strong>y</strong>의 shape</p>
</div>
</div>
</div>
<div class="cell border-box-sizing code_cell rendered">
<div class="input">

<div class="inner_cell">
<div class="input_area">
<div class="highlight hl-ipython3"><pre><span></span><span class="n">y_train</span><span class="o">.</span><span class="n">shape</span><span class="p">,</span> <span class="n">y_test</span><span class="o">.</span><span class="n">shape</span>
</pre></div>
</div>
</div>
</div>
<div class="output_wrapper">
<div class="output">
<div class="output_area">

<div class="output_text output_subarea output_execute_result">
<pre>((120,), (30,))</pre>
</div>
</div>
</div>
</div>
</div>
</div>
</div>
</body>