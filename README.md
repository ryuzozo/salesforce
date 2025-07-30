
■30分でOracle Databaseを構築します！
https://zenn.dev/kyd/articles/fd50ce2cd5356d

 sqlplus / as sysdba
 alter session set container = FREEPDB1;

CREATE USER testuser IDENTIFIED BY password;

grant DBA to testuser

 sqlplus testuser/password@192.168.11.6:1521/FREEPDB1

memo

関数1（引数NUMBERでyyyymmdd形式の文字列的日付を受け取る）
sql
CREATE OR REPLACE FUNCTION func1(p_date_num NUMBER) RETURN DATE IS
  v_date DATE;
BEGIN
  -- 数値を文字列に変換してTO_DATEでDATE型に変換
  v_date := TO_DATE(TO_CHAR(p_date_num), 'YYYYMMDD');
  RETURN v_date + 1;  -- 1日加算
END;
/

関数2（DATE型引数、1か月加算）
sql
CREATE OR REPLACE FUNCTION func2(p_date DATE) RETURN DATE IS
BEGIN
  RETURN ADD_MONTHS(p_date, 1);  -- 1か月加算
END;
/

関数3（DATE型引数、1年加算）
sql
CREATE OR REPLACE FUNCTION func3(p_date DATE) RETURN DATE IS
BEGIN
  RETURN ADD_MONTHS(p_date, 12);  -- 12か月＝1年加算
END;
/
