## Install and import Snowflake connector:


```python
#https://docs.snowflake.com/en/user-guide/python-connector-install.html
```


```python
import snowflake.connector
```

## Connect to Snowflake and create a data frame out of a SQL query:


```python
#use your email address as your username
#place your password between quotes
#authenticator=‘externalbrowser’ triggers the required snowflake 2fa

conn = snowflake.connector.connect(
                user='geoffrey.decanio@care.com',
                password='password',
                account='fca45116.us-east-1',
                role='O_P_SNOWFLAKE_DATA-ANALYST',
                authenticator='externalbrowser'
                )

cs = conn.cursor()
```

    Initiating login request with your identity provider. A browser window should have opened for you to complete the login. If you can't see it, check existing browser windows, or your OS settings. Press CTRL+C to abort and try again...



```python
#create a SQL query
```


```python
sql01 = """select 
event_properties:czen_session_id::varchar
,event_properties:"extraData.user_distance"
,event_properties:user_choice::varchar
,user_properties:care_device_id::varchar
,user_properties:visitor_id::varchar 
FROM "PRD_DB_CARE_LAKE"."AMPLITUDE"."EVENTS_188469"
where event_properties:enrollment_step in ('Care Kind')
and event_time >= '2022-04-17' and event_time <= '2022-04-23'
and event_properties:url_path in ('/app/enrollment/seeker/cc/v2/care-kind')
and event_properties:vertical in ('Childcare')
"""

#execute query:
cs.execute(sql01)
```


```python
#create a data frame:
df = cs.fetch_pandas_all()
#view your data frame
display(df)
```
