# 바닐라 JS 프로젝트 성능 개선

- url: https://front-3rd-chapter4-2-basic-omega.vercel.app

## 성능 개선 보고서

<!-- 가독성을 위해 표 형식으로 정리하는것을 추천합니다. -->

### a. 개선 이유
초기 PageSpeed와 Lighthouse로 수행한 성능 진단 결과, 각각 47점과 72%라는 낮은 점수를 기록했습니다. 특히 LCP는 9.53초로 측정되어, 빠른 네트워크 환경에서는 큰 문제가 없었으나 네트워크 상태가 다소 열악한 경우 서비스 이용에 상당한 불편을 초래할 수 있는 수준으로 확인되었습니다. 또한 접근성 점수 또한 치명적이지는 않지만 최대한 다양한 사용자가 서비스에 불편 없이 사용할 수 있는 환경을 제공하고자 했습니다.         
이러한 이유로 성능 및 접근성 개선 작업을 진행했습니다.

<img width="824" alt="init" src="https://github.com/user-attachments/assets/d3aa2185-4d0e-4157-8f8b-2cec158e10c7">


### b. 개선 방법
#### 성능 최적화
webp 도입
compress images - https://tinypng.com/
반응형 이미지 - picture 태그
이미지 크기 지정
layout shift 1,2
product.js image lazy loading
스크롤 위치에 따라 초기 js 실행 범위 축소
폰트 self hosting
defer, DOMContentLoaded

### 접근성 최적화
alt 추가


### c. 개선 후 향상된 지표

### d. 기타 등등
#### 성능측정방법
- PageSpeed : https://pagespeed.web.dev/
