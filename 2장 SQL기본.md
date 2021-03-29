## SQL 기본

### DB
특정 기업이나 조직 또는 개인이 필요에 의해 데이터를 일정한 형태로 저장해 놓은 것을 의미한다.

### DBMS
효율적인 데이터 관리뿐만 아니라 예기치 못한 사건으로 인한 데이터의 손상을 피하고, 필요시 필요한 데이터를 복구하기 위한 강력한 기능의 SW

### DB 발전
1960 : 플로우차트 중심의 개발, 파일구조 사용
1970 : DB 관리기법이 처음 태동, 계층-망형 DB등장
1980 : 관계형 DB 상용화, Oracle, Sybase 등장
1990 : 객체 관계형 DB로 발전

### SQL
관계형 DB에서 데이터 정의, 조작, 제어를 위해 사용하는 언어

### SQL 문장들의 종류
DML : SELECT, INSERT, UPDATE, DELETE 등 데이터 조작어
DDL : CREATE, ALTER, DROP, RENAME 등 데이터 정의어
DCL : GRANT, REVOKE 등 데이터 제어어
TCL : COMMIT, ROLLBACK 등 트랜잭션 제어어

### 테이블
데이터를 저장하는 객체, 로우(가로, 행)와 칼럼(세로, 열)으로 구성

### 기본키
테이블에 존재하는 각 행을 한 가지 의미로 특정할 수 있는 한 개 이상의 칼럼

### 외부키
다른 테이블의 기본키로 사용되고 있는 관계를 연결하는 칼럼

--------------------------------------------

### 데이터 유형
CHAR(s) : 고정 길이 문자열 정보
‘AA’ = ‘AA  ’
VARCHAR(s) : 가변 길이 문자열 정보
‘AA’ != ‘AA  ’
NUMERIC : 정수, 실수 등 숫자 정보
DATE : 날짜와 시각 정보

CREATE TABLE 테이블이름 (
);
테이블 명은 다른 테이블의 이름과 중복되면 안 된다.
테이블 내의 칼럼명은 중복될 수 없다.
각 칼럼들은 , 로 구분되고 ; 로 끝난다.
칼럼 뒤에 데이터 유형은 꼭 지정되어야 한다.
테이블명과 칼럼명은 반드시 문자로 시작해야한다.
A-Z,a-z,0-9,_, $, #만 사용 가능
DATETIME 데이터 유형에는 별도로 크기를 지정x

### 제약조건
1. PRIMARY KEY(기본키) : 기본키 정의
2. UNIQUE KEY(고유키) : 고유키 정의
3. NOT NULL : NULL 값 입력금지
4. CHECK : 입력 값 범위 제한
5. FOREIGN KEY(외래키) : 외래키 정의

DESC(RIBE) 테이블명; -> 테이블 구조 확인(Oracle)
exec sp_help ‘db0.테이블명’ go -> (SQL Server)

테이블 구조 변경(칼럼 추가, 삭제 등) DDL
ALTER TABLE 테이블명
-ADD 칼럼명 데이터 유형;
-DROP COLUMN 칼럼명;
-MODIFY (칼럼명 데이터유형 DEFAULT식 NOT NULL); -> 칼럼 데이터 유형, 조건 등 변경 Oracle
-ALTER COLUMN (칼럼명 데이터유형 DEFAULT식 NOT NULL); -> SQL Server
-RENAME COLUMN 변경전칼럼 TO 뉴칼럼명; Ora
sp_rename 변경전칼럼명, 뉴칼럼명, ‘COLUMN’; SQ
-DROP CONSTRAINT 조건명; 제약조건 삭제
-ADD CONSTRAINT 조건명 조건 (칼럼명); 조건 추가
