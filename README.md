# 바닐라 JS 프로젝트 성능 개선

- url: https://front-3rd-chapter4-2-basic-omega.vercel.app

## a. 개선 이유
초기 PageSpeed와 Lighthouse로 수행한 성능 진단 결과, 각각 47점과 72%라는 낮은 점수를 기록했습니다. 특히 LCP는 9.53초로 측정되어, 빠른 네트워크 환경에서는 큰 문제가 없었으나 네트워크 상태가 다소 열악한 경우 서비스 이용에 상당한 불편을 초래할 수 있는 수준으로 확인되었습니다. 또한 접근성 점수 또한 치명적이지는 않지만 최대한 다양한 사용자가 서비스에 불편 없이 사용할 수 있는 환경을 제공하고자 했습니다.         
이러한 이유로 성능 및 접근성 개선 작업을 진행했습니다.

|PageSpeed|[Git Issue (Lighthouse)](https://github.com/soyoonJ/front_3rd_chapter4-2_basic/issues/1)|
|---|---|
|<img width="824" alt="init" src="https://github.com/user-attachments/assets/d3aa2185-4d0e-4157-8f8b-2cec158e10c7">|<img width="824" alt="git issue init" src="https://github.com/user-attachments/assets/72276495-0eef-4294-bf9f-7cb7ee96d59d">|

## b. 개선 방법
### [성능 최적화]

**1. 이미지 파일 포맷 전환**
- 기존에 사용하던 PNG, JPG 포맷을 WebP로 전환
- WebP를 사용할 경우 고품질 이미지를 표현하면서도 기존 포맷보다 파일 크기가 작게 유지할 수 있어 로딩 시간에 효과가 있었습니다.
- WebP 적용으로 LCP 측정값이 9.53초에서 4.13초로 약 57% 개선되었습니다.

  | 구분 | 적용 전 | 적용 후 |
  |----------|--------|------|
  | WebP 적용 | 9.53s | 4.13s |

**2. 이미지 압축을 통한 용량 최적화**    
- [Tiny PNG](https://tinypng.com/)를 통해 이미지 압축을 진행하여 파일 크기를 줄였습니다. Tiny PNG 설명에 따르면, 자체 알고리즘을 통해 품질 변화 없이 이미지 파일 크기를 최대 80%까지 줄여줍니다. 압축을 통해 LCP 측정값을 2.78초로 개선했습니다.

  | 구분 | 적용 전 | 적용 후 |
  |----------|--------|------|
  | 이미지 압축 | 4.13s | 2.78s |

**3. 반응형 이미지 적용**    
- picture, source 태그를 사용해 반응형 이미지를 구현했습니다.
- 디바이스의 해상도와 화면 크기에 따라 적합한 이미지를 로드하도록 하여 불필요한 리소스가 로딩되는 것을 방지했습니다.

**4. CLS 개선**    
- hidden되는 이미지를 없애고, 이미지 크기를 명시하여 Layout Shift를 개선했습니다.
- 0.011에서 0.001로 개선했습니다.

  | 구분 | 적용 전 | 적용 후 |
  |----------|--------|--------|
  | 이미지 압축 | 0.011s | 0.001s |

**5. product.js image lazy loading**    
- product.js에서 사용되는 이미지에 대해 ```img.loading = "lazy";```를 추가하여 lazy loading을 적용했습니다.

**6. 스크롤 위치에 따라 초기 js 실행 범위 축소**    
- 무거운 script에 대해 사용자 스크롤이 product에 진입할 때만 실행하여 초기 로딩 시간을 단축했습니다.

**7. 폰트 self hosting**    
- 웹 폰트가 아닌 폰트 셀프 호스팅을 통해 불필요한 네트워크 요청을 줄였습니다.

**8. defer, DOMContentLoaded**    
- JavaScript script에 defer 속성을 추가하여 HTML 파싱과 script 로딩이 병렬로 진행되도록 처리했습니다. async 속성과는 다르게 defer에서 script 실행은 HTML 파싱이 모두 완료된 후 진행됩니다.
- 또한 당장 불필요한 script는 DOMContentLoaded가 된 후 실행되도록 처리하여 초기 로딩 속도를 개선했습니다.

### [접근성 최적화]
**1. 이미지 대체텍스트 추가**    
- img 태그에 alt 추가 후 이에 맞는 대체텍스트를 작성하여 접근성을 높임


## c. 개선 후 향상된 지표
|PageSpeed|[Git Issue (Lighthouse)](https://github.com/soyoonJ/front_3rd_chapter4-2_basic/issues/1)|
|---|---|
|<img width="949" alt="alt 추가" src="https://github.com/user-attachments/assets/d4e1c04b-2304-46ae-9e63-413539a998cc">|<img width="824" alt="git issue 최종" src="https://github.com/user-attachments/assets/c9adb223-0b07-4bb0-8f92-2f4ba44662f9">|


## d. 기타
### 성능측정도구
- PageSpeed : https://pagespeed.web.dev/
