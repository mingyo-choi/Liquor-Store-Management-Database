# Liquor-Store-Management-Database

팀 프로젝트 당시 github 사용하여 협업하지 않아, 임의로 개인 레포지토리에 완성본을 업로드

🔗 **JDBC를 사용한 데이터베이스 응용 프로그램**

🔗 **주류 매장 관리자 입장**에서 고객과 주류매장 사이에 이루어지는 판매, 구매, 리뷰 정보를 관리하고, 제조업체로부터 발주를 넣어 납품받은 주류의 재고를 관리할 수 있는 주류 매장 관리 시스템

- JDBC를 이용하여 MYSQL 데이터베이스로부터 정보 삽입, 갱신, 삭제, 추가하는 사용자 친화적 자바 응용 프로그램 구현
- 5인 팀 프로젝트
- 2022.03 ~ 2022.06.

🔗 **프로젝트 구상 배경**

주류 매장에 있는 주류의 경우 종류도 다양하고, 같은 명칭의 술이라고 하더라도 473ml, 500ml, 1000ml 등의 다양한 사이즈로 출시가 되고 있기 때문에 주류매장에서는 이렇게 다양한 종류의 주류의 기록을 관리하는 프로그램이 없다면 매장 운영에 무리가 있을 것으로 판단하였다. 또한 주류 매장에서는 한 번 발주를 받을 때 다양한 종류의 주류를 한 번에 받아오기 때문에 이 기록을 정리하는 것과 고객이 주류매장 이용 후 작성한 리뷰를 정리하는 것도 중요하기 때문에 이를 도와줄 수 있는 데이터베이스 프로그램을 만들기로 하였다.

🔗 **맡은 역할**

- ER Diagram 작성
- 회원 관리 기능 구현
- 리뷰 관리 기능 구현
- 회원, 리뷰, 주문, 상품 관리 기능 테스트
- 회원, 리뷰, 주문, 상품 관리 기능 보완
- 중간발표 대본 제작 및 중간발표
- 최종발표자료(ppt) 제작
- 최종발표 대본 제작
- 최종발표 녹화
- 발표비디오와 데모비디오 편집
- 최종 실시간 시연

#
**요구사항 분석**
* 매장 회원 관리 </br>
1. 주류 매장의 회원으로 가입하려면 회원 전화번호, 이름을 입력해야 한다. </br>
2. 가입한 회원에게는 회원 등급이 부여되고 누적 구매 금액에 따라 등급이 변경된다. </br>
3. 회원 등급에 따라 상품 할인율이 달라진다. </br>
4. 회원은 회원 전화번호로 식별한다. </br>
5. 회원에 대한 이름, 회원 전화번호, 누적 구매 금액, 회원등급에 대한 정보를 유지해야 한다. </br>
* <매장 상품 관리> </br>
6. 상품은 상품에 대한 상품 카테고리(주종), 상품명, 상품 사이즈, 상품 판매 가격, 제조업체, 재고량 정보를 유지해야 한다. </br>
7. 상품은 상품 이름과 사이즈로 식별한다. </br>
8. 회원은 여러 상품을 주문할 수 있고, 하나의 상품을 여러 회원이 주문할 수 있다. </br>
* <발주 내역> </br>
9. 각 상품은 여러 제조업체가 납품하고, 제조업체 하나는 여러 상품을 납품할 수 있다.</br>
10. 제조업체가 상품을 납품하면 납품 일자, 납품 시간과 납품 수량 정보가 생성된다.</br>
11. 발주 내역에 대한 제조업체명, 납품 상품 가격, 납품 시간, 납품 상품명, 납품 수량, 담당자 이름, 제조업체 전화번호에 대한 정보를 유지해야 한다.</br>
* <리뷰> </br>
12. 회원은 리뷰를 여러 개 작성할 수 있지만 한 번의 방문 영수증(하나의 영수증 번호)으로는 하나의 리뷰밖에 작성할 수 없고, 리뷰 하나는 한 명의 회원만 작성할 수 있다. </br>
13. 리뷰에 대한 영수증 번호, 구매 번호, 방문 일자, 작성자, 평점, 리뷰 작성 일자 정보를 유지해야 한다. </br>
14. 리뷰는 영수증 번호로 식별한다. </br>
* <영수증 관리> </br>
15. 회원이 상품을 주문하면 구매한 품목 전체를 대표하는 정보로서 영수증 번호, 회원 전화번호, 총 결제 금액, 판매일자를 유지해야한다. </br>
16. 영수증 번호는 결제 건수 당 한 개가 부여된다. </br>
17. 회원은 여러 상품을 구매할 수 있고, 하나의 상품을 여러 개 구매할 수도 있다. </br>
18. 전체 판매 정보는 영수증 번호로 식별한다. </br>
* <영수증 품목 관리> </br>
19. 회원이 상품을 주문하면 구매한 개별 상품에 대한 정보로서 영수증 번호, 구매한 각각의 상품에 대한 개별 상품 번호, 상품명, 수량, 가격을 유지해야 한다. </br>
20. 영수증 번호는 결제 건수 당 한 개가 부여되고, 상품 번호는 하나의 주문 품목 당 한 개가 부여된다. </br>
21. 개별 판매 정보는 영수증 번호와 상품 번호로 식별한다</br>

#
**ER 다이어그램**
![image](https://github.com/mingyo-choi/Liquor-Store-Management-Database/assets/128064550/f723cd20-c03d-42e3-a1cd-f6891daa6bcd)
</br> 회원 테이블과 상품 테이블 사이 / 상품과 발주 사이에는 many-to-many의 관계가 있고, 리뷰 테이블과 회원 사이/ 품목 테이블과 영수증 테이블 사이에는 many - to - one의 관계가 있다. 또한 리뷰 테이블과 영수증 테이블 사이에 one - to - one의 관계가 있는데, 이 모든 관계를 ER 다이어그램에 포함하였다. 또한 상품과 발주 / 품목과 영수증에는 total participation의 관계가 성립하고 리뷰의 경우에도 영수증 테이블에 대해 total participation이 성립한다.

#
**스키마 다이어그램**
![image](https://github.com/mingyo-choi/Liquor-Store-Management-Database/assets/128064550/01ed6706-fcb7-4301-9673-1d0092f78865)
</br> 
* 회원 테이블의 primary key는 회원전화번호 </br>
* 상품 테이블의 primary key는 상품번호 </br>
* 발주 테이블의 primary key는 (발주날짜, 발주시간) </br>
* 리뷰 테이블의 primary key는 영수증번호 </br>
* 영수증 테이블의 primary key는 영수증번호 </br>
* 품목 테이블의 primary key는 (영수증번호, 상품번호) </br>
</br>

* 영수증 테이블의 회원전화번호는 회원 테이블의 회원 전화번호를 foreign key로 참조 </br>
* 발주 테이블의 발주상품번호는 상품 테이블의 상품번호를 foreign key로 참조 </br>
* 품목 테이블의 영수증번호는 영수증 테이블의 영수증번호를 foreign key로 참조 </br>
* 상품번호는 상품 테이블의 상품번호를 foreign key로 참조 </br>
* 리뷰 테이블의 작성자는 회원 테이블의 회원전화번호를 foreign key로 참조 </br>

#
**기타 기능**
* 뒤로가기 기능 </br>
뒤로가기 기능을 통해 사용자가 숫자를 잘못 입력하였을 때에도 프로그램을 종료했다가 다시 시작하는 것이 아니라 뒤로 가기 버튼을 눌러 다시 숫자를 입력할 수 있다. </br>
* 영수증과 품목 테이블 분리 </br>
영수증과 품목 테이블을 분리하여 영수증 테이블에서는 영수증별 총결제금액과 전화번호(구매회원), 판매일자를 확인할 수 있고 품목 테이블에서는 영수증과 세부 구매 품목, 수량 등을 확인할 수 있다. 이를 통해 실제 가게에서의 포스기와 비슷한 기능을 구현하여 정산과 판매 관리가 쉽다. </br>
* 팀의 데이터베이스 attribute들을 바탕으로 구현한 추가적인 기능 </br>
1) 재고량이 부족한 경우 발주가 잘 이루어 지는지 파악하는 기능이 있어, 재고량이 50개 이하인 경우 발주에 그 항목이 있는지 확인할 수 있다. </br>
2) 판매 실적을 높일 수 있는 고객을 특정 조건에 따라 선별하여 관리할 수 있는 기능이 있어, 고객 만족도와 최근방문일자, 등급의 조건을 만족하는 고객들을 선별하여 단골 고객을 파악할 수 있게 해준다. </br>
3) 카카오 등에서 활용하고 있는 실험실의 형식으로 구현하여, 추후 데이터베이스의 캐주얼 사용자의 피드백을 받아서 이러한 조건을 수정할 수 있는 형태로 만들었다.
