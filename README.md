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
  
