# 📝정리 내용

- 반응형 웹

## 💡 처음 알게 된 사실

### 반응형 웹

```css
@media (min-width: 768px) { /* tablet */
  div {
    float: left;
  }

  #div1 {
    height: 562px;
  }

  #div5 {
    width: 50%;
    height: 180px;
  }

  #div6 {
    width: 50%;
    height: 180px;
  }	
}

@media (min-width: 992px) { /* desktop */
  #div5 {
    width: 25%;
    height: 175px;
  }

  #div6 {
    width: 25%;
    height: 175px;
  }
```

- ❓div{ float: left; } 값이 992px 이상일 때에도 적용되는 이유

### BootStrap
<img src="" width="50%" height="50%">
<img src="https://github.com/user-attachments/assets/014c0ed0-8d0d-4130-b89e-b698130c6081" width="50%" height="50%">


- 사용
    - css link 태그 위에 <link> 태그 추가
    - body 끝에 <script>태그 추가

<img src="https://github.com/user-attachments/assets/835e934c-dc62-4610-8a4c-f56d98713e26" width="70%" height="70%">

```css
<div class="container">
    <div class="row">
      <div class="col-3 first">first</div>
      <div class="col-6 second">second</div>
      <div class="col-4 third">third</div>
      <div class="col-7 fourth">fourth</div>
    </div>
  </div>
```

- 부트스트랩을 만든 분들은 왜 하필 `12`라는 숫자로 정했을까
    
    → `12`는 상당히 많은 숫자들(`1`, `2`, `3`, `4`, `6`, `12`)로 나누어지기 때문에 굉장히 유연
    
<img src="https://github.com/user-attachments/assets/f249eeb2-1829-430e-9293-90f13e672b29" width="70%" height="70%">

```css
<div class="container">
    <div class="row">
      <div class="col-6">
        <div class="row"> <!-- 중첩을 위한 새로운 행 -->
          <div class="col-3 first">1</div>
          <div class="col-3 second">2</div>
          <div class="col-3 third">3</div>
          <div class="col-3 fourth">4</div>
        </div>
      </div>

      <div class="col-6">
        <div class="row"> <!-- 중첩을 위한 새로운 행 -->
          <div class="col-3 first">5</div>
          <div class="col-3 second">6</div>
          <div class="col-3 third">7</div>
          <div class="col-3 fourth">8</div>
        </div>
      </div>
    </div>
  </div>
```

### BootStrap - 반응형 그리드

- 지원 구간
1. **Extra Small (< 576px)**: 모바일
2. **Small (≥ 576px)**: 모바일
3. **Medium (≥ 768px)**: 타블릿
4. **Large (≥ 992px)**: 데스크탑
5. **Extra Large (≥ 1200px)**: 와이드 데스크탑

- 컨테이너 종류
1. `<div class="container">`: 구간별로 그리드에 고정된 `width` 설정
    - 구간별 **그리드 고정** 시 레이아웃이 더 **예상** 가능 → `"container"` 클래스를 사용 추천, 디자이너에게 이렇게 구간별로 고정되는 방식으로 만들기 부탁
    
    ```css
    /* container 클래스 사용 */
    .container {
      width: 100%; /* extra small */
      padding-right: 15px;
      padding-left: 15px;
      margin-right: auto;
      margin-left: auto;
    }
    
    /* small */
    @media (min-width: 576px) {
      .container {
        max-width: 540px;
      }
    }
    
    /* medium */
    @media (min-width: 768px) {
      .container {
        max-width: 720px;
      }
    }
    
    /* large */
    @media (min-width: 992px) {
      .container {
        max-width: 960px;
      }
    }
    
    /* extra large */
    @media (min-width: 1200px) {
      .container {
        max-width: 1140px;
      }
    }
    ```
    

1. `<div class="container-fluid">`: 그리드는 항상 `width: 100%;`
    - 상황에 따라 그리드가 항상 `100%`의 가로 길이를 갖는 것이 좋을 때, `"container-fluid"` 클래스 사용
    
    ```css
    .container-fluid {
      width: 100%;
      padding-right: 15px;
      padding-left: 15px;
      margin-right: auto;
      margin-left: auto;
    }
    ```
