# Spring_part4_mreview

---
---

## 요구사항 분석

- 영화, 회원 엔티티가 있다.
- 회원이 영화 리뷰를 작성할 수 있다
- 영화에 대한 회원 평점과 리뷰를 쓸 수 있다.
- 영화에 이미지를 출력할 수 있다.
- 영화 데이터에 파일 업로드를 이용해서 영화의 이미지 파일 등을 업로드에서 처리할 수 있다.
- 목록 화면에서 **영화번호/ 영화이미지/ 영화제목/ 리뷰개수/ 평균 점수 순으로 출력**
- 영화 조회 화면에서 영화와 이미지들 , 리뷰의 평균 점수/ 리뷰 개수 같이 출력
- 리뷰에 대한 정보에는 회원의 이메일이나 닉네임(nickname)과 같은 정보를 같이 출력.
- 영화 조회 화면에서 , 영화 리뷰를 조회할 수 있고, 자신이 영화에 대한 영화 리뷰(Review)를 등록하거나 수정/삭제 할 수 있다.
- 영화를 등록과 수정할 수 있다. 이때 이미지도 등록 가능하다.
- 사용자는 버튼을 클릭해서 영화 리뷰를 입력할 수 있는 모달 창을 보게 된다.
    - 모달 창에는 별점(점수)와 감상을 부여할 수 있다.
    - 회원의 아이디와 리뷰 점수, 내용을 입력하게 한다.

## api 규격서

- 파일 규격서
    
    
    | 방식 | 호출 대상 | 파라미터 | 작업 | 반환되는 데이터 |
    | --- | --- | --- | --- | --- |
    | GET | uploadEx | 없음 | html 테스트 | 없음 |
    | POST | /uploadAjax | dataType - json | 파일 업로드를 실행 | JSON 배열 |
    | DELETE |  |  |  |  |
    | PUT |  |  |  |  |
    | 몰루 | ${org.zerock.upload.path} |  | 업로드된 파일 저장 경로 |  |
    | GET | /display | String FileName | URL 인코딩된 파일 이름을 파라미터로 받아서, 해당 파일을 byte[]로 만들어서 브라우저로 전송, ‘/display?fileName=xxxx’ |  |
    | POST | /removeFile | String FileName | 원본 파일과 섬네일 파일을 같이 삭제. |  |
    | Request | /movie |  | 영화 등록에 사용될 주소 |  |
    | GET | /movie/register | 없음 | 영화 등록 페이지 |  |
    | POST | /movie/register | MovieDTO movieDTO, RedirectAttributes redirectAttributes | POST방식으로 전달된 파라미터들을 MovieDTO로 수집해서 MovieService 타입 객체의 register()를 호출한다 | “redirect:/movie/list” |
    | GET | /movie/list | PageRequestDTO pageRequestDTO, Model model | 목록 화면 부분이 나타난다. |  |
    | GET | /movie/read    URL : /movie/read?mno=xxx  | long mno, @ModelAttribute("requestDTO") PageRequestDTO requestDTO, Model model |  |  |
    | GET | /movie/modify | long mno, @ModelAttribute("requestDTO") PageRequestDTO requestDTO, Model model |  |  |
    | GET | /reviews/영화번호/all |  | 해당 영화의 모든 리뷰 반환 | ReviewDTO 리스트 |
    | POST | /reviews/영화번호 |  | 새로운 리뷰 등록 | 생성된 리뷰 번호 |
    | PUT | /reviews/영화번호/영화리뷰번호 |  | 리뷰 수정 | 리뷰의 수정 성공 여부 |
    | DELETE | /review/영화번호/영화리뷰번호 |  | 리뷰 삭제 | 리뷰삭제 |

## 엔티티 관계도

![image](https://user-images.githubusercontent.com/96537605/183608016-220777c2-294c-44f1-97fb-7cb1f610fa7b.png)
---

## 설명

### 1. 전체 목록 창

![image](https://user-images.githubusercontent.com/96537605/183608063-2c2186a1-cdb0-4c6a-b38c-72f4f1b980a5.png)
### 2. 영화 등록하기

1. REGISTER 클릭
2. 타이틀입력 및 사진 업로드

![image](https://user-images.githubusercontent.com/96537605/183608098-6f98e989-20f0-4d13-959a-5088baa74235.png)
3. Submit

![image](https://user-images.githubusercontent.com/96537605/183608160-b5ce0b6d-4f99-4dae-ad2f-43df67754750.png)
- 등록 완료

### 3. 리뷰 등록

1. **메인 화면에서 번호 클릭 → ReviewRegister 클릭**

![image](https://user-images.githubusercontent.com/96537605/183608202-1988a901-7951-42ca-b76f-9d2bc76c573b.png)
![image](https://user-images.githubusercontent.com/96537605/183608230-70650da6-4dc5-42c3-beed-0ce8e66700a7.png)
- 별점, ID, Text 입력. ID는 숫자만 가능.

![image](https://user-images.githubusercontent.com/96537605/183608264-ca6f2cbf-422c-4312-a633-ea39287aa655.png)
### 4. 리뷰 리스트 보여주기

![image](https://user-images.githubusercontent.com/96537605/183608284-4d990345-66ad-44c2-a569-c22ad6a1aa1f.png)
### 5. 특정 리뷰 선택하기

- 수정 또는 삭제도 가능하다.

![image](https://user-images.githubusercontent.com/96537605/183608345-eb7495e6-ae64-405b-a4ea-05e860ef7266.png)
![image](https://user-images.githubusercontent.com/96537605/183608392-dcf135ec-dab3-4cf5-ab2a-c4fd65e87947.png)
