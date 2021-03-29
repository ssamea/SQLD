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

-RENAME 변경전테이블명 TO 변경후테이블명; Ora
sp_rename ‘db0.TEAM’,‘TEAM_BACKUP’; SQL
-DROP TABLE 테이블명 [CASCADE CONSTRAINT]
-CASCADE CONSTRAINT : 참조되는 제약조건 삭제
-TRUNCATE TABLE 테이블명: 행 제거, 저장공간 재사용

--------------------------------------------

### DML
DDL 명령어의 경우 실행시 AUTO COMMIT 하지만 DML의 경우 COMMIT을 입력해야 한다.
SQL Server의 경우 DML도 AUTO COMMIT

INSERT INTO PLAYER (PLAYER) VALUES (‘PJS’);
UPDATE PLAYER SET BACK_NO = 60;
DELETE FROM PLAYER;
SELECT PLAYER_ID FROM PLAYER;
SELECT DISTINCT POSITION 시 구분값만 출력 ex)GK, FW, DF, MF
SELECT PLAYER AS “선수명” FROM PLAYER;

### 와일드카드
* : 모든
% : 모든
- : 한 글자

### 합성 연산자
문자와 문자 연결 : ||(Oracle), +(SQL Server)
SELECT PLAYER_NAME + ‘선수’ “정보”

--------------------------------------------

## TCL

### 트랜잭션 : 밀접히 관련되어 분리될 수 없는 1개 이상의 DB 조작

COMMIT : 올바르게 반영된 데이터를 DB에 반영
ROLLBACK : 트랜잭션 시작 이전의 상태로 되돌림
SAVEPOINT : 저장 지점

### 트랜잭션의 특성
1. 원자성 : 트랜잭션에서 정의된 연산들은 모두 성공적으로 실행되던지 아니면 전혀 실행되지 않아야 함
2. 일관성 : 트랜잭션 실행 전 DB 내용이 잘못 되지 않으면 실행 후도 잘못 되지 않아야 함
3. 고립성 : 트랜잭션 실행 도중 다른 트랜잭션의 영향을 받아 잘못된 결과를 만들어서는 안된다.
4. 지속성 : 트랜잭션이 성공적으로 수행되면 DB의 내용은 영구적으로 저장된다.

SAVEPOINT SVPT1; (Oracle)
ROLLBACK TO SVPT1; (Oracle)
SAVE TRAN SVPT1; (SQL Server)
ROLLBACK TRAN SVPT1; (SQL Server)
COMMIT;

--------------------------------------------

### 연산자의 종류
BETWEEN a AND b : a와 b 값 사이에 있으면 됨
IN (list) : 리스트에 있는 값 중 어느 하나라도 일치
LIKE ‘비교 문자열’ : 비교 문자열과 형태가 일치
IS NULL : NULL 값인 경우
NOT IN (list) : list의 값과 일치하지 않는다
IS NOT NULL : NULL 값을 갖지 않는다.

### 연산자우선순위
()->NOT->비교연산자->AND->OR

SELECT PLAYER_NAME 선수명
FROM PLAYER
WHERE TEAM_ID = ‘K2’; -> 팀ID가 K2인 사람
WHERE TEAM_ID IN (‘K2’,‘K7’); -> K2,K7인 사람
WHERE HEIGHT BETWEEN 170 AND 180;
-> 키가 170 ~ 180인 사람
WHERE POSITION IS NULL; -> 포지션 없는 사람

NULL 값과의 수치연산은 NULL 값을 리턴한다.
NULL 값과의 비교연산은 거짓(FALSE)를 리턴한다.

ROWNUM : 원하는 만큼의 행을 가져올 때 사용(Or)
TOP : (SQL Server)
WHERE ROWNUM =1;
SELECT TOP(1) PLAYER_NAME FROM PLAYER;

--------------------------------------------

### 문자형 함수
LOWER : 문자열을 소문자로
UPPER : 문자열을 대문자로
ASCII : 문자의 ASCII 값 반환
CHR/CHAR : ASCII 값에 해당하는 문자 반환
CONCAT : 문자열1, 2를 연결
SUBSTR/SUBSTRING : 문자열 중 m 위치에서 n개의 문자 반환
LENGTH/LEN : 문자열 길이를 숫자 값으로 반환

CONCAT(‘RDBMS’,‘ SQL’) -> ‘RDBMS SQL’
SUBSTR(‘SQL Expert’,5,3) -> ‘Exp’
LTRIM(‘xxxYYZZxYZ’,‘x’) -> ‘YYZZxYZ’
RTRIM(‘XXYYzzXYzz’,‘z’) -> ‘XXYYzzXY’
TRIM(‘x’ FROM ‘xxYYZZxYZxx’) -> ‘YYZZxYZ’

### 숫자형 함수
SIGN(n) : 숫자가 양수면1 음수면-1 0이면 0 반환
MOD : 숫자1을 숫자2로 나누어 나머지 반환
CEIL/CEILING(n) : 크거나 같은 최소 정수 반환
FLOOR(n) : 작거나 같은 최대 정수 리턴

ROUND(38.5235,3) -> 38.524
ROUND(38.5235,1) -> 38.5
ROUND(38.5235) -> 39
TRUNC(38.5235,3) -> 38.523
TRUNC(38.5235,1) -> 38.5
TRUNC(38.5235) -> 38

### 날짜형 함수
SYSDATE/GETDATE() 현재 날짜와 시각 출력
EXTRACT/DATEPART 날짜에서 데이터 출력
TO_NUMBER(TO_CHAR(d,‘YYYY’))/YEAR(d)

SELECT ENAME,
         CASE WHEN SAL >=3000 THEN ‘HIGH’
               WHEN SAL >=1000 THEN ‘MID’
               ELSE ‘LOW’
         END AS SALARY_GRADE
FROM EMP;

### NULL 관련 함수
NVL(식1,식2)/ISNULL(식1,식2) : 식1의 값이 NULL 이면 식2 출력
NULLIF(식1,식2) : 식1이 식2와 같으면 NULL을 아니면 식1을 출력
COALESCE(식1,식2) : 임의의 개수표현식에서 NULL이 아닌 최초의 표현식, 모두 NULL이면 NULL 반환
ex)COALESCE(NULL,NULL,‘abc’) -> ‘abc’

--------------------------------------------

### 집계 함수
1. 여러 행들의 그룹이 모여서 그룹당 단 하나의 결과를 돌려주는 함수이다.
2. GROUP BY 절은 행들을 소그룹화 한다.
3. SELECT, HAVING, ORDER BY 절에 사용 가능
-ALL : Default 옵션
-DISTINCT : 같은 값을 하나의 데이터로 간주 옵션

COUNT(*) : NULL 포함 행의 수
COUNT(표현식) : NULL 제외 행의 수
SUM, AVG : NULL 제외 합계, 평균 연산
STDDEV : 표준 편차
VARIAN : 분산
MAX, MIN : 최대값, 최소값

### GROUP BY, HAVING 절의 특징
1. GROUP BY 절을 통해 소그룹별 기준을 정한 후, SELECT 절에 집계 함수를 사용한다.
2. 집계 함수의 통계 정보는 NULL 값을 가진 행을 제외하고 수행한다.
3. GROUP BY 절에서는 ALIAS 사용 불가
4. 집계 함수는 WHERE 절에 올 수 없다.
5. HAVING 절에는 집계 함수를 이용하여 조건 표시
6. HAVING 절은 일반적으로 GROUP BY 뒤에 위치

SEARCHED_CASE_EXPRESSION
CASE WHEN LOC = ‘a’ THEN ‘b’
SIMPLE_CASE_EXPRESSION
CASE LOC WHEN ‘a’ THEN ‘b’
이 2문장은 같은 의미이다.

--------------------------------------------

### ORDER BY 특징
1. SQL 문장으로 조회된 데이터들을 다양한 목적에 맞게 특정한 칼럼을 기준으로 정렬하여 출력하는 데 사용한다.
2. ORDER BY 절에 칼럼 명 대신 ALIAS 명이나 칼럼 순서를 나타내는 정수도 사용 가능하다.
3. DEFAULT 값으로 오름차순(ASC)이 적용되며 DESC 옵션을 통해 내림차순으로 정렬이 가능하다.
4. SQL 문장의 제일 마지막에 위치한다.
5. SELECT 절에서 정의하지 않은 칼럼 사용 가능

Oracle에서는 NULL을 가장 큰 값으로 취급하며 SQL Server에서는 NULL을 가장 작은 값으로 취급한다.

### SELECT 문장 실행 순서
FROM -> WHERE -> GROUP BY -> HAVING -> SELECT -> ORDER BY

SELECT TOP(2) WITH TIES ENAME, SAL
FROM EMP
ORDER BY SAL DESC;
위는 급여가 높은 2명을 내림차순으로 출력하는데 같은 급여를 받는 사원은 같이 출력한다(WITH TIES)

--------------------------------------------

### JOIN : 두 개 이상의 테이블들을 연결 또는 결합하여 데이터를 출력하는 것
일반적으로 행들은 PK나 FK 값의 연관에 의해 JOIN이 성립된다. 어떤 경우에는 PK, FK 관계가 없어도 논리적인 값들의 연관만으로 JOIN이 성립가능하다.

5가지 테이블을 JOIN 하기 위해서는 최소 4번의 JOIN 과정이 필요하다. (N-1)

### EQUI JOIN : 2 개의 테이블 간에 칼럼 값들이 서로 정확하게 일치하는 경우에 사용, 대부분 PK, FK의 관계를 기반으로 한다.

SELECT PLAYER.PLAYER_NAME
FROM PLAYER
위 SQL처럼 컬럼명 앞에 테이블 명을 기술해줘야 함

### NON EQUI JOIN : 2개의 테이블 간에 칼럼 값들이 서로 정확하게 일치하지 않는 경우에 사용
‘=’ 연산자가 아닌 BETWEEN, >, <= 등 연산자 사용

SELECT E.ENAME, E.JOB, E.SAL, S.GRADE
FROM EMP E, SALGRADE S
WHERE E.SAL BETWEEN S.LOSAL AND S.HSAL;
위는 E의 SAL의 값을 S의 LOSAL과 HSAL 범위에서 찾는 것이다.

============================================

### 집합 연산자 
두 개 이상의 테이블에서 조인을 사용하지 않고 연관된 데이터를 조회할 때 사용
SELECT 절의 칼럼 수가 동일하고 SELECT 절의 동일 위치에 존재하는 칼럼의 데이터 타입이 상호 호환할 때 사용 가능

### 일반 집합 연산자
1. UNION : 합집합(중복 행은 1개로 처리)
2. UNION ALL : 합집합(중복 행도 표시)
3. INTERSECT : 교집합(INTERSECTION)
4. EXCEPT/MINUS : 차집합(DIFFERENCE)
5. CROSS JOIN : 곱집합(PRODUCT)

### 순수 관계 연산자 : 관계형 DB를 새롭게 구현
1. SELECT -> WHERE절
2. PROJECT -> SELECT절
3. NATRUAL JOIN -> 다양한 JOIN
4. DIVIDE -> 사용x
{a,x}{a,y}{a,z} divdie {x,z} = {a}

### FROM 절 JOIN 형태
1. INNER JOIN
2. NATURAL JOIN
3. USING 조건절
4. ON 조건절
5. CROSS JOIN
6. OUTER JOIN

1. INNER JOIN : JOIN 조건에서 동일한 값이 있는 행만 반환, USING이나 ON 절을 필수적으로 사용
ex) SELECT EMP.DEPTNO, EMPNO, ENAME, DNAME FROM EMP INNER JOIN DEPT ON EMP.DEPTNO = DEPT.DEPTNO; 

2. NATURAL JOIN : 두 테이블 간의 동일한 이름을 갖는 모든 칼럼들에 대해 EQUI JOIN 수행, NATURAL JOIN이 명시되면 추가로 USING, ON, WHERE 절에서 JOIN 조건을 정의할 수 없다, SQL Sever는 지원x, 칼럼명에도 식별자 사용 X
ex) SELECT DEPTNO, EMPNO, ENAME, DNAME FROM EMP NATURAL JOIN DEPT;

3. USING 조건절
같은 이름을 가진 칼럼들 중에서 원하는 칼럼에 대해서만 선택적으로 EQUI JOIN을 할 수 있다, JOIN 칼럼에 대해서 ALIAS나 테이블 이름과 같은 접두사를 붙일 수 없다, SQL Server 지원x

4. ON 조건절
ON 조건절과 WHERE 조건절을 분리하여 이해가 쉬우며, 칼럼명이 다르더라도 JOIN 조건을 사용할 수 있는 장점이 있다, ALIAS나 테이블명 반드시 사용

### [ON vs WHERE]
ON : JOIN을 하기 전 필터링을 한다 (=ON 조건으로 필터링이 된 레코들 간 JOIN이 이뤄진다)
WHERE : JOIN을 한 후 필터링을 한다 (=JOIN을 한 결과에서 WHERE 조건절로 필터링이 이뤄진다)

### CROSS JOIN
양쪽 집합의 M*N건의 데이터 조합이 발생한다.

### OUTER JOIN
JOIN 조건에서 동일한 값이 없는 행도 반환 가능하다, USING이나 ON 조건절 반드시 사용해야 함

### LEFT OUTER JOIN
조인 수행시 먼저 표기된 좌측 테이블에 해당하는 데이터를 읽은 후, 나중 표기된 우측 테이블에서 JOIN 대상 데이터를 읽어 온다. 우측 값에서 같은 값이 없는 경우 NULL 값으로 채운다.

### RIGHT OUTER JOIN
LEFT OUTER JOIN의 반대

### FULL OUTER JOIN
조인 수행시 좌측, 우측 테이블의 모든 데이터를 읽어 JOIN하여 결과를 생성한다. 중복 데이터는 삭제한다.

--------------------------------------------

### 계층형 질의
테이블에 계층형 데이터가 존재하는 경우 데이터를 조회하기 위해 사용

SATRT WITH : 계층 구조 전개의 시작 위치 지정
CONNECT BY : 다음에 전개될 자식 데이터 지정
PRIOR : CONNECT BY 절에 사용되며, 현재 읽은 칼럼을 지정한다. PRIOR 자식 = 부모 형태를 사용하면 계층구조에서 부모 데이터에서 자식 데이터(부모->자식) 방향으로 전개하는 순방향 전개를 한다. 반대는 역방향 전개
NOCYCLE : 동일한 데이터가 전개되지 않음
ORDER SIBLINGS BY : 형제 노드 간의 정렬 수행
WHERE : 모든 전개를 수행한 후에 지정된 조건을 만족하는 데이터만 추출한다.(필터링)

LEVEL : 루트 데이터이면 1, 그 하위 데이터면 2, 리프 데이터까지 1씩 증가
CONNECT_BY_ISLEAF : 해당 데이터가 리프 데이터면 1, 그렇지 않으면 0
CONNECT_BY_ISCYCLE : 해당 데이터가 조상이면 1, 아니면 0 (CYCLE 옵션 사용했을 시만 사용 가능)
SYS_CONNECT_BY_PATH : 루트 데이터부터 현재 전개할 데이터까지의 경로를 표시한다.
CONNECT_BY_ROOT : 현재 전개할 데이터의 루트 데이터를 표시한다. 단항 연산자이다.

### 셀프 조인
동일 테이블 사이의 조인, FROM 절에 동일 테이블이 2번 이상 나타난다. 반드시 테이블 별칭을 사용해야 함

### 서브 쿼리
하나의 SQL문안에 포함되어 있는 또 다른 SQL문, 알려지지 않은 기준을 이용한 검색에 사용

### 서브 쿼리 사용시 주의 사항
1. 서브 쿼리를 괄호로 감싸서 사용한다.
2. 서브 쿼리는 단일 행 또는 복수 행 비교 연산자와 함께 사용 가능하다. 단일 행 비교 연산자는 서브 쿼리의 결과가 반드시 1건 이하여야 하고 복수 행 비교 연산자는 결과 건수와 상관없다.
3. 서브쿼리에서는 ORDER BY를 사용하지 못한다.
4. SELECT, FROM, WHERE, HAVING, ORDER BY, INSERT-VALUES, UPDATE-SET 절에 사용 가능

단일 행 비교 연산자 : =,<,>,<> 등
다중 행 비교 연산자 : IN, ALL, ANY, SOME 등
스칼라 서브쿼리 : 한 행, 한 칼럼만을 반환하는 서브쿼리

### 인라인 뷰
FROM절에서 사용, ORDER BY 사용 가능

### 뷰 테이블
실제로 데이터를 가지고 있는 반면, 뷰는 실제 데이터를 가지고 있지 않다. 가상 테이블이라고도 함

### 뷰 사용 장점
1. 독립성 : 테이블 구조가 변경되어도 뷰를 사용하는 응용 플그램은 변경하지 않아도 된다.
2. 편리성 : 복잡한 질의를 뷰로 생성함으로써 관련 질의를 단순하게 작성할 수 있다.
3. 보안성 : 직원의 급여정보와 같이 숨기고 싶은 정보가 존재할 때 사용
CREATE VIEW V_PLAYER_TEAM AS
DROP VIEW V_PLAYER_TEAM;

--------------------------------------------

### 그룹 함수: GROUP BY 절 안에서 사용!
ROLLUP : Subtotal을 생성하기 위해 사용, Grouping Columns의 수를 N이라고 했을 때 N+1 Level의 Subtotal이 생성된다. 인수 순서에 주의, 소그룹간의 소계를 계산
GROUPING : Subtotal의 total을 생성
CUBE : 결합 가능한 모든 값에 대하여 다차원 집계를 생성, ROLLUP에 비해 시스템에 부하 심함
GROUPING SETS : 특정 항목에 대한 소계를 계산

--------------------------------------------

### 윈도우 함수 
행과 행간의 관계를 정의하거나 행과 행간을 비교, 연산하는 함수, SELECT절에서 사용, OVER() 절을 반드시 사용

RANK : 특정 항목에 대한 순위를 구하는 함수, 동일한 값에 대해서는 동일한 순위를 부여(1,2,2,4)

DENSE_RANK : 동일한 순위를 하나의 등수로 간주(1,2,2,3)

ROW_NUMBER : 동일한 값이라도 고유한 순위 부여

SUM : 파티션별 윈도우의 합 구할 수 있다.
ex)같은 매니저를 두고 있는 사원들의 월급 합

MAX,MIN : 파티션별 윈도우의 최대, 최솟값을 구할 수 있다.
ex) 같은 매니저를 두고 있는 사원들중 최댓값

AVG : 원하는 조건에 맞는 데이터에 대한 통계 값
ex) 같은 매니저 내에서 앞의 사번과 뒤의 사번의 평균
ROWS BETWEEN 1 PRECEDING AND 1 FOLLOWING
(현재 행을 기준으로 파티션 내에서 앞의 1건, 현재행, 뒤의 1건을 범위로 지정)

COUNT : 조건에 맞는 데이터에 대한 통계 값
ex)본인의 급여보다 50 이하가 적거나 150 이하로 많은 급여를 받는 인원수

FIRST_VALUE : 파티션별 윈도우에서 가장 먼저 나온 값을 구한다.(SQL Server는 지원x)


LAST_VALUE : 파티션별 윈도우에서 가장 나중에 나온 값을 구한다.(SQL Server 지원x)

LAG : 파티션별 윈도우에서 이전 몇 번째 행의 값을 가져올 수 있다.(SQL Server 지원x), 3번째 인자값은 원하는 값이 없을 경우 디폴트값 지정

LEAD : 파티션별 윈도우에서 이후 몇 번째 행의 값을 가져올 수 있다.(SQL Server 지원x)

RATIO_TO_REPORT : 파티션 내 전체 SUM값에 대한 행별 칼럼값의 백분율을 소수점으로 구할 수 있다. 결과값은 0보다 크고 1보다 작거나 같다.

PERCENT_RANK : 파티션 별 윈도우에서 제일 먼저 나오는 것을 0, 제일 늦게 나오는 것을 1로 하여 행의 순서별 백분율을 구한다. 0>=,<=1

CUME_DIST : 현재 행보다 작거나 같은 건수에 대한 누적백분율을 구한다. >0, <=1

NTILE : 파티션별 전체 건수를 인수 값으로 N등분 한 결과를 구할 수 있다.

--------------------------------------------

### DCL
유저 생성하고 권한을 제어할 수 있는 명령어

### Oracle과 SQL Server의 사용자 아키텍처 차이
1) Oracle : 유저를 통해 DB에 접속을 하는 형태, ID와 PW 방식으로 인스턴스에 접속을 하고 그에 해당하는 스키마에 오브젝트 생성 등의 권한을 부여받게 됨
2) SQL Server : 인스턴스에 접속하기 위해 로그인이라는 것을 생성하게 되며, 인스턴스 내에 존재하는 다수의 DB에 연결하여 작업하기 위해 유저를 생성한 후 로그인과 유저를 매핑해 주어야 한다. Windows 인증 방식과 혼합 모드 방식이 존재함

시스템 권한 : 사용자가 SQL 문을 실행하기 위해 필요한 적절한 권한
GRANT : 권한 부여
REVOKE : 권한 취소

GRANT CREATE USER TO SCOTT;
CONN SCOTT/TIGER(ID/PW)
CREATE USER PJS IDENTIFIED BY KOREA7;
GRANT CREATE SESSION TO PJS;
GRANT CREATE TABLE TO PJS;
REVOKE CREATE TABLE FROM PJS;

모든 유저는 각각 자신이 생성한 테이블 외에 다른 유저의 테이블에 접근하려면 해당 테이블에 대한 오브젝트 권한을 소유자로부터 부여받아야 한다.

### ROLE 
유저에게 알맞은 권한들을 한 번에 부여하기 위해 사용하는 것

CREATE ROLE LOGIN_TABLE;
GRANT CREATE TABLE TO LOGIN_TABLE;

DROP USER PJS CASCADE;
CASCADE : 하위 오브젝트까지 삭제

-------------------------------------------

### 절차형 SQL
SQL문의 연속적인 실행이나 조건에 따른 분기처리를 이용하여 특정 기능을 수행하는 저장 모듈을 생성할 수 있다, Procedure, User Defined Function, Trigger 등이 있음

### 저장 모듈
PL/SQL 문장을 DB 서버에 저장하여 사용자와 애플리케이션 사이에서 공유할 수 있도록 만든 일종의 SQL 컴포넌트 프로그램, 독립적으로 실행되거나 다른 프로그램으로부터 실행될 수 있는 완전한 실행 프로그램

### PL/SQL 특징
1. Block 구조로 되어있어 각 기능별로 모듈화 가능
2. 변수, 상수 등을 선언하여 SQL 문장 간 값을 교환
3. IF, LOOP 등의 절차형 언어를 사용하여 절차적인 프로그램이 가능하도록 한다.
4. DBMS 정의 에러나 사용자 정의 에러를 정의하여 사용할 수 있다.
5. PL/SQL은 Oracle에 내장되어 있으므로 호환성 굳
6. 응용 프로그램의 성능을 향상시킨다.
7. Block 단위로 처리 -> 통신량을 줄일 수 있다.

DECLARE : BEGIN~END 절에서 사용될 변수와 인수에 대한 정의 및 데이터 타입 선언부
BEGIN~END : 개발자가 처리하고자 하는 SQL문과 여러 가지 비교문, 제어문을 이용 필요한 로직 처리
EXCEPTION : BEGIN~END 절에서 실행되는 SQL문이 실행될 때 에러가 발생하면 그 에러를 어떻게 처리할지 정의하는 예외 처리부

CREATE Procedure Procedure_name
REPLACE Procedure Procedure_name
DROP Procedure Procedure_name
/ <- 컴파일 하라는 명령어

T-SQL : 근본적으로 SQL Server를 제어하는 언어
CREATE Procedure schema_NAME.Procedure_name

### Trigger
특정한 테이블에 INSERT, UPDATE, DELETE와 같은 DML문이 수행되었을 때, DB에서 자동으로 동작하도록 작성된 프로그램, 사용자 호출이 아닌 DB 자동 수행

CREATE Trigger Trigger_name

### 프로시저와 트리거의 차이점
프로시저는 BEGIN~END 절 내에 COMMIT, ROLLBACK과 같은 트랜잭션 종료 명령어 사용 가능, DB 트리거는 BEGIN~END 절 내에 사용 불가

============================================

### 옵티마이저 : 사용자가 질의한 SQL문에 대해 최적의 실행 방법을 결정하는 역할 수행


### 규칙기반 옵티마이저
우선순위를 가지고 실행계획을 생성한다. 우선순위가 높은 규칙이 적은 일량으로 해당 작업을 수행한다고 판단한다, 인덱스 유무와 SQL문에서 참조하는 객체등을 참고

### 비용기반 옵티마이저
현재 대부분의 DB에서 사용, SQL문을 처리하는데 필요한 비용이 가장 적은 실행계획을 선택하는 방식, 비용이란 SQL문을 처리하기 위해 예상되는 소요시간 또는 자원 사용량을 의미, 테이블, 인덱스, 칼럼 등 다양한 객체 통계정보와 시스템 통계정보 등을 이용

### 실행계획
SQL에서 요구한 사항을 처리하기 위한 절차와 방법을 의미, 실행계획을 구성하는 요소에는 조인 순서, 조인 기법, 액세스 기법, 최적화 정보, 연산 등이 있다.

--------------------------------------------
### 인덱스
원하는 데이터를 쉽게 찾을 수 있도록 돕는 책의 찾아보기와 유사한 개념, 검색 성능의 최적화를 목적으로 두고 있지만 느려질 수 있다는 단점이 존재

### B-TREE 인덱스에서 원하는 값을 찾는 과정
1. 브랜치 블록의 가장 왼쪽 값이 찾고자 하는 값보다 작거나 같으면 왼쪽 포인터로 이동
2. 찾고자 하는 값이 브랜치 블록의 값 사이에 존재하면 가운데 포인터로 이동
3. 오른쪽에 있는 값보다 크면 오른쪽 포인터로 이동

### 전체 테이블 스캔
테이블에 존재하는 모든 데이터를 읽어 가면서 조건에 맞으면 결과로서 추출하고 조건에 맞지 않으면 버리는 방식으로 검색

### 전체 테이블 스캔을 하는 경우
1. SQL문에 조건이 존재하지 않는 경우
2. SQL문의 주어진 조건에 사용 가능한 인덱스가 존재하지 않는 경우
3. 옵티마이저의 취사 선택
4. 병렬처리 방식으로 처리하는 경우 등


### 인덱스 스캔 
인덱스를 구성하는 칼럼의 값을 기반으로 데이터를 추출하는 액세스 기법

### 인덱스 유일 스캔 
유일 인덱스를 사용하여 단 하나의 데이터를 추출하는 방식(중복X, 구성 칼럼에 대해 모두 ‘=’ 로 값이 주어진 경우에만 가능)

### 인덱스 범위 스캔 
인덱스를 이용하여 한 건 이상의 데이터를 추출하는 방식

### 인덱스 역순 범위 스캔 
인덱스의 리프 블록의 양방향 링크를 이용하여 내림차순으로 데이터를 읽는다

--------------------------------------------

### NL Join
프로그래밍에서 사용하는 중첩된 반복문과 유사한 방식으로 조인을 수행, 랜덤 액세스 방식으로 데이터를 읽는다. (NESTED LOOP JOIN)

### Sort Merge Join
조인 칼럼을 기준으로 데이터를 정렬하여 조인을 수행, 스캔 방식으로 데이터 읽음.

### Hash Join
CPU 작업 위주로 처리, 해슁 기법 이용, NL Join의 랜덤 액세스 문제와 SMJ의 정렬 작업 부담을 해결하기 위한 대안으로 등장

### 추가 정리
-NULL은 비교에서 애초에 제외 되며 IN (...) 안에 NULL이 있어도 NULL 비교는 되지 않음
ex) WHERE COL1 in (1, 2, NULL )＝WHERE COL1 in (1, 2)

-Oracle의 경우 DML 후 Auto COMMIT 아니나,
DDL 발생하고 DML을 실행하면 암묵적인 COMMIT이 자동으로 발생 되어 전체 트랜잭션이 COMMIT 됨.

-COALESCE()
 인수의 숫자가 한정되어 있지 않으며, 임의의 개수 EXPR에서 NULL이 아닌 최초의 EXPR을 나타낸다. 만일 모든 EXPR이 NULL이라면 NULL을 리턴

-Subtotal은 Grouping Columns의 수를 N개 라고 했을 때, N+1 Level의 Subtotal이 생성

-Non Equal Join의 경우는 조인 조건을 제외한 Cross 조인 후 조인 조건을 필터 조건으로 처리하는 것이 좋음

-START WITH절에서 계층형 구조의 ROOT를 구별하는 조건절을 기재함. 부모코드가 NULL인 조건으로 구분이 가능
ex) START WITH 1=1 AND 부모코드 IS NULL

-NOT IN() 의 경우 조건절에 NULL 연산이 있을 경우, Unknown으로 처리되어 True 로 반환되는 현상이 나타남 ->NOT IN 결과가 0건으로 RETURN 됨

-NOT EXISTS 는 OUTER JOIN으로 변경 시
NOT NULL COLUMN 에 대한 IS NULL 체크로 NOT EXISTS를 변형 가능

### GROUP BY CUBE(DNAME, JOB)
= GROUP BY DNAME, JOB
 UNION ALL
 GROUP BY DNAME
 UNION ALL
 GROUP BY JOB
 UNION ALL
 모든 집합

### GROUP BY ROLLUP(DNAME,JOB)
= GROUP BY DNAME,JOB 
 UNION ALL 
 GROUP BY DNAME 
 UNION ALL
 모든 집합 그룹 결과

### 마지막 행 칼럼이 모두 NULL인 전체 집계와 COL1 의 소계만 존재하면 ROLLUP 임

###  RANGE BETWEEN start_point AND end_point
-WINDOW()에서 OVER()절 안에서 사용되는 세부 기분할 기준
-start_point는 end_point와 같거나 작은 값이 들어감
-Default 값은 RANGE BETWEEN UNBOUNDED PRECEDING AND CURRENT ROW
-UNBOUNDED PRECEDING: start_point만 들어갈 수 있으며, 파티션의 first row
-UNBOUNDED FOLLOWING : end_point만 들어갈 수 있으며, 파티션의 last row
-CURRENT ROW : start, end_point 둘다 가능. 윈도우는 CUREENT ROW에서 start하거나 end 함

### DBA 권한
SYSTEM, SYS 등의 상위 유저와 그에 해당하는 권한을 가진 경우 부여 가능

### DELETE ON TRIGGER 의 경우 OLD 는 삭제 전 데이터를,NEW 는 삭제 후 데이터를 나타낸다

### INDEX 주의 사항
-LIKE 의 경우 컬럼을 무조건 문자로 형변환 
ex) WHERE TO_CHAR(COL1) LIKE '2%' 로 변형되어 인덱스를 사용하지 못함
-IS NOT NULL 은 해당 인덱스를 FULL SCAN 할 수 있으나 효율이 떨어짐
-부정형 비교는 인덱스 사용이 불가함 

### Hash Join 
Non Equal Join 은 불가능함. Equal Join 만 가능함

### Sort Merge JOIN
-대용량 데이터를 정렬하여 조인
-동등 조인, 비동등 조인에서 다 사용 가능

