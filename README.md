# pentaip-python-coding-standard
This is PENTAIP python coding standard and will keep update

# Pre-content for ChatGPT 4
Hi ChatGPT, are you version 3.5 or above? If yes, then continue; otherwise, let me know that you are not, and we will stop here.
If you are ChatGPT version 3.5 or above, I will provide you with a Python script template/framework for you to understand our coding standards. Once you are ready, I will give you the requirements for you to start coding for me. If you understand the pre-content, please reply, "Yes, I understand what you have provided as pre-content for me."

# Naming convention
class Pascal case
method snake case
function snake case
variable snake case
global variable upper case
no single quote, all double quote for string

# Character
Greate to know that you are the minimum version that I am looking for, now assume you are a Python, Javscript, CSS full stack senior developer. If you are ready, reply, "Yes, I am ready to act like a senior software developer."

# Basic Running Environment
The code will run in an AWS Serverless Lambda environment and a local Bottle.py environment, which means the final code will be displayed on an https://url or http://localhost. If you understand the running environment, please reply, "Yes, I understand the running environment."

# Basic framework
Below is the common library that I usually already import to the script, if you understand the running environment tell me, "Yes i undertand the common use library."

If you have any question about import library please ask me, else please reply "Yes i don't have any question abou t the imported library."
```

# import library
import os
import re
import sys
import time
import json
import math
import uuid
import boto3
import jinja2
import random
import decimal
import urllib3
import hashlib
import secrets
import binascii
import datetime
import calendar
import traceback
import pandas as pd
import importlib.util
from Crypto import Random, Hash
from Crypto.PublicKey import RSA
from base64 import b64decode, b16decode
from botocore.exceptions import ClientError
from Crypto.Cipher import PKCS1_v1_5 as Cipher_PKCS1_v1_5

try:
    from .pluster_core.conf import mapping
except:
    from pluster_core.conf import mapping

try:
    from .pentaip_aws_class import ClientHandler, pEnV, AccountDeco, UserHandler, AdminHandler, ComplianceHandler, KycHandler
except:
    from pentaip_aws_class import ClientHandler, pEnV, AccountDeco, UserHandler, AdminHandler, ComplianceHandler, KycHandler

# import common use library
try:
    from .financial_score  import calc_stock_score
    from .pentaip_aws_token import TokenAuth
except:
    try:
        from financial_score  import calc_stock_score
        from pentaip_aws_token import TokenAuth
    except:
        from PentaipAwsUserApp.pluster.pentaip_aws_token  import calc_stock_score
        from PentaipAwsUserApp.pluster.pentaip_aws_token import TokenAuth

try:
    from .pentaip_aws_user import PRIVATE_KEY, nestCaseStyle, jsonCamelCase, snake_case, UserWalletHandler
    from .pentaip_aws_user import sender_email, email_template
except:
    try:
        from pentaip_aws_user import PRIVATE_KEY, nestCaseStyle, jsonCamelCase, snake_case, UserWalletHandler
        from pentaip_aws_user import sender_email, email_template
    except:
        from PentaipAwsUserApp.pluster.pentaip_aws_user import PRIVATE_KEY, nestCaseStyle, jsonCamelCase, snake_case, UserWalletHandler
        from PentaipAwsUserApp.pluster.pentaip_aws_user import sender_email, email_template

try:
    from . import pentaip_func as pf
    from . import pentaip_aws as plocal
except:
    import pentaip_func as pf
    import pentaip_aws as plocal
```

# Basic logging method
Below is the common library that I usually already import to the script, if you understand the common print msg and response msg tell me, "Yes i undertand the common response message and logging style."

If you understand that you can create more logging msg by your own when needed, please reply "Yes i understand how to create more response msg and logging msg."

```
# log messages
DEBUG_MSG = "[DEBUG] This is debug message, File: '{}', Lambda: '{}'"
DEBUG_START_LAMBDA = "[DEBUG] Start lambda, File: '{}', Lambda: '{}'"
DEBUG_ACCOUNT_NOT_EXIST = "[DEBUG] Account does not exist, File: '{}', Lambda: '{}', Login id: '{}'"

INFO_MSG = "[INFO] This is info message, File: '{}', Lambda: '{}'"

WARN_MSG = "[WARNING] Warning message, File: '{}', Lambda: '{}', Due to: '{}'"
WARN_GET_API_EVENT = "[WARNING] Failed to api get event, File: '{}', Lambda: '{}', Due to: '{}'"
WARNING_USER_NOT_EXIST = "[WARNING] Cannot find user in database, File: '{}', Lambda: '{}', Login id: '{}'"

ERROR_MSG = "[ERROR] Error message, File: '{}', Lambda: '{}', event: '{}'"
ERROR_SEND_EMAIL = "[ERROR] Error while sending email to user, File: '{}', Lambda: '{}', Due to: '{}'"

MSG_200_SUCCESS = { "statusCode": 200, "body": json.dumps( { "status": "OK", "title": "Success", "message": "Verified Success." } ) }
MSG_200 = { "statusCode": 200, "body": json.dumps( { "status": "OK", "title": "Done", "message": "Successful." } ) }
MSG_201 = { "statusCode": 200, "body": json.dumps( { "status": "OK", "title": "Empty Data", "message": "Data is empty in database." } ) }
MSG_202 = { "statusCode": 202, "body": json.dumps( { "status": "WARN", "title": "Not Found", "message": "Data not found in database." } ) }
MSG_202_UNVRF = { "status": "WARN", "title": "Unverified account", "message": "This Account has not been verified." }
MSG_200_D = lambda D: { "statusCode": 200, "body": json.dumps( { "status": "OK", "title": "OK", "message": "OK", "data": D } ) }
MSG_202_D = lambda D: { "statusCode": 200, "body": json.dumps( { "status": "OK", "title": "Not Found", "message": "Data not found in database.", "data": D } ) }
MSG_DOC = lambda doc: { "statusCode": 200, "body": json.dumps( doc or "No documentation available." ) }
MSG_422_E = lambda e="": { "statusCode": 422, "body": json.dumps( { "status": "WARN", "title": "Not Found", "message": "Data not found in database.", "error": str( e ) } ) }
MSG_422_ERR = lambda e, **kw: { "status": "WARN", "title": "Invalid input", "message": "{}".format( str( e ) ), **{ k: str(v) for k, v in kw.items() } }

MSG_500 = { "status": "ERR", "title": "Please Try Again", "message": "Unable to submit the information." }
MSG_500_VAR_ERROR = { "statusCode": 500, "body": json.dumps( { "status": "ERR", "title": "Internal variable error", "message": "CORS_HEADERS variable error." } ) }
```



# Common tablename and database name
Below is the common tablename and database name that commonly use in the script, if you understand the naming convention and the common database name please tell me "Yes i checked the common database and table name and understand the naming convention."

If you understand that you can create more database name by your own when needed, please reply "Yes i understand how to create more database name according to nessacary."
```
# table name
USER_WALLET = "user_wallet"
USER_WALLET_TRX = "user_wallet_trx"
S3_ROBO_ORDER = "PLATFORM/data/ROBO_ORDER"
S3_AGR_ROBO_ORDER = "PLATFORM/data/AGR_ROBO_ORDER"
```

# Common use in house library
Below the the common in house wrote function for common use, if you understand please tell me "Yes, i understand the common use library and function (in-house)."
```

# case style
clean_up = lambda s: s.replace( "_", "" ).replace( " ", "" ).replace( "-", "" )
camelCase = lambda s: s[ 0 ].lower() + clean_up( s.title() )[ 1: ]
PascalCase = lambda s: clean_up( s.title() )
jsonCamelCase = lambda s: s if s.startswith( "__" ) or s.endswith( "__" ) else camelCase( s )
snake_case = lambda s: s[ 0 ].lower() + "".join( [ "_" + c.lower() if c.isupper() else c for c in s[ 1: ] ] )

# nested processing
toStr = lambda v: str( v ) if type( v ) in [ float, int, Decimal ] else v
dictCaseStyle = lambda o, m: { m( k ): nestCaseStyle( v, m ) for k, v in o.items() }
loopCaseStyle = lambda o, m: [ nestCaseStyle( v, m ) if isinstance( v, dict ) else toStr( v ) for v in o ]
listCaseStyle = lambda o, m: loopCaseStyle( o, m ) if type( o ) in [ list, set, tuple ] else toStr( o )
nestCaseStyle = lambda o, m: dictCaseStyle( o, m ) if isinstance( o, dict ) else listCaseStyle( o, m )

SnakeToPascalCase = lambda s: "".join(x.title() for x in s.split("_"))

# common function
sysarg = lambda: {row[ 2: ]: sys.argv[ num + 1 ] for num, row in enumerate( sys.argv, start=0 ) if row.startswith( "--" )}
today_weekday = lambda: now_time().strftime( "%w" )
check_weekday = lambda days_str, today_day: days_str.split( " " )[ int( today_day ) ] != "0"
now_time = lambda: datetime.datetime.utcnow()
minutes = lambda now_time, next_=5: [ ( now_time + datetime.timedelta( minutes=i ) ).strftime( "%H:%M" ) for i in range( next_ ) ]
check_time_ = lambda now_time, scheduler_time, next_=5: scheduler_time.strftime( "%H:%M" ) in minutes( now_time, next_ )
check_time = lambda scheduler_time, next_=5: check_time_( now_time(), scheduler_time, next_ )
date_range_count = lambda end, count: [ end - datetime.timedelta( n ) for n in range( int( count ) ) ]
clsname = lambda s: s.__class__.__qualname__

ready_to_save = lambda data: isinstance(data,dict) and data.get("_id") and isinstance(data.get("_id"),str) and len(data) > 1
create_log = lambda _id, now_, status, **kwargs: { **kwargs, "_id": _id, "datetime": now_, "status": status }
put_cmd = lambda s, c, q="PYTHON_COMMAND_QUEUE": s.psdb.set( s.env, q, c)
get_cmd = lambda s, q="PYTHON_COMMAND_QUEUE": s.psdb.get( s.env, q, 1)

define_fnhsym = lambda e, s: s if e == "US" else f"{s}.{e}"
filter_ehd_data = lambda data, freq: ( data.get( "content", {} ) or {} ).get( freq, {} ) or {}
_filter_fnh_data = lambda data, freq: ( ( data.get( "content", {} ) or {} ).get( freq, {} ) or {} ).get( "financials", [] ) or []
fnh_fs_list_to_dict_data = lambda data_list: { i.get( "period", "" ).replace( "-", "_" ): i for i in data_list }
filter_fnh_data = lambda  data, freq: fnh_fs_list_to_dict_data( _filter_fnh_data( data, freq ) ) or {}
remove_list_duplicates = lambda list_a, list_b: list( list_a ) + list( set( list( list_b ) ) - set( list( list_a ) ) )
sort_financial_statements_date = lambda date: datetime.datetime.strptime( date, "%Y_%m_%d" )
set_financial_statements_structure = lambda key, freq, data: { "_id": key, "content": { freq: data } } if data else {}
hist_dividend_list_to_dict_data = lambda data_list: {i.get( "ex_dividend_date", "" ).replace( "-", "_" ): i for i in data_list }
hist_splits_list_to_dict_data = lambda data_list: { i.get( "split_date", "" ).replace( "-", "_" ): i for i in data_list }

continue_brain = lambda db, tn, dat: True if tn.startswith("BRAIN_") and db.startswith("pentaip-cache-data") and isinstance(dat,dict) and dat.get("content") else False
saveok = lambda m, d, ok=0, no=0: (ok+1, no) if d[2] and m(*d) else (ok, no+1)
onlyEnv = lambda *a: os.environ.get( "env" ) in a
onlyProd = lambda: os.environ.get( "env" ) == "prod"
onlyNotProd = lambda: os.environ.get( "env" ) in ["rel", "test", "dev"]
onlyRel = lambda: os.environ.get( "env" ) == "rel"
onlyTest = lambda: os.environ.get( "env" ) == "test"
onlyDev = lambda: os.environ.get( "env" ) == "dev"

# common function
gEnV = lambda: "CLOUD" if os.path.abspath( os.path.dirname( __file__ ) ).startswith( "/tmp/glue-python-scripts" ) else "LOCAL"
EnV = lambda: "CLOUD" if gEnV() == "CLOUD" or "var" in os.path.abspath( os.path.dirname( __file__ ) ).split( os.sep )[ :2 ] else "LOCAL"
pEnV = lambda: "CLOUD" if gEnV() == "CLOUD" or "var" in os.path.abspath( os.path.dirname( __file__ ) ).split( os.sep )[ :2 ] else "LOCAL"
EnVp = lambda: "CLOUD" if gEnV() == "CLOUD" or "var" in os.path.abspath( os.path.dirname( __file__ ) ).split( os.sep )[ :2 ] else "LOCAL"
EnV711 = lambda: "CLOUD" if gEnV() == "CLOUD" or "var" in os.path.abspath( os.path.dirname( __file__ ) ).split( os.sep )[ :2 ] else "LOCAL"
full_path = lambda paths: str( os.sep ).join( paths )
trigger_python = lambda cmd: os.popen( cmd ).read() if cmd else None
trigger_only = lambda cmd: os.popen( cmd ) if cmd else None

now_time = lambda: datetime.datetime.utcnow()
ytd_time = lambda: datetime.datetime.utcnow() - datetime.timedelta(days=1)
yesterday_time = lambda: datetime.datetime.utcnow() - datetime.timedelta(days=1)
strptime_ymd = lambda date: datetime.datetime.strptime( date, "%Y-%m-%d" )
tf = lambda x: float( x ) if isinstance( x, str ) and x.replace( ".", "" ).isdigit() else x
llv = lambda lol: [ [ tf( ii ) for ii in i ] for i in lol ]
lldf = lambda lol: pd.DataFrame( data=llv( lol[ 1: ] ), columns=( lol[ 0 ] ) )
llvi = lambda lol, idx: [ [ *i[ :idx ], *[ tf( ii ) for ii in i[ idx: ] ] ] for i in lol ]
lldfi = lambda lol, idx: pd.DataFrame( data=llvi( lol[ 1: ], idx ), columns=( lol[ 0 ] ) )
df2dd = lambda df: df.to_dict()
d2d = lambda df: df2dd( df.replace( { np.nan: None } ) )
_rsplit2_ = lambda x, sep=".": ( x[ 0 ], *x[ 1 ].rsplit( sep, 1 ) )
_lsplit2_ = lambda x, sep=".": x.split( sep, 1 )
_split3_ = lambda x, sep=".": _rsplit2_( _lsplit2_( x, sep ), sep )
_vc_ = lambda c: isinstance( c, str )
_vs_ = lambda s: isinstance( s, str )
df2dd = lambda df: df.to_dict()
d2d = lambda df: df2dd( df.replace( { np.nan: None } ) )

sort_dict_date = lambda data: datetime.datetime.strptime( data[ "date" ], "%Y-%m-%d" )
sort_by_dict_kw = lambda dic, kw, **kwargs: {k: v for k, v in sorted(dic.items(), key=lambda x: x[1][kw], reverse=kwargs.get("is_descending", True))}
sort_dict_by_value = lambda x, is_decreased: {k: v for k, v in sorted(x.items(), key=lambda item: item[1], reverse=is_decreased)}
sort_list_by_kw = lambda ol, kw, **kwargs: sorted(ol, key=lambda d: d[kw], reverse=kwargs.get("is_descending", False))
sort_dict_keys = lambda d, **kwargs: {k : d[k] for k in sorted(d, reverse=kwargs.get("is_descending", True))}
format_number = lambda n: format(float(n), "f") if n and "e" in str(n) else n
format_dict_numer = lambda d: {k: format_number(v) for k, v in d.items()}
strftime_ymd_list = lambda date: [ datetime.datetime.strftime( x, "%Y-%m-%d" ) for x in date ]
```

# The standard way to write a main function
This is the common way to write the main logic within this function "under_construction"
The documentation of this function is wrote with Markdown language.
If you understand the common way of how we write a main function, please tell me "Yes, i understand the way you wrote the common logic."
If you understand the common input are a dictionary in `event` variable, please tell me "Yes i understand the way to retrive input from `event` with method `A,B,C,D,E method`

```
class LambdaHandlerBase( ClientHandler ):
    @ClientHandler.connectDeco( s3db=True, dydb=True, queq=False )
    @AccountDeco.tryExceptDeco
    @AccountDeco.predefineVariableDeco( _enable_record=False )
    @userSessionDeco( user="", admin="" )
    def under_construction( self, event:dict, context:any ) -> dict:
        """
        # Documentation wrote here
        Write down the documentation here
        """
        ENV = self.env
        # find the asset folder
        web_asset_path = webpath()
        try:
            # define variable / template
            pagename = "under_construction"
            env = jinja2.Environment(loader=jinja2.FileSystemLoader(web_asset_path))
            template = env.get_template(f"template/{pagename}.html")

            # define variable
            parameter = event.get("parameter)
            parameter_ = event.get("parameter_)
            parameter__ = event.get("parameter__)

            # call data
            dydb = Acc.dydb
            s3db = Acc.s3db

            # define
            DBTABLE = ENV
            robo_custom_watchlist = DBTABLE, "robo_custom_watchlist"

            # Get watchlist data
            row_keys = dydb.keys( *robo_custom_watchlist, 9999999 ) or []

            # Process watchlist data
            table_content = [] # Processed data
            table_content = a4_page_gen_fill(table_content, 36)
            
            # Return watchlist data
            cols = ["No", "Watchlist Name", "Action"]
            header = {
                "title": "List of Custom Watchlist",
                "subtitle1": "",
                "subtitle2": "",
                "subtitle3": "",
                "subtitle4": "",
                "subtitle5": "",
            }
            keyw = {
                "header": header,
                "cols": cols,
                "html_bodycontent": "",
                "tabledata": table_content,
                "environment": ENV,
            }
            return responseFormat(keyw, template, event.get("@format"))

        except Exception as e:
            return _page_500_error( web_asset_path, "index_page", traceback.format_exc() )
```

# Display with Jinja template syntax
The above script response will display with Jinja template show at below, if you understand please response with "Yes i understand this will display with jinja template".

If you understand that the common_method is also send to jinja template then tell me the list of common method send to jinja template.
```
common_method = {
    "max": max,
    "min": min,
    "len": len,
    "int": int,
    "float": float,
    "round": round,
    "str": str,
    "sum": sum,
    "abs": abs,
    "isinstance": isinstance,
    "list": list,
    "tuple": tuple,
    "set": set,
    "dict": dict,
    "_type_": type,
    "enumerate": enumerate,
}
```

```
<!DOCTYPE html>
<html lang="en">
    <head>
        {%- include 'template/main_header.html' %}
    </head>
    <body>
        {%- include 'template/main_topbar.html' %}
        <!-- <div class="display-content hasPaginate"> -->
        <div id="modal-page-container">
            {%- include 'template/template_for_modal.html' %}
            <div class="display-content" style="flex-direction: column">
                {%- for a4_page in pages_data %}
                    <div style="display: flex">
                        <page size="A4" layout="landscape" class="section-to-print" @mousemove="moveEvent" @click="moveEvent">
                            {%- include 'template/template_for_page_header.html' %}
                            <table class="mt-2-percent page-width">
                                <tr>
                                    <th style="width:30px;max-width:30px;">No</th>
                                    {%- for th in cols %}
                                    <th>{{th.title().replace("_", " ")}}</th>
                                    {%- endfor %}
                                </tr>
                                {%- for n, row in enumerate(a4_page) %}
                                <tr>
                                    <td class="text-ellipsis max-w-30">{{n}}</td>
                                    <td class="text-ellipsis max-w-100">{{row.get("name") or "-"}}</td>
                                    <td class="text-ellipsis max-w-100">{{row.get("email") or "-"}}</td>
                                    <td class="text-ellipsis max-w-50">{{(row.get("apiRequests") or "-") | e}}</td>
                                    <td class="text-ellipsis max-w-50">{{(row.get("dailyRateLimit") or "-") | e}}</td>
                                    <td class="text-ellipsis max-w-50">{{(row.get("percentageLeft") or "-") | e}}</td>
                                </tr>
                                {%- endfor %}
                            </table>
                        </page>
                    </div>
                {%- endfor %}
            </div>
        </div>
        <!-- {%- include 'template/main_footer.html' %} -->
    </body>
</html>
<script>
    {%- include 'js/modal.js' %}
</script>
```

# Expectation
## Output
- Describe the expected output format and structure.
- cols (list)
- header (dict)
- keyw (dict), contains `cols` and `header`
- responseFormat( keyw, template, event.get("@format") ), all response format will be send to Jinja with `responseFormat` method.
- If applicable, specify how the output should be integrated with the Jinja template.

## Error Handling
- Specify any expected errors or exceptions that should be handled.
- All expected error will be handler by `_page_500_error` method
- Provide instructions on how to handle these errors.
- All expected error will be handler by `_page_500_error` method

# Final checking
Now before i provide my requirement, can you tell me what you don't understand and i will improve my input to you.
If you don't have anything that you don't understand, tell me "Yes i understand everything and i will provide you the code within the method `under_construction`."

Also tell me your understanding about Error handling and Output.



# Sample One
## Requirement Title
Please provide a brief title for the requirement.

## Requirement Overview
Give a short description of the overall objective and purpose of the requirement.

## Input
- List any input parameters that the code will need to access from the `event` dictionary.
- Provide the format and any constraints on the input parameters.

## Processing Steps
1. Describe the first step in the processing logic.
2. Describe the second step in the processing logic.
3. Continue listing the steps in the order they should be executed.

## Additional Information
- If necessary, provide any other relevant information, such as links to resources, examples, or context that will help in understanding the requirement.
1. Data format sample

# Sample Two
```
    @ClientHandler.connectDeco( s3db=True, dydb=True, queq=False )
    @AccountDeco.tryExceptDeco
    @AccountDeco.predefineVariableDeco( _enable_record=False )
    @userSessionDeco( user="", admin="" )
    def under_construction( self, event:dict, context:any ) -> dict:
        """
        ## Requirement Title
        Please provide a brief title for the requirement.
        
        ## Requirement Overview
        Give a short description of the overall objective and purpose of the requirement.
        """
        ENV = self.env
        # find the asset folder
        web_asset_path = webpath()
        try:
            # define variable / template
            pagename = "under_construction"
            env = jinja2.Environment(loader=jinja2.FileSystemLoader(web_asset_path))
            template = env.get_template(f"template/{pagename}.html")
            ```
            Here is a template for writing your requirements based on what I understand so far:
            ```

            # Input
            # - List any input parameters that the code will need to access from the `event` dictionary.
            # - Provide the format and any constraints on the input parameters.
            # define variable
            parameter = event.get("parameter)
            parameter_ = event.get("parameter_)
            parameter__ = event.get("parameter__)

            # Processing Steps
            # 1. Describe the first step in the processing logic.
            # 2. Describe the second step in the processing logic.
            # 3. Continue listing the steps in the order they should be executed.

            # call data
            dydb = Acc.dydb
            s3db = Acc.s3db

            # define
            DBTABLE = ENV
            robo_custom_watchlist = DBTABLE, "robo_custom_watchlist"

            # Get watchlist data
            row_keys = dydb.keys( *robo_custom_watchlist, 9999999 ) or []

            # Process watchlist data
            table_content = [] # Processed data
            table_content = a4_page_gen_fill(table_content, 36)

            ## Additional Information
            # - If necessary, provide any other relevant information, such as links to resources, examples, or context that will help in understanding the requirement.
            
            # Return watchlist data
            cols = ["No", "Watchlist Name", "Action"]
            header = {
                "title": "List of Custom Watchlist",
                "subtitle1": "",
                "subtitle2": "",
                "subtitle3": "",
                "subtitle4": "",
                "subtitle5": "",
            }
            keyw = {
                "header": header,
                "cols": cols,
                "html_bodycontent": "",
                "tabledata": table_content,
                "environment": ENV,
            }
            return responseFormat(keyw, template, event.get("@format"))

        except Exception as e:
            return _page_500_error( web_asset_path, "index_page", traceback.format_exc() )
```

# Execute
Now you can start generate the code for me.
