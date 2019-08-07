# MatillionSnowFlakeDem
Code snippets that I showed during Matillion SnowFlake demo

Data source : data.world - Please create an account in data.world to get access to data


## create stage
 create or replace stage my_stage;
## create on time performance table, DDL
  create or replace table otp_data( Year	number,Quarter	number,Month	number,DayofMonth	number,DayOfWeek	number,FlightDate	varchar,Reporting_Airline	varchar,DOT_ID_Reporting_Airline	varchar,IATA_CODE_Reporting_Airline	varchar,Tail_Number	varchar,Flight_Number_Reporting_Airline	number,OriginAirportID	varchar,OriginAirportSeqID	varchar,OriginCityMarketID	varchar,Origin	varchar,OriginCityName	varchar,OriginState	varchar,OriginStateFips	varchar,OriginStateName	varchar,OriginWac	varchar,DestAirportID	varchar,DestAirportSeqID	varchar,DestCityMarketID	varchar,Dest	varchar,DestCityName	varchar,DestState	varchar,DestStateFips	varchar,DestStateName	varchar,DestWac	varchar,CRSDepTime	varchar,DepTime	varchar,DepDelay	varchar,DepDelayMinutes	varchar,DepDel15	varchar,DepartureDelayGroups	varchar,DepTimeBlk	varchar,TaxiOut	varchar,WheelsOff	varchar,WheelsOn	varchar,TaxiIn	varchar,CRSArrTime	varchar,ArrTime	varchar,ArrDelay	varchar,ArrDelayMinutes	varchar,ArrDel15	varchar,ArrivalDelayGroups	varchar,ArrTimeBlk	varchar,Cancelled	varchar,CancellationCode	varchar,Diverted	varchar,CRSElapsedTime	varchar,ActualElapsedTime	varchar,AirTime	varchar,Flights	varchar,Distance	varchar,DistanceGroup	varchar,CarrierDelay	varchar,WeatherDelay	varchar,NASDelay	varchar,SecurityDelay	varchar,LateAircraftDelay	varchar,FirstDepTime	varchar,TotalAddGTime	varchar,LongestAddGTime	varchar,DivAirportLandings	varchar,DivReachedDest	varchar,DivActualElapsedTime	varchar,DivArrDelay	varchar,DivDistance	varchar,Div1Airport	varchar,Div1AirportID	varchar,Div1AirportSeqID	varchar,Div1WheelsOn	varchar,Div1TotalGTime	varchar,Div1LongestGTime	varchar,Div1WheelsOff	varchar,Div1TailNum	varchar,Div2Airport	varchar,Div2AirportID	varchar,Div2AirportSeqID	varchar,Div2WheelsOn	varchar,Div2TotalGTime	varchar,Div2LongestGTime	varchar,Div2WheelsOff	varchar,Div2TailNum	varchar,Div3Airport	varchar,Div3AirportID	varchar,Div3AirportSeqID	varchar,Div3WheelsOn	varchar,Div3TotalGTime	varchar,Div3LongestGTime	varchar,Div3WheelsOff	varchar,Div3TailNum	varchar,Div4Airport	varchar,Div4AirportID	varchar,Div4AirportSeqID	varchar,Div4WheelsOn	varchar,Div4TotalGTime	varchar,Div4LongestGTime	varchar,Div4WheelsOff	varchar,Div4TailNum	varchar,Div5Airport	varchar,Div5AirportID	varchar,Div5AirportSeqID	varchar,Div5WheelsOn	varchar,Div5TotalGTime	varchar,Div5LongestGTime	varchar,Div5WheelsOff	varchar,Div5TailNum	varchar,lastCol	varchar);
## create  file format
  create or replace file format my_csv_1_format  type = csv field_delimiter = ',' skip_header = 1  field_optionally_enclosed_by = '"'
  null_if = ('NULL', 'null')   empty_field_as_null = true;

## Copy from stage to DW
   COPY INTO "PC_MATILLION_DB"."PUBLIC"."OTP_DATA" FROM @my_stage FILE_FORMAT = 'my_csv_1_format' ON_ERROR = 'ABORT_STATEMENT' PURGE = FALSE;
   
## sample python script measure count of data mart (in this case a view)
  cursor = context.cursor()
  cursor.execute("select count(*) from OTP_RITADATA_VIEW")
  result = cursor.fetchone()

  print result

## CDC demo - RDS DDL and other scripts
### create table in RDS
user airlinedb;
CREATE TABLE IF NOT EXISTS OTP_DATA (
	YEAR INT,
	QUARTER INT,
	MONTH INT,
	DAYOFMONTH INT,
	DAYOFWEEK INT,
	FLIGHTDATE VARCHAR(255),
	REPORTING_AIRLINE VARCHAR(255),
	DOT_ID_REPORTING_AIRLINE VARCHAR(255),
	IATA_CODE_REPORTING_AIRLINE VARCHAR(255),
	TAIL_INT VARCHAR(255),
	FLIGHT_INT_REPORTING_AIRLINE INT,
	ORIGINAIRPORTID VARCHAR(255),
	ORIGINAIRPORTSEQID VARCHAR(255),
	ORIGINCITYMARKETID VARCHAR(255),
	ORIGIN VARCHAR(255),
	ORIGINCITYNAME VARCHAR(255),
	ORIGINSTATE VARCHAR(255),
	ORIGINSTATEFIPS VARCHAR(255),
	ORIGINSTATENAME VARCHAR(255),
	ORIGINWAC VARCHAR(255),
	DESTAIRPORTID VARCHAR(255),
	DESTAIRPORTSEQID VARCHAR(255),
	DESTCITYMARKETID VARCHAR(255),
	DEST VARCHAR(255),
	DESTCITYNAME VARCHAR(255),
	DESTSTATE VARCHAR(255),
	DESTSTATEFIPS VARCHAR(255),
	DESTSTATENAME VARCHAR(255),
	DESTWAC VARCHAR(255),
	CRSDEPTIME VARCHAR(255),
	DEPTIME VARCHAR(255),
	DEPDELAY VARCHAR(255),
	DEPDELAYMINUTES VARCHAR(255),
	DEPDEL15 VARCHAR(255),
	DEPARTUREDELAYGROUPS VARCHAR(255),
	DEPTIMEBLK VARCHAR(255),
	TAXIOUT VARCHAR(255),
	WHEELSOFF VARCHAR(255),
	WHEELSON VARCHAR(255),
	TAXIIN VARCHAR(255),
	CRSARRTIME VARCHAR(255),
	ARRTIME VARCHAR(255),
	ARRDELAY VARCHAR(255),
	ARRDELAYMINUTES VARCHAR(255),
	ARRDEL15 VARCHAR(255),
	ARRIVALDELAYGROUPS VARCHAR(255),
	ARRTIMEBLK VARCHAR(255),
	CANCELLED VARCHAR(255),
	CANCELLATIONCODE VARCHAR(255),
	DIVERTED VARCHAR(255),
	CRSELAPSEDTIME VARCHAR(255),
	ACTUALELAPSEDTIME VARCHAR(255),
	AIRTIME VARCHAR(255),
	FLIGHTS VARCHAR(255),
	DISTANCE VARCHAR(255),
	DISTANCEGROUP VARCHAR(255),
	CARRIERDELAY VARCHAR(255),
	WEATHERDELAY VARCHAR(255),
	NASDELAY VARCHAR(255),
	SECURITYDELAY VARCHAR(255),
	LATEAIRCRAFTDELAY VARCHAR(255),
	FIRSTDEPTIME VARCHAR(255),
	TOTALADDGTIME VARCHAR(255),
	LONGESTADDGTIME VARCHAR(255),
	DIVAIRPORTLANDINGS VARCHAR(255),
	DIVREACHEDDEST VARCHAR(255),
	DIVACTUALELAPSEDTIME VARCHAR(255),
	DIVARRDELAY VARCHAR(255),
	DIVDISTANCE VARCHAR(255),
	DIV1AIRPORT VARCHAR(255),
	DIV1AIRPORTID VARCHAR(255),
	DIV1AIRPORTSEQID VARCHAR(255),
	DIV1WHEELSON VARCHAR(255),
	DIV1TOTALGTIME VARCHAR(255),
	DIV1LONGESTGTIME VARCHAR(255),
	DIV1WHEELSOFF VARCHAR(255),
	DIV1TAILNUM VARCHAR(255),
	DIV2AIRPORT VARCHAR(255),
	DIV2AIRPORTID VARCHAR(255),
	DIV2AIRPORTSEQID VARCHAR(255),
	DIV2WHEELSON VARCHAR(255),
	DIV2TOTALGTIME VARCHAR(255),
	DIV2LONGESTGTIME VARCHAR(255),
	DIV2WHEELSOFF VARCHAR(255),
	DIV2TAILNUM VARCHAR(255),
	DIV3AIRPORT VARCHAR(255),
	DIV3AIRPORTID VARCHAR(255),
	DIV3AIRPORTSEQID VARCHAR(255),
	DIV3WHEELSON VARCHAR(255),
	DIV3TOTALGTIME VARCHAR(255),
	DIV3LONGESTGTIME VARCHAR(255),
	DIV3WHEELSOFF VARCHAR(255),
	DIV3TAILNUM VARCHAR(255),
	DIV4AIRPORT VARCHAR(255),
	DIV4AIRPORTID VARCHAR(255),
	DIV4AIRPORTSEQID VARCHAR(255),
	DIV4WHEELSON VARCHAR(255),
	DIV4TOTALGTIME VARCHAR(255),
	DIV4LONGESTGTIME VARCHAR(255),
	DIV4WHEELSOFF VARCHAR(255),
	DIV4TAILNUM VARCHAR(255),
	DIV5AIRPORT VARCHAR(255),
	DIV5AIRPORTID VARCHAR(255),
	DIV5AIRPORTSEQID VARCHAR(255),
	DIV5WHEELSON VARCHAR(255),
	DIV5TOTALGTIME VARCHAR(255),
	DIV5LONGESTGTIME VARCHAR(255),
	DIV5WHEELSOFF VARCHAR(255),
	DIV5TAILNUM VARCHAR(255),
	LASTCOL VARCHAR(255)
);
### Grant permissions and load data
GRANT LOAD FROM S3 ON *.* TO 'admin'@'YourRDSInstance';
### Load data into RDS
mysqlimport --local     --compress     --user=admin     --password     --host=YourRDSInstance     --fields-terminated-by=',' airlinedb    ./OTP_DATA.csv;     
